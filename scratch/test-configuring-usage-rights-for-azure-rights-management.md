---
title: TEST Configuration des droits d’utilisation pour Azure Rights Management
ms.custom: na
ms.reviewer: na
ms.service: rights-management
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: TEST
author: Cabailey
---
# AVANT : Configuration des droits d’utilisation pour Azure Rights Management
Lorsque vous définissez la protection de fichiers ou de messages électroniques à l'aide d'Azure Rights Management (Azure RMS) et n'utilisez pas de modèle, vous devez configurer les droits d'utilisation vous-même. En outre, lorsque vous configurez des modèles personnalisés pour Azure RMS, vous sélectionnez les droits d’utilisation qui seront ensuite appliqués automatiquement lorsque le modèle sera sélectionné par des utilisateurs, administrateurs ou services configurés. Par exemple, dans le portail Azure Classic, vous pouvez sélectionner des rôles qui configurent un regroupement logique de droits d’utilisation, ou configurer les droits individuels.

Utilisez cet article pour vous aider à configurer les droits d’utilisation de l’application que vous utilisez et pour comprendre comment ces droits sont interprétés par les applications.

## Descriptions et droits d'utilisation
Les sections suivantes répertorient et décrivent les droits d’utilisation pris en charge par Rights Management, et la manière dont ils sont utilisés et interprétés. Dans ces sections, le **Nom commun** correspond à la manière dont le droit d’utilisation est généralement affiché ou référencé sous une forme plus conviviale que la valeur de mot unique utilisée dans le code (valeur d’**Encodage dans la stratégie**). La **Constante ou valeur d’API** est le nom SDK d’un appel d’API MSIPC utilisé quand vous écrivez une application compatible avec RMS qui recherche un droit d’utilisation ou en ajoute un à une stratégie.

### Nom commun : Modifier le contenu, Modifier

**Encodage dans la stratégie :**

- DOCEDIT

**Description :**

- Permet à l'utilisateur de modifier, réorganiser, mettre en forme ou filtrer le contenu de l'application. N'accorde pas le droit d'enregistrer la copie modifiée.

**Implémentation dans les droits personnalisés d’Office :**

- En relation avec les options **Modifier** et **Contrôle total** .

**Nom dans le portail Azure Classic :**

- **Modifier le contenu**

**Nom dans les modèles AD RMS :**

- **Éditer**

**Constante ou valeur d’API**

- Non applicable

**Informations supplémentaires :**

- Dans les applications Office, ce droit permet également à l'utilisateur d'enregistrer le document.

---

### Nom commun : Enregistrer

**Encodage dans la stratégie :**

- MODIFIER

**Description :**

- Permet à l'utilisateur d'enregistrer le document à son emplacement actuel.

**Implémentation dans les droits personnalisés d’Office :**

- En relation avec les options **Modifier** et **Contrôle total** .

**Nom dans le portail Azure Classic :**

- **Enregistrer le fichier**

**Nom dans les modèles AD RMS :**

- Enregistrer

**Constante ou valeur d’API**

- IPC_GENERIC_WRITEL"EDIT"

**Informations supplémentaires :**

- Dans les applications Office, ce droit permet également à l'utilisateur de modifier le document.

---

### Nom commun : Commentaire

**Encodage dans la stratégie :**

- COMMENTAIRE

**Description :**

- Active l'option d'ajout d'annotations ou de commentaires au contenu.

**Implémentation dans les droits personnalisés d’Office :**

- Non implémentée.

**Nom dans le portail Azure Classic :**

- Non implémentée.

**Nom dans les modèles AD RMS :**

- Non implémentée.

**Constante ou valeur d’API**

- IPC_GENERIC_COMMENTL"COMMENT

**Informations supplémentaires :**

- Ce droit, disponible dans le SDK, est disponible en tant que stratégie ad hoc dans le module de protection RMS pour Windows PowerShell. Il a été implémenté dans certaines applications de fournisseur de logiciel. Toutefois, il n'est pas largement utilisé et n'est pas actuellement pris en charge par les applications Office.

---

### Nom commun : Enregistrer sous, Exporter

**Encodage dans la stratégie :**

- EXPORTER

**Description :**

- Active l'option d'enregistrement du contenu sous un autre nom de fichier (Enregistrer sous). Selon l'application, le fichier peut être enregistré sans protection.

**Implémentation dans les droits personnalisés d’Office :**

- En relation avec les options **Modifier** et **Contrôle total** .

**Nom dans le portail Azure Classic :**

- **Exporter le contenu (Enregistrer sous)**

**Nom dans les modèles AD RMS :**

- **Exporter (Enregistrer sous)**

**Constante ou valeur d’API**

- IPC_GENERIC_EXPORTL"EXPORT"

**Informations supplémentaires :**

- Ce droit permet également à l'utilisateur d'utiliser d'autres options d'exportation dans les applications, telles que **Envoyer à OneNote**.

---

### Nom commun : Transférer

**Encodage dans la stratégie :**

- TRANSFÉRER

**Description :**

- Active l'option de transfert de message électronique et d'ajout de destinataires aux lignes **À** et **CC** .

**Implémentation dans les droits personnalisés d’Office :**

- Refusée en cas d'utilisation de la stratégie standard **Ne pas transférer** .

**Nom dans le portail Azure Classic :**

- **Prédictif**

**Nom dans les modèles AD RMS :**

- **Prédictif**

**Constante ou valeur d’API**

- IPC_EMAIL_FORWARDL"FORWARD"

**Informations supplémentaires :**

- N'autorise pas le redirecteur à accorder des droits à d'autres utilisateurs dans le cadre de l'action de transfert.

---

### Nom commun : Contrôle total

**Encodage dans la stratégie :**

- OWNER

**Description :**

- Accorde tous les droits sur le document. Toutes les actions disponibles peuvent être effectuées.

**Implémentation dans les droits personnalisés d’Office :**

- Comme l'option personnalisée **Contrôle total** .

**Nom dans le portail Azure Classic :**

- **Contrôle total**

**Nom dans les modèles AD RMS :**

- **Contrôle total**

**Constante ou valeur d’API**

- IPC_GENERIC_ALLL"OWNER"

**Informations supplémentaires :**

- Inclut la possibilité de supprimer la protection.

---

### Nom commun : Imprimer

**Encodage dans la stratégie :**

- PRINT

**Description :**

- Active les options d'impression du contenu.

**Implémentation dans les droits personnalisés d’Office :**

- Comme l'option **imprimer le contenu** dans les autorisations personnalisées. N’est pas un paramètre par destinataire.

**Nom dans le portail Azure Classic :**

- **Imprimer**

**Nom dans les modèles AD RMS :**

- **Imprimer**

**Constante ou valeur d’API**

- IPC_GENERIC_PRINTL"PRINT

---

### Nom commun : Répondre

**Encodage dans la stratégie :**

- RÉPONDRE

**Description :**

- Active l'option Répondre dans un client de messagerie sans autoriser de modification des lignes **À** ou **CC** .

**Implémentation dans les droits personnalisés d’Office :**

- Non applicable

**Nom dans le portail Azure Classic :**

- **Répondre**

**Nom dans les modèles AD RMS :**

- **Répondre**

**Constante ou valeur d’API**

- IPC_EMAIL_REPLY

---

### Nom commun : Répondre à tous

**Encodage dans la stratégie :**

- REPLYALL

**Description :**

- Active l'option **Répondre à tous** dans un client de messagerie, mais ne permet pas à l'utilisateur d'ajouter des destinataires aux lignes **À** ou **CC** .

**Implémentation dans les droits personnalisés d’Office :**

- Non applicable

**Nom dans le portail Azure Classic :**

- **Répondre à tous**

**Nom dans les modèles AD RMS :**

- **Répondre à tous**

**Constante ou valeur d’API**

- IPC_EMAIL_REPLYALLL"REPLYALL"

---

### Nom commun : Afficher, Ouvrir, Lire

**Encodage dans la stratégie :**

- AFFICHAGE

**Description :**

- Permet à l'utilisateur d'ouvrir le document et d'en voir le contenu.

**Implémentation dans les droits personnalisés d’Office :**

- Comme l'option **Afficher** de la stratégie personnalisée **Lecture** .

**Nom dans le portail Azure Classic :**

- **Afficher le contenu**

**Nom dans les modèles AD RMS :**

- **Afficher**

**Constante ou valeur d’API**

- IPC_GENERIC_READL"VIEW"

---

### Nom commun : Afficher les droits

**Encodage dans la stratégie :**

- AFFICHAGERIGHTSDATA

**Description :**

- Permet à l'utilisateur d'afficher la stratégie appliquée au document.

**Implémentation dans les droits personnalisés d’Office :**

- Non implémentée.

**Nom dans le portail Azure Classic :**

- **Afficher les droits affectés**

**Nom dans les modèles AD RMS :**

- **Afficher les droits**

**Constante ou valeur d’API**

- IPC_READ_RIGHTSL"VIEWRIGHTSDATA"

---

### Nom commun : Afficher les droits

**Encodage dans la stratégie :**

- AFFICHAGERIGHTSDATA

**Description :**

- Permet à l'utilisateur d'afficher la stratégie appliquée au document.

**Implémentation dans les droits personnalisés d’Office :**

- Non implémentée.

**Nom dans le portail Azure Classic :**

- **Afficher les droits affectés**

**Nom dans les modèles AD RMS :**

- **Afficher les droits**

**Constante ou valeur d’API**

- IPC_READ_RIGHTSL"VIEWRIGHTSDATA"

**Informations supplémentaires :**

- Ignoré par certaines applications.

---

### Nom commun : Modifier les droits

**Encodage dans la stratégie :**

- EDITRIGHTSDATA

**Description :**

- Permet à l'utilisateur de modifier la stratégie appliquée au document. Inclut notamment la suppression de la protection.

**Implémentation dans les droits personnalisés d’Office :**

- Non implémentée.

**Nom dans le portail Azure Classic :**

- **Modifier les droits**

**Nom dans les modèles AD RMS :**

- **Modifier les droits**

**Constante ou valeur d’API**

- IPC_WRITE_RIGHTSL"EDITRIGHTSDATA"

---

### Nom commun : Autoriser les macros

**Encodage dans la stratégie :**

- OBJMODEL

**Description :**

- Active l'option permettant d'exécuter des macros ou d'effectuer d'autres opérations d'accès à distance ou par programme au contenu d'un document.

**Implémentation dans les droits personnalisés d’Office :**

- Comme l'option de stratégie personnalisée **Autoriser l'accès par programme** . N’est pas un paramètre par destinataire.

**Nom dans le portail Azure Classic :**

- **Autoriser les macros**

**Nom dans les modèles AD RMS :**

- **Autoriser les macros**

**Constante ou valeur d’API**

- Non applicable

---


|Nom commun|Encodage dans la stratégie|Description|Implémentation dans les droits personnalisés Office|Connectez-vous au portail Azure Classic.|Nom dans les modèles AD RMS|API constant ou value|Informations supplémentaires|
|---------------|----------------------|---------------|------------------------------------------|-------------------------------------|----------------------------|-------------------------|--------------------------|
|Modifier le contenu, Modifier|DOCEDIT|Permet à l'utilisateur de modifier, réorganiser, mettre en forme ou filtrer le contenu de l'application. N'accorde pas le droit d'enregistrer la copie modifiée.|En relation avec les options **Modifier** et **Contrôle total** .|**Modifier le contenu**|**Éditer**|Non applicable|Dans les applications Office, ce droit permet également à l'utilisateur d'enregistrer le document.|
|Enregistrer|MODIFIER|Permet à l'utilisateur d'enregistrer le document à son emplacement actuel.|En relation avec les options **Modifier** et **Contrôle total** .|**Enregistrer le fichier**|**Enregistrer**|IPC_GENERIC_WRITEL"EDIT"|Dans les applications Office, ce droit permet également à l’utilisateur de modifier le document.|
|Commentaire|COMMENTAIRE|Active l’option d’ajout d’annotations ou de commentaires au contenu.|Non implémenté|Non implémenté|Non implémenté|IPC_GENERIC_COMMENTL"COMMENT"|Ce droit, disponible dans le SDK, est disponible en tant que stratégie ad hoc dans le module de protection RMS pour Windows PowerShell. Il a été implémenté dans certaines applications de fournisseur de logiciel. Toutefois, il n’est pas largement utilisé et n’est pas actuellement pris en charge par les applications Office.|
|Enregistrer sous, Exporter|EXPORTER|Active l'option d'enregistrement du contenu sous un autre nom de fichier (Enregistrer sous). Selon l'application, le fichier peut être enregistré sans protection.|En relation avec les options **Modifier** et **Contrôle total** .|**Exporter le contenu (Enregistrer sous)**|**Exporter (Enregistrer sous)**|IPC_GENERIC_EXPORTL"EXPORT"|Ce droit permet également à l'utilisateur d'utiliser d'autres options d'exportation dans les applications, telles que **Envoyer à OneNote**.|
|Prédictif|TRANSFÉRER|Active l'option de transfert de message électronique et d'ajout de destinataires aux lignes **À** et **CC** .|Refusée en cas d'utilisation de la stratégie standard **Ne pas transférer** .|**Prédictif**|**Prédictif**|IPC_EMAIL_FORWARDL"FORWARD"|N’autorise pas le redirecteur à accorder des droits à d’autres utilisateurs dans le cadre de l’action de transfert.|
|Contrôle total|OWNER|Accorde tous les droits sur le document. Toutes les actions disponibles peuvent être effectuées.|Comme l'option personnalisée **Contrôle total** .|**Contrôle total**|**Contrôle total**|IPC_GENERIC_ALLL"OWNER"|Inclut la possibilité de supprimer la protection.|
|Imprimer|PRINT|Active les options d'impression du contenu.|Comme l'option **imprimer le contenu** dans les autorisations personnalisées. N’est pas un paramètre par destinataire.|**Imprimer**|**Imprimer**|IPC_GENERIC_PRINTL"PRINT|Aucune information supplémentaire|
|Répondre|RÉPONDRE|Active l'option Répondre dans un client de messagerie sans autoriser de modification des lignes **À** ou **CC** .|Non applicable|**Répondre**|**Répondre**|IPC_EMAIL_REPLY|Aucune information supplémentaire|
|Répondre à tous|REPLYALL|Active l'option **Répondre à tous** dans un client de messagerie, mais ne permet pas à l'utilisateur d'ajouter des destinataires aux lignes **À** ou **CC** .|Non applicable|**Répondre à tous**|**Répondre à tous**|IPC_EMAIL_REPLYALLL"REPLYALL"|Aucune information supplémentaire|
|Afficher, Ouvrir, Lire|AFFICHAGE|Permet à l'utilisateur d'ouvrir le document et d'en voir le contenu.|Comme l'option **Afficher** de la stratégie personnalisée **Lecture** .|**Afficher le contenu**|**View**|IPC_GENERIC_READL"VIEW"|Aucune information supplémentaire|
|Copier|EXTRACT|Active les options permettant de copier des données (y compris des captures d’écran) du document vers le même document ou un autre document.|Comme l'option de stratégie personnalisée **Autoriser les utilisateurs bénéficiant d'accès en lecture à copier le contenu** .|**Copier et Extraire le contenu**|**Extraction**|IPC_GENERIC_EXTRACTL"EXTRACT"|Dans certaines applications, permet également d’enregistrer l’ensemble du document sous forme non protégée.|
|Afficher les droits|AFFICHAGERIGHTSDATA|Permet à l'utilisateur d'afficher la stratégie appliquée au document.|Non implémenté|**Afficher les droits affectés**|**Afficher les droits**|IPC_READ_RIGHTSL"VIEWRIGHTSDATA"|Ignoré par certaines applications.|
|Modifier les droits|EDITRIGHTSDATA|Permet à l'utilisateur de modifier la stratégie appliquée au document. Inclut notamment la suppression de la protection.|Non implémenté|**Modifier les droits**|**Modifier les droits**|IPC_WRITE_RIGHTSL"EDITRIGHTSDATA"|Aucune information supplémentaire|
|Autoriser les macros|OBJMODEL|Active l'option permettant d'exécuter des macros ou d'effectuer d'autres opérations d'accès à distance ou par programme au contenu d'un document.|Comme l'option de stratégie personnalisée **Autoriser l'accès par programme** . N’est pas un paramètre par destinataire.|**Autoriser les macros**|**Autoriser les macros**|Non applicable|Aucune information supplémentaire|

## Droits inclus dans les niveaux d’autorisation
Certaines applications regroupent les droits d’utilisation dans des niveaux d’autorisation, ce qui facilite la sélection de droits d’utilisation qui sont généralement utilisés ensemble. Ces niveaux d’autorisation permettent de réduire la complexité, si bien que les utilisateurs peuvent choisir des options basées sur des rôles.  Par exemple, **Réviseur** et **Coauteur**. Bien que ces options montrent souvent aux utilisateurs un récapitulatif des droits, il peut arriver qu’elles n’incluent pas tous les droits répertoriés dans le tableau précédent.

Envisagez le tableau suivant comme une liste de ces niveaux d’autorisation et comme une liste complète des droits qu’ils renferment.

|Niveau d’autorisation|Applications|Droits inclus (nom commun)|
|---------------------|----------------|---------------------------------|
|Observateur|Portail Azure Classic<br /><br />Application de partage Rights Management pour Windows|Afficher, Ouvrir, Lire<br /><br />Répondre<br /><br />Répondre à tous|
|Réviseur|Portail Azure Classic<br /><br />Application de partage Rights Management pour Windows|Afficher, Ouvrir, Lire<br /><br />Enregistrer<br /><br />Modifier le contenu, Modifier<br /><br />Répondre [note 1]<br /><br />Répondre à tous [note 1]<br /><br />Transférer [note 1]|
|Coauteur|Portail Azure Classic<br /><br />Application de partage Rights Management pour Windows|Afficher, Ouvrir, Lire<br /><br />Enregistrer<br /><br />Modifier le contenu, Modifier<br /><br />Copier<br /><br />Afficher les droits<br /><br />Modifier les droits<br /><br />Autoriser les macros<br /><br />Enregistrer sous, Exporter<br /><br />Imprimer<br /><br />Répondre [note 1]<br /><br />Répondre à tous [note 1]<br /><br />Transférer [note 1]|
|Copropriétaire|Portail Azure Classic<br /><br />Application de partage Rights Management pour Windows|Afficher, Ouvrir, Lire<br /><br />Enregistrer<br /><br />Modifier le contenu, Modifier<br /><br />Copier<br /><br />Afficher les droits<br /><br />Modifier les droits<br /><br />Autoriser les macros<br /><br />Enregistrer sous, Exporter<br /><br />Imprimer<br /><br />Répondre [note 1]<br /><br />Répondre à tous [note 1]<br /><br />Transférer [note 1]<br /><br />Contrôle total|
Note 1 : Non applicable à l’application de partage Rights Management pour Windows

## Droits inclus dans les modèles par défaut
Les droits inclus avec les modèles par défaut sont les suivants :

|Nom d’affichage|Droits inclus (nom commun)|
|----------------|---------------------------------|
|&lt;nom de l’organisation&gt; - Affichage confidentiel uniquement|Afficher, Ouvrir, Lire|
|&lt;nom de l’organisation&gt; - Confidentiel|Afficher, Ouvrir, Lire<br /><br />Enregistrer<br /><br />Modifier le contenu, Modifier<br /><br />Afficher les droits<br /><br />Autoriser les macros<br /><br />Prédictif<br /><br />Répondre<br /><br />Répondre à tous|

## Voir aussi
[Configuration d'Azure Rights Management](configuring-azure-rights-management.md)



<!--HONumber=Apr16_HO3-->


