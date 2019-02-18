---
title: Télécharger et installer le client d’étiquetage unifié Azure Information Protection (préversion)
description: Instructions destinées aux utilisateurs pour installer la préversion du client d’étiquetage unifié Azure Information Protection pour Windows, afin de pouvoir classifier et protéger des documents et des e-mails.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 10/17/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 2bf09690-9dba-43b7-9e0a-0110915d4081
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 6ee27b9aedd35ae135fc7150a3211be43ca2f092
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56250889"
---
# <a name="download-and-install-the-azure-information-protection-unified-labeling-client-preview"></a>Télécharger et installer le client d’étiquetage unifié Azure Information Protection (préversion)

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1*

> [!NOTE]
> Ce client est en préversion et susceptible d’être modifié. Il utilise le magasin d’étiquetage unifié et télécharge une stratégie avec des étiquettes de sensibilité à partir du Centre de sécurité et conformité Office 365. Pour utiliser ces étiquettes, vous devez tout d’abord les publier à partir du Centre de sécurité et conformité. [Plus d’informations](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Announcing-the-availability-of-unified-labeling-management-in/ba-p/262492)

Vous devez être administrateur local de votre PC pour installer ce client en préversion, de sorte qu’il puisse étiqueter et protéger vos documents et vos e-mails.

De plus :

- Le client d’étiquetage unifié Azure Information Protection nécessite une version minimale de Microsoft .NET Framework 4.6.2. Si cette version est manquante, le programme d’installation tente de télécharger et d’installer ce prérequis. Lorsque ce composant requis est installé dans le cadre de l’installation du client, votre ordinateur doit être redémarré.

- Si vous disposez de Windows 7 SP1, le client d’étiquetage unifié Azure Information Protection exige une mise à jour spécifique, KB 2533623. Si votre PC a besoin de cette mise à jour, mais qu’elle n’est pas installée, l’installation s’effectue, mais un message apparaît vous indiquant que le client d’étiquetage unifié Azure Information Protection a besoin de cette mise à jour. Tant que cette mise à jour n’est pas installée, vous ne pourrez pas utiliser toutes les fonctionnalités du client d’étiquetage unifié Azure Information Protection. 

## <a name="to-download-and-install-the-azure-information-protection-unified-labeling-client"></a>Pour télécharger et installer le client d’étiquetage unifié Azure Information Protection

Avant d’installer le client d’étiquetage unifié Azure Information Protection, vérifiez que des étiquettes de sensibilité dans le Centre de sécurité et conformité Office 365 sont publiées pour les utilisateurs. 

Si des étiquettes sont actuellement publiées à partir du portail Azure pour Azure Information Protection, vous pouvez [migrer ces étiquettes](../configure-policy-migrate-labels.md) vers le Centre de sécurité et conformité.

1. Téléchargez le client en préversion depuis le [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=57440).

2. Exécutez le fichier exécutable qui a été téléchargé, **AzInfoProtection_For_Unified_Labeling.exe**. Si vous êtes invité à continuer, cliquez sur **Oui**.    

3. Dans la page **Installer le client Azure Information Protection** :     
    - Sélectionnez l’option d’installation d’une stratégie de démonstration si vous ne pouvez pas vous connecter au cloud mais souhaitez évaluer l’expérience avec le côté client d’Azure Information Protection à l’aide d’une stratégie locale à des fins de démonstration. Quand votre client se connecte au Centre de sécurité et conformité Office 365, cette stratégie de démonstration est remplacée par la stratégie d’étiquette de votre organisation.

    - Cliquez sur **J’accepte** quand vous avez lu les termes du contrat de licence.    

4. Si vous êtes invité à continuer, cliquez sur **Oui** et attendez que l’installation se termine.    

6. Cliquez sur **Fermer**. Avant de commencer à utiliser le client d’étiquetage unifié Azure Information Protection :    

    - Si votre ordinateur exécute Office 2010, redémarrez votre ordinateur et passez à la section suivante pour la dernière étape.    
        
    - Pour les autres versions d’Office, redémarrez toutes les applications Office et toutes les instances de l’Explorateur de fichiers. L’installation est à présent terminée. Vous pouvez désormais utiliser le client pour étiqueter et protéger vos documents et vos e-mails.    

### <a name="installing-the-azure-information-protection-unified-labeling-client-with-office-2010"></a>Installation du client d’étiquetage unifié Azure Information Protection avec Office 2010

Une fois le client d’étiquetage unifié Azure Information Protection installé à l’aide des instructions précédentes :

1. Ouvrez Microsoft Word. Lorsque vous exécutez une application Office 2010 pour la première fois après avoir installé le client Azure Information Protection, une boîte de dialogue **Microsoft Azure Information Protection** s’affiche. Cette boîte de dialogue vous indique que des informations d’identification administrateur sont requises pour terminer la connexion.

2. Dans la boîte de dialogue **Microsoft Azure Information Protection**, cliquez sur **OK**.

3. Si une boîte de dialogue **Contrôle d’accès utilisateur** s’affiche, cliquez sur **Oui**, afin que le client Azure Information Protection puisse mettre à jour le registre.

L’installation est à présent terminée et vous pouvez utiliser le client d’étiquetage unifié Azure Information Protection pour étiqueter et protéger vos documents et vos e-mails.

## <a name="next-steps"></a>Étapes suivantes

Pour en savoir plus sur le magasin d’étiquetage unifié utilisé désormais par le Centre de sécurité et de conformité Office 365, lisez le billet de blog suivant : [Announcing the availability of unified labeling management in the Security & Compliance Center](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Announcing-the-availability-of-unified-labeling-management-in/ba-p/262492).

