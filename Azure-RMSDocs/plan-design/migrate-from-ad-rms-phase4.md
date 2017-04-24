---
title: "Migrer un déploiement AD RMS vers Azure Information Protection - Phase 4"
description: "Phase 4 de la migration d’AD RMS vers Azure Information Protection, couvrant les étapes 8 et 9 de la migration d’AD RMS vers Azure Information Protection"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/06/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8b039ad5-95a6-4c73-9c22-78c7b0e12cb7
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: c6646b6e3df72105d0808e23b40fe01e444e164a
ms.sourcegitcommit: 384461f0e3fccd73cd7eda3229b02e51099538d4
translationtype: HT
---
# <a name="migration-phase-4---supporting-services-configuration"></a>Phase de migration 4 : Configuration des services de prise en charge

>*S’applique à : Services AD RMS, Azure Information Protection, Office 365*


Utilisez les informations suivantes pour la Phase 4 de la migration d’AD RMS vers Azure Information Protection. Ces procédures couvrent les étapes 8 et 9 de la rubrique [Migration d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).



## <a name="step-8-configure-irm-integration-for-exchange-online"></a>Étape 8. Configurer l'intégration de l'IRM pour Exchange Online

Si vous avez précédemment importé votre TDP d’AD RMS dans Exchange Online, vous devez supprimer cette TDP pour éviter des conflits de modèles et de stratégies après la migration vers Azure Information Protection. Pour ce faire, utilisez l’applet de commande [Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/library/jj200720%28v=exchg.150%29.aspx) d’Exchange Online.

Si vous avez choisi une topologie de clé de locataire Azure Information Protection **Gérée par Microsoft** :

1. Utilisez les instructions de la section [Exchange Online : configuration d’IRM](../deploy-use/configure-office365.md#exchange-online-irm-configuration) de l’article [Office 365 : Configuration pour les clients et les services en ligne](../deploy-use/configure-office365.md). Cette section inclut des commandes spécifiques à exécuter, qui établissent une connexion au service Exchange Online, importent la clé de locataire à partir d’Azure Information Protection, puis activent les fonctionnalités IRM (Gestion des droits relatifs à l’information) pour Exchange Online. Après avoir effectué ces étapes, vous disposez de toutes les fonctionnalités de la protection Azure Rights Management avec Exchange Online.

2. Outre la configuration standard pour activer IRM pour Exchange Online, exécutez les commandes PowerShell suivantes pour vérifier que les utilisateurs sont en mesure de lire les e-mails qui ont été envoyés à l’aide de la protection AD RMS.

    Remplacez *\<votresociété.domaine>* par le nom de domaine de votre propre organisation.

        $irmConfig = Get-IRMConfiguration
        $list = $irmConfig.LicensingLocation
        $list += "https://adrms.<yourcompany.domain>/_wmcs/licensing"
        Set-IRMConfiguration -LicensingLocation $list
        Set-IRMConfiguration -internallicensingenabled $false
        Set-IRMConfiguration -internallicensingenabled $true


Si vous avez choisi une topologie de clé de locataire Azure Information Protection **Gérée par le client (BYOK)** :

-   Vous disposez de fonctionnalités de protection Rights Management réduites avec Exchange Online, comme décrit dans l’article [Tarifs et restrictions BYOK](byok-price-restrictions.md).


## <a name="step-9-configure-irm-integration-for-exchange-server-and-sharepoint-server"></a>Étape 9. Configurer l’intégration d’IRM pour Exchange Server et SharePoint Server

Si vous avez utilisé la fonctionnalité IRM (Information Rights Management) d’Exchange Server ou de SharePoint Server avec AD RMS, vous devez déployer le connecteur RMS (Rights Management) qui fait office d’interface de communication (un relais) entre vos serveurs locaux et le service de protection pour Azure Information Protection.

Cette étape aborde l’installation et la configuration du connecteur, la désactivation d’IRM pour Exchange et SharePoint ainsi que la configuration de ces serveurs pour utiliser le connecteur. Enfin, si vous avez importé des fichiers de configuration de données (.xml) AD RMS dans Azure Information Protection qui ont été utilisés pour protéger des e-mails, vous devez modifier manuellement le Registre sur les ordinateurs Exchange Server pour rediriger toutes les URL de domaine de publication approuvé vers le connecteur RMS.

> [!NOTE]
> Avant de commencer, vérifiez les versions des serveurs locaux prises en charge par le service Azure Rights Management, dans [Serveurs locaux prenant en charge Azure RMS](../get-started/requirements-servers.md).

### <a name="install-and-configure-the-rms-connector"></a>Installation et configuration du connecteur RMS

Suivez les instructions de l’article [Déploiement du connecteur Azure Rights Management](../deploy-use/deploy-rms-connector.md) et effectuez les étapes 1 à 4. Ne démarrez pas encore l’étape 5 à partir des instructions du connecteur. 

### <a name="disable-irm-on-exchange-servers-and-remove-ad-rms-configuration"></a>Désactivation de l'IRM sur les serveurs Exchange et suppression de la configuration AD RMS

1.  Sur chaque serveur Exchange, recherchez le dossier suivant, puis supprimez toutes ses entrées : **\ProgramData\Microsoft\DRM\Server\S-1-5-18**

2. À partir de l’un des serveurs Exchange, exécutez les commandes PowerShell suivantes pour vérifier que les utilisateurs seront en mesure de lire les e-mails qui sont protégés à l’aide d’Azure Rights Management.

    Avant d’exécuter ces commandes, remplacez *\<URL de votre locataire>* par votre propre URL du service Azure Rights Management.

        $irmConfig = Get-IRMConfiguration
        $list = $irmConfig.LicensingLocation 
        $list + "<Your Tenant URL>/_wmcs/licensing"
        Set-IRMConfiguration -LicensingLocation $list

3.  Désactivez maintenant les fonctionnalités IRM pour les messages envoyés à des destinataires internes :

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $false
    ```

4. Utilisez ensuite la même applet de commande pour désactiver IRM dans Microsoft Office Outlook Web App et dans Microsoft Exchange ActiveSync :

    ```
    Set-IRMConfiguration -ClientAccessServerEnabled $false
    ```

5.  Enfin, utilisez la même applet de commande pour effacer les certificats mis en cache :

    ```
    Set-IRMConfiguration -RefreshServerCertificates
    ```

6.  Sur chaque serveur Exchange, réinitialisez IIS, par exemple, en exécutant une invite de commandes en tant qu’administrateur et en tapant **iisreset**.

### <a name="disable-irm-on-sharepoint-servers-and-remove-ad-rms-configuration"></a>Désactivation d'IRM sur les serveurs SharePoint et suppression de la configuration AD RMS

1.  Assurez-vous qu'aucun document n'est extrait des bibliothèques protégées par RMS. Les documents extraits deviendront inaccessibles à la fin de cette procédure.

2.  Sur le site web Administration centrale de SharePoint, dans la section **Lancement rapide**, cliquez sur **Sécurité**.

3.  Dans la page **Sécurité**, dans la section **Stratégie d'information**, cliquez sur **Configurer la gestion des droits relatifs à l'information**.

4.  Dans la page **Gestion des droits relatifs à l'information**, dans la section **Gestion des droits relatifs à l'information**, sélectionnez **Ne pas utiliser IRM sur ce serveur**, puis cliquez sur **OK**.

5.  Sur chaque ordinateur SharePoint Server, supprimez le contenu du dossier \ProgramData\Microsoft\MSIPC\Server\\<*SID du compte exécutant SharePoint Server>*.

### <a name="configure-exchange-and-sharepoint-to-use-the-connector"></a>Configurer Exchange et SharePoint pour utiliser le connecteur

1. Revenez aux instructions pour le déploiement du connecteur RMS : [Étape 5 : Configuration de serveurs afin d’utiliser le connecteur RMS](../deploy-use/configure-servers-rms-connector.md)

    Si vous ne disposez que de SharePoint Server, accédez directement à [Étapes suivantes](#next-steps) pour poursuivre la migration. 

2. Sur chaque serveur Exchange, ajoutez manuellement les clés de Registre dans la section suivante pour chaque fichier de données de configuration (.xml) que vous avez importé pour rediriger les URL de domaine de publication approuvé vers le connecteur RMS. Ces entrées de Registre sont spécifiques de la migration et ne sont pas ajoutées par l'outil de configuration de serveur pour le connecteur Microsoft RMS.

    Lorsque vous apportez ces modifications au Registre, suivez les instructions suivantes :

    -   Remplacez *FQDN du connecteur* par le nom défini dans DNS pour le connecteur. Par exemple, **rmsconnector.contoso.com**.

    -   Utilisez le préfixe HTTP ou HTTPS pour l'URL du connecteur, selon que vous avez configuré le connecteur pour utiliser le protocole HTTP ou HTTPS pour communiquer avec vos serveurs locaux.

#### <a name="registry-edits-for-exchange"></a>Modifications du Registre pour Exchange

Pour tous les serveurs Exchange, supprimez les valeurs de Registre que vous avez ajoutées pour LicenseServerRedirection pendant la phase de préparation. Ces valeurs ont été ajoutées aux chemins suivants :

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection


Pour Exchange 2013 et Exchange 2016 - Modification du Registre 1 :


**Chemin du Registre :**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**Type :** Reg_SZ

**Valeur :** https://\<URL de licence intranet AD RMS\>/_wmcs/licensing

**Données :**

L'une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur Exchange et votre connecteur RMS :

- http://\<FQDN du connecteur\>/_wmcs/licensing

- https://\<FQDN du connecteur\>/_wmcs/licensing


---

Pour Exchange 2013 - Modification du Registre 2 :

**Chemin du Registre :**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection 

**Type :** Reg_SZ

**Valeur :** https://\<URL de licence extranet AD RMS\>/_wmcs/licensing

**Données :**

L'une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur Exchange et votre connecteur RMS :

- http://\<FQDN du connecteur\>/_wmcs/licensing

- https://\<FQDN du connecteur\>/_wmcs/licensing

---

Pour Exchange 2010 - Modification du Registre 1 :


**Chemin du Registre :**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**Type :** Reg_SZ

**Valeur :** https://\<URL de licence intranet AD RMS\>/_wmcs/licensing

**Données :**

L'une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur Exchange et votre connecteur RMS :

- http://\<FQDN du connecteur\>/_wmcs/licensing

- https://\<Nom du connecteur\>/_wmcs/licensing


---

Pour Exchange 2010 - Modification du Registre 2 :


**Chemin du Registre :**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**Type :** Reg_SZ

**Valeur :** https://\<URL de licence extranet AD RMS\>/_wmcs/licensing

**Données :**

L'une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur Exchange et votre connecteur RMS :

- http://\<FQDN du connecteur\>/_wmcs/licensing

- https://\<FQDN du connecteur\>/_wmcs/licensing

---


## <a name="next-steps"></a>Étapes suivantes
Pour poursuivre la migration, passez à la [Phase 5 - Tâches de post-migration](migrate-from-ad-rms-phase5.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]