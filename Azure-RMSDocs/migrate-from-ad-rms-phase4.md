---
title: Migrer un déploiement AD RMS vers Azure Information Protection - Phase 4
description: Phase 4 de la migration d’AD RMS vers Azure Information Protection, couvrant les étapes 8 et 9 de la migration d’AD RMS vers Azure Information Protection
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/26/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8b039ad5-95a6-4c73-9c22-78c7b0e12cb7
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: e7431ebdf016b89e1750b833dc4fca2d9646b195
ms.sourcegitcommit: d31cb53de64bafa2097e682550645cadc612ec3e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/30/2020
ms.locfileid: "96316719"
---
# <a name="migration-phase-4---supporting-services-configuration"></a>Phase de migration 4 : Configuration des services de prise en charge

>*S’applique à : services AD RMS (Active Directory Rights Management Services), [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Utilisez les informations suivantes pour la Phase 4 de la migration d’AD RMS vers Azure Information Protection. Ces procédures couvrent les étapes 8 et 9 de la rubrique [Migration d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

## <a name="step-8-configure-irm-integration-for-exchange-online"></a>Étape 8 : Configurer l'intégration de l'IRM pour Exchange Online

> [!IMPORTANT]
> Vous ne pouvez pas contrôler les destinataires que les utilisateurs migrés peuvent sélectionner pour les e-mails protégés.
>
> Par conséquent, assurez-vous que tous les utilisateurs et groupes à extension messagerie de votre organisation ont un compte dans Azure AD qui peut être utilisé avec Azure Information Protection.
>
> Pour plus d’informations, consultez [Préparation des utilisateurs et groupes pour Azure Information Protection](prepare.md).

Quelle que soit la topologie de clé de locataire Azure Information Protection que vous avez choisie, procédez comme suit :

1. **Condition préalable**: pour qu’Exchange Online puisse déchiffrer les messages électroniques protégés par AD RMS, il doit savoir que l’URL de AD RMS de votre cluster correspond à la clé qui est disponible dans votre locataire. 

    Pour ce faire, la SRV du DNS doit être enregistrée pour votre cluster AD RMS, qui est également utilisé pour reconfigurer les clients Office afin d’utiliser Azure Information Protection. 

    Si vous n’avez pas créé l’enregistrement DNS SRV pour la reconfiguration du client à l' [étape 7](migrate-from-ad-rms-phase3.md#step-7-reconfigure-windows-computers-to-use-azure-information-protection), créez-le maintenant pour prendre en charge Exchange Online. [Instructions](migrate-from-ad-rms-phase3.md#client-reconfiguration-by-using-dns-redirection)
    
    Quand cet enregistrement DNS est en place, les utilisateurs d’Outlook sur des clients de messagerie web et mobiles peuvent afficher les e-mails protégés par les services AD RMS dans ces applications, et Exchange sera en mesure d’utiliser la clé que vous avez importée à partir d’AD RMS pour déchiffrer, indexer, journaliser et protéger le contenu qui a été protégé par AD RMS.  

1. **Exécutez la commande Exchange Online [-IRMConfiguration](/powershell/module/exchange/get-irmconfiguration) .** 

    Si vous avez besoin d’aide pour exécuter cette commande, consultez les instructions détaillées dans [Exchange Online : Configuration d’IRM](configure-office365.md#exchangeonline-irm-configuration).
    
    Dans la sortie, vérifiez si **AzureRMSLicensingEnabled** a la valeur **True**:
    
    - Si **AzureRMSLicensingEnabled** a la valeur **true**, aucune autre configuration n’est nécessaire pour cette étape. 
    
    - Si **AzureRMSLicensingEnabled** a la valeur **false**, exécutez, `Set-IRMConfiguration -AzureRMSLicensingEnabled $true` puis vérifiez qu’Exchange Online est prêt à utiliser le service Azure Rights Management. 
    
        Pour plus d’informations, consultez les étapes de vérification de la section [configurer de nouvelles Microsoft 365 fonctionnalités de chiffrement de message basées sur Azure information protection](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e).

## <a name="step-9-configure-irm-integration-for-exchange-server-and-sharepoint-server"></a>Étape 9. Configurer l’intégration d’IRM pour Exchange Server et SharePoint Server

Si vous avez utilisé la fonctionnalité d’informations Rights Management (IRM) d’Exchange Server ou de SharePoint Server avec AD RMS, vous devrez déployer le connecteur Rights Management (RMS).

Le connecteur agit comme une interface de communication (relais) entre vos serveurs locaux et le service de protection pour Azure Information Protection.

Cette étape aborde l’installation et la configuration du connecteur, la désactivation d’IRM pour Exchange et SharePoint, ainsi que la configuration de ces serveurs pour utiliser le connecteur. 

Enfin, si vous avez importé des fichiers de configuration de données AD RMS. XML qui ont été utilisés pour protéger les messages électroniques dans à Azure Information Protection, vous devez modifier manuellement le registre sur les ordinateurs Exchange Server pour rediriger toutes les URL trusted publishing domain vers le connecteur RMS.

> [!NOTE]
> Avant de commencer, vérifiez les versions des serveurs locaux prises en charge par le service Azure Rights Management, dans [Serveurs locaux prenant en charge Azure RMS](requirements.md#supported-on-premises-servers-for-azure-rights-management-data-protection).

### <a name="install-and-configure-the-rms-connector"></a>Installation et configuration du connecteur RMS

Suivez les instructions de l’article [déploiement du connecteur Azure Rights Management](./deploy-rms-connector.md) et effectuez les étapes 1 à 4. 

Ne démarrez pas encore l’étape 5 à partir des instructions du connecteur.

### <a name="disable-irm-on-exchange-servers-and-remove-ad-rms-configuration"></a>Désactivation de l'IRM sur les serveurs Exchange et suppression de la configuration AD RMS

> [!IMPORTANT]
> Si vous n’avez pas encore configuré IRM sur l’un de vos serveurs Exchange, effectuez simplement les étapes 2 et 6.
> 
> Effectuez toutes ces étapes si toutes les URL de licence de tous vos clusters de AD RMS ne sont pas affichées dans le paramètre *LicensingLocation* lorsque vous exécutez la méthode [IRMConfiguration](/powershell/module/exchange/encryption-and-certificates/get-irmconfiguration).

1. Sur chaque serveur Exchange, recherchez le dossier suivant, puis supprimez toutes ses entrées : **\ProgramData\Microsoft\DRM\Server\S-1-5-18**

2. À partir de l’un des serveurs Exchange, exécutez les commandes PowerShell suivantes pour vérifier que les utilisateurs seront en mesure de lire les e-mails qui sont protégés à l’aide d’Azure Rights Management.

    Avant d’exécuter ces commandes, remplacez par votre propre URL du service Azure Rights Management *\<Your Tenant URL>* .

    ```PowerShell
    $irmConfig = Get-IRMConfiguration
    $list = $irmConfig.LicensingLocation 
    $list += "<Your Tenant URL>/_wmcs/licensing"
    Set-IRMConfiguration -LicensingLocation $list
    ```

    Désormais, lorsque vous exécutez la [IRMConfiguration](/powershell/module/exchange/encryption-and-certificates/get-irmconfiguration), vous devriez voir toutes vos URL de licence de cluster AD RMS et votre URL de service Azure Rights Management affichées pour le paramètre *LicensingLocation* .

3.  Désactivez maintenant les fonctionnalités IRM pour les messages envoyés à des destinataires internes :

    ```PowerShell
    Set-IRMConfiguration -InternalLicensingEnabled $false
    ```

4. Utilisez ensuite la même applet de commande pour désactiver IRM dans Microsoft Office Outlook Web App et dans Microsoft Exchange ActiveSync :

    ```PowerShell
    Set-IRMConfiguration -ClientAccessServerEnabled $false
    ```

5.  Enfin, utilisez la même applet de commande pour effacer les certificats mis en cache :

    ```PowerShell
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

1. Pour **exchange 2013 et exchange 2016,** ajoutez la valeur de Registre suivante :

    - **Chemin du Registre :**`HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection`

    - **Tapez :** Reg_SZ

    - **Valeur :** `https://\<AD RMS Intranet Licensing URL\>/_wmcs/licensing`

    - **Données :** L’une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur Exchange et votre connecteur RMS :

        - `http://\<connector FQDN\>/_wmcs/licensing`
        
        - `https://\<connector FQDN\>/_wmcs/licensing`

1. Pour Exchange 2013, ajoutez la valeur de Registre supplémentaire suivante :

    - **Chemin du Registre :**`HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection` 

    - **Tapez :** Reg_SZ

    - **Valeur :** https:// \<AD RMS Extranet Licensing URL\> /_wmcs/Licensing

    - **Données :** L’une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur Exchange et votre connecteur RMS :

        - `http://\<connector FQDN\>/_wmcs/licensing`

        - `https://\<connector FQDN\>/_wmcs/licensing`

## <a name="next-steps"></a>Étapes suivantes
Pour poursuivre la migration, passez à la [Phase 5 - Tâches de post-migration](migrate-from-ad-rms-phase5.md).