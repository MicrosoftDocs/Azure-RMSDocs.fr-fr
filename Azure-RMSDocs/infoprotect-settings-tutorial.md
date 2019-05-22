---
title: 'Tutoriel : utiliser les paramètres de stratégie Azure Information Protection pour classer les données'
description: Tutoriel d’introduction qui vous guide dans la configuration des paramètres de stratégie Azure Information Protection pour classer les documents et e-mails de votre organisation.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 05/20/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: information-protection
ms.openlocfilehash: 2341bfbdc443a15096d178b143e6bd1464b1a53e
ms.sourcegitcommit: 8532536b778a26b971dba89436772158869ab84d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65935078"
---
# <a name="tutorial-configure-azure-information-protection-policy-settings-that-work-together"></a>Tutoriel : Configurer les paramètres de stratégie Azure Information Protection qui interagissent

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Instructions pour : [Client Azure Information Protection pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Dans ce tutoriel, vous allez apprendre à :
> [!div class="checklist"]
> * configurer des paramètres de stratégie qui fonctionnent ensemble ;
> * voir vos paramètres en pratique.

Au lieu de demander aux utilisateurs d’étiqueter manuellement leurs documents et e-mails, vous pouvez utiliser les paramètres de stratégie pour :

- garantir un niveau de classification de base pour le nouveau contenu et le contenu modifié ;

- informer les utilisateurs sur les étiquettes et leur faciliter le travail pour qu’ils puissent appliquer la bonne étiquette.

Ce tutoriel prend environ 15 minutes.

## <a name="prerequisites"></a>Prérequis 

Pour suivre ce tutoriel, il vous faut :

1. Un abonnement comportant le plan Azure Information Protection 1 ou 2.
    
    Si vous n’avez pas ce type d’abonnement, vous pouvez créer un compte [gratuit](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) pour votre organisation.

2. Vous avez ajouté le panneau Azure Information Protection au Portail Azure et vérifié que le service de protection est activé.

    Si vous avez besoin d’aide avec ces actions, consultez [Démarrage rapide : Ajouter Azure Information Protection au portail Azure et afficher la stratégie](quickstart-viewpolicy.md)

3. Le client Azure Information Protection est installé sur votre ordinateur. 
    
    Pour installer le client, accédez au [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018) et téléchargez **AzInfoProtection.exe** sur la page Azure Information Protection.

4. Un ordinateur Windows (au minimum Windows 7 avec Service Pack 1) sur lequel vous avez établi une connexion aux applications Office de l’une des catégories suivantes :
    
    - Applications Office version minimale 1805, build 9330.2078 d’Office 365 Business ou de Microsoft 365 Business quand une licence Azure Rights Management (également appelé Azure Information Protection pour Office 365) vous est affectée.
    
    - Office 365 ProPlus.
    
    - Office Professionnel Plus 2019.
    
    - Office Professionnel Plus 2016.
    
    - Office Professionnel Plus 2013 avec Service Pack 1.
    
    - Office Professionnel Plus 2010 avec Service Pack 2.

Pour obtenir la liste complète des prérequis d’Azure Information Protection, voir [Prérequis d’Azure Information Protection](requirements.md).

C’est parti !

## <a name="edit-the-azure-information-protection-policy"></a>Modifier la stratégie Azure Information Protection

Au lieu de demander aux utilisateurs d’étiqueter manuellement leurs documents et e-mails, vous pouvez utiliser certains paramètres de stratégie pour garantir un niveau de classification de base. 

Sur le Portail Azure, nous allons modifier la stratégie globale de façon à changer les paramètres de stratégie pour tous les utilisateurs.

1. Ouvrez une nouvelle fenêtre de navigateur et connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur général. Accédez ensuite à **Azure Information Protection**. 
    
    Par exemple, dans le menu hub, cliquez sur **Tous les services** et tapez **Informations** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.
    
    Si vous n’êtes pas l’administrateur général, utilisez le lien suivant pour les autres rôles : [Connexion au portail Azure](configure-policy.md#signing-in-to-the-azure-portal)

2. Sélectionnez **Classifications** > **Stratégies** > **Global** pour ouvrir le panneau **Stratégie : Globale**. 

3. Localisez les paramètres de stratégie après les étiquettes, dans la section **Configurer les paramètres à présenter et à appliquer aux utilisateurs finaux d’Information Protection**. Vos paramètres peuvent avoir des valeurs différentes de celles qui s’affichent :
    
    ![Tutoriel Azure Information Protection – paramètres par défaut](./media/defaultsettings-aip.png)

4. Modifiez vos paramètres en les remplaçant par la valeur du tableau suivant. Prenez note des paramètres que vous modifiez au cas où vous souhaiteriez les rechanger après la fin de ce tutoriel. 

    |Paramètre|Valeur|Informations|
    |-------|-----|-----|
    |**Sélectionner l’étiquette par défaut**|**Général**|Si vous n’avez pas d’étiquette nommée **Général**, sélectionnez une autre étiquette dans la liste déroulante. Elle s’applique automatiquement comme classification de base aux documents et aux e-mails sans étiquette. Toutefois, les utilisateurs peuvent remplacer l’étiquette que vous avez sélectionnée par une autre.|
    |**Tous les documents et les e-mails doivent avoir une étiquette**|**Activé**|Ce paramètre est souvent appelé étiquetage obligatoire, car il empêche les utilisateurs d’enregistrer des documents ou d’envoyer des e-mails sans étiquette. En parallèle de l’étiquette par défaut, les documents et les e-mails auront soit l’étiquette par défaut que vous avez définie, soit l’étiquette de leur choix.
    |**Pour les e-mails avec pièces jointes, appliquez une étiquette correspondant à la classification la plus élevée de ces pièces jointes**|**Recommandé**|Ce paramètre invite aux utilisateurs à sélectionner une étiquette de classification plus élevée pour leurs e-mails quand ils joignent des documents ayant une classification plus élevée que l’étiquette que vous avez sélectionnée par défaut.
    |**Afficher la barre Information Protection dans les applications Office**|**Activé**|L’affichage de la barre Information Protection permet aux utilisateurs d’afficher et de modifier plus facilement l’étiquette par défaut.
    
    Les paramètres devraient maintenant se présenter ainsi :
    
    ![Tutoriel Azure Information Protection – modification des paramètres par défaut](./media/defaultsettings-aip-changed.png)

5. Sélectionnez **Enregistrer** dans ce panneau **Stratégie : Globale** et, si vous êtes invité à confirmer votre action, sélectionnez **OK**. 

## <a name="see-your-policy-settings-in-action"></a>Voir vos paramètres de stratégie en pratique 

Pour ce tutoriel, nous allons utiliser Word et Outlook pour voir les modifications de la stratégie en pratique. Si ces applications étaient déjà chargées avant que vous ne changiez les paramètres de stratégie, redémarrez-les pour télécharger les modifications.

### <a name="default-label-and-the-information-protection-bar"></a>Étiquette par défaut et barre Azure Information Protection

Ouvrez un nouveau document dans Word. Comme vous le voyez, le document est automatiquement étiqueté comme **Général**, sans qu’il soit demandé aux utilisateurs de sélectionner une étiquette. 

La barre Information Protection, qui présente les étiquettes disponibles, permet aux utilisateurs de voir l’étiquette actuellement sélectionnée et de la modifier si l’étiquette par défaut n’est pas adaptée :

![Tutoriel Azure Information Protection – nouveau document avec l’étiquette par défaut](./media/defaultlabel-word.png)

Au lieu de modifier l’étiquette, fermez la barre Information Protection pour comparer l’expérience lorsque la barre n’est pas affichée :

![Tutoriel Azure Information Protection : fermer la barre](./media/infoprotect-bar-close.png)

L’étiquette **Général**, quoique toujours sélectionnée, est beaucoup moins évidente. Le moyen de sélectionner une autre étiquette apparaît également moins clairement. Pour cela, les utilisateurs doivent sélectionner le bouton **Protéger** :

![Tutoriel Azure Information Protection – bouton Protéger sélectionné](./media/infoprotect-protectbutton-pulldown.png)

On voit maintenant que l’étiquette **Général** est sélectionnée dans le menu déroulant au fait qu’il y a une coche à côté. Pour modifier l’étiquette actuellement sélectionnée, les utilisateurs peuvent en sélectionner une autre dans la liste. Les utilisateurs qui ne connaissent pas l’étiquetage ne penseront probablement pas à sélectionner le bouton **Protéger** à chaque fois. Ils ne se rendent pas forcément compte qu’ils peuvent sélectionner une autre étiquette.

Pour afficher à nouveau la barre Information Protection, sélectionnez **Afficher la barre** dans le menu déroulant.

> [!TIP]
> Vous pouvez sélectionner une autre étiquette par défaut pour Outlook, en configurant un [paramètre client avancé](./rms-client/client-admin-guide-customizations.md#set-a-different-default-label-for-outlook).

### <a name="mandatory-labeling"></a>Étiquetage obligatoire

Vous pouvez remplacer l’étiquette **Général** actuellement sélectionnée par une autre étiquette, mais pas la supprimer. Puisque nous avons **activé** **Tous les documents et e-mails doivent avoir une étiquette**, l’icône **Supprimer l’étiquette** n’est pas disponible sur la barre Information Protection. 

Si nous n’avions pas modifié ce paramètre, la barre Information Protection montrerait cette icône :

![Tutoriel Azure Information Protection : fermer la barre](./media/infoprotect-deletelabel-icon.png)

Avec une étiquette par défaut, l’étiquetage obligatoire permet de garantir que les nouveaux documents et les documents modifiés (tout comme les e-mails) ont une classification de base de votre choix. 

Si nous n’avions pas défini d’étiquette par défaut avec le paramètre d’étiquetage obligatoire, les utilisateurs seraient toujours invités à sélectionner une étiquette lorsqu’ils enregistreraient un document sans étiquette ou enverraient un e-mail sans étiquette. Pour de nombreux utilisateurs, ces invites continuelles peuvent être agaçantes et occasionner un étiquetage moins précis. Le fait d’être invité à sélectionner une étiquette après avoir fini de travailler sur un document ou un e-mail interrompt le flux de travail ; il est alors tentant de sélectionner une étiquette au hasard afin de pouvoir passer à la tâche suivante.

### <a name="recommendations-for-emails-with-attachments"></a>Recommandations pour les e-mails avec pièces jointes

Pour le document Word ouvert, choisissez une étiquette ayant une classification plus élevée que **Général** : par exemple, l’une des sous-étiquettes sous **Confidentiel**, comme **Confidentiel – Tout le monde (non protégé)**. Enregistrez le document localement et donnez-lui n’importe quel nom. 

Démarrez Outlook et créez un e-mail. Comme nous l’avons vu avec Word, le nouvel e-mail est automatiquement étiqueté comme **Général** et la barre Information Protection s’affiche.

Ajoutez le document Word que vous venez d’étiqueter en pièce jointe à l’e-mail. Il vous est proposé de remplacer l’étiquette de l’e-mail par l’étiquette **Confidentiel** correspondant à la pièce jointe Word. Vous pouvez accepter la recommandation ou l’ignorer :

![Tutoriel Azure Information Protection – invite à réétiqueter l’e-mail en fonction de la pièce jointe étiquetée](./media/infoprotect-matchemail-label.png)

Si vous cliquez sur **Ignorer**, la nouvelle étiquette n’est pas appliquée et l’e-mail conserve l’étiquette par défaut que nous avons configurée, **Général**. Les étiquettes disponibles sont toujours visibles et peuvent être sélectionnées.

Si vous sélectionnez **Modifier maintenant**, l’e-mail est réétiqueté avec la sous-étiquette **Confidentiel**. Toutefois, les utilisateurs peuvent toujours changer cette étiquette avant d’envoyer l’e-mail, en sélectionnant l’icône Modifier l’étiquette :

![Tutoriel Azure Information Protection : modifier l’icône d’une étiquette](./media/infoprotect-editlabel-icon.png)

La barre Information Protection s’affiche à nouveau pour permettre aux utilisateurs de sélectionner une autre étiquette.

Étant donné que l’étiquette est sélectionnée avant que l’e-mail soit envoyé, il n’est pas nécessaire d’envoyer l’e-mail pour observer le fonctionnement de ce paramètre de stratégie. Vous pouvez fermer l’e-mail sans l’envoyer ni l’enregistrer.

Toutefois, il peut être intéressant de répéter cet exercice, mais aussi de joindre un autre document qui possède une classification plus élevée (une sous-étiquette de l’étiquette **Hautement confidentiel**). L’invite sera alors différente : elle proposera d’appliquer l’étiquette de classification la plus élevée. Si vous testez plusieurs pièces jointes avec des sous-étiquettes qui ont la même étiquette parente, vous devez configurer [un paramètre client avancé](./rms-client/client-admin-guide-customizations.md#enable-order-support-for-sublabels-on-attachments) pour prendre en charge leur classement dans le portail Azure.

## <a name="clean-up-resources"></a>Nettoyer les ressources

Si vous ne souhaitez pas conserver les modifications que vous avez effectuées dans ce tutoriel, procédez ainsi :

1. Sélectionnez **Classifications** > **Stratégies** > **Global** pour ouvrir le panneau **Stratégie : Globale**.

2. Rétablissez les valeurs d’origine (dont vous avez pris note) des paramètres de stratégie, puis sélectionnez **Enregistrer**.

Redémarrez vos applications Word et Outlook pour télécharger ces modifications.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la modification des paramètres de stratégie Azure Information Protection, voir [Guide pratique pour configurer les paramètres de stratégie pour Azure Information Protection](configure-policy-settings.md).

Les paramètres de stratégie que nous avons modifiés ont permis de garantir un niveau de classification de base, mais aussi d’encourager les utilisateurs à sélectionner une étiquette adaptée. L’étape suivante consiste à renforcer cette stratégie en examinant le contenu de documents et des e-mails, puis en recommandant ou en appliquant automatiquement la bonne étiquette. Il faut pour cela configurer les conditions dans les étiquettes. Pour plus d’informations, voir [Guide pratique pour configurer des conditions pour la classification automatique et recommandée pour Azure Information Protection](configure-policy-classification.md).
