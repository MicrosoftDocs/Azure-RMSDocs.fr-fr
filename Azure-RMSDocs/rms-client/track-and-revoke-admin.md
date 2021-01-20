---
title: Suivre et révoquer l’accès-Azure Information Protection
description: Décrit comment les administrateurs peuvent suivre l’accès aux documents pour les documents protégés, ainsi que révoquer l’accès si nécessaire.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 01/20/2021
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 643c762e-23ca-4b02-bc39-4e3eeb657a1d
ms.subservice: doctrack
ms.reviewer: esaggese
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 935e6a3439a06887a91981cb8ed69a342172b686
ms.sourcegitcommit: 99a58f50b08abc546073657c66247553faeecf8b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/20/2021
ms.locfileid: "98608619"
---
# <a name="administrator-guide-track-and-revoke-document-access-with-azure-information-protection-public-preview"></a>Guide de l’administrateur : suivre et révoquer l’accès aux documents avec Azure Information Protection (version préliminaire publique)

>***S’applique à**: [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8 *
>
>***Concerne**: [client d’étiquetage unifié AIP uniquement](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Pour le client Classic, consultez [le Guide de l’administrateur : configuration et utilisation du suivi des documents pour AIP à l’aide du client classique](client-admin-guide-document-tracking.md). *

Si vous avez effectué une mise à niveau vers la [version 2.9.111.0](unifiedlabelingclient-version-release-history.md#version-291110) ou ultérieure, tous les documents protégés qui ne sont pas encore enregistrés pour le suivi sont automatiquement enregistrés la prochaine fois qu’ils sont ouverts via le client d’étiquetage unifié AIP. Les documents protégés sont pris en charge pour la suivi et la révocation, même s’ils ne sont pas étiquetés.

L’inscription d’un document pour le suivi permet à [Microsoft 365 administrateurs généraux](/microsoft-365/admin/add-users/about-admin-roles#commonly-used-microsoft-365-admin-center-roles) de suivre les détails de l’accès, y compris les événements d’accès réussis et les tentatives refusées, ainsi que de révoquer l’accès si nécessaire. 

Les fonctionnalités Track et REVOKE du client d’étiquetage unifié sont actuellement en version préliminaire. Les [Conditions d’utilisation supplémentaires des préversions Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) incluent des conditions légales supplémentaires qui s’appliquent aux fonctionnalités Azure en version bêta, en préversion ou pas encore disponibles dans la version en disponibilité générale. 

## <a name="track-document-access"></a>Suivre l’accès aux documents

Les administrateurs généraux peuvent suivre l’accès aux documents protégés via PowerShell à l’aide du **contentid** généré pour le document protégé pendant l’inscription.

**Pour afficher les détails de l’accès au document**:

Utilisez les applets de commande suivantes pour rechercher les détails du document dont vous souhaitez effectuer le suivi :

1. Recherchez la valeur **contentid** pour le document dont vous souhaitez effectuer le suivi.
    
    Utilisez la [AipServiceDocumentLog](/powershell/module/aipservice/get-aipservicedocumentlog) pour rechercher un document à l’aide du nom de fichier et/ou de l’adresse de messagerie de l’utilisateur qui a appliqué la protection.
    
    Par exemple :
        
    ```PowerShell
    Get-AipServiceDocumentLog -ContentName "test.docx" -Owner “alice@contoso.com” -FromTime "12/01/2020 00:00:00" -ToTime "12/31/2020 23:59:59"
    ```
 
    Cette commande retourne le **contentid** pour tous les documents de correspondance et protégés qui sont inscrits pour le suivi.

    > [!NOTE]
    > Les documents protégés sont enregistrés pour le suivi lorsqu’ils sont ouverts pour la première fois sur un ordinateur sur lequel le client d’étiquetage unifié est installé. Si cette commande ne retourne pas le ContentID pour votre fichier protégé, ouvrez-le sur un ordinateur sur lequel le client d’étiquetage unifié est installé pour inscrire le document à des fins de suivi.

1. Utilisez l’applet de commande [AipServiceTrackingLog](/powershell/module/aipservice/get-aipservicetrackinglog) avec le **contentid** de votre document pour retourner vos données de suivi.

    Par exemple :
    
    ```PowerShell
    Get-AipServiceTrackingLog -ContentId c03bf90c-6e40-4f3f-9ba0-2bcd77524b87
    ```

    Les données de suivi sont retournées, y compris les e-mails des utilisateurs qui ont tenté d’accéder, si l’accès a été accordé ou refusé, l’heure et la date de la tentative, ainsi que le domaine et l’emplacement d’où provient la tentative d’accès.

## <a name="revoke-document-access-from-powershell"></a>Révoquer l’accès au document à partir de PowerShell

Les administrateurs généraux peuvent révoquer l’accès pour tout document protégé stocké dans leurs partages de contenu locaux, à l’aide de l’applet de commande [Set-AIPServiceDocumentRevoked](/powershell/module/aipservice/set-aipservicedocumentrevoked) .

1. Recherchez la valeur **contentid** pour le document pour lequel vous souhaitez révoquer l’accès.
    
    Utilisez la [AipServiceDocumentLog](/powershell/module/aipservice/get-aipservicedocumentlog) pour rechercher un document à l’aide du nom de fichier et/ou de l’adresse de messagerie de l’utilisateur qui a appliqué la protection.
    
    Par exemple :
        
    ```PowerShell
    Get-AipServiceDocumentLog -ContentName "test.docx" -Owner “alice@contoso.com” -FromTime "12/01/2020 00:00:00" -ToTime "12/31/2020 23:59:59"
    ```

    Les données retournées incluent la valeur ContentID de votre document.

    > [!TIP]
    > Seuls les documents qui ont été protégés et inscrits pour le suivi ont une valeur **contentid** . 
    >
    > Si votre document n’a pas de **contentid**, ouvrez-le sur un ordinateur sur lequel est installé le client d’étiquetage unifié pour enregistrer le fichier à des fins de suivi.

1. Utilisez l’instruction [Set-AIPServiceDocumentRevoked](/powershell/module/aipservice/set-aipservicedocumentrevoked) avec le contentid de votre document pour révoquer l’accès.

    Par exemple :

    ```PowerShell
    Set-AipServiceDocumentRevoked -ContentId 0e421e6d-ea17-4fdb-8f01-93a3e71333b8 -IssuerName testIssuer
    ```

> [!NOTE]
> Si l' [accès hors connexion](/microsoft-365/compliance/encryption-sensitivity-labels#assign-permissions-now) est autorisé, les utilisateurs continuent d’accéder aux documents qui ont été révoqués jusqu’à l’expiration de la période de stratégie hors connexion. 
> 

> [!TIP]
> Les utilisateurs peuvent également révoquer l’accès à tous les documents où ils ont appliqué la protection directement à partir du menu **sensibilité** dans leurs applications Office. Pour plus d’informations, consultez [Guide de l’utilisateur : révoquer l’accès aux documents avec Azure information protection](revoke-access-user.md)

### <a name="un-revoke-access"></a>Annuler la révocation de l’accès

Si vous avez refusé accidentellement l’accès à un document spécifique, utilisez la même valeur **contentid** avec l’applet de commande [Clear-AipServiceDocumentRevoked](/powershell/module/aipservice/clear-aipservicedocumentrevoked) pour annuler la révocation de l’accès. 

Par exemple :

```PowerShell
Clear-AipServiceDocumentRevoked -ContentId   0e421e6d-ea17-4fdb-8f01-93a3e71333b8 -IssuerName testIssuer
```

L’accès au document est accordé à l’utilisateur que vous avez défini dans le paramètre **IssuerName** .

## <a name="turn-off-track-and-revoke-features-for-your-tenant"></a>Désactiver les fonctionnalités de suivi et de révocation pour votre locataire

Si vous devez désactiver les fonctionnalités de suivi et de révocation pour votre locataire, par exemple pour les besoins de confidentialité dans votre organisation ou votre région, effectuez les deux étapes suivantes :

1. Exécutez l’applet [de commande Disable-AipServiceDocumentTrackingFeature](/powershell/module/aipservice/disable-aipservicedocumenttrackingfeature) .

1. Affectez la valeur **false** au paramètre du client avancé [EnableTrackAndRevoke](clientv2-admin-guide-customizations.md#turn-off-document-tracking-features-public-preview) . 

Le suivi des documents et les options permettant de révoquer l’accès sont désactivés pour votre locataire :

- L’ouverture de documents protégés avec le client d’étiquetage unifié AIP n’enregistre plus les documents pour le suivi et la révocation.
- Les journaux d’accès ne sont pas stockés lorsque des documents protégés qui sont déjà inscrits sont ouverts. Les journaux d’accès qui étaient stockés avant la désactivation de ces fonctionnalités sont toujours disponibles. 
- Les administrateurs ne peuvent pas suivre ou révoquer l’accès via PowerShell, et les utilisateurs finaux ne voient plus l’option de menu [**révoquer**](revoke-access-user.md#revoke-access-from-microsoft-office-apps) dans leurs applications Office.

> [!NOTE]
> Pour activer le suivi et la révocation, affectez la valeur **true** à [EnableTrackAndRevoke](clientv2-admin-guide-customizations.md#turn-off-document-tracking-features-public-preview) et exécutez également l’applet de commande [Enable-AipServiceDocumentTrackingFeature](/powershell/module/aipservice/enable-aipservicedocumenttrackingfeature) .
>
## <a name="next-steps"></a>Étapes suivantes

Pour plus d'informations, consultez les pages suivantes :

- [Guide de l’utilisateur du client d’étiquetage unifié AIP](clientv2-user-guide.md)
- [Guide de l’administrateur du client d’étiquetage unifié AIP](clientv2-admin-guide.md)
- [Problèmes connus pour les fonctionnalités de suivi et de révocation](../known-issues.md#known-issues-for-track-and-revoke-features-public-preview)
