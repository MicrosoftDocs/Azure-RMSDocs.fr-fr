---
title: Problèmes connus - Azure Information Protection
description: Recherchez et parcourez les problèmes connus et les limitations de Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/15/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: e18c18322783a4f953c898cb96232ab35b642dca
ms.sourcegitcommit: efeb486e49c3e370d7fd8244687cd3de77cd8462
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97583623"
---
# <a name="known-issues---azure-information-protection"></a>Problèmes connus - Azure Information Protection

>***S’applique à** : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>*Concerne : client **d'** [étiquetage unifié AIP et client Classic](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Pour fournir une expérience client unifiée et homogène, le **client classique Azure Information Protection** et la **gestion des étiquettes** dans le portail Azure seront **dépréciés** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Utilisez les listes et les tableaux ci-dessous pour trouver des informations sur les problèmes connus et les limitations liées aux fonctionnalités de Azure Information Protection.

## <a name="client-support-for-container-files-such-as-zip-files"></a>Prise en charge des fichiers de conteneur par les clients, tels que les fichiers. zip

Les fichiers conteneurs sont des fichiers qui incluent d’autres fichiers, comme l’exemple classique des fichiers .zip qui contiennent des fichiers compressés. D’autres exemples incluent les fichiers .rar, .7z, .msg et les documents PDF qui incluent des pièces jointes.

Vous pouvez classifier et protéger ces fichiers conteneurs, mais la classification et la protection ne sont pas appliquées à chaque fichier situé à l’intérieur du conteneur.

Si vous avez un fichier conteneur qui inclut des fichiers classifiés et protégés, vous devez d’abord extraire ces fichiers pour modifier leurs paramètres de classification ou de protection. Toutefois, vous pouvez supprimer la protection pour tous les fichiers inclus dans des fichiers conteneurs pris en charge à l’aide de l’applet de commande [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile).

La visionneuse Azure Information Protection ne peut pas ouvrir les pièces jointes dans un document PDF protégé. Dans ce scénario, lorsque le document est ouvert dans la visionneuse, les pièces jointes ne sont pas visibles.

Pour plus d’informations, consultez [le Guide de l’administrateur : types de fichiers pris en charge par le client Azure information protection](rms-client/client-admin-guide-file-types.md).

## <a name="known-issues-for-aip-and-exploit-protection"></a>Problèmes connus liés à AIP et à la protection contre les attaques

Le client Azure Information Protection n’est pas pris en charge sur les ordinateurs disposant de .NET 2 ou 3, où la [protection contre l’exploitation](/windows/security/threat-protection/microsoft-defender-atp/enable-exploit-protection) est activée et entraîne un comportement inattendu des applications Office.

Si vous disposez d’une version 2 ou 3 de .NET en plus d’une version de .NET 4. x requise pour votre système, veillez à désactiver la protection contre l’exploitation avant AIP. 

Pour désactiver la protection contre les attaques par le biais de PowerShell, exécutez la commande suivante :

```PowerShell
Set-ProcessMitigation -Name "OUTLOOK.EXE" -Disable EnableExportAddressFilterPlus, EnableExportAddressFilter, EnableImportAddressFilter
```

Pour plus d’informations, voir [conditions préalables supplémentaires pour le client d’étiquetage unifié Azure information protection](rms-client/clientv2-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-unified-labeling-client).

## <a name="powershell-support-for-the-azure-information-protection-client"></a>Prise en charge de PowerShell pour le client Azure Information Protection

La version actuelle du module PowerShell **AzureInformationProtection** qui est installée avec le client Azure information protection présente les problèmes connus suivants :

- **Dossiers personnels Outlook (* fichiers. pst *) * *. La protection native des fichiers *. pst* n’est pas prise en charge à l’aide du module **AzureInformationProtection** .

- **Messages électroniques protégés par Outlook *(fichiers. rpmsg* )**. La déprotection des messages électroniques protégés par Outlook est prise en charge par le module **AzureInformationProtection** uniquement s’ils se trouvent dans un dossier personnel Outlook *(fichier. pst* ).

    La déprotection des messages électroniques en dehors d’un fichier *. pst* n’est pas prise en charge.

Pour plus d’informations, consultez [le Guide de l’administrateur : utilisation de PowerShell avec le client Azure information protection](rms-client/client-admin-guide-powershell.md).

## <a name="aip-known-issues-in-office-applications"></a>Problèmes connus liés à AIP dans les applications Office

|Fonctionnalité  |Problèmes connus  |
|---------|---------|
|**Plusieurs versions d’Office**    | Les clients Azure Information Protection, y compris les étiquetages classiques et unifiés, ne prennent pas en charge plusieurs versions d’Office sur le même ordinateur ou n’échangent pas de comptes d’utilisateur dans Office.       |
|**Affichages multiples** |Si vous utilisez plusieurs affichages et que vous avez une application Office ouverte : <br><br>-Vous pouvez rencontrer des problèmes de performances dans vos applications Office.<br>-La barre de Azure Information Protection peut sembler flotter au milieu de l’écran du bureau, sur l’un ou l’autre des écrans <br><br>Pour garantir des performances cohérentes et que la barre reste à l’emplacement approprié, ouvrez la boîte de dialogue **options** de votre application Office et, sous **général**, sélectionnez **optimiser pour la compatibilité** plutôt que **optimiser pour une meilleure apparence**.    |
|**Prise en charge d’IRM dans Office 2016**| Le paramètre de Registre [DRMEncryptProperty](/deployoffice/security/protect-sensitive-messages-and-documents-by-using-irm-in-office#office-2016-irm-registry-key-options) , qui contrôle le chiffrement des métadonnées dans Office 2016, n’est pas pris en charge pour les étiquettes de Azure information protection.|
|**Marquages de contenu dans Word**    | Les [marquages de contenu](configure-policy-markings.md) AIP dans les en-têtes ou pieds de page de Microsoft Word peuvent être décalés ou placés de manière incorrecte, ou peuvent être masqués entièrement, lorsque ce même en-tête ou pied de page contient également un tableau.<br><br>Pour plus d’informations, consultez la page [quand des marquages visuels sont appliqués](configure-policy-markings.md#when-visual-markings-are-applied). |
|**Fichiers joints aux courriers électroniques** |En raison d’une limitation dans les mises à jour Windows récentes, lorsque [Microsoft Outlook est protégé par Azure Rights Management](office-apps-services-support.md), les fichiers joints aux courriers électroniques peuvent être verrouillés après l’ouverture du fichier. |
|**Fusion et publipostage**    |  La fonctionnalité [Publipostage](https://support.office.com/article/use-mail-merge-for-bulk-email-letters-labels-and-envelopes-f488ed5b-b849-4c11-9cff-932c49474705) n’est pas prise en charge avec les fonctionnalités Azure Information Protection.       |
| **Courriers électroniques S/MIME** | L’ouverture des e-mails S/MIME dans le volet de lecture d’Outlook peut entraîner des problèmes de performances. <br><br>Pour éviter les problèmes de performances avec les e-mails S/MIME, activez la propriété avancée [**OutlookSkipSmimeOnReadingPaneEnabled**](rms-client/clientv2-admin-guide-customizations.md#prevent-outlook-performance-issues-with-smime-emails) . <br><br>**Remarque**: l’activation de cette propriété empêche l’affichage de la barre AIP ou de la classification des messages dans le volet de lecture d’Outlook. |
|**Option Envoyer vers l’Explorateur de fichiers** |Si vous choisissez de cliquer avec le bouton droit sur un fichier dans l’Explorateur de fichiers et que vous sélectionnez **Envoyer à > destinataire du courrier**, le message Outlook qui s’ouvre avec le fichier joint peut ne pas afficher la barre d’outils AIP. <br><br>Si cela se produit et que vous devez utiliser les options de la barre d’outils AIP, commencez votre adresse de messagerie à partir d’Outlook, puis accédez au fichier que vous souhaitez envoyer et joignez-le.|
| | |

## <a name="known-issues-in-policies"></a>Problèmes connus dans les stratégies

La publication des stratégies peut prendre jusqu’à 24 heures.

## <a name="known-issues-in-the-aip-client"></a>Problèmes connus dans le client AIP

- [Tailles maximales de fichiers](#maximum-file-sizes)
- [Visionneuse AIP](#aip-viewer)
- [Suivi et révocation de l’accès aux documents](#tracking-and-revoking-document-access-public-preview)

### <a name="maximum-file-sizes"></a>Tailles maximales de fichiers

Les fichiers de plus de 2 Go sont pris en charge pour la protection, mais pas pour le déchiffrement.

### <a name="aip-viewer"></a>Visionneuse AIP

La visionneuse AIP affiche des images en mode portrait, et certaines images larges et de vue paysage peuvent sembler étirées.

Par exemple, une image d’origine est représentée ci-dessous à gauche, avec une version en mode portrait étirée dans la visionneuse AIP à droite. 
    
:::image type="content" source="media/client-viewer-stretched-images.PNG" alt-text="Image étirée dans la visionneuse cliente":::
    
Pour plus d’informations, consultez :

- [**Client classique**: afficher les fichiers protégés avec la visionneuse de Azure information protection](rms-client/client-view-use-files.md)
- [**Client d’étiquetage unifié**: afficher les fichiers protégés avec la visionneuse de Azure information protection](rms-client/clientv2-view-use-files.md)

### <a name="tracking-and-revoking-document-access-public-preview"></a>Suivi et révocation de l’accès aux documents (préversion publique)

Le suivi et la révocation de l’accès aux documents à l’aide du client d’étiquetage unifié présente les problèmes connus suivants :

- [Plusieurs pièces jointes dans un e-mail protégé](#multiple-attachments-in-a-protected-email)
- [Documents accessibles via SharePoint](#documents-accessed-via-sharepoint)

Pour plus d’informations, consultez [le Guide de l’administrateur : suivre et révoquer l’accès aux documents avec Azure information protection et le](rms-client/track-and-revoke-admin.md) Guide de l' [utilisateur : révoquer l’accès aux documents avec Azure information protection](rms-client/revoke-access-user.md).

#### <a name="multiple-attachments-in-a-protected-email"></a>Plusieurs pièces jointes dans un e-mail protégé

Si vous joignez plusieurs documents à un message électronique, puis Protégez l’e-mail et l’envoyez, chacune des pièces jointes obtient la même valeur ContentID. 

Cette valeur ContentID est retournée uniquement avec le premier fichier qui avait été ouvert. La recherche des autres pièces jointes ne retourne pas la valeur ContentID requise pour obtenir les données de suivi.      

En outre, la révocation de l’accès pour l’une des pièces jointes révoque également l’accès aux autres pièces jointes dans le même e-mail protégé.

#### <a name="documents-accessed-via-sharepoint"></a>Documents accessibles via SharePoint
    
- Les documents protégés qui sont téléchargés sur SharePoint perdent leur valeur ContentID. 

    Cela signifie que les données ne sont pas suivies et que les révocations d’accès ne s’appliquent pas au fichier stocké dans SharePoint.

- Si un utilisateur télécharge le fichier à partir de SharePoint et y accède à partir de son ordinateur local, une nouvelle ContentID est appliquée au document lorsqu’il l’ouvre localement. 
    
    L’utilisation de la valeur ContentID d’origine pour le suivi des données n’inclut pas les accès effectués pour le fichier téléchargé de l’utilisateur. En outre, la révocation de l’accès basé sur la valeur ContentID d’origine ne révoque pas l’accès pour les fichiers téléchargés.

    Dans ce cas, les administrateurs peuvent être en mesure de localiser les fichiers téléchargés à l’aide de PowerShell pour rechercher les nouvelles valeurs ContentID pour suivre ou révoquer l’accès.

## <a name="aip-for-windows-and-office-versions-in-extended-support"></a>AIP pour Windows et les versions d’Office dans le support étendu

- La [**prise en charge étendue de Windows 7 a pris fin le 14 janvier 2020**](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet). 

    Nous vous encourageons vivement à effectuer une mise à niveau vers une version plus récente de Windows 10. Toutefois, si vous avez étendu des mises à jour de sécurité (UDE) et un contrat de support, le support AIP est disponible pour maintenir la sécurité de vos systèmes Windows 7.

    Pour plus d’informations, consultez votre contact de support technique.

- [**Office 2010 est actuellement en support étendu**](https://support.microsoft.com/lifecycle/search?alpha=office%202010). 

    Cette prise en charge prendra fin le 13 octobre 2020 et ne sera pas étendue. En outre, UDE n’est pas proposée pour Office 2010 et nous vous encourageons vivement à effectuer une mise à niveau vers une version plus récente d’Office 365. 
    
    Pour les clients qui exécutent actuellement Office 2010 dans le support étendu, le support AIP est disponible jusqu’au 13 octobre 2020. 

    Pour plus d’informations, consultez votre contact de support technique.

## <a name="aip-based-conditional-access-policies"></a>Stratégies d’accès conditionnel basées sur AIP

Les utilisateurs externes qui reçoivent du contenu protégé par des [stratégies d’accès conditionnel](/azure/active-directory/conditional-access/concept-conditional-access-policy-common) doivent disposer d’un compte d’utilisateur invité de collaboration Business-to-Business (B2B) Azure Active Directory (Azure AD) pour pouvoir afficher le contenu.

Bien que vous puissiez inviter des utilisateurs externes à activer un compte d’utilisateur invité, ce qui leur permet de s’authentifier et de répondre aux exigences en matière d’accès conditionnel, il peut être difficile de s’assurer que cela se produit pour tous les utilisateurs externes requis.

Nous vous recommandons d’activer les stratégies d’accès conditionnel basé sur AIP pour vos utilisateurs internes uniquement.

**Activez les stratégies d’accès conditionnel pour AIP pour les utilisateurs internes uniquement**:

1.  Dans le Portail Azure, accédez au panneau **accès conditionnel** , puis sélectionnez la stratégie d’accès conditionnel que vous souhaitez modifier. 
2.  Sous **affectations**, sélectionnez **utilisateurs et groupes**, puis sélectionnez **tous les utilisateurs**. Assurez-vous que l’option **tous les utilisateurs invités et externes** n’est *pas* sélectionnée.
3.  Enregistrez vos changements. 
 
Vous pouvez également désactiver entièrement l’autorité de certification dans Azure Information Protection si cette fonctionnalité n’est pas requise pour votre organisation, afin d’éviter ce problème potentiel. 

Pour plus d’informations, consultez la [documentation relative à l’accès conditionnel](/azure/active-directory/conditional-access/concept-conditional-access-users-groups).

## <a name="more-information"></a>Informations complémentaires

Les articles supplémentaires suivants peuvent être utiles pour répondre à des questions sur les problèmes connus dans Azure Information Protection :

- [Forum aux questions sur Azure Information Protection](faqs.md)
- [Forum aux questions sur la protection des données dans Azure Information Protection](faqs-rms.md)
- [Forum aux questions sur la classification et l’étiquetage dans Azure Information Protection](faqs-infoprotect.md)
- [FAQ pour l’application Microsoft Azure Information Protection pour iOS et Android](rms-client/mobile-app-faq.md)