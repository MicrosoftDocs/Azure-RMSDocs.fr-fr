---
title: "Afficher et utiliser des fichiers qui ont été protégés par Rights Management | Azure Information Protection"
description: "Instructions pour afficher et utiliser un fichier protégé qui vous oblige à installer le client Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/07/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ce1c7d4c-b5ff-4672-8b9a-a72129bac992
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 364891123720daaacacbea1b382b7d101d75cd1a


---

# <a name="view-and-use-files-that-have-been-protected-by-rights-management"></a>Afficher et utiliser des fichiers qui ont été protégés par Rights Management

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1*

**[Cette version du client est une préversion susceptible d’être modifiée.]**

Quand le [client Azure Information Protection est installé sur votre ordinateur](install-client-app.md), vous pouvez afficher un fichier protégé tout simplement en l’ouvrant. Par exemple, vous pouvez double-cliquer sur une pièce jointe à un e-mail ou sur un fichier dans l’Explorateur de fichiers, ou bien vous pouvez cliquer sur un lien vers un fichier.

> [!NOTE]
> Pour que vous puissiez afficher le fichier protégé, le service Rights Management doit confirmer que vous y êtes autorisé. Pour ce faire, il vérifie vos nom d’utilisateur et mot de passe. Dans certains cas, cette opération peut être mise en cache de sorte que vous ne voyez pas d'invite vous demandant vos informations d'identification. Dans d'autres cas, vous êtes invité à fournir vos informations d'identification.
>
> Si votre organisation ne dispose pas d’un compte cloud que vous pouvez utiliser (pour Office 365 ou Azure) et qu’elle n’utilise pas les services AD RMS, vous pouvez obtenir un compte gratuit qui accepte vos informations d’identification afin de pouvoir ouvrir des fichiers protégés par Rights Management :
>
> -   Pour demander ce compte, cliquez sur le lien [RMS for Individuals](http://go.microsoft.com/fwlink/?LinkId=309469).
>
>     Lorsque vous vous inscrivez, utilisez l'adresse de messagerie de votre organisation plutôt qu'une adresse personnelle. Si vous vous inscrivez parce que vous reçu une pièce protégée jointe à un message électronique, utilisez l'adresse de messagerie à laquelle ce message a été envoyé.
> -   Pour plus d’informations, consultez [RMS for individuals et Azure Rights Management](../understand-explore/rms-for-individuals.md).

## <a name="to-view-and-use-a-protected-file"></a>Pour afficher et utiliser un fichier protégé

1. Ouvrez le fichier protégé (par exemple, en double-cliquant sur le fichier ou la pièce jointe, ou en cliquant sur le lien vers le fichier). Si vous êtes invité à sélectionner une application, sélectionnez **Azure Information Protection Viewer (préversion)**. 

2. Si vous voyez une page de **connexion** ou d’**inscription** : cliquez sur **Se connecter** et entrez vos informations d’identification. Si le fichier protégé vous a été envoyé comme pièce jointe, veillez à spécifier la même adresse e-mail que celle utilisée pour vous envoyer le fichier.
    
    Si vous n’avez pas de compte accepté, consultez la remarque en haut de cette page. Inscrivez-vous pour obtenir un compte gratuit et revenez à ces instructions.

3. Une version en lecture seule du fichier s’ouvre dans **Azure Information Protection Viewer**. Si vous disposez des autorisations suffisantes, vous pouvez imprimer le fichier et le modifier. 

    Vous pouvez vérifier vos autorisations sur le fichier en cliquant sur **Autorisations**. Dans la boîte de dialogue **Autorisations**, vous pouvez également identifier le propriétaire du fichier à contacter si vous voulez lui demander une nouvelle version du fichier avec des autorisations supplémentaires.
    
    Pour plus d’informations sur les autorisations et les droits d’utilisation de chacune d’elle, consultez [Droits inclus dans les niveaux d’autorisation](../deploy-use/configure-usage-rights.md#rights-included-in-permissions-levels).

4. Pour modifier le fichier, cliquez sur **Enregistrer sous**, ce qui vous permet d’enregistrer le fichier sans protection avec son extension de nom de fichier d’origine. Vous pouvez ensuite le modifier à l’aide de l’application associée à son type.

5. Si vous avez des fichiers protégés supplémentaires à ouvrir, vous pouvez y accéder directement depuis la visionneuse, en utilisant l’option **Ouvrir**. Votre fichier sélectionné remplace le fichier d’origine dans la visionneuse. 

> [!TIP]
> Si le fichier protégé ne s’ouvre pas, téléchargez et utilisez l’[outil Analyseur RMS](https://www.microsoft.com/en-us/download/details.aspx?id=46437). Suivez les instructions contenues dans l’outil pour rechercher la présence de problèmes éventuels sur votre ordinateur qui pourraient empêcher l’ouverture d’un document protégé.


## <a name="other-instructions"></a>Autres instructions
Pour obtenir des instructions pratiques, consultez les sections suivantes du guide de l’utilisateur Azure Information Protection :

-   [Que voulez-vous faire ?](client-user-guide.md#what-do-you-want-to-do)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO4-->


