---
title: "Configuration des droits d’utilisation pour Azure Rights Management | Azure Information Protection"
description: "Découvrez et identifiez les droits spécifiques qui sont utilisés quand vous protégez des fichiers ou des e-mails à l’aide du service Azure Rights Management d’Azure Information Protection."
author: cabailey
manager: mbaldwin
ms.date: 10/05/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 97ddde38-b91b-42a5-8eb4-3ce6ce15393d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f17cf257607b0f74ca8bdaef13130da2f62dd587
ms.openlocfilehash: 0b160fff849b9f8bda71fd6ccf07d8fb07487b13


---

# Configuration des droits d’utilisation pour Azure Rights Management

>*S’applique à : Azure Information Protection, Office 365*

Quand vous définissez la protection de fichiers ou d’e-mails à l’aide du service Azure Rights Management d’Azure Information Protection et que vous n’utilisez pas de modèle, vous devez configurer les droits d’utilisation vous-même. En outre, quand vous configurez des modèles personnalisés pour Azure Rights Management, vous sélectionnez les droits d’utilisation qui seront ensuite appliqués automatiquement quand le modèle sera sélectionné par des utilisateurs, administrateurs ou services configurés. Par exemple, dans le portail Azure Classic, vous pouvez sélectionner des rôles qui configurent un regroupement logique de droits d’utilisation, ou configurer les droits individuels.

Utilisez cet article pour vous aider à configurer les droits d’utilisation de l’application que vous utilisez et pour comprendre comment ces droits sont interprétés par les applications.

## Descriptions et droits d’utilisation
Le tableau suivant répertorie et décrit les droits d'utilisation pris en charge par Rights Management, et la manière dont ils sont utilisés et interprétés. Ils sont répertoriés selon le **Nom commun**, qui correspond à la manière dont le droit d’utilisation est généralement affiché ou référencé sous une forme plus conviviale que la valeur de mot unique utilisée dans le code (valeur d’**Encodage dans la stratégie**). La **Constante ou valeur d’API** est le nom SDK d’un appel d’API MSIPC utilisé quand vous écrivez une application compatible avec RMS qui recherche un droit d’utilisation ou en ajoute un à une stratégie.


|Right|Description|Implémentation|
|-------------------------------|---------------------------|-----------------|
|Nom commun : **Modifier le contenu, Modifier** <br /><br />Encodage dans la stratégie : **DOCEDIT**|Permet à l'utilisateur de modifier, réorganiser, mettre en forme ou filtrer le contenu de l'application. N'accorde pas le droit d'enregistrer la copie modifiée.|Droits personnalisés Office : En relation avec les options **Modifier** et **Contrôle total**. <br /><br />Nom dans le portail Azure Classic : **Modifier le contenu**<br /><br />Nom dans les modèles AD RMS : **Modifier** <br /><br />Constante ou valeur d’API : Non applicable|
|Nom commun : **Enregistrer** <br /><br />Encodage dans la stratégie : **EDIT**|Permet à l'utilisateur d'enregistrer le document à son emplacement actuel.<br /><br />Dans les applications Office, ce droit permet également à l'utilisateur de modifier le document.|Droits personnalisés Office : En relation avec les options **Modifier** et **Contrôle total**. <br /><br />Nom dans le portail Azure Classic : **Enregistrer le fichier**<br /><br />Nom dans les modèles AD RMS : **Enregistrer** <br /><br />Constante ou valeur d’API `IPC_GENERIC_WRITE L"EDIT"`|
|Nom commun : **Commentaire** <br /><br />Encodage dans la stratégie : **COMMENT**|Active l'option d'ajout d'annotations ou de commentaires au contenu.<br /><br />Ce droit, disponible dans le SDK, est disponible en tant que stratégie ad hoc dans le module de protection RMS pour Windows PowerShell. Il a été implémenté dans certaines applications de fournisseur de logiciel. Toutefois, il n’est pas largement utilisé et n’est pas actuellement pris en charge par les applications Office.|Droits personnalisés Office : Non implémenté. <br /><br />Nom dans le portail Azure Classic : Non implémenté.<br /><br />Nom dans les modèles AD RMS : Non implémenté. <br /><br />Constante ou valeur d’API `IPC_GENERIC_COMMENT L"COMMENT`|
|Nom commun : **Enregistrer sous, Exporter** <br /><br />Encodage dans la stratégie : **EXPORT**|Active l'option d'enregistrement du contenu sous un autre nom de fichier (Enregistrer sous). Pour les documents Office, le fichier peut être enregistré sans protection.<br /><br />Ce droit permet également à l'utilisateur d'utiliser d'autres options d'exportation dans les applications, telles que **Envoyer à OneNote**.|Droits personnalisés Office : En relation avec les options **Modifier** et **Contrôle total**. <br /><br />Nom dans le portail Azure Classic : **Exporter le contenu (Enregistrer sous)**<br /><br />Nom dans les modèles AD RMS : **Exporter (Enregistrer sous)** <br /><br />Constante ou valeur d’API `IPC_GENERIC_EXPORT L"EXPORT"`|
|Nom commun : **Transférer** <br /><br />Encodage dans la stratégie : **FORWARD**|Active l'option de transfert de message électronique et d'ajout de destinataires aux lignes **À** et **CC** . Ce droit ne s’applique pas aux documents, mais uniquement aux e-mails.<br /><br />N'autorise pas le redirecteur à accorder des droits à d'autres utilisateurs dans le cadre de l'action de transfert.|Droits personnalisés Office : Refusés en cas d’utilisation de la stratégie standard **Ne pas transférer**.<br /><br />Nom dans le portail Azure Classic : **Transférer**<br /><br />Nom dans les modèles AD RMS : **Transférer** <br /><br />Constante ou valeur d’API `IPC_EMAIL_FORWARD L"FORWARD"`|
|Nom commun : **Contrôle total** <br /><br />Encodage dans la stratégie : **OWNER**|Accorde tous les droits sur le document. Toutes les actions disponibles peuvent être effectuées.<br /><br />Inclut la possibilité de supprimer la protection et de reprotéger un document.|Droits personnalisés Office : Comme l’option personnalisée **Contrôle total**.<br /><br />Nom dans le portail Azure Classic : **Contrôle total**<br /><br />Nom dans les modèles AD RMS : **Contrôle total** <br /><br />Constante ou valeur d’API `IPC_GENERIC_ALL L"OWNER"`|
|Nom commun : **Imprimer** <br /><br />Encodage dans la stratégie : **PRINT**|Active les options d'impression du contenu.|Droits personnalisés Office : Comme l’option **Imprimer le contenu** dans les autorisations personnalisées. N’est pas un paramètre par destinataire.<br /><br />Nom dans le portail Azure Classic : **Imprimer**<br /><br />Nom dans les modèles AD RMS : **Imprimer** <br /><br />Constante ou valeur d’API `IPC_GENERIC_PRINT L"PRINT"`|
|Nom commun : **Répondre** <br /><br />Encodage dans la stratégie : **REPLY**|Active l’option **Répondre** dans un client de messagerie sans autoriser de modification des lignes **À** ou **Cc**.|Droits personnalisés Office : Non implémenté.<br /><br />Nom dans le portail Azure Classic : **Répondre**<br /><br />Nom dans les modèles AD RMS : **Répondre** <br /><br />Constante ou valeur d’API `IPC_EMAIL_REPLY`|
|Nom commun : **Répondre à tous** <br /><br />Encodage dans la stratégie : **REPLYALL**|Active l'option **Répondre à tous** dans un client de messagerie, mais ne permet pas à l'utilisateur d'ajouter des destinataires aux lignes **À** ou **CC** .|Droits personnalisés Office : Non implémenté.<br /><br />Nom dans le portail Azure Classic : **Répondre à tous**<br /><br />Nom dans les modèles AD RMS : **Répondre à tous** <br /><br />Constante ou valeur d’API `IPC_EMAIL_REPLYALL L"REPLYALL"`|
|Nom commun : **Afficher, Ouvrir, Lire** <br /><br />Encodage dans la stratégie : **VIEW**|Permet à l'utilisateur d'ouvrir le document et d'en voir le contenu.|Droits personnalisés Office : Comme l’option **Afficher** de la stratégie personnalisée **Lecture**.<br /><br />Nom dans le portail Azure classique : **Afficher**<br /><br />Nom dans les modèles AD RMS : **Répondre à tous** <br /><br />Constante ou valeur d’API `IPC_GENERIC_READ L"VIEW"`|
|Nom commun : **Copier** <br /><br />Encodage dans la stratégie : **EXTRACT**|Active les options permettant de copier des données du document (y compris des captures d’écran) vers un autre emplacement du document ou vers un autre document.<br /><br />Dans certaines applications, permet également d’enregistrer l’ensemble du document sous forme non protégée.|Droits personnalisés Office : comme l’option de stratégie personnalisée **Autoriser les utilisateurs bénéficiant d’accès en lecture à copier le contenu**.<br /><br />Nom dans le portail Azure Classic : **Copier et Extraire le contenu**<br /><br />Nom dans les modèles AD RMS : **Extraire** <br /><br />Constante ou valeur d’API `IPC_GENERIC_EXTRACT L"EXTRACT"`|
|Nom commun : **Autoriser les macros** <br /><br />Encodage dans la stratégie : **OBJMODEL**|Active l'option permettant d'exécuter des macros ou d'effectuer d'autres opérations d'accès à distance ou par programme au contenu d'un document.|Droits personnalisés Office : Comme l’option de la stratégie personnalisée **Autoriser l’accès par programme**. N’est pas un paramètre par destinataire.<br /><br />Nom dans le portail Azure Classic : **Autoriser les macros**<br /><br />Nom dans les modèles AD RMS : **Autoriser les macros** <br /><br />Constante ou valeur d’API : Non applicable|



## Droits inclus dans les niveaux d’autorisation

Certaines applications regroupent les droits d’utilisation dans des niveaux d’autorisation, ce qui facilite la sélection de droits d’utilisation qui sont généralement utilisés ensemble. Ces niveaux d’autorisation permettent de réduire la complexité, si bien que les utilisateurs peuvent choisir des options basées sur des rôles.  Par exemple, **Réviseur** et **Coauteur**. Bien que ces options montrent souvent aux utilisateurs un récapitulatif des droits, il peut arriver qu’elles n’incluent pas tous les droits répertoriés dans le tableau précédent.

Envisagez le tableau suivant comme une liste de ces niveaux d’autorisation et comme une liste complète des droits qu’ils renferment.

|Niveau d’autorisation|Applications|Droits inclus (nom commun)|
|---------------------|----------------|---------------------------------|
|Observateur|Portail Azure Classic<br /><br />Application de partage Rights Management pour Windows|Afficher, Ouvrir, Lire ; Répondre ; Répondre à tous|
|Réviseur|Portail Azure Classic<br /><br />Application de partage Rights Management pour Windows|Afficher, Ouvrir, Lire ; Enregistrer ; Modifier le contenu, Modifier ; Répondre [[1]](#footnote-1) ; Répondre à tous [[1]](#footnote-1) ; Transférer [[1]](#footnote-1)|
|Coauteur|Portail Azure Classic<br /><br />Application de partage Rights Management pour Windows|Afficher, Ouvrir, Lire ; Enregistrer ; Modifier le contenu, Modifier ; Copier ; Afficher les droits ; Autoriser les macros ; Enregistrer sous, Exporter ; Imprimer ; Répondre [[1]](#footnote-1) ; Répondre à tous [[1]](#footnote-1) ; Transférer [[1]](#footnote-1)|
|Copropriétaire|Portail Azure Classic<br /><br />Application de partage Rights Management pour Windows|Afficher, Ouvrir, Lire ; Enregistrer ; Modifier le contenu, Modifier ; Copier ; Afficher les droits ; Autoriser les macros ; Enregistrer sous, Exporter ; Imprimer ; Répondre [[1]](#footnote-1) ; Répondre à tous [[1]](#footnote-1) ; Transférer [[1]](#footnote-1) ; Contrôle total|

----

###### Note de bas de page 1
non applicable à l’application de partage Rights Management pour Windows.

## Droits inclus dans les modèles par défaut
Les droits inclus avec les modèles par défaut sont les suivants :

|Nom d’affichage|Droits inclus (nom commun)|
|----------------|---------------------------------|
|&lt;*nom de l’organisation*&gt; *- Affichage confidentiel uniquement*|Afficher, Ouvrir, Lire|
|&lt;*nom de l’organisation*&gt; *- Confidentiel*|Afficher, Ouvrir, Lire ; Enregistrer ; Modifier le contenu, Modifier ; Afficher les droits ; Autoriser les macros ; Transférer ; Répondre ; Répondre à tous|

## Option Ne pas transférer pour les e-mails

Les clients et services Exchange (par exemple, le client Outlook, l’application Outlook Web Access et les règles de transport Exchange) ont une option de protection des droits d’information supplémentaire pour les e-mails : **Ne pas transférer**. 

Même si cette option apparaît aux utilisateurs (les administrateurs Exchange) comme s’il s’agissait d’un modèle de gestion des droits par défaut qu’ils peuvent sélectionner, **Ne pas transférer** n’est pas un modèle. Cela explique pourquoi vous ne pouvez pas la voir dans le portail classique Azure quand vous affichez et gérez des modèles pour Azure Rights Management. L’option **Ne pas transférer** correspond plutôt à un ensemble de droits appliqué dynamiquement par les utilisateurs à leurs destinataires.

Quand l’option **Ne pas transférer** est appliquée à un e-mail, les destinataires ne peuvent pas le transférer, l’imprimer, en copier le contenu, enregistrer des pièces jointes ou l’enregistrer sous un autre nom. Par exemple, dans le client Outlook, le bouton Transférer n’est pas disponible. Les options de menu **Enregistrer sous**, **Enregistrer les pièces jointes** et **Imprimer** ne sont pas disponibles non plus. Vous ne pouvez pas ajouter ou modifier des destinataires dans les zones **À**, **Cc** ou **Cci**.

Il existe une distinction importante entre l’application de l’option **Ne pas transférer** et celle d’un modèle qui n’accorde pas le droit d’être transféré à un e-mail : l’option **Ne pas transférer** utilise une liste dynamique des utilisateurs autorisés qui se base sur les destinataires choisis de l’utilisateur de l’e-mail d’origine, tandis que les droits du modèle ont une liste statique d’utilisateurs autorisés que l’administrateur a spécifiée au préalable. Quelle est la différence ? Prenons un exemple : 

Une utilisatrice veut envoyer certaines informations par e-mail à certaines personnes du service Marketing. Ces informations ne doivent être partagées avec personne d’autre. A-t-elle intérêt à protéger l’e-mail avec un modèle qui restreint les droits (affichage, réponse et enregistrement) au service Marketing ?  Ou doit-elle choisir d’utiliser l’option **Ne pas transférer** ? Ces deux possibilités ont pour résultat d’empêcher les destinataires de transférer l’e-mail. 

- Si elle applique le modèle, les destinataires peuvent quand même partager les informations avec d’autres utilisateurs du service Marketing. Par exemple, un destinataire pourrait utiliser l’Explorateur pour glisser-déplacer l’e-mail vers un emplacement partagé ou un lecteur USB. Ainsi, toute personne du service Marketing (dont le propriétaire de l’e-mail) qui a accès à cet emplacement peut afficher les informations contenues dans l’e-mail.
 
- Si elle applique l’option **Ne pas transférer**, les destinataires ne pourront pas partager les informations avec d’autres personnes du service Marketing en déplaçant l’e-mail vers un autre emplacement. Dans ce scénario, seuls les destinataires d’origine (et le propriétaire du message) sont en mesure d’afficher les informations contenues dans l’e-mail.

> [!NOTE] 
> Utilisez l’option **Ne pas transférer** quand il est important que seuls les destinataires choisis par l’expéditeur puissent consulter les informations contenues dans l’e-mail. Utilisez un modèle pour les e-mails afin de restreindre les droits à un groupe de personnes que l’administrateur spécifie à l’avance, indépendamment des destinataires choisis de l’expéditeur.




## Voir aussi
[Configuration de modèles personnalisés pour le service Azure Rights Management](configure-custom-templates.md)




<!--HONumber=Oct16_HO1-->


