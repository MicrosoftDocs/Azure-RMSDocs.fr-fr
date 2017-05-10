---
title: "Configurer des droits d’utilisation pour Azure Rights Management - AIP"
description: "Découvrez et identifiez les droits spécifiques qui sont utilisés quand vous protégez des fichiers ou des e-mails à l’aide du service Azure Rights Management d’Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/26/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 97ddde38-b91b-42a5-8eb4-3ce6ce15393d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: ed06deca76ed1241f0c9b3f104fd922263c5a6cd
ms.sourcegitcommit: dd5a63bfee309c8b68ee9f8cd071a574ab0f6b4a
ms.translationtype: HT
ms.contentlocale: fr-FR
---
# <a name="configuring-usage-rights-for-azure-rights-management"></a>Configuration des droits d’utilisation pour Azure Rights Management

>*S’applique à : Azure Information Protection, Office 365*

Quand vous définissez la protection de fichiers ou d’e-mails à l’aide du service Azure Rights Management d’Azure Information Protection et que vous n’utilisez pas de modèle, vous devez configurer les droits d’utilisation vous-même. En outre, quand vous configurez des modèles personnalisés pour Azure Rights Management, vous sélectionnez les droits d’utilisation qui seront ensuite appliqués automatiquement quand le modèle sera sélectionné par des utilisateurs, administrateurs ou services configurés. Par exemple, dans le portail Azure Classic, vous pouvez sélectionner des rôles qui configurent un regroupement logique de droits d’utilisation, ou configurer les droits de façon individuelle.

Utilisez cet article pour vous aider à configurer les droits d’utilisation de l’application que vous utilisez et pour comprendre comment ces droits sont interprétés par les applications.

## <a name="usage-rights-and-descriptions"></a>Descriptions et droits d’utilisation
Le tableau suivant répertorie et décrit les droits d'utilisation pris en charge par Rights Management, et la manière dont ils sont utilisés et interprétés. Ils sont répertoriés selon le **Nom commun**, qui correspond à la manière dont le droit d’utilisation est généralement affiché ou référencé sous une forme plus conviviale que la valeur de mot unique utilisée dans le code (valeur d’**Encodage dans la stratégie**). 

La **Constante ou valeur d’API** est le nom SDK d’un appel d’API MSIPC utilisé quand vous écrivez une application compatible avec RMS qui recherche un droit d’utilisation ou en ajoute un à une stratégie.


|Right|Description|Implémentation|
|-------------------------------|---------------------------|-----------------|
|Nom commun : **Modifier le contenu, Modifier** <br /><br />Encodage dans la stratégie : **DOCEDIT**|Permet à l'utilisateur de modifier, réorganiser, mettre en forme ou filtrer le contenu de l'application. N'accorde pas le droit d'enregistrer la copie modifiée.|Droits personnalisés Office : En relation avec les options **Modifier** et **Contrôle total**. <br /><br />Nom dans le portail Azure Classic : **Modifier le contenu**<br /><br />Nom dans le portail Azure : Inclus dans **Modifier et enregistrer**<br /><br />Nom dans les modèles AD RMS : **Modifier** <br /><br />Constante ou valeur d’API : Non applicable|
|Nom commun : **Enregistrer** <br /><br />Encodage dans la stratégie : **EDIT**|Permet à l'utilisateur d'enregistrer le document à son emplacement actuel.<br /><br />Dans les applications Office, ce droit permet également à l'utilisateur de modifier le document.|Droits personnalisés Office : En relation avec les options **Modifier** et **Contrôle total**. <br /><br />Nom dans le portail Azure Classic : **Enregistrer le fichier**<br /><br />Nom dans le portail Azure : Inclus dans **Modifier et enregistrer**<br /><br />Nom dans les modèles AD RMS : **Enregistrer** <br /><br />Constante ou valeur d’API : `IPC_GENERIC_WRITE L"EDIT"`|
|Nom commun : **Commentaire** <br /><br />Encodage dans la stratégie : **COMMENT**|Active l'option d'ajout d'annotations ou de commentaires au contenu.<br /><br />Ce droit, disponible dans le SDK, est disponible en tant que stratégie ad hoc dans le module AzureInformationProtection et de protection RMS pour Windows PowerShell. Il a été implémenté dans certaines applications de fournisseur de logiciel. Toutefois, il n’est pas largement utilisé et n’est pas actuellement pris en charge par les applications Office.|Droits personnalisés Office : Non implémenté. <br /><br />Nom dans le portail Azure Classic : Non implémenté.<br /><br />Nom dans le portail Azure : Non implémenté.<br /><br />Nom dans les modèles AD RMS : Non implémenté. <br /><br />Constante ou valeur d’API : `IPC_GENERIC_COMMENT L"COMMENT`|
|Nom commun : **Enregistrer sous, Exporter** <br /><br />Encodage dans la stratégie : **EXPORT**|Active l'option d'enregistrement du contenu sous un autre nom de fichier (Enregistrer sous). Pour les documents Office et le client Azure Information Protection, le fichier peut être enregistré sans protection.<br /><br />Ce droit permet également à l'utilisateur d'utiliser d'autres options d'exportation dans les applications, telles que **Envoyer à OneNote**.<br /><br /> Remarque : si ce droit n’est pas accordé, les applications Office permettent à un utilisateur d’enregistrer un document sous un nouveau nom si le format de fichier sélectionné en mode natif prend en charge la protection Rights Management.|Droits personnalisés Office : En relation avec les options **Modifier** et **Contrôle total**. <br /><br />Nom dans le portail Azure Classic : **Exporter le contenu (Enregistrer sous)** <br /><br />Nom dans le portail Azure : Inclus dans **Contrôle total**<br /><br />Nom dans les modèles AD RMS : **Exporter (Enregistrer sous)** <br /><br />Constante ou valeur d’API : `IPC_GENERIC_EXPORT L"EXPORT"`|
|Nom commun : **Transférer** <br /><br />Encodage dans la stratégie : **FORWARD**|Active l'option de transfert de message électronique et d'ajout de destinataires aux lignes **À** et **CC** . Ce droit ne s’applique pas aux documents, mais uniquement aux e-mails.<br /><br />N'autorise pas le redirecteur à accorder des droits à d'autres utilisateurs dans le cadre de l'action de transfert. <br /><br />Quand vous accordez ce droit, vous devez également accorder le droit **Modifier le contenu, Modifier** (nom commun) pour que l’e-mail d’origine soit inclus dans le corps de l’e-mail transféré, et pas sous forme de pièce jointe. Ce droit est également obligatoire pour envoyer un e-mail à une autre organisation qui utilise le client Outlook ou Outlook Web App.|Droits personnalisés Office : Refusés en cas d’utilisation de la stratégie standard **Ne pas transférer**.<br /><br />Nom dans le portail Azure Classic : **Transférer**<br /><br />Nom dans le portail Azure : **Transférer**<br /><br />Nom dans les modèles AD RMS : **Transférer** <br /><br />Constante ou valeur d’API : `IPC_EMAIL_FORWARD L"FORWARD"`|
|Nom commun : **Contrôle total** <br /><br />Encodage dans la stratégie : **OWNER**|Accorde tous les droits sur le document. Toutes les actions disponibles peuvent être effectuées.<br /><br />Inclut la possibilité de supprimer la protection et de reprotéger un document. <br /><br />Notez que ce droit d’utilisation n’est pas le même que le [propriétaire Rights Management](#rights-management-issuer-and-rights-management-owner).|Droits personnalisés Office : Comme l’option personnalisée **Contrôle total**.<br /><br />Nom dans le portail Azure Classic : **Contrôle total**<br /><br />Nom dans le portail Azure : **Contrôle total**<br /><br />Nom dans les modèles AD RMS : **Contrôle total** <br /><br />Constante ou valeur d’API : `IPC_GENERIC_ALL L"OWNER"`|
|Nom commun : **Imprimer** <br /><br />Encodage dans la stratégie : **PRINT**|Active les options d'impression du contenu.|Droits personnalisés Office : Comme l’option **Imprimer le contenu** dans les autorisations personnalisées. N’est pas un paramètre par destinataire.<br /><br />Nom dans le portail Azure Classic : **Imprimer**<br /><br />Nom dans le portail Azure : **Imprimer**<br /><br />Nom dans les modèles AD RMS : **Imprimer** <br /><br />Constante ou valeur d’API : `IPC_GENERIC_PRINT L"PRINT"`|
|Nom commun : **Répondre** <br /><br />Encodage dans la stratégie : **REPLY**|Active l’option **Répondre** dans un client de messagerie sans autoriser de modification des lignes **À** ou **Cc**.<br /><br />Quand vous accordez ce droit, vous devez également accorder le droit **Modifier le contenu, Modifier** (nom commun) pour que l’e-mail d’origine soit inclus dans le corps de l’e-mail transféré, et pas sous forme de pièce jointe. Ce droit est également obligatoire pour envoyer un e-mail à une autre organisation qui utilise le client Outlook ou Outlook Web App.|Droits personnalisés Office : Non implémenté.<br /><br />Nom dans le portail Azure Classic : **Répondre**<br /><br />Nom dans les modèles AD RMS : **Répondre** <br /><br />Constante ou valeur d’API : `IPC_EMAIL_REPLY`|
|Nom commun : **Répondre à tous** <br /><br />Encodage dans la stratégie : **REPLYALL**|Active l'option **Répondre à tous** dans un client de messagerie, mais ne permet pas à l'utilisateur d'ajouter des destinataires aux lignes **À** ou **CC** .<br /><br />Quand vous accordez ce droit, vous devez également accorder le droit **Modifier le contenu, Modifier** (nom commun) pour que l’e-mail d’origine soit inclus dans le corps de l’e-mail transféré, et pas sous forme de pièce jointe. Ce droit est également obligatoire pour envoyer un e-mail à une autre organisation qui utilise le client Outlook ou Outlook Web App.|Droits personnalisés Office : Non implémenté.<br /><br />Nom dans le portail Azure Classic : **Répondre à tous**<br /><br />Nom dans le portail Azure : **Répondre à tous**<br /><br />Nom dans les modèles AD RMS : **Répondre à tous** <br /><br />Constante ou valeur d’API : `IPC_EMAIL_REPLYALL L"REPLYALL"`|
|Nom commun : **Afficher, Ouvrir, Lire** <br /><br />Encodage dans la stratégie : **VIEW**|Permet à l'utilisateur d'ouvrir le document et d'en voir le contenu.|Droits personnalisés Office : Comme l’option **Afficher** de la stratégie personnalisée **Lecture**.<br /><br />Nom dans le portail Azure classique : **Afficher**<br /><br />Nom dans le portail Azure : **Afficher le contenu**<br /><br />Nom dans les modèles AD RMS : **Répondre à tous** <br /><br />Constante ou valeur d’API : `IPC_GENERIC_READ L"VIEW"`|
|Nom commun : **Copier** <br /><br />Encodage dans la stratégie : **EXTRACT**|Active les options permettant de copier des données du document (y compris des captures d’écran) vers un autre emplacement du document ou vers un autre document.<br /><br />Dans certaines applications, permet également d’enregistrer l’ensemble du document sous forme non protégée.|Droits personnalisés Office : comme l’option de stratégie personnalisée **Autoriser les utilisateurs bénéficiant d’accès en lecture à copier le contenu**.<br /><br />Nom dans le portail Azure Classic : **Copier et Extraire le contenu**<br /><br />Nom dans le portail Azure : **Copier et extraire le contenu**<br /><br />Nom dans les modèles AD RMS : **Extraire** <br /><br />Constante ou valeur d’API : `IPC_GENERIC_EXTRACT L"EXTRACT"`|
|Nom commun : **Autoriser les macros** <br /><br />Encodage dans la stratégie : **OBJMODEL**|Active l'option permettant d'exécuter des macros ou d'effectuer d'autres opérations d'accès à distance ou par programme au contenu d'un document.|Droits personnalisés Office : Comme l’option de la stratégie personnalisée **Autoriser l’accès par programme**. N’est pas un paramètre par destinataire.<br /><br />Nom dans le portail Azure Classic : **Autoriser les macros**<br /><br />Nom dans le portail Azure : Inclus dans tous les droits que vous pouvez sélectionner, car ce droit est obligatoire pour utiliser la barre Azure Information Protection dans les applications Office.<br /><br />Nom dans les modèles AD RMS : **Autoriser les macros** <br /><br />Constante ou valeur d’API : Non applicable|

## <a name="rights-included-in-permissions-levels"></a>Droits inclus dans les niveaux d’autorisation

Certaines applications regroupent les droits d’utilisation dans des niveaux d’autorisation, ce qui facilite la sélection de droits d’utilisation qui sont généralement utilisés ensemble. Ces niveaux d’autorisation permettent de réduire la complexité, si bien que les utilisateurs peuvent choisir des options basées sur des rôles.  Par exemple, **Réviseur** et **Coauteur**. Bien que ces options montrent souvent aux utilisateurs un récapitulatif des droits, il peut arriver qu’elles n’incluent pas tous les droits répertoriés dans le tableau précédent.

Envisagez le tableau suivant comme une liste de ces niveaux d’autorisation et comme une liste complète des droits qu’ils renferment.

|Niveau d’autorisation|Applications|Droits inclus (nom commun)|
|---------------------|----------------|---------------------------------|
|Observateur|Portail Azure Classic <br /><br />Portail Azure<br /><br /> Application de partage Rights Management pour Windows<br /><br />Client Azure Information Protection pour Windows|Afficher, Ouvrir, Lire ; Répondre ; Répondre à tous ; Autoriser les macros [[1]](#footnote-1)<br /><br />Remarque : Pour les e-mails, utilisez plutôt le niveau d’autorisation Réviseur pour vous assurer que la réponse à un e-mail sera reçue sous forme d’e-mail, et non de pièce jointe. Le niveau Réviseur est également obligatoire pour envoyer un e-mail à une autre organisation qui utilise le client Outlook ou Outlook Web App.|
|Réviseur|Portail Azure Classic <br /><br />Portail Azure<br /><br />Application de partage Rights Management pour Windows<br /><br />Client Azure Information Protection pour Windows|Afficher, Ouvrir, Lire ; Enregistrer ; Modifier le contenu, Modifier ; Répondre : Répondre à tous [[2]](#footnote-2) ; Transférer [[2]](#footnote-2) ; Autoriser les macros [[1]](#footnote-1)|
|Coauteur|Portail Azure Classic <br /><br />Portail Azure<br /><br />Application de partage Rights Management pour Windows<br /><br />Client Azure Information Protection pour Windows|Afficher, Ouvrir, Lire ; Enregistrer ; Modifier le contenu, Modifier ; Copier ; Afficher les droits ; Autoriser les macros ; Enregistrer sous, Exporter [[3]](#footnote-3) ; Imprimer ; Répondre [[2]](#footnote-2) ; Répondre à tous [[2]](#footnote-2) ; Transférer [[2]](#footnote-2)|
|Copropriétaire|Portail Azure Classic <br /><br />Portail Azure<br /><br />Application de partage Rights Management pour Windows<br /><br />Client Azure Information Protection pour Windows|Afficher, Ouvrir, Lire ; Enregistrer ; Modifier le contenu, Modifier ; Copier ; Afficher les droits ; Autoriser les macros ; Enregistrer sous, Exporter ; Imprimer ; Répondre [[2]](#footnote-2) ; Répondre à tous [[2]](#footnote-2) ; Transférer [[2]](#footnote-2) ; Contrôle total|

----

###### <a name="footnote-1"></a>Note 1

Pour le client Azure Information Protection pour Windows, ce droit est nécessaire pour la barre Information Protection dans les applications Office.

###### <a name="footnote-2"></a>Note 2
Ne s’applique pas au client Azure Information Protection pour Windows, ni à l’application de partage Rights Management pour Windows.

###### <a name="footnote-3"></a>Note 3
Non inclus dans le client Azure Information Protection pour Windows. Dans ce client, le droit d’utilisation Exporter inclut la possibilité de supprimer la protection.


## <a name="rights-included-in-the-default-templates"></a>Droits inclus dans les modèles par défaut
Les droits inclus avec les modèles par défaut sont les suivants :

|Nom d’affichage|Droits inclus (nom commun)|
|----------------|---------------------------------|
|&lt;*nom de l’organisation*&gt; *- Affichage confidentiel uniquement*|Afficher, Ouvrir, Lire|
|&lt;*nom de l’organisation*&gt; *- Confidentiel*|Afficher, Ouvrir, Lire ; Enregistrer ; Modifier le contenu, Modifier ; Afficher les droits ; Autoriser les macros ; Transférer ; Répondre ; Répondre à tous|

## <a name="do-not-forward-option-for-emails"></a>Option Ne pas transférer pour les e-mails

Les clients et services Exchange (par exemple, le client Outlook, l’application Outlook Web Access et les règles de transport Exchange) ont une option de protection des droits d’information supplémentaire pour les e-mails : **Ne pas transférer**. 

Même si cette option apparaît aux utilisateurs (les administrateurs Exchange) comme s’il s’agissait d’un modèle de gestion des droits par défaut qu’ils peuvent sélectionner, **Ne pas transférer** n’est pas un modèle. Cela explique pourquoi vous ne pouvez pas la voir dans le portail classique Azure quand vous affichez et gérez des modèles pour Azure Rights Management. L’option **Ne pas transférer** correspond plutôt à un ensemble de droits appliqué dynamiquement par les utilisateurs à leurs destinataires.

Quand l’option **Ne pas transférer** est appliquée à un e-mail, les destinataires ne peuvent pas le transférer, l’imprimer, en copier le contenu, enregistrer des pièces jointes ou l’enregistrer sous un autre nom. Par exemple, dans le client Outlook, le bouton Transférer n’est pas disponible. Les options de menu **Enregistrer sous**, **Enregistrer les pièces jointes** et **Imprimer** ne sont pas disponibles non plus. Vous ne pouvez pas ajouter ou modifier des destinataires dans les zones **À**, **Cc** ou **Cci**.

Il existe une distinction importante entre l’application de l’option **Ne pas transférer** et celle d’un modèle qui n’accorde pas le droit d’être transféré à un e-mail : l’option **Ne pas transférer** utilise une liste dynamique des utilisateurs autorisés qui se base sur les destinataires choisis de l’utilisateur de l’e-mail d’origine, tandis que les droits du modèle ont une liste statique d’utilisateurs autorisés que l’administrateur a spécifiée au préalable. Quelle est la différence ? Prenons un exemple : 

Une utilisatrice veut envoyer certaines informations par e-mail à certaines personnes du service Marketing. Ces informations ne doivent être partagées avec personne d’autre. A-t-elle intérêt à protéger l’e-mail avec un modèle qui restreint les droits (affichage, réponse et enregistrement) au service Marketing ?  Ou doit-elle choisir d’utiliser l’option **Ne pas transférer** ? Ces deux possibilités ont pour résultat d’empêcher les destinataires de transférer l’e-mail. 

- Si elle applique le modèle, les destinataires peuvent quand même partager les informations avec d’autres utilisateurs du service Marketing. Par exemple, un destinataire pourrait utiliser l’Explorateur pour glisser-déplacer l’e-mail vers un emplacement partagé ou un lecteur USB. Ainsi, toute personne du service Marketing (dont le propriétaire de l’e-mail) qui a accès à cet emplacement peut afficher les informations contenues dans l’e-mail.
 
- Si elle applique l’option **Ne pas transférer**, les destinataires ne pourront pas partager les informations avec d’autres personnes du service Marketing en déplaçant l’e-mail vers un autre emplacement. Dans ce scénario, seuls les destinataires d’origine (et le propriétaire du message) sont en mesure d’afficher les informations contenues dans l’e-mail.

> [!NOTE] 
> Utilisez l’option **Ne pas transférer** quand il est important que seuls les destinataires choisis par l’expéditeur puissent consulter les informations contenues dans l’e-mail. Utilisez un modèle pour les e-mails afin de restreindre les droits à un groupe de personnes que l’administrateur spécifie à l’avance, indépendamment des destinataires choisis de l’expéditeur.

## <a name="rights-management-issuer-and-rights-management-owner"></a>Émetteur Rights Management et propriétaire Rights Management

Quand un document ou un e-mail est protégé à l’aide du service Azure Rights Management, le compte qui protège ce contenu devient automatiquement l’émetteur Rights Management pour ce contenu. Ce compte est enregistré sous la désignation **issuer** dans les [journaux d’utilisation](log-analyze-usage.md#how-to-interpret-your-azure-rights-management-usage-logs). 

L’émetteur Rights Management a toujours le droit d’utilisation Contrôle total pour le document ou l’e-mail, plus les droits suivants :

- Si les paramètres de protection incluent une date d’expiration, l’émetteur Rights Management garde le droit d’ouvrir et de modifier le document ou l’e-mail après cette date.

- L’émetteur Rights Management garde le droit d’accéder au document ou à l’e-mail en mode hors connexion.

- L’émetteur Rights Management garde le droit d’ouvrir un document ayant été révoqué. 

Par défaut, ce compte est également le **propriétaire Rights Management** de ce contenu, ce qui est le cas quand le créateur du document ou de l’e-mail démarre la protection. Dans certains scénarios, un administrateur ou un service peut protéger du contenu pour le compte d’utilisateurs. Exemple :

- Un administrateur protège les fichiers en bloc sur un partage de fichiers : le compte Administrateur dans Azure AD protège les documents des utilisateurs.

- Le connecteur Rights Management protège les documents Office dans un dossier Windows Server : le compte du principal du service qui est créé dans Azure AD pour le connecteur RMS protège les documents des utilisateurs.

Dans ces scénarios, l’émetteur Rights Management peut attribuer la propriété Rights Management à un autre compte à l’aide des kits SDK Azure Information Protection ou de PowerShell. Par exemple, si vous utilisez l’applet de commande PowerShell [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) avec le client Azure Information Protection, vous pouvez définir le paramètre **OwnerEmail** pour attribuer la propriété Rights Management à un autre compte. 

Quand l’émetteur Rights Management protège du contenu pour le compte d’utilisateurs, l’attribution de la propriété Rights Management permet de garantir que le propriétaire du document ou de l’e-mail d’origine a le même niveau de contrôle sur son contenu protégé que s’il avait démarré lui-même la protection. 

Par exemple, un utilisateur peut imprimer un document qu’il a créé, même si ce document est maintenant protégé avec un modèle qui n’inclut pas le droit d’utilisation Imprimer. Ce même utilisateur garde l’accès à son document, indépendamment du paramètre d’accès hors connexion ou de la date d’expiration qui ont éventuellement été configurés dans ce modèle. De plus, étant donné que le propriétaire Rights Management a le droit d’utilisation Contrôle total, cet utilisateur peut également reprotéger le document pour accorder l’accès à des utilisateurs supplémentaires (l’utilisateur devient alors l’émetteur Rights Management, en plus d’être le propriétaire Rights Management). De la même façon, cet utilisateur peut aussi supprimer la protection. En revanche, seul l’émetteur Rights Management peut suivre et révoquer un document.

Le propriétaire Rights Management d’un document ou d’un e-mail est enregistré sous la désignation **owner-email** dans les [journaux d’utilisation](log-analyze-usage.md#how-to-interpret-your-azure-rights-management-usage-logs).

Notez que le propriétaire Rights Management est indépendant du propriétaire du système de fichiers Windows. Les deux propriétaires sont souvent les mêmes, mais ils peuvent être différents, même si vous n’utilisez pas les kits SDK ou PowerShell.

## <a name="see-also"></a>Voir aussi
[Configuration de modèles personnalisés pour le service Azure Rights Management](configure-custom-templates.md)

[Configuration de super utilisateurs pour Azure Rights Management et les services de découverte ou la récupération de données](configure-super-users.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

