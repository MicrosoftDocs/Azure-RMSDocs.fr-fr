---
title: Migrer un déploiement AD RMS vers Azure Information Protection - Phase 4
description: Phase 4 de la migration d’AD RMS vers Azure Information Protection, couvrant les étapes 8 et 9 de la migration d’AD RMS vers Azure Information Protection
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 04/02/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8b039ad5-95a6-4c73-9c22-78c7b0e12cb7
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 01cf998fc6d4c872339d5bfa241eed4f1c9f4b6b
ms.sourcegitcommit: d1f6f10c9cb95de535d8121e90b211f421825caf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87298153"
---
# <a name="migration-phase-4---supporting-services-configuration"></a>Phase de migration 4 : Configuration des services de prise en charge

>*S’applique à : services AD RMS (Active Directory Rights Management Services), [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Utilisez les informations suivantes pour la Phase 4 de la migration d’AD RMS vers Azure Information Protection. Ces procédures couvrent les étapes 8 et 9 de la rubrique [Migration d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

## <a name="step-8-configure-irm-integration-for-exchange-online"></a>Étape 8 : Configurer l'intégration de l'IRM pour Exchange Online

> [!IMPORTANT]
> Du fait que vous n’avez aucun contrôle sur les destinataires que peuvent sélectionner les utilisateurs ayant migré pour les e-mails protégés, veillez à ce que tous les utilisateurs et groupes à extension messagerie de votre organisation disposent d’un compte dans Azure AD pouvant être utilisé avec Azure Information Protection. [Plus d’informations](prepare.md)

Indépendamment de la topologie de la clé du locataire Azure Information Protection que vous avez choisie, effectuez les actions suivantes :

1. Pour qu’Exchange Online puisse déchiffrer les messages électroniques protégés par AD RMS, il doit savoir que l’URL de AD RMS de votre cluster correspond à la clé qui est disponible dans votre locataire. Pour ce faire, la SRV du DNS doit être enregistrée pour votre cluster AD RMS, qui est également utilisé pour reconfigurer les clients Office afin d’utiliser Azure Information Protection. Si vous n’avez pas créé l’enregistrement DNS SRV pour la reconfiguration du client à l’étape 7, créez-le maintenant pour prendre en charge Exchange Online. [Instructions](migrate-from-ad-rms-phase3.md#client-reconfiguration-by-using-dns-redirection)
    
    Quand cet enregistrement DNS est en place, les utilisateurs d’Outlook sur des clients de messagerie web et mobiles peuvent afficher les e-mails protégés par les services AD RMS dans ces applications, et Exchange sera en mesure d’utiliser la clé que vous avez importée à partir d’AD RMS pour déchiffrer, indexer, journaliser et protéger le contenu qui a été protégé par AD RMS.  

2. Exécutez la commande Exchange Online [Get-IRMConfiguration](https://technet.microsoft.com/library/dd776120(v=exchg.160).aspx). Si vous avez besoin d’aide pour exécuter cette commande, consultez les instructions détaillées dans [Exchange Online : Configuration d’IRM](configure-office365.md#exchangeonline-irm-configuration).
    
    Dans la sortie, vérifiez si **AzureRMSLicensingEnabled** a la valeur **True**:
    
    - Si AzureRMSLicensingEnabled a la valeur **True**, aucune configuration supplémentaire n’est nécessaire pour cette étape. 
    
    - Si AzureRMSLicensingEnabled a la valeur **False**, exécutez `Set-IRMConfiguration -AzureRMSLicensingEnabled $true`, puis utilisez les étapes de vérification de [Configurer les nouvelles fonctionnalités de chiffrement de messages Office 365 reposant sur Azure Information Protection](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e) pour confirmer qu’Exchange Online est maintenant prêt à utiliser le service Azure Rights Management. 

## <a name="step-9-configure-irm-integration-for-exchange-server-and-sharepoint-server"></a>Étape 9. Configurer l’intégration d’IRM pour Exchange Server et SharePoint Server

Si vous avez utilisé la fonctionnalité IRM (Gestion des droits relatifs à l'information) d’Exchange Server ou de SharePoint Server avec AD RMS, vous devez déployer le connecteur RMS (Rights Management), qui fait office d’interface de communication (de relais) entre vos serveurs locaux et le service de protection pour Azure Information Protection.

Cette étape aborde l’installation et la configuration du connecteur, la désactivation d’IRM pour Exchange et SharePoint, ainsi que la configuration de ces serveurs pour utiliser le connecteur. Enfin, si vous avez importé des fichiers de configuration de données (.xml) AD RMS dans Azure Information Protection qui ont été utilisés pour protéger des e-mails, vous devez modifier manuellement le Registre sur les ordinateurs Exchange Server pour rediriger toutes les URL de domaine de publication approuvé vers le connecteur RMS.

> [!NOTE]
> Avant de commencer, vérifiez les versions des serveurs locaux prises en charge par le service Azure Rights Management, dans [Serveurs locaux prenant en charge Azure RMS](requirements.md#supported-on-premises-servers-for-azure-rights-management-data-protection).

### <a name="install-and-configure-the-rms-connector"></a>Installation et configuration du connecteur RMS

Suivez les instructions de l’article [Déploiement du connecteur Azure Rights Management](./deploy-rms-connector.md) et effectuez les étapes 1 à 4. Ne démarrez pas encore l’étape 5 à partir des instructions du connecteur.

### <a name="disable-irm-on-exchange-servers-and-remove-ad-rms-configuration"></a>Désactivation de l'IRM sur les serveurs Exchange et suppression de la configuration AD RMS

> [!IMPORTANT]
> Si vous n’avez pas encore configuré IRM sur l’un de vos serveurs Exchange, effectuez simplement les étapes 2 et 6.
> 
> Effectuez toutes ces étapes si toutes les URL de licence de tous vos clusters de AD RMS ne sont pas affichées dans le paramètre *LicensingLocation* lorsque vous exécutez la méthode [IRMConfiguration](https://docs.microsoft.com/powershell/module/exchange/encryption-and-certificates/get-irmconfiguration?view=exchange-ps).

1. Sur chaque serveur Exchange, recherchez le dossier suivant, puis supprimez toutes ses entrées : **\ProgramData\Microsoft\DRM\Server\S-1-5-18**

2. À partir de l’un des serveurs Exchange, exécutez les commandes PowerShell suivantes pour vérifier que les utilisateurs seront en mesure de lire les e-mails qui sont protégés à l’aide d’Azure Rights Management.

    Avant d’exécuter ces commandes, remplacez par votre propre URL du service Azure Rights Management *\<Your Tenant URL>* .

    ```ps
    $irmConfig = Get-IRMConfiguration
    $list = $irmConfig.LicensingLocation 
    $list += "<Your Tenant URL>/_wmcs/licensing"
    Set-IRMConfiguration -LicensingLocation $list
    ```

    Désormais, lorsque vous exécutez la [IRMConfiguration](https://docs.microsoft.com/powershell/module/exchange/encryption-and-certificates/get-irmconfiguration?view=exchange-ps), vous devriez voir toutes vos URL de licence de cluster AD RMS et votre URL de service Azure Rights Management affichées pour le paramètre *LicensingLocation* .

3.  Désactivez maintenant les fonctionnalités IRM pour les messages envoyés à des destinataires internes :

    ```ps
    Set-IRMConfiguration -InternalLicensingEnabled $false
    ```

4. Utilisez ensuite la même cmdlet pour désactiver IRM dans Microsoft Office Outlook Web App et dans Microsoft Exchange ActiveSync :

    ```ps
    Set-IRMConfiguration -ClientAccessServerEnabled $false
    ```

5.  Enfin, utilisez la même applet de commande pour effacer les certificats mis en cache :

    ```ps
    Set-IRMConfiguration -RefreshServerCertificates
    ```

6.  Sur chaque serveur Exchange, réinitialisez IIS, par exemple, en exécutant une invite de commandes en tant qu'administrateur et en tapant **iisreset**.

### <a name="disable-irm-on-sharepoint-servers-and-remove-ad-rms-configuration"></a>Désactivation d'IRM sur les serveurs SharePoint et suppression de la configuration AD RMS

1.  Assurez-vous qu'aucun document n'est extrait des bibliothèques protégées par RMS. Les documents extraits deviendront inaccessibles à la fin de cette procédure.

2.  Sur le site web Administration centrale de SharePoint, dans la section **Lancement rapide**, cliquez sur **Sécurité**.

3.  Dans la page **Sécurité**, dans la section **Stratégie d'information**, cliquez sur **Configurer la gestion des droits relatifs à l'information**.

4.  Dans la page **Gestion des droits relatifs à l'information**, dans la section **Gestion des droits relatifs à l'information**, sélectionnez **Ne pas utiliser IRM sur ce serveur**, puis cliquez sur **OK**.

5.  Sur chaque ordinateur SharePoint Server, supprimez le contenu du dossier \ProgramData\Microsoft\MSIPC\Server\\<*SID du compte exécutant SharePoint Server>*.

### <a name="configure-exchange-and-sharepoint-to-use-the-connector"></a>Configurer Exchange et SharePoint pour utiliser le connecteur

1. Revenez aux instructions pour le déploiement du connecteur RMS : [Étape 5 : Configuration de serveurs afin d’utiliser le connecteur RMS](./configure-servers-rms-connector.md)

    Si vous ne disposez que de SharePoint Server, accédez directement à [Étapes suivantes](#next-steps) pour poursuivre la migration. 

2. Sur chaque serveur Exchange, ajoutez manuellement les clés de Registre dans la section suivante pour chaque fichier de données de configuration (.xml) que vous avez importé pour rediriger les URL de domaine de publication approuvé vers le connecteur RMS. Ces entrées de Registre sont spécifiques de la migration et ne sont pas ajoutées par l'outil de configuration de serveur pour le connecteur Microsoft RMS.

    Lorsque vous apportez ces modifications au Registre, suivez les instructions suivantes :

    -   Remplacez *FQDN du connecteur* par le nom défini dans DNS pour le connecteur. Par exemple, **rmsconnector.contoso.com**.

    -   Utilisez le préfixe HTTP ou HTTPS pour l'URL du connecteur, selon que vous avez configuré le connecteur pour utiliser le protocole HTTP ou HTTPS pour communiquer avec vos serveurs locaux.

#### <a name="registry-edits-for-exchange"></a>Modifications du Registre pour Exchange

Pour tous les serveurs Exchange, ajoutez les valeurs de registre suivantes pour LicenseServerRedirection, selon les versions d’Exchange :

---

Pour Exchange 2013 et Exchange 2016 - Modification du Registre 1 :


**Chemin du Registre :**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**Tapez :** Reg_SZ

**Valeur :** https:// \<AD RMS Intranet Licensing URL\> /_wmcs/Licensing

**Métadonnée**

L'une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur Exchange et votre connecteur RMS :

- http://\<connector FQDN\>/_wmcs/licensing

- https://\<connector FQDN\>/_wmcs/licensing


---

Exchange 2013 – modification du registre 2 :

**Chemin du Registre :**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection 

**Tapez :** Reg_SZ

**Valeur :** https:// \<AD RMS Extranet Licensing URL\> /_wmcs/Licensing

**Métadonnée**

L'une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur Exchange et votre connecteur RMS :

- http://\<connector FQDN\>/_wmcs/licensing

- https://\<connector FQDN\>/_wmcs/licensing

---

Pour Exchange 2010 - Modification du Registre 1 :


**Chemin du Registre :**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**Tapez :** Reg_SZ

**Valeur :** https:// \<AD RMS Intranet Licensing URL\> /_wmcs/Licensing

**Métadonnée**

L'une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur Exchange et votre connecteur RMS :

- http://\<connector FQDN\>/_wmcs/licensing

- https://\<connector Name\>/_wmcs/licensing


---

Pour Exchange 2010 - Modification du Registre 2 :


**Chemin du Registre :**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**Tapez :** Reg_SZ

**Valeur :** https:// \<AD RMS Extranet Licensing URL\> /_wmcs/Licensing

**Métadonnée**

L'une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur Exchange et votre connecteur RMS :

- http://\<connector FQDN\>/_wmcs/licensing

- https://\<connector FQDN\>/_wmcs/licensing

---


## <a name="next-steps"></a>Étapes suivantes
Pour poursuivre la migration, passez à la [Phase 5 - Tâches de post-migration](migrate-from-ad-rms-phase5.md).
