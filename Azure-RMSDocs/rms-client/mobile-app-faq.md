---
title: FAQ relatives à l’application Azure Information Protection pour iOS et Android
description: Quelques questions fréquemment posées pour vous aider à utiliser l’application Azure Information Protection pour iOS et Android
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/12/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 539b4ff8-5d3b-4c4d-9c84-c14da83ff76d
ms.reviewer: esaggese
ms.suite: ems
ms.custom: user
ms.openlocfilehash: cd8cef4bae59fbffa66ce18737558888f101ef47
ms.sourcegitcommit: 2d75192e7cd2e322ab422fc2115aa063e8dda18b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/13/2020
ms.locfileid: "75913265"
---
# <a name="faqs-for-microsoft-azure-information-protection-app-for-ios-and-android"></a>Forum aux questions sur l’application Microsoft Azure Information Protection pour iOS et Android

*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Cette page fournit des réponses aux questions les plus fréquemment posées sur l’application Azure Information Protection pour iOS et Android.

## <a name="what-can-i-do-with-the-azure-information-protection-app"></a>Que puis-je faire avec l’application Azure Information Protection ?

Cette application vous permet d’afficher des e-mails protégés par des droits (fichiers .rpmsg) si votre application de messagerie ne prend pas en charge la protection des données Rights Management. Cette application vous permet également d’afficher les documents PDF, les images et les fichiers texte protégés par des droits. 

Cette application étant une visionneuse, vous ne pouvez pas l’utiliser pour créer des e-mails protégés, y répondre, ou créer ou modifier des fichiers protégés. En outre, l’application ne peut pas ouvrir de pièces jointes pour les fichiers que vous affichez. Par exemple, des pièces jointes dans des documents PDF protégés ou dans des e-mails protégés par des droits.

## <a name="can-i-open-pdf-files-that-are-in-sharepoint-protected-libraries-and-onedrive-for-business"></a>Puis-je ouvrir des fichiers PDF qui se trouvent dans des bibliothèques protégées SharePoint et dans OneDrive Entreprise ?

Oui, vous pouvez ouvrir des fichiers PDF protégés que d’autres ont partagés avec vous par l’intermédiaire de SharePoint et de OneDrive Entreprise. Appuyez sur le lien, puis choisissez cette application pour ouvrir automatiquement le fichier. 

Cette application peut également ouvrir les fichiers PDF qui ont été protégés en dehors de SharePoint et de OneDrive Entreprise (PDF protégés et fichiers .ppdf).

## <a name="can-my-mobile-device-run-the-azure-information-protection-app"></a>Mon appareil mobile peut-il exécuter l’application Azure Information Protection ?

L’application Azure Information Protection nécessite une version minimale d' **iOS 11** ou **Android 6,0**. Notez que l’application Azure Information Protection **ne peut pas** s’exécuter sur des processeurs Intel. 

Si vous disposez de ces versions ou de versions ultérieures, vous pouvez installer l’application pour l'exécuter sur votre appareil mobile :

- Si votre appareil mobile est géré par Microsoft Intune, vous pourrez peut-être installer l’application Azure Information Protection à partir de votre portail d’entreprise.

- Si votre appareil mobile n’est pas géré par Microsoft Intune ou si Azure Information Protection n’est pas disponible sur votre portail d’entreprise, vous pouvez installer l’application directement à partir de l’iTunes Store et du Google Play Store, ou par un clic sur l’icône iOS ou Android dans la section **Appareils mobiles** sur la [page de téléchargement Azure Information Protection](https://portal.azurerms.com/#/download). 

## <a name="how-do-i-get-started-with-the-viewer-app"></a>Comment commencer à utiliser l’application de visionneuse ?

Une fois que vous avez installé l’application, vous n’avez rien d’autre à faire à ce stade. Patientez jusqu'à ce que vous receviez un e-mail ou un fichier protégé que vous souhaitez afficher, puis choisissez la **visionneuse AIP** pour l’ouvrir. Vous serez invité à vous connecter avec votre compte professionnel ou scolaire, ou invité à sélectionner un certificat. Une fois ces informations d’identification authentifiées, vous pourrez lire le contenu.

Toutefois, si vous ne souhaitez pas attendre, vous pouvez utiliser les instructions suivantes pour vous envoyer un e-mail ou un fichier protégé : [Bien démarrer avec l’application Microsoft Azure Information Protection pour iOS et Android](mobile-app-get-started.md) 

## <a name="what-credentials-should-i-use-to-sign-in-to-this-app"></a>Quelles informations d’identification utiliser pour se connecter à cette application ?

Si votre organisation dispose déjà d’AD RMS locaux (avec l’extension d’appareil mobile) ou utilise Azure Information Protection, utilisez vos informations d’identification professionnelles pour vous connecter. 

Si votre adresse e-mail personnelle a été utilisée pour protéger le fichier, utilisez les informations d’identification d’un [compte Microsoft](https://signup.live.com) gratuit pour vous connecter.

## <a name="can-i-sign-up-for-the-free-account-with-my-personal-email-address-such-as-a-hotmail-or-gmail-account"></a>Puis-je m’inscrire au compte gratuit avec mon adresse e-mail personnelle, comme un compte Hotmail ou Gmail ?

Oui, lorsque vous demandez un compte Microsoft, vous pouvez spécifier votre adresse Hotmail ou Gmail, ou toute autre adresse e-mail que vous possédez. 

Toutefois, même si cette visionneuse peut ouvrir des fichiers protégés avec ce compte, toutes les applications ne peuvent pas ouvrir du contenu protégé lorsqu’un compte Microsoft est utilisé pour l’authentification. [Informations complémentaires](../secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)

## <a name="which-file-extensions-can-i-open-with-this-app"></a>Quelles extensions de fichier puis-je ouvrir avec cette application ?

Vous pouvez ouvrir les fichiers .rpmsg, .pdf, .ppdf, .pjpg, .pjpeg, .ptiff, .ppng, .ptxt, .pxml et plusieurs autres formats de fichiers texte et image.

Pour obtenir la liste complète des extensions de nom de fichier texte et image, consultez la première table de la section [Types de fichier pris en charge pour la classification et la protection](clientv2-admin-guide-file-types.md#supported-file-types-for-classification-and-protection) du guide d’administration.

##  <a name="how-do-i-provide-feedback-about-this-app"></a>Comment envoyer des commentaires concernant cette application ?

Dans l’application, accédez à **Paramètres** > **Envoyer des commentaires**.


## <a name="my-question-has-not-been-answeredwhat-should-i-do"></a>Aucune réponse n’a été apportée à ma question. Que dois-je faire ?

Postez votre question sur notre [site Yammer](https://www.yammer.com/AskIPTeam).
