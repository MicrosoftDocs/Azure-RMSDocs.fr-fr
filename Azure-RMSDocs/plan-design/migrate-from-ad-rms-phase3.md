---
title: "Migration d’AD RMS vers Azure Information Protection - Phase 3 | Azure Information Protection"
description: "Phase 3 de la migration d’AD RMS vers Azure Information Protection, couvrant les étapes 6 et 7 de la migration d’AD RMS vers Azure Information Protection"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8b039ad5-95a6-4c73-9c22-78c7b0e12cb7
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f1bf7377e5e8079025dff638a185c825256a5cc7
ms.openlocfilehash: fba8e46993e414fe63414f7240779f5939166c4a


---

# <a name="migration-phase-3-supporting-services-configuration"></a>Phase de migration 3 : Configuration des services de prise en charge

>*S’applique à : Services AD RMS, Azure Information Protection, Office 365*


Utilisez les informations suivantes pour la Phase 3 de la migration d’AD RMS vers Azure Information Protection. Ces procédures couvrent les étapes 6 et 7 de la rubrique [Migration d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).


## <a name="step-6-configure-irm-integration-for-exchange-online"></a>Étape 6. Configurer l'intégration de l'IRM pour Exchange Online

Si vous avez précédemment importé votre TDP d’AD RMS dans Exchange Online, vous devez supprimer cette TDP pour éviter des conflits de modèles et de stratégies après la migration vers Azure Information Protection. Pour ce faire, utilisez l’applet de commande [Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/library/jj200720%28v=exchg.150%29.aspx) d’Exchange Online.

Si vous avez choisi une topologie de clé de locataire Azure Information Protection **Gérée par Microsoft** :

-   Consultez la section [Exchange Online : configuration d’IRM](../deploy-use/configure-office365.md#exchange-online-irm-configuration) de l’article [Office 365 : Configuration pour les clients et les services en ligne](../deploy-use/configure-office365.md). Cette section inclut des commandes spécifiques à exécuter, qui établissent une connexion au service Exchange Online, importent la clé de locataire à partir d’Azure Information Protection, puis activent les fonctionnalités IRM (Gestion des droits relatifs à l’information) pour Exchange Online. Après avoir effectué ces étapes, vous disposez de toutes les fonctionnalités de la protection Azure Rights Management avec Exchange Online.

Si vous avez choisi une topologie de clé de locataire Azure Information Protection **Gérée par le client (BYOK)** :

-   Vous disposez de fonctionnalités de protection Rights Management réduites avec Exchange Online, comme décrit dans l’article [Tarifs et restrictions BYOK](byok-price-restrictions.md).

## <a name="step-7-deploy-the-rms-connector"></a>Étape 7. Déployer le connecteur RMS
Si vous avez utilisé la fonctionnalité Information Rights Management (IRM) d'Exchange Server ou de SharePoint Server avec AD RMS, vous devez d'abord désactiver l'IRM sur ces serveurs, puis supprimer la configuration AD RMS. Ensuite, déployez le connecteur Rights Management (RMS), qui fait office d’interface de communication (relais) entre les serveurs locaux et le service de protection pour Azure Information Protection.

Enfin, pour cette étape, si vous avez importé plusieurs fichiers de configuration de données (.xml) AD RMS dans Azure Information Protection qui ont été utilisés pour protéger des e-mails, vous devez modifier manuellement le Registre sur les ordinateurs Exchange Server pour rediriger toutes les URL de domaine de publication approuvé vers le connecteur RMS.

> [!NOTE]
> Avant de commencer, vérifiez les versions des serveurs locaux prises en charge par le service Azure Rights Management, dans [Serveurs locaux prenant en charge Azure RMS](../get-started/requirements-servers.md).

### <a name="disable-irm-on-exchange-servers-and-remove-ad-rms-configuration"></a>Désactivation de l'IRM sur les serveurs Exchange et suppression de la configuration AD RMS

1.  Sur chaque serveur Exchange, recherchez le dossier suivant, puis supprimez toutes ses entrées : \ProgramData\Microsoft\DRM\Server\S-1-5-18

2.  Sur l'un des serveurs Exchange, commencez par utiliser l'applet de commande [Set_IRMConfiguration](http://technet.microsoft.com/library/dd979792.aspx) pour désactiver les fonctionnalités de l'IRM pour les messages envoyés à des destinataires internes :

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $false
    ```

3.  Puis, utilisez la même applet de commande pour désactiver les fonctionnalités IRM pour les messages envoyés à des destinataires externes :

    ```
    Set-IRMConfiguration -ExternalLicensingEnabled $false
    ```

4.  Ensuite, utilisez la même applet de commande pour désactiver IRM dans Microsoft Office Outlook Web App et dans Microsoft Exchange ActiveSync :

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

5.  Sur chaque ordinateur SharePoint Server, supprimez le contenu du dossier \ProgramData\Microsoft\MSIPC\Server\*&lt;SID du compte exécutant SharePoint Server&gt;*.

#### <a name="install-and-configure-the-rms-connector"></a>Installation et configuration du connecteur RMS

-   Suivez les instructions de l’article [Déploiement du connecteur Azure Rights Management](../deploy-use/deploy-rms-connector.md).

#### <a name="for-exchange-only-and-multiple-tpds-edit-the-registry"></a>Pour Exchange uniquement et plusieurs TPD : modifier le Registre

-   Sur chaque serveur Exchange, ajoutez manuellement les clés de Registre suivantes pour chaque fichier de configuration de données (.xml) que vous avez importé pour rediriger les URL de domaine de publication approuvé vers le connecteur RMS. Ces entrées de Registre sont spécifiques de la migration et ne sont pas ajoutées par l'outil de configuration de serveur pour le connecteur Microsoft RMS.

    Lorsque vous apportez ces modifications au Registre, suivez les instructions suivantes :

    -   Remplacez *ConnectorFQDN* par le nom défini dans le DNS pour le connecteur. Par exemple, **rmsconnector.contoso.com**.

    -   Utilisez le préfixe HTTP ou HTTPS pour l'URL du connecteur, selon que vous avez configuré le connecteur pour utiliser le protocole HTTP ou HTTPS pour communiquer avec vos serveurs locaux.

Pour Exchange 2013 - Modification du Registre 1 :


**Chemin du Registre :**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**Type :**

Reg_SZ

**Valeur :**

https://<AD RMS Intranet Licensing URL>/_wmcs/licensing

**Données :**

L'une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur Exchange et votre connecteur RMS :

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorName>/_wmcs/licensing


---

Pour Exchange 2013 - Modification du Registre 2 :

**Chemin du Registre :**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection 


**Type :**

Reg_SZ

**Valeur :**

https://<AD RMS Extranet Licensing URL>/_wmcs/licensing


**Données :**

L'une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur Exchange et votre connecteur RMS :

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorFQDN>/_wmcs/licensing

---

Pour Exchange 2010 - Modification du Registre 1 :



**Chemin du Registre :**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**Type :**

Reg_SZ

**Valeur :**

https://<AD RMS Intranet Licensing URL>/_wmcs/licensing

**Données :**

L'une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur Exchange et votre connecteur RMS :

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorName>/_wmcs/licensing


---

Pour Exchange 2010 - Modification du Registre 2 :


**Chemin du Registre :**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection
 

**Type :**

Reg_SZ

**Valeur :**

https://<AD RMS Extranet Licensing URL>/_wmcs/licensing


**Données :**

L'une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur Exchange et votre connecteur RMS :

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorFQDN>/_wmcs/licensing

---

Une fois ces procédures terminées, vous pouvez lire la section **Étapes suivantes** de l’article [Déploiement du connecteur Azure Rights Management](../deploy-use/deploy-rms-connector.md).

## <a name="next-steps"></a>Étapes suivantes
Pour poursuivre la migration, passez à la [Phase 4 - Tâches de post-migration](migrate-from-ad-rms-phase4.md).


<!--HONumber=Nov16_HO2-->


