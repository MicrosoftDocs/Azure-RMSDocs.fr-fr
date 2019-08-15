---
title: Télécharger & installer le client d’étiquetage unifié Azure Information Protection
description: Instructions permettant aux utilisateurs d’installer le client d’étiquetage unifié Azure Information Protection pour Windows, afin que vous puissiez classer et protéger vos documents et e-mails.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 08/13/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 3c92a57864d81a20577ced49ad6346b03617d6a6
ms.sourcegitcommit: b02dc1b575213ea85ca984a0da457dd99f27b762
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/13/2019
ms.locfileid: "68994413"
---
# <a name="user-guide-download-and-install-the-azure-information-protection-unified-labeling-client"></a>Guide de l’utilisateur : Télécharger et installer le client d’étiquetage unifié Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1*
>
> *Instructions pour : [Azure Information Protection client d’étiquetage unifié pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Si votre administrateur n’installe pas le client d’étiquetage unifié Azure Information Protection pour vous, vous pouvez le faire vous-même. Vous devez être un administrateur local de votre PC pour installer ce client, de sorte qu’il puisse étiqueter et protéger vos documents et vos e-mails.

De plus :

- Le client d’étiquetage unifié Azure Information Protection nécessite une version minimale de Microsoft .NET Framework 4.6.2. Si cette version est manquante, le programme d’installation tente de télécharger et d’installer ce prérequis. Lorsque ce composant requis est installé dans le cadre de l’installation du client, votre ordinateur doit être redémarré.

- Si vous disposez de Windows 7 SP1, le client d’étiquetage unifié Azure Information Protection exige une mise à jour spécifique, KB 2533623. Si votre PC a besoin de cette mise à jour, mais qu’elle n’est pas installée, l’installation s’effectue, mais un message apparaît vous indiquant que le client d’étiquetage unifié Azure Information Protection a besoin de cette mise à jour. Tant que cette mise à jour n’est pas installée, vous ne pourrez pas utiliser toutes les fonctionnalités du client d’étiquetage unifié Azure Information Protection. 

## <a name="to-download-and-install-the-azure-information-protection-unified-labeling-client"></a>Pour télécharger et installer le client d’étiquetage unifié Azure Information Protection

Avant d’installer le client d’étiquetage unifié Azure Information Protection, vérifiez auprès de votre administrateur ou de votre support technique que vous utilisez des [étiquettes de sensibilité](https://docs.microsoft.com/Office365/SecurityCompliance/sensitivity-labels) pour classifier et protéger des documents et des e-mails.

1. Téléchargez **AzInfoProtection_UL. exe** à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

2. Exécutez le fichier exécutable qui a été téléchargé et, si vous êtes invité à continuer, cliquez sur **Oui**.

3. Dans la page **Installer le client Azure Information Protection**, cliquez sur **J’accepte** après avoir lu les termes du contrat de licence.

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

## <a name="other-instructions"></a>Autres instructions    
Pour plus d’instructions, reAzure Information Protection Guide de l’utilisateur du client d’étiquetage unifié:

- [Que voulez-vous faire ?](clientv2-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Informations supplémentaires pour les administrateurs    
Consultez [installer le client d’étiquetage unifié Azure information protection pour les utilisateurs](clientv2-admin-guide-install.md) à partir du Guide de l' [administrateur](clientv2-admin-guide.md).
