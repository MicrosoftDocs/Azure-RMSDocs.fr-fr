---
title: Configurer Exchange Online IRM pour le service Azure Rights Management d’Azure Information Protection
description: Informations et instructions permettant aux administrateurs de configurer Exchange Online pour le service Azure Rights Management quand le locataire Office 365 ne prend pas en charge les nouvelles fonctionnalités du chiffrement de messages Office 365.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/11/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ''
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: e452f5ac4e3297106a54a2034d64f57d8f6d5302
ms.sourcegitcommit: affda7572064edaf9e3b63d88f4a18d0d6932b13
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/16/2018
---
# <a name="exchange-online-irm-configuration-to-import-a-trusted-publishing-domain"></a>Configuration d’Exchange Online IRM pour importer un domaine de publication approuvé

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Utilisez ces instructions uniquement si votre locataire n’est pas en mesure d’utiliser les nouvelles fonctionnalités de chiffrement de messages Office 365. Pour confirmer, exécutez la commande Exchange Online [Get-IRMConfiguration] (https://technet.microsoft.com/library/dd776120(v=exchg.160\).aspx) et vérifiez si vous disposez d’un paramètre **AzureRMSLicensingEnabled**. Si vous voyez ce paramètre, votre locataire peut utiliser les nouvelles fonctionnalités de chiffrement de messages Office 365 :

- Si **AzureRMSLicensingEnabled** a la valeur **True**, votre locataire utilise déjà les nouvelles fonctionnalités de chiffrement de messages Office 365 ; vous ne devez donc pas utiliser les instructions indiquées dans la section suivante.

- Si **AzureRMSLicensingEnabled** a la valeur **False**, votre locataire prend en charge les nouvelles fonctionnalités de chiffrement de messages Office 365, mais n’est pas encore configuré à cette fin. Pour configurer votre locataire pour ces nouvelles fonctionnalités, consultez [Configurer de nouvelles fonctionnalités de chiffrement de messages Office 365 reposant sur Azure Information Protection](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e). 

N’utilisez les instructions qui suivent que si votre locataire ne peut pas prendre en charge les nouvelles fonctionnalités de chiffrement de messages Office 365.

## <a name="exchange-online-irm-configuration"></a>Configuration de la gestion des droits relatifs à l’information Exchange Online

Pour configurer la gestion des droits relatifs à l’information Exchange Online, utilisez Windows PowerShell (inutile d’installer un module séparé) et exécutez des [commandes PowerShell pour Exchange Online](https://technet.microsoft.com/library/jj200677.aspx).

> [!NOTE]
> Tant que Microsoft n’a pas migré votre locataire Office 365 pour qu’il prenne en charge les nouvelles fonctionnalités, vous ne pouvez pas configurer Exchange Online pour prendre en charge le service Azure Rights Management si vous utilisez une clé de locataire gérée par le client (BYOK) pour Azure Information Protection au lieu de la configuration par défaut d’une clé de locataire gérée par Microsoft.
>
> Si vous essayez de configurer Exchange Online quand le service Azure Rights Management utilise BYOK, la commande pour importer la clé (étape 5, dans la procédure suivante) échoue avec le message d’erreur **[FailureCategory=Cmdlet-FailedToGetTrustedPublishingDomainFromRmsOnlineException]**.

Les étapes suivantes décrivent un ensemble spécifique de commandes à exécuter pour activer la gestion des droits relatifs à l’information Exchange Online :

1.  Si vous n'avez jamais utilisé Windows PowerShell pour Exchange Online sur votre ordinateur, vous devez configurer Windows PowerShell pour exécuter des scripts signés. Démarrez votre session Windows PowerShell à l'aide de l'option **Exécuter en tant qu'administrateur** , puis tapez :

    ```
    Set-ExecutionPolicy RemoteSigned
    ```

2.  Dans votre session Windows PowerShell, connectez-vous à Exchange Online à l'aide d'un compte activé pour l'accès aux environnements distants. Par défaut, tous les comptes créés dans Exchange Online sont activés pour l’accès aux environnements distants, mais il est possible de les désactiver (et activer) à l’aide de la commande [Set-User &lt;identité_utilisateur&gt; -RemotePowerShellEnabled](https://technet.microsoft.com/library/jj984292%28v=exchg.160%29.aspx).

    Pour vous connecter, tapez :

    ```
    $UserCredential = Get-Credential
    ```
    Dans la boîte de dialogue **Demande d'informations d'identification Windows PowerShell** , entrez vos nom d'utilisateur et mot de passe Office 365.

3.  Connectez-vous au service Exchange Online en exécutant les deux commandes suivantes :

    ```
    $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection
    ```

    ```
    Import-PSSession $Session
    ```

4.  Spécifiez l’emplacement de la clé de locataire Azure Information Protection, selon l’emplacement où le locataire de votre organisation a été créé :

    Pour l'Amérique du Nord :

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.na.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    Pour l'Europe :

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.eu.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    Pour l'Asie :

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.ap.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    Pour l'Amérique du Sud :

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.sa.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    Pour Office 365 Secteur Public (cloud de la communauté Secteur Public) :

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.govus.aadrm.com/TenantManagement/ServicePartner.svc"
    ```

5.  Importez les données de configuration du service Azure Rights Management dans Exchange Online, sous la forme du domaine de publication approuvé (TPD). Cela inclut la clé de locataire Azure Information Protection et les modèles Azure Rights Management :

    ```
    Import-RMSTrustedPublishingDomain -RMSOnline -name "RMS Online"
    ```
    Dans cette commande, nous avons utilisé le nom **RMS Online** comme nom de base du TPD pour Azure Rights Management dans Exchange Online. Une fois le TPD importé, il est nommé **RMS Online - 1** dans Exchange Online.

6.  Activez la fonctionnalité Azure Rights Management afin que les fonctionnalités IRM soient disponibles pour Exchange Online :

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $true
    ```
    Après l'exécution de cette commande, Rights Management est automatiquement activé pour le client Outlook, Outlook Web App et Exchange Active Sync.

7.  Vous pouvez également tester la réussite de cette configuration à l'aide de la commande suivante :

    ```
    Test-IRMConfiguration -Sender <user email address>
    ```
    Par exemple : **Test-IRMConfiguration -Sender  adams@contoso.com**

    Cette commande exécute une série de vérifications qui inclut la vérification de la connectivité au service, l'extraction de la configuration, ainsi que l'extraction d'URI, de licences et de modèles. La session Windows PowerShell indique les résultats de chaque vérification et, à la fin, si tous les contrôles ont été concluants : **OVERALL RESULT: PASS**

8.  Déconnectez votre session PowerShell distante :

    ```
    Remove-PSSession $Session
    ```

Les utilisateurs peuvent maintenant protéger leurs e-mails en utilisant le service Azure Rights Management. Par exemple, dans Outlook Web App, dans le menu étendu, sélectionnez **Définir les autorisations** (**...**), puis choisissez **Ne pas transférer** ou un des modèles disponibles pour appliquer la protection des informations au message e-mail et aux éventuelles pièces jointes. Toutefois, étant donné qu'Outlook Web App met en cache l'interface utilisateur pendant une journée, attendez l'expiration de cette période avant de tenter d'appliquer la protection des informations au messages électroniques après avoir exécuté ces commandes de configuration. Tant que l'interface utilisateur n'a pas été actualisée pour refléter la nouvelle configuration, aucune option du menu **Définir les autorisations** n'est visible.

> [!IMPORTANT]
> Si vous créez des [modèles personnalisés](configure-custom-templates.md) pour Azure Rights Management ou mettez à jour les modèles, vous devez chaque fois exécuter la commande Exchange Online PowerShell suivante (si nécessaire, exécutez d’abord les étapes 2 et 3) pour synchroniser ces modifications sur Exchange Online : `Import-RMSTrustedPublishingDomain -Name "RMS Online - 1" -RefreshTemplates –RMSOnline`

En tant qu’administrateur Exchange, vous pouvez maintenant configurer des fonctionnalités qui appliquent automatiquement la protection des informations, telles que les [règles de transport](https://technet.microsoft.com/library/dd302432.aspx), les [stratégies de protection contre la perte des données (DLP)](https://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx) et la [messagerie vocale protégée](https://technet.microsoft.com/library/dn198211%28v=exchg.150%29.aspx) (messagerie unifiée).


### <a name="office-365-message-encryption"></a>Chiffrement de messages Office 365
Exécutez les étapes décrites dans la section précédente mais, si vous ne voulez pas que les modèles soient affichés, avant l’étape 6, exécutez la commande suivante pour empêcher que les modèles IRM soient disponibles dans Outlook Web App et le client Outlook : `Set-IRMConfiguration -ClientAccessServerEnabled $false`

Ensuite, vous êtes prêt à configurer les [règles de transport](https://technet.microsoft.com/library/dd302432.aspx) pour modifier automatiquement la sécurité des messages quand les destinataires sont situés en dehors de l'organisation, puis sélectionnez l'option **Appliquer le chiffrement des messages Office 365** .

Pour plus d'informations sur le chiffrement des messages, consultez [Chiffrement dans Office 365](https://technet.microsoft.com/library/dn569286.aspx) dans la bibliothèque Exchange.


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
