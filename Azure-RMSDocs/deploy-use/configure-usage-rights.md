---
title: "Configurer des droits d’utilisation pour Azure Rights Management - AIP"
description: "Découvrez et identifiez les droits spécifiques qui sont utilisés quand vous protégez des fichiers ou des e-mails à l’aide du service Azure Rights Management d’Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/27/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 97ddde38-b91b-42a5-8eb4-3ce6ce15393d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: faa00eee76e6c084db1a4dfb1d477e491fae5fee
ms.sourcegitcommit: 3e9b3c2206807e82cc4721a50862b74152906f63
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/28/2018
---
# <a name="configuring-usage-rights-for-azure-rights-management"></a>Configuration des droits d’utilisation pour Azure Rights Management

>*S’applique à : Azure Information Protection, Office 365*

Quand vous définissez la protection de fichiers ou d’e-mails à l’aide du service Azure Rights Management d’Azure Information Protection et que vous n’utilisez pas de modèle, vous devez configurer les droits d’utilisation vous-même. En outre, quand vous configurez des modèles ou des étiquettes pour la protection Azure Rights Management, vous sélectionnez les droits d’utilisation qui sont ensuite appliqués automatiquement quand le modèle est sélectionné par des utilisateurs, des administrateurs ou des services configurés. Par exemple, dans le portail Azure, vous pouvez sélectionner des rôles qui configurent un regroupement logique de droits d’utilisation, ou vous pouvez configurer les droits individuels.

Utilisez cet article pour vous aider à configurer les droits d’utilisation de l’application que vous utilisez et pour comprendre comment ces droits sont interprétés par les applications.

> [!NOTE] 
> Dans un souci d’exhaustivité, cet article contient les valeurs du portail Azure Classic qui a été mis hors service le 8 janvier 2018.
>
> Pour vous aider à migrer vers le nouveau portail, consultez [Tâches que vous aviez l’habitude d’effectuer avec le portail Azure Classic](migrate-portal.md).

## <a name="usage-rights-and-descriptions"></a>Descriptions et droits d’utilisation
Le tableau suivant répertorie et décrit les droits d'utilisation pris en charge par Rights Management, et la manière dont ils sont utilisés et interprétés. Ils sont répertoriés selon le **nom commun**, qui correspond à la manière dont le droit d’utilisation est généralement affiché ou référencé sous une forme plus conviviale que la valeur à un seul mot utilisée dans le code (valeur d’**Encodage dans la stratégie**). 

La **Constante ou valeur d’API** est le nom SDK d’un appel d’API MSIPC utilisé quand vous écrivez une application compatible avec RMS qui recherche un droit d’utilisation ou en ajoute un à une stratégie.


|Droit d’utilisation|Description|Implémentation|
|-------------------------------|---------------------------|-----------------|
|Nom commun : **Modifier le contenu, Modifier** <br /><br />Encodage dans la stratégie : **DOCEDIT**|Permet à l’utilisateur de modifier, réorganiser, mettre en forme ou filtrer le contenu de l’application. N'accorde pas le droit d'enregistrer la copie modifiée.|Droits personnalisés Office : En relation avec les options **Modifier** et **Contrôle total**. <br /><br />Nom dans le portail Azure Classic : **Modifier le contenu**<br /><br />Nom dans le portail Azure : **Modifier le contenu, Modifier (DOCEDIT)**<br /><br />Nom dans les modèles AD RMS : **Modifier** <br /><br />Constante ou valeur d’API : Non applicable|
|Nom commun : **Enregistrer** <br /><br />Encodage dans la stratégie : **EDIT**|Permet à l'utilisateur d'enregistrer le document à son emplacement actuel.<br /><br />Dans les applications Office, ce droit permet également à l'utilisateur de modifier le document.|Droits personnalisés Office : En relation avec les options **Modifier** et **Contrôle total**. <br /><br />Nom dans le portail Azure Classic : **Enregistrer le fichier**<br /><br />Nom dans le portail Azure : **Enregistrer (EDIT)**<br /><br />Nom dans les modèles AD RMS : **Enregistrer** <br /><br />Constante ou valeur d’API : `IPC_GENERIC_WRITE L"EDIT"`|
|Nom commun : **Commentaire** <br /><br />Encodage dans la stratégie : **COMMENT**|Active l’option d’ajout d’annotations ou de commentaires au contenu.<br /><br />Ce droit, disponible dans le SDK, est disponible en tant que stratégie ad hoc dans le module AzureInformationProtection et de protection RMS pour Windows PowerShell. Il a été implémenté dans certaines applications de fournisseur de logiciel. Toutefois, il n’est pas largement utilisé et n’est pas actuellement pris en charge par les applications Office.|Droits personnalisés Office : Non implémenté. <br /><br />Nom dans le portail Azure Classic : Non implémenté.<br /><br />Nom dans le portail Azure : Non implémenté.<br /><br />Nom dans les modèles AD RMS : Non implémenté. <br /><br />Constante ou valeur d’API : `IPC_GENERIC_COMMENT L"COMMENT`|
|Nom commun : **Enregistrer sous, Exporter** <br /><br />Encodage dans la stratégie : **EXPORT**|Active l'option d'enregistrement du contenu sous un autre nom de fichier (Enregistrer sous). <br /><br />Pour les documents Office et le client Azure Information Protection, le fichier peut être enregistré sans protection et reprotégé avec de nouveaux paramètres et autorisations. Ces actions autorisées signifient qu’un utilisateur disposant de ce droit peut changer ou supprimer une étiquette Azure Information Protection dans un document ou un e-mail protégé. <br /><br />Ce droit permet également à l'utilisateur d'utiliser d'autres options d'exportation dans les applications, telles que **Envoyer à OneNote**.<br /><br /> Remarque : si ce droit n’est pas accordé, les applications Office permettent à un utilisateur d’enregistrer un document sous un nouveau nom si le format de fichier sélectionné en mode natif prend en charge la protection Rights Management.|Droits personnalisés Office : En relation avec les options **Modifier** et **Contrôle total**. <br /><br />Nom dans le portail Azure Classic : **Exporter le contenu (Enregistrer sous)** <br /><br />Nom dans le portail Azure : **Enregistrer sous, Exporter (EXPORT)**<br /><br />Nom dans les modèles AD RMS : **Exporter (Enregistrer sous)** <br /><br />Constante ou valeur d’API : `IPC_GENERIC_EXPORT L"EXPORT"`|
|Nom commun : **Transférer** <br /><br />Encodage dans la stratégie : **FORWARD**|Active l'option de transfert de message électronique et d'ajout de destinataires aux lignes **À** et **CC** . Ce droit ne s’applique pas aux documents, mais uniquement aux e-mails.<br /><br />N'autorise pas le redirecteur à accorder des droits à d'autres utilisateurs dans le cadre de l'action de transfert. <br /><br />Quand vous accordez ce droit, vous devez également accorder le droit **Modifier le contenu, Modifier** (nom commun) pour que l’e-mail d’origine soit inclus dans le corps de l’e-mail transféré, et pas sous forme de pièce jointe. Ce droit est également obligatoire pour envoyer un e-mail à une autre organisation qui utilise le client Outlook ou Outlook Web App. Il est également obligatoire pour les utilisateurs de votre organisation qui sont exemptés de l’utilisation du service Azure Rights Management, car vous avez implémenté des [contrôles d’intégration](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy).|Droits personnalisés Office : Refusés en cas d’utilisation de la stratégie standard **Ne pas transférer**.<br /><br />Nom dans le portail Azure Classic : **Transférer**<br /><br />Nom dans le portail Azure : **Transférer (FORWARD)**<br /><br />Nom dans les modèles AD RMS : **Transférer** <br /><br />Constante ou valeur d’API : `IPC_EMAIL_FORWARD L"FORWARD"`|
|Nom commun : **Contrôle total** <br /><br />Encodage dans la stratégie : **OWNER**|Accorde tous les droits sur le document. Toutes les actions disponibles peuvent être effectuées.<br /><br />Inclut la possibilité de supprimer la protection et de reprotéger un document. <br /><br />Notez que ce droit d’utilisation n’est pas le même que le [propriétaire Rights Management](#rights-management-issuer-and-rights-management-owner).|Droits personnalisés Office : Comme l’option personnalisée **Contrôle total**.<br /><br />Nom dans le portail Azure Classic : **Contrôle total**<br /><br />Nom dans le portail Azure : **Contrôle total (OWNER)**<br /><br />Nom dans les modèles AD RMS : **Contrôle total** <br /><br />Constante ou valeur d’API : `IPC_GENERIC_ALL L"OWNER"`|
|Nom commun : **Imprimer** <br /><br />Encodage dans la stratégie : **PRINT**|Active les options d'impression du contenu.|Droits personnalisés Office : Comme l’option **Imprimer le contenu** dans les autorisations personnalisées. N’est pas un paramètre par destinataire.<br /><br />Nom dans le portail Azure Classic : **Imprimer**<br /><br />Nom dans le portail Azure : **Imprimer (PRINT)**<br /><br />Nom dans les modèles AD RMS : **Imprimer** <br /><br />Constante ou valeur d’API : `IPC_GENERIC_PRINT L"PRINT"`|
|Nom commun : **Répondre** <br /><br />Encodage dans la stratégie : **REPLY**|Active l’option **Répondre** dans un client de messagerie sans autoriser de modification des lignes **À** ou **Cc**.<br /><br />Quand vous accordez ce droit, vous devez également accorder le droit **Modifier le contenu, Modifier** (nom commun) pour que l’e-mail d’origine soit inclus dans le corps de l’e-mail transféré, et pas sous forme de pièce jointe. Ce droit est également obligatoire pour envoyer un e-mail à une autre organisation qui utilise le client Outlook ou Outlook Web App. Il est également obligatoire pour les utilisateurs de votre organisation qui sont exemptés de l’utilisation du service Azure Rights Management, car vous avez implémenté des [contrôles d’intégration](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy).|Droits personnalisés Office : Non implémenté.<br /><br />Nom dans le portail Azure Classic : **Répondre**<br /><br />Nom dans le portail Azure : **Répondre (REPLY)**<br /><br />Nom dans les modèles AD RMS : **Répondre** <br /><br />Constante ou valeur d’API : `IPC_EMAIL_REPLY`|
|Nom commun : **Répondre à tous** <br /><br />Encodage dans la stratégie : **REPLYALL**|Active l'option **Répondre à tous** dans un client de messagerie, mais ne permet pas à l'utilisateur d'ajouter des destinataires aux lignes **À** ou **CC** .<br /><br />Quand vous accordez ce droit, vous devez également accorder le droit **Modifier le contenu, Modifier** (nom commun) pour que l’e-mail d’origine soit inclus dans le corps de l’e-mail transféré, et pas sous forme de pièce jointe. Ce droit est également obligatoire pour envoyer un e-mail à une autre organisation qui utilise le client Outlook ou Outlook Web App. Il est également obligatoire pour les utilisateurs de votre organisation qui sont exemptés de l’utilisation du service Azure Rights Management, car vous avez implémenté des [contrôles d’intégration](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy).|Droits personnalisés Office : Non implémenté.<br /><br />Nom dans le portail Azure Classic : **Répondre à tous**<br /><br />Nom dans le portail Azure : **Répondre à tous (REPLY ALL)**<br /><br />Nom dans les modèles AD RMS : **Répondre à tous** <br /><br />Constante ou valeur d’API : `IPC_EMAIL_REPLYALL L"REPLYALL"`|
|Nom commun : **Afficher, Ouvrir, Lire** <br /><br />Encodage dans la stratégie : **VIEW**|Permet à l'utilisateur d'ouvrir le document et d'en voir le contenu.|Droits personnalisés Office : Comme l’option **Afficher** de la stratégie personnalisée **Lecture**.<br /><br />Nom dans le portail Azure classique : **Afficher**<br /><br />Nom dans le portail Azure : **Afficher, Ouvrir, Lire (VIEW)**<br /><br />Nom dans les modèles AD RMS : **Répondre à tous** <br /><br />Constante ou valeur d’API : `IPC_GENERIC_READ L"VIEW"`|
|Nom commun : **Copier** <br /><br />Encodage dans la stratégie : **EXTRACT**|Active les options permettant de copier des données du document (y compris des captures d’écran) vers un autre emplacement du document ou vers un autre document.<br /><br />Dans certaines applications, permet également d’enregistrer l’ensemble du document sous forme non protégée.|Droits personnalisés Office : comme l’option de stratégie personnalisée **Autoriser les utilisateurs bénéficiant d’accès en lecture à copier le contenu**.<br /><br />Nom dans le portail Azure Classic : **Copier et Extraire le contenu**<br /><br />Nom dans le portail Azure : **Copier (EXTRACT)**<br /><br />Nom dans les modèles AD RMS : **Extraire** <br /><br />Constante ou valeur d’API : `IPC_GENERIC_EXTRACT L"EXTRACT"`|
|Nom commun : **Afficher les droits** <br /><br />Encodage dans la stratégie : **VIEWRIGHTSDATA**|Permet à l'utilisateur d'afficher la stratégie appliquée au document.|Droits personnalisés Office : Non implémenté.<br /><br />Nom dans le portail Azure Classic : **Afficher les droits affectés**<br /><br />Nom dans le portail Azure : **Afficher les droits (VIEWRIGHTSDATA)**.<br /><br />Nom dans les modèles AD RMS : **Afficher les droits** <br /><br />Constante ou valeur d’API : `IPC_READ_RIGHTS L"VIEWRIGHTSDATA"`|
|Nom commun : **Modifier les droits** <br /><br />Encodage dans la stratégie : **EDITRIGHTSDATA**|Permet à l'utilisateur de modifier la stratégie appliquée au document. Inclut notamment la suppression de la protection.|Droits personnalisés Office : Non implémenté.<br /><br />Nom dans le portail Azure Classic : **Modifier les droits**<br /><br />Nom dans le portail Azure : **Modifier les droits (EDITRIGHTSDATA)**.<br /><br />Nom dans les modèles AD RMS : **Modifier les droits** <br /><br />Constante ou valeur d’API : `PC_WRITE_RIGHTS L"EDITRIGHTSDATA"`|
|Nom commun : **Autoriser les macros** <br /><br />Encodage dans la stratégie : **OBJMODEL**|Active l'option permettant d'exécuter des macros ou d'effectuer d'autres opérations d'accès à distance ou par programme au contenu d'un document.|Droits personnalisés Office : Comme l’option de la stratégie personnalisée **Autoriser l’accès par programme**. N’est pas un paramètre par destinataire.<br /><br />Nom dans le portail Azure Classic : **Autoriser les macros**<br /><br />Nom dans le portail Azure : **Autoriser les macros (OBJMODEL)**<br /><br />Nom dans les modèles AD RMS : **Autoriser les macros** <br /><br />Constante ou valeur d’API : Non applicable|

## <a name="rights-included-in-permissions-levels"></a>Droits inclus dans les niveaux d’autorisation

Certaines applications regroupent les droits d’utilisation dans des niveaux d’autorisation, ce qui facilite la sélection de droits d’utilisation qui sont généralement utilisés ensemble. Ces niveaux d’autorisation permettent de réduire la complexité, si bien que les utilisateurs peuvent choisir des options basées sur des rôles.  Par exemple, **Réviseur** et **Coauteur**. Bien que ces options montrent souvent aux utilisateurs un récapitulatif des droits, il peut arriver qu’elles n’incluent pas tous les droits répertoriés dans le tableau précédent.

Utilisez le tableau suivant pour obtenir la liste de ces niveaux d’autorisation et la liste complète des droits d’utilisation qu’ils renferment. Les droits d’utilisation sont répertoriés selon leur [nom commun](#usage-rights-and-descriptions).

|Niveau d’autorisation|Applications|Droits d’utilisation inclus|
|---------------------|----------------|---------------------------------|
|Observateur|Portail Azure Classic <br /><br />Portail Azure<br /><br /> Application de partage Rights Management pour Windows<br /><br />Client Azure Information Protection pour Windows|Afficher, Ouvrir, Lire ; Afficher les droits ; Répondre [[1]](#footnote-1) ; Répondre à tous [[1]](#footnote-1) ; Autoriser les macros [[2]](#footnote-2)<br /><br />Remarque : Pour les e-mails, utilisez plutôt le niveau d’autorisation Réviseur pour vous assurer que la réponse à un e-mail sera reçue sous forme d’e-mail, et non de pièce jointe. Le niveau Réviseur est également obligatoire pour envoyer un e-mail à une autre organisation qui utilise le client Outlook ou Outlook Web App. Il est également obligatoire pour les utilisateurs de votre organisation qui sont exemptés de l’utilisation du service Azure Rights Management, car vous avez implémenté des [contrôles d’intégration](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy).|
|Réviseur|Portail Azure Classic <br /><br />Portail Azure<br /><br />Application de partage Rights Management pour Windows<br /><br />Client Azure Information Protection pour Windows|Afficher, Ouvrir, Lire ; Enregistrer ; Modifier le contenu, Modifier ; Afficher les droits ; Répondre : Répondre à tous [[3]](#footnote-3) ; Transférer [[3]](#footnote-3) ; Autoriser les macros [[2]](#footnote-2)|
|Coauteur|Portail Azure Classic <br /><br />Portail Azure<br /><br />Application de partage Rights Management pour Windows<br /><br />Client Azure Information Protection pour Windows|Afficher, Ouvrir, Lire ; Enregistrer ; Modifier le contenu, Modifier ; Copier ; Afficher les droits ; Autoriser les macros ; Enregistrer sous, Exporter [[4]](#footnote-4) ; Imprimer ; Répondre [[3]](#footnote-3) ; Répondre à tous [[3]](#footnote-3) ; Transférer [[3]](#footnote-3)|
|Copropriétaire|Portail Azure Classic <br /><br />Portail Azure<br /><br />Application de partage Rights Management pour Windows<br /><br />Client Azure Information Protection pour Windows|Afficher, Ouvrir, Lire ; Enregistrer ; Modifier le contenu, Modifier ; Copier ; Afficher les droits ; Modifier les droits ; Autoriser les macros ; Enregistrer sous, Exporter ; Imprimer ; Répondre [[3]](#footnote-3) ; Répondre à tous [[3]](#footnote-3) ; Transférer [[3]](#footnote-3) ; Contrôle total|

----

###### <a name="footnote-1"></a>Note 1

Non inclus dans le portail Azure.

###### <a name="footnote-2"></a>Note 2

Pour le client Azure Information Protection pour Windows, ce droit est nécessaire pour la barre Information Protection dans les applications Office.

###### <a name="footnote-3"></a>Note 3
Ne s’applique pas au client Azure Information Protection pour Windows, ni à l’application de partage Rights Management pour Windows.

###### <a name="footnote-4"></a>Note 4
Non inclus dans le portail Azure ou le client Azure Information Protection pour Windows.

## <a name="rights-included-in-the-default-templates"></a>Droits inclus dans les modèles par défaut
Le tableau suivant répertorie les droits d’utilisation inclus quand les modèles par défaut sont créés. Les droits d’utilisation sont répertoriés selon leur [nom commun](#usage-rights-and-descriptions).

Ces modèles par défaut sont créés quand vous achetez votre abonnement, et vous pouvez [changer](configure-policy-templates.md) les noms et les droits d’utilisation dans le portail Azure. 

|Nom d’affichage du modèle|Droits d’utilisation postérieurs au 6 octobre 2017|Droits d’utilisation antérieurs au 6 octobre 2017|
|----------------|--------------------|----------|
|\<*nom de l’organisation> - Affichage confidentiel uniquement* <br /><br />ou<br /><br /> *Hautement confidentiel \ Tous les employés*|Afficher, Ouvrir, Lire ; Copier ; Afficher les droits ; Autoriser les macros ; Imprimer ; Transférer ; Répondre ; Répondre à tous ; Enregistrer ; Modifier le contenu, Modifier|Afficher, Ouvrir, Lire|
|\<*nom de l’organisation> - Confidentiel* <br /><br />ou <br /><br />*Confidentiel \ Tous les employés*|Afficher, Ouvrir, Lire ; Enregistrer sous, Exporter ; Copier ; Afficher les droits ; Modifier les droits ; Autoriser les macros ; Imprimer ; Transférer ; Répondre ; Répondre à tous ; Enregistrer ; Modifier le contenu, Modifier ; Contrôle total|Afficher, Ouvrir, Lire ; Enregistrer sous ; Exporter ; Modifier le contenu, Modifier ; Afficher les droits ; Autoriser les macros ; Transférer ; Répondre ; Répondre à tous|

## <a name="do-not-forward-option-for-emails"></a>Option Ne pas transférer pour les e-mails

Les clients et services Exchange (par exemple, le client Outlook, l’application Outlook Web Access et les règles de transport Exchange) disposent d’une option de protection des droits d’information supplémentaire pour les e-mails : **Ne pas transférer**. 

Même si cette option apparaît aux utilisateurs (les administrateurs Exchange) comme s’il s’agissait d’un modèle de gestion des droits par défaut qu’ils peuvent sélectionner, **Ne pas transférer** n’est pas un modèle. Ceci explique pourquoi vous ne pouvez pas la voir dans le portail Azure quand vous visualisez et que vous gérez des modèles pour Azure Rights Management. L’option **Ne pas transférer** correspond plutôt à un ensemble de droits appliqué dynamiquement par les utilisateurs à leurs destinataires.

Lorsque l’option **Ne pas transférer** est appliquée à un e-mail, cet e-mail est chiffré et les destinataires doivent être authentifiés. Les destinataires ne peuvent alors pas le transférer, l’imprimer, en copier le contenu, enregistrer des pièces jointes ou l’enregistrer sous un autre nom. Par exemple, dans le client Outlook, le bouton Transférer n’est pas disponible. Les options de menu **Enregistrer sous**, **Enregistrer les pièces jointes** et **Imprimer** ne sont pas disponibles non plus. Vous ne pouvez pas ajouter ou modifier des destinataires dans les zones **À**, **Cc** ou **Cci**.

Il existe une distinction importante entre l’application de l’option **Ne pas transférer** et celle d’un modèle qui n’accorde pas le droit d’être transféré à un e-mail : l’option **Ne pas transférer** utilise une liste dynamique des utilisateurs autorisés qui se base sur les destinataires choisis de l’utilisateur de l’e-mail d’origine, tandis que les droits du modèle ont une liste statique d’utilisateurs autorisés que l’administrateur a spécifiée au préalable. Quelle est la différence ? Prenons un exemple : 

Une utilisatrice veut envoyer certaines informations par e-mail à certaines personnes du service Marketing. Ces informations ne doivent être partagées avec personne d’autre. A-t-elle intérêt à protéger l’e-mail avec un modèle qui restreint les droits (affichage, réponse et enregistrement) au service Marketing ?  Ou doit-elle choisir d’utiliser l’option **Ne pas transférer** ? Ces deux possibilités ont pour résultat d’empêcher les destinataires de transférer l’e-mail. 

- Si elle applique le modèle, les destinataires peuvent quand même partager les informations avec d’autres utilisateurs du service Marketing. Par exemple, un destinataire pourrait utiliser l’Explorateur pour glisser-déplacer l’e-mail vers un emplacement partagé ou un lecteur USB. Ainsi, toute personne du service Marketing (dont le propriétaire de l’e-mail) qui a accès à cet emplacement peut afficher les informations contenues dans l’e-mail.
 
- Si elle applique l’option **Ne pas transférer**, les destinataires ne pourront pas partager les informations avec d’autres personnes du service Marketing en déplaçant l’e-mail vers un autre emplacement. Dans ce scénario, seuls les destinataires d’origine (et le propriétaire du message) sont en mesure d’afficher les informations contenues dans l’e-mail.

> [!NOTE] 
> Utilisez l’option **Ne pas transférer** quand il est important que seuls les destinataires choisis par l’expéditeur puissent consulter les informations contenues dans l’e-mail. Utilisez un modèle pour les e-mails afin de restreindre les droits à un groupe de personnes que l’administrateur spécifie à l’avance, indépendamment des destinataires choisis de l’expéditeur.

## <a name="encrypt-only-option-for-emails"></a>Option Chiffrement seul pour les e-mails

Quand Exchange Online utilise les nouvelles fonctionnalités de chiffrement des messages Office 365, une nouvelle option d’e-mail est disponible : **Chiffrement seul**.

Cette option est en cours de déploiement pour les locataires qui utilisent Exchange Online, réservée à la base à Outlook sur le web et comme nouvelle option de protection des droits pour une règle de transport. Pour plus d’informations, consultez le billet de blog suivant de l’équipe Office : [Encrypt only rolling out in Office 365 Message Encryption](https://aka.ms/omefeb2018).

Lorsque cette option est sélectionnée, l’e-mail est chiffré et les destinataires doivent être authentifiés. Ensuite, les destinataires ont tous les droits d’utilisation, à l’exception de Contrôle total. Cette combinaison de droits d’utilisation signifie que les destinataires n’ont aucune restriction, mis à part qu’ils ne peuvent pas supprimer la protection. Par exemple, un destinataire peut copier, imprimer et transférer l’e-mail. De même, tout document Office qui est joint et automatiquement protégé peut être enregistré, copié et imprimé.

## <a name="rights-management-issuer-and-rights-management-owner"></a>Émetteur Rights Management et propriétaire Rights Management

Quand un document ou un e-mail est protégé à l’aide du service Azure Rights Management, le compte qui protège ce contenu devient automatiquement l’émetteur Rights Management pour ce contenu. Ce compte est enregistré sous la désignation **issuer** dans les [journaux d’utilisation](log-analyze-usage.md#how-to-interpret-your-azure-rights-management-usage-logs). 

L’émetteur Rights Management a toujours le droit d’utilisation Contrôle total pour le document ou l’e-mail, plus les droits suivants :

- Si les paramètres de protection incluent une date d’expiration, l’émetteur Rights Management garde le droit d’ouvrir et de modifier le document ou l’e-mail après cette date.

- L’émetteur Rights Management garde le droit d’accéder au document ou à l’e-mail en mode hors connexion.

- L’émetteur Rights Management garde le droit d’ouvrir un document ayant été révoqué. 

Par défaut, ce compte est également le **propriétaire Rights Management** de ce contenu, ce qui est le cas quand le créateur du document ou de l’e-mail démarre la protection. Dans certains scénarios, un administrateur ou un service peut protéger du contenu pour le compte d’utilisateurs. Par exemple :

- Un administrateur protège les fichiers en bloc sur un partage de fichiers : le compte Administrateur dans Azure AD protège les documents des utilisateurs.

- Le connecteur Rights Management protège les documents Office dans un dossier Windows Server : le compte du principal du service qui est créé dans Azure AD pour le connecteur RMS protège les documents des utilisateurs.

Dans ces scénarios, l’émetteur Rights Management peut attribuer la propriété Rights Management à un autre compte à l’aide des kits SDK Azure Information Protection ou de PowerShell. Par exemple, si vous utilisez l’applet de commande PowerShell [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) avec le client Azure Information Protection, vous pouvez définir le paramètre **OwnerEmail** pour attribuer la propriété Rights Management à un autre compte. 

Quand l’émetteur Rights Management protège du contenu pour le compte d’utilisateurs, l’attribution de la propriété Rights Management permet de garantir que le propriétaire du document ou de l’e-mail d’origine a le même niveau de contrôle sur son contenu protégé que s’il avait démarré lui-même la protection. 

Par exemple, un utilisateur peut imprimer un document qu’il a créé, même si ce document est maintenant protégé avec un modèle qui n’inclut pas le droit d’utilisation Imprimer. Ce même utilisateur garde l’accès à son document, indépendamment du paramètre d’accès hors connexion ou de la date d’expiration qui ont éventuellement été configurés dans ce modèle. De plus, le propriétaire Rights Management ayant le droit d’utilisation Contrôle total, cet utilisateur peut également reprotéger le document pour accorder l’accès à des utilisateurs supplémentaires (l’utilisateur devient alors l’émetteur Rights Management ainsi que le propriétaire Rights Management). Cet utilisateur peut même supprimer la protection. En revanche, seul l’émetteur Rights Management peut suivre et révoquer un document.

Le propriétaire Rights Management d’un document ou d’un e-mail est enregistré sous la désignation **owner-email** dans les [journaux d’utilisation](log-analyze-usage.md#how-to-interpret-your-azure-rights-management-usage-logs).

Notez que le propriétaire Rights Management est indépendant du propriétaire du système de fichiers Windows. Les deux propriétaires sont souvent les mêmes, mais ils peuvent être différents, même si vous n’utilisez pas les kits SDK ou PowerShell.

## <a name="rights-management-use-license"></a>Licence d’utilisation Rights Management

Quand un utilisateur ouvre un document ou un e-mail protégé par Azure Rights Management, une licence d’utilisation Rights Management est accordée à l’utilisateur pour ce contenu. Cette licence d’utilisation est un certificat qui contient les droits d’utilisation de l’utilisateur pour le document ou l’e-mail, ainsi que la clé de chiffrement utilisée pour chifrer le contenu. La licence d’utilisation contient également une date d’expiration, si celle-ci a été définie, et une durée de validité.

Pendant la durée de la licence d’utilisation, l’utilisateur n’est ni réauthentifié ni réautorisé. Il peut ainsi continuer à ouvrir le document ou l’e-mail protégé sans connexion Internet. Au terme de la période de validité de la licence d’utilisation, l’utilisateur doit être réauthentifié et réautorisé s’il souhaite accéder au document ou à l’e-mail protégé. 

Quand les documents et les e-mails sont protégés à l’aide d’une étiquette ou d’un modèle définissant les paramètres de protection, vous pouvez changer ces paramètres dans votre étiquette ou votre modèle sans avoir à reprotéger le contenu. Si l’utilisateur a déjà accédé au contenu, les changements prennent effet après l’expiration de sa licence d’utilisation. Cependant, quand des utilisateurs appliquent des autorisations personnalisées (ou « stratégie de droits ad hoc ») et que ces autorisations doivent être changées après la protection du document ou de l’e-mail, ce contenu doit être reprotégé avec les nouvelles autorisations. Les autorisations personnalisées pour un e-mail sont implémentées avec l’option Ne pas transférer.

Pour un locataire, la période de validité par défaut de la licence est de 30 jours. Vous pouvez configurer cette valeur à l’aide de l’applet de commande PowerShell [Set-AadrmMaxUseLicenseValidityTime](/powershell/module/aadrm/set-aadrmmaxuselicensevaliditytime). Vous pouvez configurer un paramètre plus restrictif quand la protection est appliquée à l’aide d’une étiquette ou d’un modèle :

- Quand vous configurez une étiquette ou un modèle dans le portail Azure, la période de validité de la licence d’utilisation est définie avec la valeur du paramètre **Autoriser l’accès hors connexion**. 
    
    Pour plus d’informations et de conseils sur la configuration de ce paramètre dans le portail Azure, consultez le tableau à l’étape 9 du [Guide pratique pour configurer une étiquette pour la protection Rights Management](configure-policy-protection.md).

- Quand vous configurez un modèle à l’aide de PowerShell, la période de validité de la licence d’utilisation est définie avec la valeur du paramètre *LicenseValidityDuration* dans les applets de commande [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty) et [Add-AadrmTemplate](/powershell/module/aadrm/add-aadrmtemplate).
    
    Pour plus d’informations et de conseils sur la configuration de ce paramètre à l’aide de PowerShell, consultez l’aide de chaque applet de commande.


## <a name="see-also"></a>Voir aussi
[Configuration et gestion des modèles pour Azure Information Protection](configure-policy-templates.md)

[Configuration de super utilisateurs pour Azure Rights Management et les services de découverte ou la récupération de données](configure-super-users.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

