---
title: Applications Azure Information Protection pour iOS & Android
description: Découvrez les principes de base des applications Azure Information Protection (AIP) pour les appareils iOS et Android
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/07/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 539b4ff8-5d3b-4c4d-9c84-c14da83ff76d
ms.reviewer: esaggese
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 0f849dfefa6af9ffd95dcca0c731ed216f465b11
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/07/2020
ms.locfileid: "86046400"
---
# <a name="what-is-the-azure-information-protection-app-for-ios-or-android"></a>Qu’est-ce que l’application Azure Information Protection pour iOS ou Android ?

*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Les applications d’Azure Information Protection (AIP) pour iOS et Android vous permettent d’afficher les messages électroniques protégés par des droits (fichiers **. rpmsg** ) lorsque votre application de messagerie ne prend pas en charge la protection des données Rights Management en mode natif.  

Les applications AIP vous permettent également d’afficher des documents PDF protégés par des droits (fichiers PDF protégés et fichiers **. ppdf** ), des images et des fichiers texte.

> [!NOTE]
> Les applications AIP sont uniquement des observateurs et ne vous permettent pas de créer ou de répondre à des messages électroniques protégés, ni de créer ou de modifier des fichiers protégés. Les applications ne peuvent pas non plus ouvrir les pièces jointes des fichiers que vous affichez, comme les pièces jointes aux documents PDF protégés ou aux e-mails.
>

## <a name="aip-mobile-app-requirements"></a>Configuration requise pour l’application mobile AIP

Les applications mobiles AIP pour iOS et Android peuvent être utilisées avec les systèmes suivants :

- [Versions de système d’exploitation mobiles prises en charge](#supported-mobile-os-versions)
- [Informations d’identification de connexion prises en charge](#supported-sign-in-credentials)
- [Extensions de fichiers prises en charge](#supported-file-extensions)

### <a name="supported-mobile-os-versions"></a>Versions de système d’exploitation mobiles prises en charge

Les applications mobiles AIP nécessitent l’un des systèmes d’exploitation mobiles minimaux suivants : 

- iOS 11 
- Android 6,0 

> [!NOTE]
> Les applications mobiles AIP ne sont pas prises en charge sur les processeurs Intel.
> 

### <a name="supported-sign-in-credentials"></a>Informations d’identification de connexion prises en charge

Pour vous connecter à AIP, utilisez l’une des méthodes suivantes : 

- **Informations d’identification professionnelles ou scolaires.** Utilisez si votre organisation a déjà AD RMS localement avec l’extension d’appareil mobile, ou utilise Azure Information Protection.
 
- **Compte Microsoft**. Si votre adresse de messagerie personnelle a été utilisée pour protéger le fichier, connectez-vous à l’aide d’un [compte Microsoft](https://signup.live.com). 

    - Vous pouvez utiliser votre propre adresse de messagerie Hotmail, Gmail ou toute autre adresse de messagerie que vous possédez lorsque vous appliquez pour une compte Microsoft.
    
> [!NOTE]
> Toutes les applications ne peuvent pas ouvrir du contenu protégé lorsqu’un compte Microsoft est utilisé. Pour plus d’informations, consultez [scénarios pris en charge pour l’ouverture de documents protégés](../secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents).
> 

### <a name="supported-file-extensions"></a>Extensions de fichiers prises en charge

Vous pouvez ouvrir les fichiers .rpmsg, .pdf, .ppdf, .pjpg, .pjpeg, .ptiff, .ppng, .ptxt, .pxml et plusieurs autres formats de fichiers texte et image.

Pour obtenir la liste complète des extensions de nom de fichier texte et image, consultez la première table de la section [Types de fichier pris en charge pour la classification et la protection](clientv2-admin-guide-file-types.md#supported-file-types-for-classification-and-protection) du guide d’administration.

## <a name="installing-your-aip-mobile-apps-and-viewing-files"></a>Installation de vos applications mobiles AIP et affichage des fichiers

Si votre appareil mobile est géré par Microsoft Intune, vous pourrez peut-être télécharger les applications à partir de votre portail d’entreprise.

Dans le cas contraire, accédez aux applications à partir de :

- Le magasin [iTunes](https://apps.apple.com/app/microsoft-rights-management/id689516635) ou [Google Play](https://play.google.com/store/apps/details?id=com.microsoft.ipviewer)
- [Page de téléchargement Azure information protection](https://portal.azurerms.com/#/download). Sélectionnez les icônes [iOS](https://apps.apple.com/app/microsoft-rights-management/id689516635) ou [Android](https://play.google.com/store/apps/details?id=com.microsoft.ipviewer) dans la section **périphériques mobiles** .

Une fois l’installation terminée, patientez jusqu’à ce que vous ayez reçu un e-mail ou un fichier protégé, puis sélectionnez la **visionneuse AIP** lors de son ouverture.

Vous êtes invité à vous connecter avec votre compte professionnel ou scolaire, ou vous êtes invité à sélectionner un certificat. Une fois que vous avez été authentifié, votre e-mail ou fichier s’ouvre et vous pouvez lire son contenu.

> [!TIP]
> Pour essayer immédiatement, envoyez-vous un e-mail ou un fichier protégé à afficher. 
>
> Pour plus d’informations, consultez [prise en main de l’application Microsoft Azure information protection pour iOS et Android](mobile-app-get-started.md).
> 

## <a name="next-steps"></a>Étapes suivantes

Utilisez l’une des méthodes suivantes pour fournir des commentaires sur les applications mobiles AIP :

- Accéder aux **paramètres**  >  **Envoyer des commentaires**
- Publiez votre question sur notre [site Yammer](https://www.yammer.com/AskIPTeam)
