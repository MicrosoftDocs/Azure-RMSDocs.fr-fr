---
# required metadata

title: Configuration des droits d’utilisation pour Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 06/08/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 97ddde38-b91b-42a5-8eb4-3ce6ce15393d

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Configuration des droits d’utilisation pour Azure Rights Management

*S’applique à : Azure Rights Management, Office 365*

Lorsque vous définissez la protection de fichiers ou de messages électroniques à l'aide d'Azure Rights Management (Azure RMS) et n'utilisez pas de modèle, vous devez configurer les droits d'utilisation vous-même. En outre, lorsque vous configurez des modèles personnalisés pour Azure RMS, vous sélectionnez les droits d’utilisation qui seront ensuite appliqués automatiquement lorsque le modèle sera sélectionné par des utilisateurs, administrateurs ou services configurés. Par exemple, dans le portail Azure Classic, vous pouvez sélectionner des rôles qui configurent un regroupement logique de droits d’utilisation, ou configurer les droits individuels.

Utilisez cet article pour vous aider à configurer les droits d’utilisation de l’application que vous utilisez et pour comprendre comment ces droits sont interprétés par les applications.

## Descriptions et droits d’utilisation
Les sections suivantes répertorient et décrivent les droits d’utilisation pris en charge par Rights Management et la manière dont ils sont utilisés et interprétés. Ils sont répertoriés selon le **Nom commun**, qui correspond à la manière dont le droit d’utilisation est généralement affiché ou référencé sous une forme plus conviviale que la valeur de mot unique utilisée dans le code (valeur d’**Encodage dans la stratégie**). La **Constante ou valeur d’API** est le nom SDK d’un appel d’API MSIPC utilisé quand vous écrivez une application compatible avec RMS qui recherche un droit d’utilisation ou en ajoute un à une stratégie.


### Modifier le contenu, Modifier

Permet à l'utilisateur de modifier, réorganiser, mettre en forme ou filtrer le contenu de l'application. N'accorde pas le droit d'enregistrer la copie modifiée.

**Encodage dans la stratégie** : DOCEDIT

**Implémentation dans les droits personnalisés Office** : En relation avec les options *Modifier* et *Contrôle total*.

**Nom dans le portail Azure Classic** : *Modifier le contenu*

**Nom dans les modèles AD RMS** : *Modifier*

**Constante ou valeur d’API** : *Non applicable*

---

### Enregistrer

Permet à l'utilisateur d'enregistrer le document à son emplacement actuel.

**Encodage dans la stratégie** : EDIT

**Implémentation dans les droits personnalisés Office** : En relation avec les options *Modifier* et *Contrôle total*.

**Nom dans le portail Azure Classic** : *Enregistrer le fichier*

**Nom dans les modèles AD RMS** : *Enregistrer*

**Constante ou valeur d’API** : IPC_GENERIC_WRITEL"EDIT"

Dans les applications Office, ce droit permet également à l'utilisateur de modifier le document.

---

### Commentaire

Active l'option d'ajout d'annotations ou de commentaires au contenu.

**Encodage dans la stratégie** : COMMENT

**Implémentation dans les droits personnalisés Office** : Non implémenté.

**Nom dans le portail Azure Classic** : Non implémenté.

**Nom dans les modèles AD RMS** : Non implémenté.

**Constante ou valeur d’API** : IPC_GENERIC_COMMENTL"COMMENT

Ce droit, disponible dans le SDK, est disponible en tant que stratégie ad hoc dans le module de protection RMS pour Windows PowerShell. Il a été implémenté dans certaines applications de fournisseur de logiciel. Toutefois, il n’est pas largement utilisé et n’est pas actuellement pris en charge par les applications Office.

---

### Enregistrer sous, Exporter

Active l'option d'enregistrement du contenu sous un autre nom de fichier (Enregistrer sous). Pour les documents Office, le fichier peut être enregistré sans protection.

**Encodage dans la stratégie** : EXPORT

**Implémentation dans les droits personnalisés Office** : En relation avec les options *Modifier* et *Contrôle total*.

**Nom dans le portail Azure Classic** : *Exporter le contenu (Enregistrer sous)*

**Nom dans les modèles AD RMS** : *Exporter (Enregistrer sous)*

**Constante ou valeur d’API** : IPC_GENERIC_EXPORTL"EXPORT"

Ce droit permet également à l’utilisateur d’utiliser d’autres options d’exportation dans les applications, telles que *Envoyer à OneNote*.

---

### Prédictif

Active l’option de transfert de message électronique et d’ajout de destinataires aux lignes *À* et *Cc*. Ce droit ne s’applique pas aux documents, mais uniquement aux e-mails.

**Encodage dans la stratégie** : FORWARD

**Implémentation dans les droits personnalisés Office** : Refusée en cas d’utilisation de la stratégie standard *Ne pas transférer*.

**Nom dans le portail Azure Classic** : *Transférer*

**Nom dans les modèles AD RMS** : *Transférer*

**Constante ou valeur d’API** : IPC_EMAIL_FORWARDL"FORWARD"

N'autorise pas le redirecteur à accorder des droits à d'autres utilisateurs dans le cadre de l'action de transfert.

---

### Contrôle total

Accorde tous les droits sur le document. Toutes les actions disponibles peuvent être effectuées.

**Encodage dans la stratégie** : OWNER

**Implémentation dans les droits personnalisés Office** : Comme l’option personnalisée *Contrôle total*.

**Nom dans le portail Azure Classic** : *Contrôle total*

**Nom dans les modèles AD RMS** : *Contrôle total*

**Constante ou valeur d’API** : IPC_GENERIC_ALLL"OWNER"

Inclut la possibilité de supprimer la protection.

---

### Imprimer

Active les options d'impression du contenu.

**Encodage dans la stratégie** : PRINT

**Implémentation dans les droits personnalisés Office** : Comme l’option *Imprimer le contenu* dans les autorisations personnalisées. N’est pas un paramètre par destinataire.

**Nom dans le portail Azure Classic** : *Imprimer*

**Nom dans les modèles AD RMS** : *Imprimer*

**Constante ou valeur d’API** : IPC_GENERIC_PRINTL"PRINT

---

### Répondre

Active l’option Répondre dans un client de messagerie sans autoriser de modification des lignes *À* ou *Cc*.

**Encodage dans la stratégie** : REPLY

**Implémentation dans les droits personnalisés Office** : Non applicable.

**Nom dans le portail Azure Classic** : *Répondre*

**Nom dans les modèles AD RMS** : *Répondre*

**Constante ou valeur d’API** : IPC_EMAIL_REPLY

---

### Répondre à tous

Active l’option *Répondre à tous* dans un client de messagerie, mais ne permet pas à l’utilisateur d’ajouter des destinataires aux lignes *À* ou *Cc*.

**Encodage dans la stratégie** : REPLYALL

**Implémentation dans les droits personnalisés Office** : Non applicable.

**Nom dans le portail Azure Classic** : *Répondre à tous*

**Nom dans les modèles AD RMS** : *Répondre à tous*

**Constante ou valeur d’API** : IPC_EMAIL_REPLYALLL"REPLYALL"

---

### Afficher, Ouvrir, Lire

Permet à l'utilisateur d'ouvrir le document et d'en voir le contenu.

**Encodage dans la stratégie** : VIEW

**Implémentation dans les droits personnalisés Office** : Comme l’option *Afficher* de la stratégie personnalisée *Lecture*.

**Nom dans le portail Azure Classic** : *Afficher le contenu*

**Nom dans les modèles AD RMS** : *Afficher*

**Constante ou valeur d’API** : IPC_GENERIC_READL"VIEW"

---

### Copier

Active les options permettant de copier des données du document (y compris des captures d’écran) vers un autre emplacement du document ou vers un autre document.

**Encodage dans la stratégie** : EXTRACT

**Implémentation dans les droits personnalisés Office :** comme l’option de stratégie personnalisée *Autoriser les utilisateurs bénéficiant d’accès en lecture à copier le contenu*.

**Nom dans le portail Azure Classic :** *Copier et Extraire le contenu*

**Nom dans les modèles AD RMS :** *Extraire*

**Constante ou valeur d’API :** IPC_GENERIC_EXTRACTL"EXTRACT"

Dans certaines applications, permet également d’enregistrer l’ensemble du document sous forme non protégée.

---


### Autoriser les macros

Active l'option permettant d'exécuter des macros ou d'effectuer d'autres opérations d'accès à distance ou par programme au contenu d'un document.

**Encodage dans la stratégie** : OBJMODEL

**Implémentation dans les droits personnalisés Office** : Comme l’option de la stratégie personnalisée *Autoriser l’accès par programme*. N’est pas un paramètre par destinataire.

**Nom dans le portail Azure Classic** : *Autoriser les macros*

**Nom dans les modèles AD RMS** : *Autoriser les macros*

**Constante ou valeur d’API** : Non applicable


## Droits inclus dans les niveaux d’autorisation

Certaines applications regroupent les droits d’utilisation dans des niveaux d’autorisation, ce qui facilite la sélection de droits d’utilisation qui sont généralement utilisés ensemble. Ces niveaux d’autorisation permettent de réduire la complexité, si bien que les utilisateurs peuvent choisir des options basées sur des rôles.  Par exemple, **Réviseur** et **Coauteur**. Bien que ces options montrent souvent aux utilisateurs un récapitulatif des droits, il peut arriver qu’elles n’incluent pas tous les droits répertoriés dans le tableau précédent.

Envisagez le tableau suivant comme une liste de ces niveaux d’autorisation et comme une liste complète des droits qu’ils renferment.

|Niveau d’autorisation|Applications|Droits inclus (nom commun)|
|---------------------|----------------|---------------------------------|
|Observateur|Portail Azure Classic<br /><br />Application de partage Rights Management pour Windows|Afficher, Ouvrir, Lire ; Répondre ; Répondre à tous|
|Réviseur|Portail Azure Classic<br /><br />Application de partage Rights Management pour Windows|Afficher, Ouvrir, Lire ; Enregistrer ; Modifier le contenu, Modifier ; Répondre [[1]](#footnote-1) ; Répondre à tous [[1]](#footnote-1) ; Transférer [[1]](#footnote-1)|
|Coauteur|Portail Azure Classic<br /><br />Application de partage Rights Management pour Windows|Afficher, Ouvrir, Lire ; Enregistrer ; Modifier le contenu, Modifier ; Copier ; Afficher les droits ; Modifier les droits ; Autoriser les macros ; Enregistrer sous, Exporter ; Imprimer ; Répondre [[1]](#footnote-1) ; Répondre à tous [[1]](#footnote-1) ; Transférer [[1]](#footnote-1)|
|Copropriétaire|Portail Azure Classic<br /><br />Application de partage Rights Management pour Windows|Afficher, Ouvrir, Lire ; Enregistrer ; Modifier le contenu, Modifier ; Copier ; Afficher les droits ; Modifier les droits ; Autoriser les macros ; Enregistrer sous, Exporter ; Imprimer ; Répondre [[1]](#footnote-1) ; Répondre à tous [[1]](#footnote-1) ; Transférer [[1]](#footnote-1) ; Contrôle total|

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

Même si cette option apparaît aux utilisateurs (les administrateurs Exchange) comme s’il s’agissait d’un modèle de gestion des droits par défaut qu’ils peuvent sélectionner, **Ne pas transférer** n’est pas un modèle. Cela explique pourquoi vous ne pouvez pas la voir dans le portail classique Azure quand vous affichez et gérez des modèles pour Azure RMS. L’option **Ne pas transférer** correspond plutôt à un ensemble de droits appliqué dynamiquement par les utilisateurs à leurs destinataires.

Quand l’option **Ne pas transférer** est appliquée à un e-mail, les destinataires ne peuvent pas le transférer, l’imprimer, en copier le contenu, enregistrer des pièces jointes ou l’enregistrer sous un autre nom. Par exemple, dans le client Outlook, le bouton Transférer n’est pas disponible. Les options de menu **Enregistrer sous**, **Enregistrer les pièces jointes** et **Imprimer** ne sont pas disponibles non plus. Vous ne pouvez pas ajouter ou modifier des destinataires dans les zones **À**, **Cc** ou **Cci**.

Il existe une distinction importante entre l’application de l’option **Ne pas transférer** et celle d’un modèle qui n’accorde pas le droit d’être transféré à un e-mail : l’option **Ne pas transférer** utilise une liste dynamique des utilisateurs autorisés qui se base sur les destinataires choisis de l’utilisateur de l’e-mail d’origine, tandis que les droits du modèle ont une liste statique d’utilisateurs autorisés que l’administrateur a spécifiée au préalable. Quelle est la différence ? Prenons un exemple : 

Une utilisatrice veut envoyer certaines informations par e-mail à certaines personnes du service Marketing. Ces informations ne doivent être partagées avec personne d’autre. A-t-elle intérêt à protéger l’e-mail avec un modèle qui restreint les droits (affichage, réponse et enregistrement) au service Marketing ?  Ou doit-elle choisir d’utiliser l’option **Ne pas transférer** ? Ces deux possibilités ont pour résultat d’empêcher les destinataires de transférer l’e-mail. 

- Si elle applique le modèle, les destinataires peuvent quand même partager les informations avec d’autres utilisateurs du service Marketing. Par exemple, un destinataire pourrait utiliser l’Explorateur pour glisser-déplacer l’e-mail vers un emplacement partagé ou un lecteur USB. Ainsi, toute personne du service Marketing (dont le propriétaire de l’e-mail) qui a accès à cet emplacement peut afficher les informations contenues dans l’e-mail.
 
- Si elle applique l’option **Ne pas transférer**, les destinataires ne pourront pas partager les informations avec d’autres personnes du service Marketing en déplaçant l’e-mail vers un autre emplacement. Dans ce scénario, seuls les destinataires d’origine (et le propriétaire du message) sont en mesure d’afficher les informations contenues dans l’e-mail.

> [!NOTE] Utilisez l’option **Ne pas transférer** quand il est important que seuls les destinataires choisis par l’expéditeur puissent consulter les informations contenues dans l’e-mail. Utilisez un modèle pour les e-mails afin de restreindre les droits à un groupe de personnes que l’administrateur spécifie à l’avance, indépendamment des destinataires choisis de l’expéditeur.




## Voir aussi
[Configuration de modèles personnalisés pour Azure Rights Management](configure-custom-templates.md)



<!--HONumber=Jun16_HO2-->


