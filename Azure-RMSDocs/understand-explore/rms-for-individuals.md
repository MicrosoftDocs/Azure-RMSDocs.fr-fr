---
title: RMS for individuals et Azure Information Protection
description: Informations relatives à RMS for Individuals, un abonnement libre-service gratuit destiné aux utilisateurs qui ont reçu des fichiers protégés, mais ne peuvent pas s’authentifier, car leur service informatique ne gère pas de compte en leur nom dans Azure.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/17/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 2efcb440-fefd-45e9-872b-f471573aadf2
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 43890652ab65ff55182bdf954cf3f1e473fea20a
ms.sourcegitcommit: 44ff610dec678604c449d42cc0b0863ca8224009
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39370531"
---
# <a name="rms-for-individuals-and-azure-information-protection"></a>RMS for individuals et Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

RMS for individuals est un abonnement gratuit en libre-service destiné aux utilisateurs qui doivent ouvrir des fichiers protégés par Azure Information Protection. Si ces utilisateurs ne peuvent pas être authentifiés par Azure Active Directory, ce service d’abonnement gratuit peut leur créer un compte dans Azure Active Directory. Ainsi, ces utilisateurs peuvent s’authentifier avec leur e-mail professionnel et lire les fichiers protégés sur des ordinateurs ou des appareils mobiles.

RMS for individuals utilise une inscription en libre service Azure Active Directory. Si des utilisateurs ont créé des comptes pour votre organisation dans le cadre de cet abonnement, vous pouvez, en tant qu’administrateur de votre organisation, revendiquer la propriété et [prendre le contrôle de leurs comptes](/active-directory/domains-admin-takeover#external-admin-takeover). 


> [!NOTE]
> Cet abonnement gratuit est une option permettant de garantir que les personnes autorisées à l’extérieur de votre organisation peuvent toujours lire des fichiers protégés par votre organisation. Une autre option consiste à envoyer les documents par e-mail en utilisant le [chiffrement de messages Office 365 avec de nouvelles fonctionnalités](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e). Cette solution de messagerie fonctionne pour toutes les adresses e-mail sur tous les appareils et est recommandée pour le partage sécurisé d’informations et l’affichage de documents Office dans un navigateur avec des personnes extérieures à votre organisation.
> 
> Une autre option consiste à utiliser des comptes Microsoft. Toutefois, toutes les applications ne peuvent pas ouvrir du contenu protégé lorsqu’un compte Microsoft est utilisé pour l’authentification. [Plus d’informations](../get-started/secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents) 

Pour obtenir un compte gratuit, les utilisateurs doivent accéder à la [page Microsoft Azure Information Protection](https://aka.ms/rms-signup) et indiquez leur adresse e-mail professionnelle. Ils reçoivent en retour un e-mail de Microsoft qui leur permet d’effectuer l’inscription en entrant les détails nécessaires à la création de leur compte. 

Une fois le compte créé, la dernière page affiche des liens pour télécharger le client ou la visionneuse Azure Information Protection pour différents appareils, un lien vers le guide de l’utilisateur, ainsi qu’un lien vers la dernière liste des applications offrant une prise en charge native de la protection Rights Management. 

## <a name="to-sign-up-for-rms-for-individuals"></a>Inscription à RMS for individuals

1. À partir d’un ordinateur Windows ou Mac, ou d’un appareil mobile, accédez à la page [Microsoft Azure Information Protection](https://aka.ms/rms-signup).

2. Tapez l’adresse e-mail qui a été utilisée pour protéger le document que vous devez ouvrir.

3. Cliquez sur **S’inscrire**.

    Microsoft utilise votre adresse e-mail pour vérifier si votre organisation a déjà un [abonnement pour Azure Information Protection Premium](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing) ou un [abonnement Office 365 qui inclut la protection des données par le biais d’Azure Information Protection](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf). Si aucun de ces abonnements n’est détecté, vous n’avez pas besoin de RMS for Individuals. Vous êtes connecté immédiatement et l’inscription en libre-service à RMS for Individuals est annulée. Si aucun abonnement n’est détecté, vous passez à l’étape suivante.

4. Attendez qu'un e-mail de confirmation soit envoyé à l'adresse que vous avez indiquée. Il provient de l’équipe Office 365 (support@email.microsoftonline.com) et présente l’objet suivant : **Terminer l’inscription à Microsoft Azure Information Protection**.

5. À la réception de l’e-mail, cliquez sur **Oui, c’est moi** pour vérifier votre adresse e-mail et terminer le processus d’inscription.

6. Dans la page **Dernière chose...** qui s’affiche, vous allez maintenant entrer les informations de votre compte. Tapez vos nom et prénom, entrez et confirmez le mot de passe de votre choix, puis cliquez sur **Démarrer**.

7. Une fois votre compte créé, une nouvelle page Microsoft Azure Information Protection s’affiche. Dans celle-ci, vous pouvez soit télécharger et installer le client Azure Information Protection, soit cliquer sur le lien [Guide de l’utilisateur](../rms-client/client-user-guide.md) pour obtenir des guides pratiques pour les ordinateurs Windows.

Maintenant que votre compte est créé, si vous êtes invité à vous connecter pour lire des fichiers protégés, entrez l’adresse e-mail et le mot de passe que vous avez utilisés pour créer le compte RMS for Individuals.

> [!IMPORTANT]
> Bien que vous puissiez désormais également protéger des fichiers avec ce compte, ne le faites pas tant que votre organisation n’a pas un [abonnement d’évaluation ou payant](https://azure.microsoft.com/pricing/details/information-protection/) pour Azure Information Protection. Si vous protégez des fichiers et des messages électroniques à l’aide de cet abonnement gratuit et que votre organisation prend ensuite le contrôle de votre compte, le contenu préalablement protégé risque de devenir inaccessible.


## <a name="next-steps"></a>Étapes suivantes
RMS for Individuals est un exemple d'utilisation de l’inscription en libre-service prise en charge par Azure Active Directory. Pour plus d’informations sur son fonctionnement, voir [Qu’est-ce qu’une inscription libre-service à Azure ?](/active-directory/active-directory-self-service-signup) dans la documentation d’Azure Active Directory.

