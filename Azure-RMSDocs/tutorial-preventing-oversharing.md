---
title: Tutoriel - Empêcher les partages inappropriés avec Azure Information Protection (AIP)
description: Tutoriel détaillé sur l’utilisation du client Azure Information Protection (AIP) pour empêcher les utilisateurs de partager votre contenu de façon inappropriée.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/09/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 8d86d6f114bd1a0886883b9cda277ffd6ae9904b
ms.sourcegitcommit: 2cf5002f34eee9929cdc22d6b6e64d5734dec816
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/09/2020
ms.locfileid: "94377131"
---
# <a name="tutorial-preventing-oversharing-in-outlook-using-azure-information-protection-aip"></a>Tutoriel : Empêcher les partages inappropriés dans Outlook avec Azure Information Protection (AIP)

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>*Instructions pour : [Client d’étiquetage unifié Azure Information Protection pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

En tant qu’administrateur système, vous devez faire en sorte que le contenu de votre organisation reste sécurisé et partagé seulement avec des utilisateurs approuvés. Une des façons les plus courantes avec laquelle les utilisateurs partagent le contenu de manière inappropriée est l’e-mail. Configurez votre stratégie pour empêcher le partage inapproprié via Outlook, par exemple en limitant l’accès à des utilisateurs spécifiques ou en autorisant les utilisateurs à partager du contenu seulement avec des utilisateurs externes approuvés.

**Temps nécessaire :** Vous pouvez suivre ce tutoriel en 30 minutes.

Dans ce tutoriel, vous allez apprendre à :
> [!div class="checklist"]
> * Configurer des comportements d’avertissement, de justification et de blocage pour des conditions d’étiquetage spécifiques
> * voir vos paramètres en pratique.
> * Passer en revue les actions et messages utilisateur journalisés dans le journal des événements 

## <a name="tutorial-prerequisites"></a>Configuration requise pour le didacticiel

Avant de commencer ce tutoriel, veillez à disposer de la configuration système requise suivante.

|Prérequis  |Description  |
|---------|---------|
|**Configuration requise pour la machine**     | Veillez à : <br /><br />- Disposer d’un ordinateur Windows, avec le client d’étiquetage unifié Azure Information Protection installé. Pour plus d’informations, consultez [Démarrage rapide : Déploiement du client d’étiquetage unifié Azure Information Protection (AIP)](quickstart-deploy-client.md) <br /><br />- Avoir PowerShell installé et pouvoir l’exécuter en tant qu’administrateur. <br /><br />- Pouvoir vous connecter à Outlook. Vous devrez peut-être redémarrer Outlook plusieurs fois au cours de ce tutoriel.     |
|**Abonnement à Azure Information Protection**     |   Vous devez avoir un [abonnement](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) Azure incluant le **Plan 2 d’Azure Information Protection**.      |
|**Des étiquettes de sensibilité et une stratégie de test**     |  Une étiquette de sensibilité **Général** configurée dans votre stratégie. <br /><br />Configurez des étiquettes de sensibilité dans le Centre d’administration d’étiquetage, notamment le Centre de conformité Microsoft 365, le Centre de sécurité Microsoft 365 ou le Centre de sécurité et de conformité Microsoft 365. Pour plus d’informations, consultez la [documentation Microsoft 365](https://docs.microsoft.com/microsoft-365/compliance/create-sensitivity-labels). <br /><br />Nous vous recommandons d’utiliser une stratégie de test pour ce tutoriel afin de ne pas affecter votre stratégie en cours. <br />Veillez à avoir le nom de votre stratégie sous la main ainsi que le GUID pour votre étiquette **Général**.   |
| | |

Allons-y. 

## <a name="implement-a-warning-message-for-emails-labeled-as-general"></a>Implémenter un message d’avertissement pour les e-mails étiquetés « Général »

Cette procédure décrit comment configurer votre stratégie pour avertir les utilisateurs Outlook avant qu’ils envoient un e-mail étiqueté **Général**. 

Les utilisateurs peuvent choisir de tenir compte de l’avertissement, et de changer l’étiquette ou le contenu, ou ils peuvent choisir d’envoyer quand même l’e-mail.

1. Sur l’ordinateur client, exécutez PowerShell en tant qu’administrateur.

1. Exécutez la commande suivante pour définir un message d’avertissement pour l’étiquette **Général**. Quand vous copiez cette commande, remplacez **Global** par le nom de votre stratégie et la longue chaîne de caractères par l’ID de votre propre étiquette.

    ```PowerShell
    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookWarnUntrustedCollaborationLabel="8faca7b8-8d20-48a3-8ea2-0f96310a848e"}
    ```

    Dans cet exemple, la stratégie est nommée **Global** et le GUID de l’étiquette **Général** est **8faca7b8-8d20-48a3-8ea2-0f96310a848e**.

    > [!TIP]
    > Si vous souhaitez appliquer ce paramètre à plusieurs étiquettes, listez leurs GUID dans la valeur, en les séparant par des virgules.

1. Testez votre paramètre dans Outlook :

    1. Sur votre ordinateur client, ouvrez ou redémarrez Outlook pour appliquer les paramètres mis à jour.

    1. Créez un e-mail et appliquez l’étiquette **Général**. Dans la barre d’outils du message, sélectionnez le bouton :::image type="icon" source="media/i-sensitivity.PNG" border="false"::: **Sensibilité**, puis sélectionnez **Général**.

    1. Définissez le champ **À** sur votre propre adresse e-mail et le **champ Objet** sur `Testing a warning message for the General label`, puis envoyez l’e-mail.

        Vous voyez normalement l’avertissement suivant, qui vous invite à confirmer votre souhait d’envoyer l’e-mail. Exemple :

        :::image type="content" source="media/qs-tutor/ul-see-warnmessage.png" alt-text="Test d’un message d’avertissement pour l’étiquette Général":::

    1. Supposons que vous avez tenté par inadvertance d’envoyer par e-mail quelque chose qui était étiqueté **Général**. Dans ce cas, vous voulez tenir compte de l’avertissement, donc sélectionnez **Annuler**.

        Votre e-mail n’est pas envoyé, mais il reste ouvert pour vous permettre de changer le contenu ou l’étiquette.

    1. Il n’est pas nécessaire d’effectuer des modifications et vous pouvez décider que le contenu peut être envoyé. Sélectionnez à nouveau **Envoyer**. Cette fois, quand l’avertissement apparaît, sélectionnez **Confirmer et envoyer**.

        L’e-mail est envoyé.

Poursuivez avec [Montrer un message d’avertissement pour les e-mails « Général » seulement quand ils sont envoyés en externe](#show-a-warning-message-for-general-emails-only-when-theyre-sent-externally).

## <a name="show-a-warning-message-for-general-emails-only-when-theyre-sent-externally"></a>Montrer un message d’avertissement pour les e-mails « Général » seulement quand ils sont envoyés en externe

Cette procédure décrit comment ajouter une exception au message d’avertissement que vous avez configuré précédemment, afin que ce message s’affiche seulement pour les destinataires externes.

Lors de l’envoi d’un e-mail **Général** en interne, le message d’avertissement n’est pas affiché.

1. Sur l’ordinateur client, exécutez PowerShell en tant qu’administrateur.

1. Exécutez la commande suivante pour définir votre domaine en tant que domaine approuvé pour les messages d’avertissement. Quand vous copiez cette commande, remplacez **Global** par le nom de votre stratégie et **contoso.com** par votre propre domaine.

    ```PowerShell
    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookWarnTrustedDomains="contoso.com"}    
    ```

    > [!TIP]
    > Si vous voulez appliquer ce paramètre à plusieurs domaines, par exemple si vous souhaitez ajouter des partenaires approuvés, listez leurs domaines dans la valeur en les séparant par des virgules.

1. Testez votre paramètre dans Outlook :

    1. Sur votre ordinateur client, ouvrez ou redémarrez Outlook pour appliquer les paramètres mis à jour.

    1. Créez un e-mail et appliquez l’étiquette **Général**. Dans la barre d’outils du message, sélectionnez le bouton :::image type="icon" source="media/i-sensitivity.PNG" border="false"::: **Sensibilité**, puis sélectionnez **Général**.

    1. Définissez le champ **À** sur votre propre adresse e-mail et le **champ Objet** sur `Testing a warning message for the General label`, puis envoyez l’e-mail.

        L’e-mail est envoyé et aucun avertissement n’est affiché.

## <a name="request-users-to-justify-sending-unlabeled-content"></a>Demander aux utilisateurs de justifier l’envoi de contenu sans étiquette

Cette procédure décrit comment configurer des paramètres avancés afin que les utilisateurs doivent justifier leur raisonnement pour l’envoi de contenu sans étiquette. 

1. Sur l’ordinateur client, exécutez PowerShell en tant qu’administrateur.

1. Pour qu’Outlook affiche un message de justification pour vos utilisateurs s’ils essaient d’envoyer un e-mail sans étiquette, remplacez **Global** par le nom de votre stratégie, puis exécutez :
 
    ```PowerShell
    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookUnlabeledCollaborationAction="Justify"}
    ```

1. Testez votre paramètre dans Outlook :

    1. Sur votre ordinateur client, ouvrez ou redémarrez Outlook pour appliquer les paramètres mis à jour.

    1. Créez un nouvel e-mail et vérifiez qu’aucune étiquette ne lui est appliquée.
    
        Par exemple, si votre stratégie applique une étiquette par défaut, utilisez le bouton :::image type="icon" source="media/i-sensitivity.PNG" border="false"::: pour la supprimer. 

    1. Définissez le champ **À** sur votre propre adresse e-mail et le **champ Objet** sur `Testing the justification message for unlabeled content`, puis envoyez l’e-mail.
    
        Une fenêtre contextuelle similaire à l’exemple suivant est affichée :

        :::image type="content" source="media/qs-tutor/ul-see-nolabljustify.png" alt-text="Exemple de message de justification pour du contenu sans étiquette":::

    1. Sélectionnez l'une des options. Si vous sélectionnez la troisième option **Autre, voir explication**, entrez un exemple de texte dans la zone de texte. 
    
    1. Sélectionnez **Confirmer et envoyer**.
    
        L’e-mail est envoyé.

Poursuivez avec [Personnaliser l’invite de justification de justification en texte libre](#customize-the-free-text-justification-prompt).

## <a name="customize-the-free-text-justification-prompt"></a>Personnaliser l’invite de justification de justification en texte libre

Cette procédure décrit comment personnaliser la troisième option dans le message de justification par défaut. 

Par exemple, vous voulez y ajouter du texte pour inviter l’utilisateur à ajouter des détails spécifiques ou rappeler aux utilisateurs de ne pas entrer de données sensibles.

1. Sur l’ordinateur client, exécutez PowerShell en tant qu’administrateur.

1. Pour personnaliser l’invite en texte libre dans le message de justification affiché, remplacez **Global** par le nom de votre stratégie, puis exécutez :

    ```PowerShell
    Set-LabelPolicy -Identity Global -AdvancedSettings @{JustificationTextForUserText="Other (please explain) - Do not enter sensitive info"}
    ```

    > [!TIP]
    > N’hésitez pas à remplacer la valeur entre guillemets par un autre texte que vous voulez ajouter à la place. 

1. Testez votre paramètre dans Outlook :

    1. Sur votre ordinateur client, ouvrez ou redémarrez Outlook pour appliquer les paramètres mis à jour.

    1. Créez un nouvel e-mail et vérifiez qu’aucune étiquette ne lui est appliquée. 

        Par exemple, si votre stratégie applique une étiquette par défaut, utilisez le bouton :::image type="icon" source="media/i-sensitivity.PNG" border="false"::: pour la supprimer. 

    1. Définissez le champ **À** sur votre propre adresse e-mail et le **champ Objet** sur `Testing a customized free text justification prompt`, puis envoyez l’e-mail.
    
        La fenêtre contextuelle de justification s’affiche, cette fois avec votre texte personnalisé. Exemple : 

        :::image type="content" source="media/qs-tutor/ul-see-nolabljustify-custom.png" alt-text="Exemple d’invite de justification avec une invite en texte libre personnalisée":::
        
## <a name="block-users-from-sending-unlabeled-powerpoint-messages"></a>Empêcher les utilisateurs d’envoyer des messages PowerPoint sans étiquette

Cette procédure décrit comment empêcher les utilisateurs d’envoyer des fichiers PowerPoint sans étiquette à partir d’Outlook.

1. Sur l’ordinateur client, exécutez PowerShell en tant qu’administrateur.

1. Pour empêcher l’envoi d’un contenu sans étiquette à partir d’Outlook, remplacez **Global** par le nom de votre stratégie, puis exécutez :

    ```PowerShell
    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookUnlabeledCollaborationAction="Block"}
    ```

1. Pour limiter le comportement de blocage aux types de fichiers PowerPoint spécifiques, remplacez **Global** par le nom de votre stratégie, puis exécutez :

    ```PowerShell
    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookOverrideUnlabeledCollaborationExtensions=".PPTX,.PPTM,.POTX,.POTM,.POT,.PPTX"}
    ```

1. Testez votre paramètre dans Outlook :

    1. Sur votre ordinateur client, ouvrez PowerPoint et créez un fichier **.pptx**, en veillant à laisser le fichier sans étiquette.

    1. Ouvrez ou redémarrez Outlook pour appliquer les paramètres mis à jour.
    
    1. Attachez votre fichier PowerPoint sans étiquette à un nouveau message Outlook.

    1. Définissez le champ **À** sur votre propre adresse e-mail et le **champ Objet** sur `Testing sending unlabeled PowerPoint files`, puis envoyez l’e-mail.
    
        Outlook bloque l’envoi de l’e-mail et affiche le message suivant :

        :::image type="content" source="media/qs-tutor/ul-see-blockmessage.png" alt-text="Exemple de message de blocage pour une pièce jointe PowerPoint sans étiquette":::

Poursuivez avec [Personnaliser le message de blocage pour les messages PowerPoint sans étiquette](#customize-the-block-message-for-unlabeled-powerpoint-messages).

## <a name="customize-the-block-message-for-unlabeled-powerpoint-messages"></a>Personnaliser le message de blocage pour les messages PowerPoint sans étiquette

Cette procédure décrit comment personnaliser le message qui apparaît quand un utilisateur tente d’envoyer un fichier PowerPoint sans étiquette à des utilisateurs externes.

> [!IMPORTANT]
> Cette procédure va remplacer tous les paramètres que vous avez déjà définis en utilisant la propriété avancée **OutlookUnlabeledCollaborationAction** et elle est montrée seulement pour les objectifs de ce tutoriel.
>
> En production, nous vous recommandons d’éviter les complications en utilisant la propriété avancée **OutlookUnlabeledCollaborationAction** pour définir vos règles *ou* en définissant des règles complexes avec un fichier JSON, comme indiqué ci-dessous, mais *pas les deux*.
>

**Pour définir votre règle en utilisant un fichier JSON :**

1. Créez un fichier **.json** nommé **OutlookCollaborationRule_1.json** avec le code suivant :

    ```JSON
    {   
    "type" : "And",     
    "nodes" : [         
        {           
            "type" : "Except" ,             
            "node" :{               
                "type" : "SentTo",                  
                "Domains" : [                   
                    "contoso.com",                  
                ]               
            }       
        },
        {           
            "type" : "Or",          
            "nodes" : [                 
                {           
                    "type" : "AttachmentLabel",
                     "LabelId" : null,
                    "Extensions": [
                                    ".PPTX",
                                    ".PPTM",
                                    ".POTX",
                                    ".POTM",
                                    ".POT",
                                    ".PPTX"
                                 ]
                    
                },
                {                   
                    "type" : "EmailLabel",
                     "LabelId" : null
                }
            ]
        },      
        {           
            "type" : "Email Block",             
            "LocalizationData": {               
                "en-us": {                
                    "Title": "Email Blocked",                 
                    "Body": "Sending PowerPoint files to external recipients requires that you label your files so that we can classify and protect Contoso content.<br><br>List of attachments that are not labeled:<br><br>${MatchedAttachmentName}<br><br><br>This message will not be sent.<br>You are responsible for ensuring compliance to classification requirement as per Contoso’s policies.<br><br>Label your document and send it again."              
                },          
            },          
            "DefaultLanguage": "en-us"      
        }   
      ] 
    }
    ```
1. Enregistrez votre fichier **OutlookCollaborationRule_1.json** à un emplacement accessible par votre ordinateur client.

1. Sur l’ordinateur client, exécutez PowerShell en tant qu’administrateur.

1. Pour personnaliser votre message de blocage, copiez le code suivant, en remplaçant **C:\ OutlookCollaborationRule_1.json** par le chemin de votre fichier .json et **Général** par le nom de votre stratégie. 

    ```PowerShell
    $filedata = Get-Content "C:\OutlookCollaborationRule_1.json”
    Set-LabelPolicy -Identity General -AdvancedSettings @{OutlookCollaborationRule_1 ="$filedata"}    
    ```

    Exécutez le code pour implémenter les paramètres définis dans votre fichier .json.

1. Testez votre paramètre dans Outlook :

    1. Sur votre ordinateur client, ouvrez PowerPoint et créez un fichier **.pptx**, en veillant à laisser le fichier sans étiquette.

    1. Ouvrez ou redémarrez Outlook pour appliquer les paramètres mis à jour.
    
    1. Attachez votre fichier PowerPoint sans étiquette à un nouveau message Outlook.

    1. Définissez le champ **À** sur votre propre adresse e-mail et le **champ Objet** sur `Testing customized blocking message for unlabeled PowerPoint files`, puis envoyez l’e-mail.
    
        Outlook bloque l’envoi de l’e-mail et affiche le message suivant :

        :::image type="content" source="media/qs-tutor/ul-see-custom-blockmessage.png" alt-text="Message de blocage personnalisé pour les fichiers PowerPoint sans étiquette":::

Poursuivez avec [Utiliser le journal des événements afin d’identifier les messages et actions utilisateur pour l’étiquette Général](#use-event-log-to-identify-the-messages-and-user-actions-for-the-general-label)

## <a name="use-event-log-to-identify-the-messages-and-user-actions-for-the-general-label"></a>Utiliser le journal des événements afin d’identifier les messages et actions utilisateur pour l’étiquette Général

Dans ce tutoriel , vous avez découvert comment personnaliser le comportement d’AIP dans Outlook pour empêcher certains types de partages inappropriés, notamment les messages d’avertissement, de justification et de blocage. Vous avez également vérifié le comportement d’Outlook sur votre ordinateur client local.

Vous pouvez maintenant démarrer l’observateur d’événements Windows pour rechercher dans les journaux les actions qui se sont produites.

**Pour rechercher les événements de journalisation AIP dans l’observateur d’événements :**

Sur votre ordinateur client, ouvrez l’application Observateur d’événements Windows et accédez à **Journaux des applications et des services** > **Azure Information Protection**.

Vous allez voir un événement d’information journalisé pour chaque test que vous avez effectué, notamment des détails sur le message et sur la réponse de l’utilisateur :

- **Messages d’avertissement :** ID d’information 301
- **Messages de justification :** ID d’information 302
- **Messages de blocage :** ID d’information 303

Exemple :

- [Rechercher les tests de votre message d’avertissement dans le journal des événements](#check-the-event-log-for-your-warning-message-tests)
- [Rechercher les tests de votre message de justification dans le journal des événements](#check-the-event-log-for-your-justify-message-tests)
- [Rechercher les tests de votre message de blocage dans le journal des événements](#check-the-event-log-for-your-block-message-tests)

### <a name="check-the-event-log-for-your-warning-message-tests"></a>Rechercher les tests de votre message d’avertissement dans le journal des événements

Le premier test était d’avertir l’utilisateur, et vous avez sélectionné **Annuler**. Dans ce cas, la **Réponse de l’utilisateur** indique **Ignoré** dans le premier événement 301 :

```
Client Version: 2.8.85.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing a warning message for the General label.msg
Item Name: Testing a warning message for the General label
Process Name: OUTLOOK
Action: Warn
Label After Action: General
Label ID After Action: 0e421e6d-ea17-4fdb-8f01-93a3e71333b8
Action Source: 
User Response: Dismissed
```

Toutefois, vous avez ensuite sélectionné **Confirmer et envoyer**, ce que reflète l’événement 301 suivant, où la **Réponse de l’utilisateur** indique **Confirmé** :

```
Client Version: 2.8.85.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing a warning message for the General label.msg
Item Name: Testing a warning message for the General label
Process Name: OUTLOOK
Action: Warn
Label After Action: General
Label ID After Action: 0e421e6d-ea17-4fdb-8f01-93a3e71333b8
Action Source: 
User Response: Confirmed
```

### <a name="check-the-event-log-for-your-justify-message-tests"></a>Rechercher les tests de votre message de justification dans le journal des événements

Le même modèle est répété pour le message de justification, qui a un événement 302. Le premier événement a **Ignoré** comme **Réponse de l’utilisateur**, tandis que le second indique la justification qui a été sélectionnée. Par exemple :

```
Client Version: 2.8.85.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing the justification message for unlabeled content.msg
Item Name: Testing the justification message for unlabeled content
Process Name: OUTLOOK
Action: Justify
Label After Action: General
Label ID After Action: 0e421e6d-ea17-4fdb-8f01-93a3e71333b8
User Justification: I confirm the recipients are approved for sharing this content
Action Source: 
User Response: Confirmed

```

### <a name="check-the-event-log-for-your-block-message-tests"></a>Rechercher les tests de votre message de blocage dans le journal des événements

Au début du journal des événements se trouve le message de prévention, qui a un événement 303. Par exemple :

```
Client Version: 2.8.85.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing sending unlabeled PowerPoint files.msg
Item Name: Testing sending unlabeled PowerPoint files
Process Name: OUTLOOK
Action: Block
Label After Action: General
Label ID After Action: 0e421e6d-ea17-4fdb-8f01-93a3e71333b8
Action Source: 
```

## <a name="clean-up-resources"></a>Nettoyer les ressources

Une fois que vous avez terminé ce tutoriel, vous pouvez conserver la stratégie de test pour vous y référer ultérieurement ou bien la supprimer pour nettoyer vos ressources.

Si vous voulez supprimer votre stratégie, faites-le dans le Centre d’administration où elle a été créée, c’est-à-dire le Centre de conformité Microsoft 365, le Centre de sécurité Microsoft 365 ou le Centre de sécurité et de conformité de Microsoft 365.

Pour plus d’informations, consultez la [documentation Microsoft 365](https://docs.microsoft.com/microsoft-365/compliance/create-sensitivity-labels#publish-sensitivity-labels-by-creating-a-label-policy).

Une fois la stratégie supprimée, redémarrez Outlook sur l’ordinateur client pour qu’il ne soit plus configuré avec les paramètres définis dans ce tutoriel.

## <a name="next-steps"></a>Étapes suivantes

Pour que les tests soient plus rapides, ce tutoriel utilise un e-mail pour un seul destinataire et sans pièces jointes. 

Appliquez les mêmes méthodes avec plusieurs destinataires et étiquettes ou à des pièces jointes, où l’état d’étiquetage est parfois moins évident pour les utilisateurs.

Par exemple, vous pouvez faire en sorte qu’un message contextuel apparaisse sur les e-mails étiquetés **Public**, mais qu’une présentation PowerPoint soit étiquetée **Général**.

Pour plus d’informations sur les propriétés avancées et les personnalisations d’Outlook, consultez [Guide de l’administrateur : Configurations personnalisées pour le client d’étiquetage unifié Azure Information Protection](rms-client/clientv2-admin-guide-customizations.md).
