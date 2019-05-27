---
title: 'Tutoriel : utiliser Azure Information Protection pour contrôler le surpartage - AIP'
description: Tutoriel d’introduction montrant comment configurer et voir en action les paramètres clients avancés du client Azure Information Protection pour avertir, demander une justification ou bloquer l’envoi de messages depuis Outlook.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 05/20/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: information-protection
ms.openlocfilehash: 889e10192cc36f7fba913683f21c18ee5e577280
ms.sourcegitcommit: fe23bc3e24eb09b7450548dc32b4ef09c8970615
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/27/2019
ms.locfileid: "65934706"
---
# <a name="tutorial-configure-azure-information-protection-to-control-oversharing-of-information-using-outlook"></a>Tutoriel : configurer Azure Information Protection pour contrôler le surpartage d’informations à l’aide d’Outlook

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Instructions pour : [Client Azure Information Protection pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Dans ce tutoriel, vous allez apprendre à :
> [!div class="checklist"]
> * Configurer des paramètres qui implémentent des messages contextuels d’avertissement, de justification ou de prévention dans Outlook
> * voir vos paramètres en pratique.
> * Passer en revue les actions et messages utilisateur journalisés dans le journal des événements 

L’e-mail est une des méthodes les plus courantes à l’aide desquelles les utilisateurs partagent des informations de façon inappropriée, qu’elles se trouvent dans l’e-mail proprement dit ou dans des pièces jointes. Vous pouvez utiliser des solutions de protection contre la perte de données qui peuvent identifier les informations sensibles connues et empêcher qu’elles franchissent les limites de votre organisation. Toutefois, vous pouvez également utiliser le client Azure Information Protection avec certains paramètres clients avancés pour empêcher le surpartage et également former vos utilisateurs avec des messages interactifs qui fournissent des commentaires en temps réel.

Ce tutoriel vous explique comment effectuer une configuration de base qui utilise une seule étiquette pour illustrer les messages d’avertissement, de justification et de prévention que les utilisateurs peuvent voir et auxquels ils peuvent répondre.

Ce tutoriel prend environ 15 minutes.

## <a name="prerequisites"></a>Prérequis 

Pour suivre ce tutoriel, il vous faut :

1. Un abonnement comportant le plan Azure Information Protection 2.
    
    Si vous n’avez pas ce type d’abonnement, vous pouvez créer un compte [gratuit](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) pour votre organisation.

2. Vous avez ajouté le panneau Azure Information Protection au portail Azure et avez au moins une étiquette.
    
    Bien que ce tutoriel utilise l’étiquette par défaut, **Général**, vous pouvez remplacer cette étiquette par une autre si vous préférez. Si vous avez besoin d’aide pour ajouter le panneau Azure Information Protection ou si vous n’avez pas d’étiquettes, consultez [Démarrage rapide : Ajouter Azure Information Protection au portail Azure et afficher la stratégie](quickstart-viewpolicy.md).

3. Un ordinateur exécutant Windows (au minimum Windows 7 avec Service Pack 1). Sur cet ordinateur, vous pouvez vous connecter à Outlook. Vous devrez peut-être redémarrer Outlook plusieurs fois au cours de ce tutoriel.

4. Le client Azure Information Protection est installé sur votre ordinateur.
    
    Pour installer le client, accédez au [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018) et téléchargez **AzInfoProtection.exe** sur la page Azure Information Protection.

Pour obtenir la liste complète des prérequis d’Azure Information Protection, voir [Prérequis d’Azure Information Protection](requirements.md).

C’est parti !

## <a name="identify-a-label-id-for-testing"></a>Identifier un ID d’étiquette pour le test

Pour ce tutoriel, nous allons utiliser une étiquette afin de voir le comportement qui en résulte pour les utilisateurs. Vous pouvez utiliser n’importe quelle étiquette, mais un bon exemple pour le test est l’étiquette par défaut nommée **Général**, qui convient généralement pour les données métier qui ne sont pas destinées à une utilisation publique et qui n’applique pas de protection.

Pour spécifier l’étiquette de votre choix, vous devez connaître son ID, que vous identifiez à partir du portail Azure :

1. Ouvrez une nouvelle fenêtre de navigateur et connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur général. Accédez ensuite à **Azure Information Protection**. 
    
    Par exemple, dans le menu hub, cliquez sur **Tous les services** et tapez **Informations** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.
    
    Si vous n’êtes pas l’administrateur général, utilisez le lien suivant pour les autres rôles : [Connexion au portail Azure](configure-policy.md#signing-in-to-the-azure-portal)

2. Sélectionnez **Classifications** > **Étiquettes**, puis sélectionnez l’étiquette **Général** pour ouvrir le panneau **Étiquette : Général**. 

3. Recherchez l’ID de l’étiquette au bas du panneau :
    
    ![Tutoriel Azure Information Protection : rechercher l’ID de étiquette](./media/label-id.png)

4. Copiez et collez la valeur d’ID de l’étiquette dans un fichier temporaire afin de pouvoir facilement copier cette valeur à une étape ultérieure. Dans notre exemple, cette valeur d’ID d’étiquette est **0e421e6d-ea17-4fdb-8f01-93a3e71333b8**.

5. Fermez le panneau **Étiquette : Général**, mais ne fermez pas le portail Azure.

## <a name="create-a-scoped-policy-to-test-the-new-advanced-client-settings"></a>Créer une stratégie délimitée pour tester les nouveaux paramètres clients avancés

Nous allons créer une stratégie délimitée afin que les nouveaux paramètres clients avancés s’appliquent uniquement à vous, à des fins de test.

1. Dans le panneau **Azure Information Protection - Stratégies**, sélectionnez **Ajouter une nouvelle stratégie**. Vous voyez alors le panneau **Stratégie** qui affiche les étiquettes et les paramètres à partir de votre stratégie globale existante.

2. Spécifiez le nom de stratégie **Tutoriel sur le surpartage** et, éventuellement, la description **Paramètres clients avancés pour contrôler le surpartage avec Outlook**.

3. Sélectionnez **Spécifier les utilisateurs/groupes qui obtiennent cette stratégie** et, à l’aide des panneaux suivants, spécifiez votre propre compte d’utilisateur.

4. Une fois que le nom de votre compte s’affiche dans le panneau **Stratégie**, sélectionnez **Enregistrer** sans apporter de modifications supplémentaires aux étiquettes ou paramètres de ce panneau. Vous pouvez être invité à confirmer votre choix. 

Cette stratégie délimitée est maintenant prête à ajouter des paramètres clients avancés. Fermez le panneau **Stratégie : Tutoriel sur le surpartage**, mais ne fermez pas le portail Azure.

## <a name="configure-and-test-advanced-client-settings-to-warn-prompt-for-justification-or-block-emails-that-have-the-general-label"></a>Configurer et tester les paramètres clients avancés pour les e-mails d’avertissement, de demande de justification ou de prévention qui ont l’étiquette Général

Pour cette étape du tutoriel, nous allons spécifier les paramètres clients avancés suivants et les tester à tour de rôle :

- **OutlookWarnUntrustedCollaborationLabel**
- **OutlookJustifyUntrustedCollaborationLabel**
- **OutlookBlockUntrustedCollaborationLabel**

### <a name="create-the-advanced-client-setting-to-warn-users-if-an-email-or-attachment-has-the-general-label"></a>Créer le paramètre client avancé pour avertir les utilisateurs si un e-mail ou une pièce jointe a l’étiquette Général

À l’aide de la stratégie délimitée créée, nous allons ajouter un nouveau paramètre client avancé nommé **OutlookWarnUntrustedCollaborationLabel** avec l’ID de votre étiquette **Général** : 

1. De retour dans le panneau **Azure Information Protection - Stratégies**, sélectionnez le menu contextuel ( **...** ) en regard de **Tutoriel sur le surpartage**. Ensuite, sélectionnez **Paramètres avancés**.

2. Dans le panneau **Paramètres avancés**, tapez le nom du paramètre avancé, **OutlookWarnUntrustedCollaborationLabel**, et collez votre propre ID d’étiquette en guise de valeur. Utilisation de notre exemple d’ID d’étiquette :
    
    
    ![Tutoriel Azure Information Protection : créer le paramètre client avancé OutlookWarnUntrustedCollaborationLabel ](./media/configure-warnmessage.png)

3. Sélectionnez **Enregistrer et fermer**.

Ne fermez pas le panneau **Stratégies** ou le portail Azure.

### <a name="test-the-advanced-client-setting-to-warn-users-if-an-email-or-attachment-has-the-general-label"></a>Tester le paramètre client avancé pour avertir les utilisateurs si un e-mail ou une pièce jointe a l’étiquette Général

Sur votre ordinateur client, nous allons maintenant voir les résultats de la configuration de ce paramètre client avancé.

1. Sur votre ordinateur client, ouvrez Outlook. 
    
    Si Outlook est déjà ouvert, redémarrez-le. Le redémarrage est nécessaire pour télécharger la modification que nous venons d’effectuer.

2. Créez un e-mail et appliquez l’étiquette **Général**. Par exemple, sous l’onglet **Fichier**, sélectionnez le bouton **Protéger**, puis sélectionnez **Général**.

3. Spécifiez votre propre adresse e-mail pour le champ **À** et, pour l’objet, tapez **Testing the General label for the Warn message**. Ensuite, envoyez l’e-mail.

4. Résultat du paramètre client avancé, vous voyez l’avertissement suivant, qui vous invite à confirmer votre souhait d’envoyer l’e-mail. Par exemple :
    
    ![Tutoriel Azure Information Protection : voir le paramètre client avancé OutlookWarnUntrustedCollaborationLabel ](./media/see-warnmessage.png)
    
5. Comme si vous aviez tenté par inadvertance d’envoyer un élément par e-mail portant l’étiquette **Général**, sélectionnez **Annuler**. Vous voyez que l’e-mail n’est pas envoyé, mais il reste accessible afin que vous puissiez apporter des modifications, telles que changer le contenu ou l’étiquette.

6. Sans apporter de modifications, resélectionnez **Envoyer**. Cette fois, comme si vous reconnaissiez que le contenu est approprié pour l’envoi, sélectionnez **Confirmer et envoyer**. L’e-mail est envoyé.

### <a name="change-the-advanced-client-setting-to-prompt-users-to-justify-if-an-email-has-the-general-label"></a>Changer le paramètre client avancé pour inviter les utilisateurs à justifier l’association de l’étiquette Général à un e-mail

Nous allons modifier le paramètre client avancé existant pour remplacer le nom par **OutlookJustifyUntrustedCollaborationLabel** tout en conservant votre ID d’étiquette **Général** : 

1. Dans le panneau **Azure Information Protection - Stratégies**, sélectionnez le menu contextuel ( **...** ) en regard de **Tutoriel sur le surpartage**. Ensuite, sélectionnez **Paramètres avancés**.

2. Dans le panneau **Paramètres avancés**, remplacez le nom du paramètre avancé précédent que vous avez créé, **OutlookWarnUntrustedCollaborationLabel**, par le nouveau nom, **OutlookJustifyUntrustedCollaborationLabel** :
    
    ![Tutoriel Azure Information Protection : créer le paramètre client avancé OutlookJustifyUntrustedCollaborationLabel ](./media/configure-justifymessage.png)

3. Sélectionnez **Enregistrer et fermer**.

Ne fermez pas le panneau **Stratégies** ou le portail Azure.

### <a name="test-the-advanced-client-setting-to-prompt-users-to-justify-if-an-email-has-the-general-label"></a>Tester le paramètre client avancé pour inviter les utilisateurs à justifier l’association de l’étiquette Général à un e-mail

Sur votre ordinateur client, nous allons maintenant voir les résultats de ce nouveau paramètre client avancé.

1. Sur votre ordinateur client, redémarrez Outlook pour télécharger la modification que vous venez d’effectuer.

2. Créez un e-mail et, comme auparavant, appliquez l’étiquette **Général**. Par exemple, sous l’onglet **Fichier**, sélectionnez le bouton **Protéger**, puis sélectionnez **Général**.

3. Spécifiez votre propre adresse e-mail pour le champ **À** et, pour l’objet, tapez **Test de l’étiquette Général pour le message de justification**. Ensuite, envoyez l’e-mail.

4. Cette fois, vous voyez le message suivant, vous invitant à indiquer une justification avant d’envoyer l’e-mail. Par exemple :
    
    ![Tutoriel Azure Information Protection : voir le paramètre client avancé OutlookJustifyUntrustedCollaborationLabel ](./media/see-justifymessage.png)
    
5. Comme si vous aviez tenté par inadvertance d’envoyer un élément par e-mail portant l’étiquette **Général**, sélectionnez **Annuler**. Vous voyez que l’e-mail n’est pas envoyé, mais il reste accessible afin que vous puissiez apporter des modifications, telles que changer le contenu ou l’étiquette.

6. Sans apporter de modifications, resélectionnez **Envoyer**. Cette fois, sélectionnez une des options de justification, telles que **Je confirme que les destinataires sont approuvés pour partager ce contenu**, puis sélectionnez **Confirmer et envoyer**. L’e-mail est envoyé.

### <a name="change-the-advanced-client-setting-to-block-users-from-sending-an-email-that-has-the-general-label"></a>Changer le paramètre client avancé pour empêcher les utilisateurs d’envoyer un e-mail portant l’étiquette Général

Nous allons modifier le paramètre client avancé existant une fois de plus pour remplacer le nom par **OutlookBlockUntrustedCollaborationLabel** tout en conservant votre ID d’étiquette **General** : 

1. Dans le portail Azure, dans le panneau **Azure Information Protection - Stratégies**, sélectionnez le menu contextuel ( **...** ) en regard de **Tutoriel sur le surpartage**. Ensuite, sélectionnez **Paramètres avancés**.

2. Dans le panneau **Paramètres avancés**, remplacez le nom du paramètre avancé précédent que vous avez créé, **OutlookJustifyUntrustedCollaborationLabel**, par le nouveau nom, **OutlookBlockUntrustedCollaborationLabel** :
    
    ![Tutoriel Azure Information Protection : créer le paramètre client avancé OutlookBlockUntrustedCollaborationLabel ](./media/configure-blockmessage.png)

3. Sélectionnez **Enregistrer et fermer**.

Ne fermez pas le panneau **Stratégies** ou le portail Azure.

### <a name="test-the-advanced-client-setting-to-block-users-from-sending-an-email-that-has-the-general-label"></a>Tester le paramètre client avancé pour empêcher les utilisateurs d’envoyer un e-mail portant l’étiquette Général

Sur votre ordinateur client, nous allons maintenant voir les résultats de ce nouveau paramètre client avancé.

1. Sur votre ordinateur client, redémarrez Outlook pour télécharger la modification que vous venez d’effectuer.

2. Créez un e-mail et, comme auparavant, appliquez l’étiquette **Général**. Par exemple, sous l’onglet **Fichier**, sélectionnez le bouton **Protéger**, puis sélectionnez **Général**.

3. Spécifiez votre propre adresse e-mail pour le champ **À** et, pour l’objet, tapez **Test de l’étiquette Général pour le message de prévention**. Ensuite, envoyez l’e-mail.

4. Cette fois, vous voyez le message suivant qui empêche l’envoi de l’e-mail. Par exemple :
    
    ![Tutoriel Azure Information Protection : empêcher l’envoi d’un e-mail avec un message contextuel](./media/see-blockmessage.png)

5. En tant qu’utilisateur, vous voyez que la seule option disponible est **OK**, qui vous ramène à l’e-mail, dans lequel vous pouvez apporter des modifications. Sélectionnez **OK** et annulez cet e-mail.

### <a name="use-event-log-to-identify-the-messages-and-user-actions-for-the-general-label"></a>Utiliser le journal des événements afin d’identifier les messages et actions utilisateur pour l’étiquette Général

Avant de passer au scénario suivant portant sur l’absence d’étiquette pour un e-mail ou une pièce jointe, démarrez l’observateur d’événements et accédez à **Journaux des applications et des services** > **Azure Information Protection**.

Pour chacun des tests que vous avez effectués, des événements d’information sont créés pour enregistrer le message et la réponse de l’utilisateur :

- Messages d’avertissement : ID d’information 301

- Justifier les messages : ID d’information 302

- Messages de blocage : ID d’information 303

Par exemple, le premier test consistait à avertir l’utilisateur, et vous avez sélectionné **Annuler** ; ainsi, la **Réponse de l’utilisateur** indique **Ignoré** dans le premier événement 301. Par exemple :

```
Client Version: 1.48.204.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing the General label for the Warn message.msg
Item Name: Testing the General label for the Warn message
Process Name: OUTLOOK
Action: Warn
Label After Action: General
Label ID After Action: 0e421e6d-ea17-4fdb-8f01-93a3e71333b8
Action Source: 
User Response: Dismissed
```

Toutefois, vous avez ensuite sélectionné **Confirmer et envoyer**, ce que reflète l’événement 301 suivant, où la **Réponse de l’utilisateur** indique **Confirmé** :

```
Client Version: 1.48.204.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing the General label for the Warn message.msg
Item Name: Testing the General label for the Warn message
Process Name: OUTLOOK
Action: Warn
Label After Action: General
Label ID After Action: 0e421e6d-ea17-4fdb-8f01-93a3e71333b8
Action Source: 
User Response: Confirmed
```

Le même modèle est répété pour le message de justification, qui a un événement 302. Le premier événement a **Ignoré** comme **Réponse de l’utilisateur**, tandis que le second indique la justification qui a été sélectionnée. Par exemple :

```
Client Version: 1.48.204.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing the General label for the Justify message.msg
Item Name: Testing the General label for the Justify message
Process Name: OUTLOOK
Action: Justify
Label After Action: General
Label ID After Action: 0e421e6d-ea17-4fdb-8f01-93a3e71333b8
User Justification: I confirm the recipients are approved for sharing this content
Action Source: 
User Response: Confirmed

```

Au début du journal des événements se trouve le message de prévention, qui a un événement 303. Par exemple :

```
Client Version: 1.48.204.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing the General label for the Block message.msg
Item Name: Testing the General label for the Block message
Process Name: OUTLOOK
Action: Block
Label After Action: General
Label ID After Action: 0e421e6d-ea17-4fdb-8f01-93a3e71333b8
Action Source: 
```

## <a name="configure-and-test-an-advanced-client-setting-to-warn-prompt-for-justification-or-block-emails-that-dont-have-a-label"></a>Configurer et tester un paramètre client avancé pour les e-mails d’avertissement, de demande de justification ou de prévention qui n’ont pas d’étiquette

Pour cette étape du tutoriel, nous allons spécifier un nouveau paramètre client avancé avec différentes valeurs et tester celles-ci à tour de rôle :

- **OutlookUnlabeledCollaborationAction**

### <a name="create-the-advanced-client-setting-to-warn-users-if-an-email-doesnt-have-a-label"></a>Créer le paramètre client avancé pour avertir les utilisateurs si un e-mail n’a pas d’étiquette

Ce nouveau paramètre client avancé nommé **OutlookUnlabeledCollaborationAction** n’a pas besoin d’ID d’étiquette, mais spécifie l’action à entreprendre pour le contenu sans étiquette : 

1. Dans le portail Azure, de retour dans le panneau **Azure Information Protection - Stratégies**, sélectionnez le menu contextuel ( **...** ) en regard de **Tutoriel sur le surpartage**. Ensuite, sélectionnez **Paramètres avancés**.

2. Dans le panneau **paramètres avancés**, tapez le nom du paramètre avancé, **OutlookUnlabeledCollaborationAction** et, en guise de valeur, spécifiez **Avertir** :
    
    ![Tutoriel Azure Information Protection : créer le paramètre client avancé OutlookUnlabeledCollaborationAction avec la valeur Avertir ](./media/configure-nolablewarn.png)

3. Sélectionnez **Enregistrer et fermer**.

Ne fermez pas le panneau **Stratégies** ou le portail Azure.

### <a name="test-the-advanced-client-setting-to-warn-users-if-an-email-doesnt-have-a-label"></a>Tester le paramètre client avancé pour avertir les utilisateurs si un e-mail n’a pas d’étiquette

Sur votre ordinateur client, nous allons maintenant voir les résultats de la configuration de ce nouveau paramètre client avancé dans les situations où le contenu n’a pas d’étiquette :

1. Sur votre ordinateur client, redémarrez Outlook pour télécharger la modification que vous venez d’effectuer.

2. Créez un e-mail et, cette fois, n’appliquez pas d’étiquette.

3. Spécifiez votre propre adresse e-mail pour le champ **À** et, pour l’objet, tapez **Test de l’envoi d’un e-mail sans étiquette pour le message d’avertissement**. Ensuite, envoyez l’e-mail.

4. Cette fois, vous voyez un message **Confirmation requise**, auquel vous pouvez répondre en choisissant **Confirmer et envoyer** ou **Annuler** :
    
    ![Tutoriel Azure Information Protection : voir le paramètre client avancé OutlookUnlabeledCollaborationAction avec la valeur Avertir](./media/see-nolablewarn.png)

5. Sélectionnez **Confirmer et envoyer**.

### <a name="change-the-advanced-client-setting-to-prompt-users-to-justify-if-an-email-is-unlabeled"></a>Changer le paramètre client avancé pour inviter les utilisateurs à justifier l’absence d’étiquette pour un e-mail

Nous allons modifier le paramètre client avancé existant pour remplacer la valeur par **Justifier** tout en conservant le nom **OutlookUnlabeledCollaborationAction** : 

1. Dans le panneau **Azure Information Protection - Stratégies**, sélectionnez le menu contextuel ( **...** ) en regard de **Tutoriel sur le surpartage**. Ensuite, sélectionnez **Paramètres avancés**.

2. Dans le panneau **Paramètres avancés**, recherchez le paramètre **OutlookUnlabeledCollaborationAction** et remplacez la valeur précédente, **Avertir**, par la nouvelle valeur, **Justifier** :
    
    ![Tutoriel Azure Information Protection : définir le paramètre client avancé OutlookUnlabeledCollaborationAction sur la valeur Justifier](./media/configure-justifymessage2.png)

3. Sélectionnez **Enregistrer et fermer**.

Ne fermez pas le panneau **Stratégies** ou le portail Azure.

### <a name="test-the-advanced-client-setting-to-prompt-users-to-justify-if-an-email-isnt-labeled"></a>Tester le paramètre client avancé pour inviter les utilisateurs à justifier l’absence d’étiquette pour un e-mail

Sur votre ordinateur client, nous allons maintenant voir les résultats de la modification de la valeur de ce paramètre client avancé.

1. Sur votre ordinateur client, redémarrez Outlook pour télécharger la modification que vous venez d’effectuer.

2. Créez un e-mail et, comme auparavant, n’appliquez pas d’étiquette.

3. Spécifiez votre propre adresse e-mail pour le champ **À** et, pour l’objet, tapez **Test de l’envoi d’un e-mail sans étiquette pour le message de justification**. Ensuite, envoyez l’e-mail.

4. Cette fois, vous voyez un message **Justification requise** avec différentes options :
    
    ![Tutoriel Azure Information Protection : voir le paramètre client avancé OutlookUnlabeledCollaborationAction avec la valeur Justifier](./media/see-nolabljustify.png)

5. Sélectionnez une option, telle que **Mon responsable a approuvé le partage de ce contenu**. Ensuite, sélectionnez **Confirmer et envoyer**.

### <a name="change-the-advanced-client-setting-to-block-users-from-sending-an-email-that-isnt-labeled"></a>Changer le paramètre client avancé pour empêcher les utilisateurs d’envoyer un e-mail ne portant pas d’étiquette

Comme auparavant, nous allons modifier le paramètre client avancé existant pour remplacer la valeur par **Empêcher** tout en conservant le nom **OutlookUnlabeledCollaborationAction** : 

1. Dans le panneau **Azure Information Protection - Stratégies**, sélectionnez le menu contextuel ( **...** ) en regard de **Tutoriel sur le surpartage**. Ensuite, sélectionnez **Paramètres avancés**.

2. Dans le panneau **Paramètres avancés**, recherchez le paramètre **OutlookUnlabeledCollaborationAction** et remplacez la valeur précédente, **Justifier**, par la nouvelle valeur, **Empêcher** :
    
    ![Tutoriel Azure Information Protection : définir le paramètre client avancé OutlookUnlabeledCollaborationAction sur la valeur Empêcher](./media/configure-blockmessage2.png)

3. Sélectionnez **Enregistrer et fermer**.

Ne fermez pas le panneau **Stratégies** ou le portail Azure.

### <a name="test-the-advanced-client-setting-to-block-users-from-sending-an-email-that-isnt-labeled"></a>Tester le paramètre client avancé pour empêcher les utilisateurs d’envoyer un e-mail ne portant pas d’étiquette

Sur votre ordinateur client, nous allons maintenant voir les résultats de la modification de la valeur de ce paramètre client avancé.

1. Sur votre ordinateur client, redémarrez Outlook pour télécharger la modification que vous venez d’effectuer.

2. Créez un e-mail et, comme auparavant, n’appliquez pas d’étiquette.

3. Spécifiez votre propre adresse e-mail pour le champ **À** et, pour l’objet, tapez **Test de l’envoi d’un e-mail sans étiquette pour le message de prévention**. Ensuite, envoyez l’e-mail.

4. Cette fois, vous voyez le message suivant qui empêche l’envoi de l’e-mail, avec une explication pour l’utilisateur. Par exemple :
    
    ![Tutoriel Azure Information Protection : voir le paramètre client avancé OutlookWarnUntrustedCollaborationLabel avec la valeur Empêcher](./media/see-blockmessage2.png)

5. En tant qu’utilisateur, vous voyez que la seule option disponible est **OK**, qui vous ramène à l’e-mail, dans lequel vous pouvez sélectionner une étiquette.
    
    Sélectionnez **OK** et annulez cet e-mail.

### <a name="use-event-log-to-identify-the-messages-and-user-actions-for-the-unlabeled-email"></a>Utiliser le journal des événements afin d’identifier les messages et actions utilisateur pour l’e-mail sans étiquette

Comme auparavant, les messages et réponses de l’utilisateur sont journalisés dans l’observateur d’événements (**Journaux des applications et des services** > **Azure Information Protection**), avec les mêmes ID d’événement.

- Messages d’avertissement : ID d’information 301

- Justifier les messages : ID d’information 302

- Messages de blocage : ID d’information 303

Par exemple, voici les résultats de notre invite de justification quand l’e-mail ne porte pas d’étiquette :

```
Client Version: 1.48.204.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing send an email without a label for the Justify message.msg
Item Name: Testing send an email without a label for the Justify message
Process Name: OUTLOOK
Action: Justify
User Justification: My manager approved sharing of this content
Action Source: 
User Response: Confirmed
```

## <a name="create-an-advanced-client-setting-to-exempt-these-messages-for-internal-recipients"></a>Créer un paramètre client avancé pour ne pas envoyer ces messages aux destinataires internes

Nous avons testé ces messages en utilisant votre propre adresse e-mail comme destinataire. Toutefois, dans un environnement de production, vous pouvez choisir de réserver l’affichage de ces messages aux destinataires qui ne font pas partie de votre organisation. Vous pouvez étendre cette exemption aux partenaires avec lesquels votre organisation travaille régulièrement.

En guise d’illustration, nous allons créer un paramètre client avancé nommé **OutlookBlockTrustedDomains** et spécifier votre propre nom de domaine à partir de votre adresse e-mail. Ainsi, le message de prévention ne s’affiche pas pour les destinataires dont l’adresse e-mail partage votre nom de domaine. De même, vous pouvez créer des paramètres clients avancés pour **OutlookWarnTrustedDomains** et **OutlookJustifyTrustedDomains**.

1. Dans le portail Azure, dans le panneau **Azure Information Protection - Stratégies**, sélectionnez le menu contextuel ( **...** ) en regard de **Tutoriel sur le surpartage**. Ensuite, sélectionnez **Paramètres avancés**.

2. Dans le panneau **paramètres avancés**, tapez le nom du paramètre avancé, **OutlookBlockTrustedDomains**, et, en guise de valeur, collez votre nom de domaine à partir de votre adresse e-mail. Par exemple :
    
    ![Tutoriel Azure Information Protection : créer le paramètre client avancé OutlookBlockTrustedDomains](./media/configure-exemptblockdomain.png)

4. Sélectionnez **Enregistrer et fermer**. Ne fermez pas le panneau **Stratégies** ou le portail Azure.

5. Répétez le [test précédent pour envoyer un e-mail sans étiquette à votre propre adresse](#test-the-advanced-client-setting-to-block-users-from-sending-an-email-that-isnt-labeled) ; vous ne voyez plus le message de prévention. Toutefois, si vous ajoutez un nouveau destinataire n’appartenant pas à votre organisation, le message de prévention réapparaît.

## <a name="clean-up-resources"></a>Nettoyer les ressources

Si vous ne souhaitez pas conserver les modifications que vous avez effectuées dans ce tutoriel, procédez ainsi :

1. Dans le portail Azure, dans le panneau **Azure Information Protection - Stratégies**, sélectionnez le menu contextuel ( **...** ) en regard de **Tutoriel sur le surpartage**. Ensuite, sélectionnez **Supprimer la stratégie**.

2. Si vous êtes invité à confirmer, sélectionnez **OK**.

Redémarrez Outlook afin qu’il ne soit plus configuré pour les paramètres que nous avons définis pour ce tutoriel.

## <a name="next-steps"></a>Étapes suivantes

Pour que les tests soient plus rapides, ce tutoriel utilise un e-mail pour un seul destinataire et sans pièces jointes. Mais vous pouvez appliquer la même méthode avec plusieurs destinataires, plusieurs étiquettes et également appliquer la même logique aux pièces jointes dont l’état d’étiquetage est souvent moins évident pour les utilisateurs. Par exemple, l’e-mail proprement dit est étiqueté Public, mais la présentation PowerPoint jointe est étiquetée Général. Pour plus d’informations, consultez la section suivante dans le guide de l’administrateur : [Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](./rms-client/client-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)

Le guide de l’administrateur contient également des informations sur les autres paramètres clients avancés que vous pouvez utiliser pour personnaliser le comportement du client. Pour obtenir la liste complète, consultez [Paramètres client avancés disponibles](./rms-client/client-admin-guide-customizations.md#available-advanced-client-settings).
