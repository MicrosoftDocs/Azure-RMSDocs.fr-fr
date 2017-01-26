---
title: "Télécharger et installer le client Azure Information Protection | Azure Information Protection"
description: "Instructions destinées aux utilisateurs pour installer le client Azure Information Protection pour Windows, afin de pouvoir classifier et protéger des documents et des e-mails."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/13/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 2bf09690-9dba-43b7-9e0a-0110915d4081
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 22af60687ad030e686ba843ced6d450487353a0e
ms.openlocfilehash: 72266181c5334ed7e03b2022df61c4065f1c3ac7


---

# <a name="download-and-install-the-azure-information-protection-client"></a>Télécharger et installer le client Azure Information Protection

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1*

**[Cette version du client est une préversion susceptible d’être modifiée.]**

Si votre administrateur n’installe pas le client Azure Information Protection pour vous, vous pouvez le faire vous-même. Vous devez être administrateur local de votre PC pour installer ce client. 

### <a name="office-2010-only"></a>Office 2010 uniquement

Lorsque vous utilisez cette version d’Office, le client Azure Information Protection doit définir des clés de registre nécessitant des droits d’administrateur : 

Suivez les instructions pour télécharger et installez le client, puis suivez les instructions de la section suivante pour Office 2010.

## <a name="to-download-and-install-the-azure-information-protection-client"></a>Pour télécharger et installer le client Azure Information Protection

1.  Accédez au [site de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018) et téléchargez la **préversion** du client Azure Information Protection.

2. Double-cliquez sur le fichier exécutable qui a été téléchargé. 

3. Dans la page **Installer le client Azure Information Protection** : 
    
    - Sélectionnez l’option d’installation d’une stratégie de démonstration si vous ne pouvez pas vous connecter au cloud mais souhaitez évaluer l’expérience avec le côté client d’Azure Information Protection à l’aide d’une stratégie locale à des fins de démonstration. Lorsque votre client se connecte à un service Azure Information Protection, cette stratégie de démonstration est remplacée par la stratégie Azure Information Protection de votre organisation.
    
    - Cliquez sur **J’accepte** quand vous avez lu les termes du contrat de licence.

4. Si vous êtes invité à continuer, cliquez sur **Oui** et attendez que l’installation se termine.

3. Cliquez sur **Fermer**. Avant de commencer à utiliser le client Azure Information Protection :

    - Si votre ordinateur exécute Office 2010, redémarrez votre ordinateur et passez à la section suivante pour la dernière étape.
    
    - Pour les autres versions d’Office, redémarrez toutes les applications Office et toutes les instances de l’Explorateur de fichiers. L’installation est à présent terminée. Vous pouvez désormais utiliser le client pour étiqueter et protéger vos documents et vos e-mails.

> [!NOTE]
> Si vous disposez de Windows 7 SP1, le client Azure Information Protection exige la mise à jour spécifique [KB 2533623](https://support.microsoft.com/en-us/kb/2533623). Si votre PC a besoin de cette mise à jour, mais qu’elle n’est pas installée, un message s’affiche quand vous essayez d’utiliser le client indiquant que cette mise à jour doit être installée pour que vous puissiez utiliser toutes les fonctionnalités du client Azure Information Protection.

### <a name="installing-the-azure-information-protection-client-with-office-2010"></a>Installation du client Azure Information Protection avec Office 2010

Une fois le client Azure Information Protection installé à l’aide des instructions précédentes :

1. Ouvrez Microsoft Word. Lorsque vous exécutez une application Office 2010 pour la première fois après avoir installé le client Azure Information Protection, une boîte de dialogue **Microsoft Azure Information Protection** s’affiche. Cette boîte de dialogue vous indique que des informations d’identification administrateur sont requises pour terminer la connexion.

2. Dans la boîte de dialogue **Microsoft Azure Information Protection**, cliquez sur **OK**.

2. Si une boîte de dialogue **Contrôle d’accès utilisateur** s’affiche, cliquez sur **Oui**, afin que le client Azure Information Protection puisse mettre à jour le registre.

L’installation est à présent terminée. Vous pouvez désormais utiliser Azure Information Protection pour étiqueter et protéger vos documents et vos e-mails.

## <a name="other-instructions"></a>Autres instructions
Pour obtenir des instructions pratiques, consultez les sections suivantes du guide de l’utilisateur Azure Information Protection :

-   [Que voulez-vous faire ?](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Informations supplémentaires pour les administrateurs
[Installation du client Azure Information Protection](info-protect-client.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]



<!--HONumber=Jan17_HO4-->


