---
title: "Configurer les droits d’utilisation pour Azure Rights Management - AIP"
description: "Comprendre et identifier les droits spécifiques utilisés lorsque vous protégez des fichiers ou des e-mails avec le service Azure Rights Management à partir de Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/29/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 97ddde38-b91b-42a5-8eb4-3ce6ce15393d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: ceada043abfa1bee18c6407b3804815d95e89453
ms.sourcegitcommit: 972acdb468ac32a28e3e24c90694aff4b75206fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/29/2018
---
# <a name="configuring-usage-rights-for-azure-rights-management"></a>Configuration des droits d’utilisation pour Azure Rights Management

>*S’applique à : Azure Information Protection, Office 365*

Lorsque vous définissez une protection sur des fichiers ou des e-mails en utilisant le service Azure Rights Management à partir de Azure Information Protection et que vous n’utilisez pas de modèle, vous devez configurer vous-même les droits d’utilisation. De plus, lorsque vous configurez des modèles ou des étiquettes pour la protection de Azure Rights Management, vous sélectionnez les droits d’utilisation qui seront appliqués automatiquement une fois le modèle ou l’étiquette sélectionné par des utilisateurs, des administrateurs ou des services configurés. Par exemple, dans le portail Azure, vous pouvez sélectionner des rôles qui configurent un regroupement logique de droits d’utilisation, ou bien vous pouvez configurer les droits individuels.

Utilisez cet article pour vous aider à configurer les droits d’utilisation souhaités pour l’application que vous utilisez et pour comprendre comment ces droits sont interprétés par les applications.

> [!NOTE] 
> Par souci d’exhaustivité, cet article contient des valeurs tirées du portail Azure Classic, qui n’est plus en service depuis le 8 janvier 2018.
>
> Pour vous aider à migrer vers le nouveau portail, consultez l’article [Les tâches que vous faisiez avec le portail Azure Classic](migrate-portal.md).

## <a name="usage-rights-and-descriptions"></a>Droits d’utilisation et descriptions
Le tableau suivant répertorie et décrit les droits d’utilisation pris en charge par Rights Management, ainsi que la façon dont ils sont utilisés et interprétés. Ils sont répertoriés par leur **nom commun**, généralement la façon dont ils sont affichés ou référencés, sous une forme plus conviviale que la valeur uniterme utilisée dans le code (la valeur **Encodage dans la stratégie**). 

La **constante ou valeur API** est le nom du SDK pour un appel d’API MSIPC, utilisé quand vous écrivez une application compatible avec RMS qui vérifie un droit d’utilisation, ou en ajoute un à une stratégie.


|Droits d’utilisation|Description|Implémentation|
|-------------------------------|---------------------------|-----------------|
|Nom commun : **Modifier le contenu, Modifier** <br /><br />Encodage dans la stratégie : **DOCEDIT**|Permet à l’utilisateur de modifier, réorganiser, mettre en forme ou filtrer le contenu à l’intérieur de l’application. Il n’accorde pas le droit d’enregistrer la copie modifiée.|Droits personnalisés Office : dans le cadre des options **Modifier** et **Contrôle total**. <br /><br />Nom dans le portail Azure Classic : **Modifier le contenu**<br /><br />Nom dans le portail Azure : **Modifier le contenu, Modifier (DOCEDIT)**<br /><br />Nom dans les modèles AD RMS : **Modifier** <br /><br />Constante ou valeur API : non applicable.|
|Nom commun : **Enregistrer** <br /><br />Encodage dans la stratégie : **EDIT**|Permet à l’utilisateur d’enregistrer le document à son emplacement actuel.<br /><br />Dans les applications Office, ce droit permet également à l’utilisateur de modifier le document.|Droits personnalisés Office : dans le cadre des options **Modifier** et **Contrôle total**. <br /><br />Nom dans le portail Azure Classic : **Enregistrer le fichier**<br /><br />Nom dans le portail Azure : **Enregistrer (EDIT)**<br /><br />Nom dans les modèles AD RMS : **Enregistrer** <br /><br />Constante ou valeur API :`IPC_GENERIC_WRITE L"EDIT"`|
|Nom commun : **Commentaire** <br /><br />Encodage dans la stratégie : **COMMENT**|Active l’option d’ajout d’annotations ou de commentaires au contenu.<br /><br />Ce droit est disponible dans le SDK, il est disponible en tant que stratégie ad hoc dans les modules AzureInformationProtection et Protection RMS pour Windows PowerShell et il a été implémenté dans certaines applications d’éditeurs de logiciels. Toutefois, il n’est pas largement utilisé et il n’est actuellement pas pris en charge par les applications Office.|Droits personnalisés Office : non implémenté. <br /><br />Nom dans le portail Azure Classic : non implémenté.<br /><br />Nom dans le portail Azure : non implémenté.<br /><br />Nom dans les modèles AD RMS : non implémenté. <br /><br />Constante ou valeur API :`IPC_GENERIC_COMMENT L"COMMENT`|
|Nom commun : **Enregistrer sous, Exporter** <br /><br />Encodage dans la stratégie : **EXPORT**|Active l’option d’enregistrement du contenu sous un autre nom de fichier (Enregistrer sous). Pour les documents Office et le client Azure Information Protection, le fichier peut être enregistré sans protection.<br /><br />Ce droit permet également à l’utilisateur d’utiliser d’autres options d’exportation dans les applications, telles que **Envoyer à OneNote**.<br /><br /> Remarque : Si ce droit n’est pas accordé, les applications Office permettent à un utilisateur d’enregistrer un document sur un nouveau nom si le format du fichier sélectionné nativement prend en charge la protection de Rights Management.|Droits personnalisés Office : dans le cadre des options **Modifier** et **Contrôle total**. <br /><br />Nom dans le portail Azure Classic : **Exporter le contenu (Enregistrer sous)** <br /><br />Nom dans le portail Azure : **Enregistrer sous, Exporter (EXPORT)**<br /><br />Nom dans les modèles AD RMS : **Exporter (Enregistrer sous)** <br /><br />Constante ou valeur API :`IPC_GENERIC_EXPORT L"EXPORT"`|
|Nom commun : **Transférer** <br /><br />Encodage dans la stratégie : **FORWARD**|Active l’option permettant de transférer un e-mail et d’ajouter des destinataires aux lignes **À** et **CC**. Ce droit ne s’applique pas aux documents, uniquement aux e-mails.<br /><br />Il n’autorise pas le redirecteur à accorder des droits à d’autres utilisateurs dans le cadre du transfert. <br /><br />Lorsque vous accordez ce droit, accordez également le droit **Modifier le contenu, Modifier** (nom commun) pour vous assurer que l’e-mail d’origine fasse partie de l’e-mail transféré et non pas sous la forme d’une pièce jointe. Ce droit est également requis lorsque vous envoyez un e-mail à une autre organisation utilisant le client ou l’application web Outlook. Ou, pour les utilisateurs de votre organisation exempts de l’utilisation du service Azure Rights Management après l’implémentation des [contrôles d’intégration](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy).|Droits personnalisés Office : refusé lorsque vous utilisez la stratégie standard **Ne pas transférer**.<br /><br />Nom dans le portail Azure Classic : **Transférer**<br /><br />Nom dans le portail Azure : **Transférer (FORWARD)**<br /><br />Nom dans les modèles AD RMS : **Transférer** <br /><br />Constante ou valeur API :`IPC_EMAIL_FORWARD L"FORWARD"`|
|Nom commun : **Contrôle total** <br /><br />Encodage dans la stratégie : **OWNER**|Accorde tous les droits au document, toutes les actions disponibles peuvent être effectuées.<br /><br />Inclut la possibilité de supprimer la protection et de reprotéger un document. <br /><br />Notez que ce droit d’utilisation n’est pas le même que le [propriétaire Rights Management](#rights-management-issuer-and-rights-management-owner).|Droits personnalisés Office : comme l’option personnalisée **Contrôle total**.<br /><br />Nom dans le portail Azure Classic : **Contrôle total**<br /><br />Nom dans le portail Azure : **Contrôle total (OWNER)**<br /><br />Nom dans les modèles AD RMS : **Contrôle total** <br /><br />Constante ou valeur API :`IPC_GENERIC_ALL L"OWNER"`|
|Nom commun : **Imprimer** <br /><br />Encodage dans la stratégie : **PRINT**|Active les options d’impression du contenu.|Droits personnalisés Office : comme l’option **imprimer le contenu** dans les autorisations personnalisées. Ce n’est pas un paramètre par destinataire.<br /><br />Nom dans le portail Azure Classic : **Imprimer**<br /><br />Nom dans le portail Azure : **Imprimer (PRINT)**<br /><br />Nom dans les modèles AD RMS : **Imprimer** <br /><br />Constante ou valeur API :`IPC_GENERIC_PRINT L"PRINT"`|
|Nom commun : **Répondre** <br /><br />Encodage dans la stratégie : **REPLY**|Active l’option **Répondre** dans un client de messagerie, sans autoriser la modification des lignes **À** ou **CC**.<br /><br />Lorsque vous accordez ce droit, accordez également le droit **Modifier le contenu, Modifier** (nom commun) pour vous assurer que l’e-mail d’origine fasse partie de l’e-mail transféré et non pas sous la forme d’une pièce jointe. Ce droit est également requis lorsque vous envoyez un e-mail à une autre organisation utilisant le client ou l’application web Outlook. Ou, pour les utilisateurs de votre organisation exempts de l’utilisation du service Azure Rights Management après l’implémentation des [contrôles d’intégration](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy).|Droits personnalisés Office : non applicable.<br /><br />Nom dans le portail Azure Classic : **Répondre**<br /><br />Nom dans le portail Azure Classic : **Répondre (REPLY)**<br /><br />Nom dans les modèles AD RMS : **Répondre** <br /><br />Constante ou valeur API :`IPC_EMAIL_REPLY`|
|Nom commun : **Répondre à tous** <br /><br />Encodage dans la stratégie : **REPLYALL**|Active l’option **Répondre à tous** dans un client de messagerie, sans autoriser l’ajout de destinataires aux lignes **À** ou **CC**.<br /><br />Lorsque vous accordez ce droit, accordez également le droit **Modifier le contenu, Modifier** (nom commun) pour vous assurer que l’e-mail d’origine fasse partie de l’e-mail transféré et non pas sous la forme d’une pièce jointe. Ce droit est également requis lorsque vous envoyez un e-mail à une autre organisation utilisant le client ou l’application web Outlook. Ou, pour les utilisateurs de votre organisation exempts de l’utilisation du service Azure Rights Management après l’implémentation des [contrôles d’intégration](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy).|Droits personnalisés Office : non applicable.<br /><br />Nom dans le portail Azure Classic : **Répondre à tous**<br /><br />Nom dans le portail Azure : **Répondre à tous (REPLY ALL)**<br /><br />Nom dans les modèles AD RMS : **Répondre à tous** <br /><br />Constante ou valeur API :`IPC_EMAIL_REPLYALL L"REPLYALL"`|
|Nom commun : **Afficher, Ouvrir, Lire** <br /><br />Encodage dans la stratégie : **VIEW**|Permet à l’utilisateur d’ouvrir le document et de voir son contenu.|Droits personnalisés Office : comme la stratégie personnalisée **Lire**, l’option **Afficher**.<br /><br />Nom dans le portail Azure Classic : **Afficher**<br /><br />Nom dans le portail Azure : **Afficher, Ouvrir, Lire (VIEW)**<br /><br />Nom dans les modèles AD RMS : **Répondre à tous** <br /><br />Constante ou valeur API :`IPC_GENERIC_READ L"VIEW"`|
|Nom commun : **Copier** <br /><br />Encodage dans la stratégie : **EXTRACT**|Active les options permettant de copier des données (y compris des captures d’écran) à partir du document dans ce même document ou dans un autre.<br /><br />Dans certaines applications, il permet également d’enregistrer le document entier dans un format non protégé.|Droits personnalisés Office: comme l’option de stratégie personnalisée **Autoriser les utilisateurs disposant de l’accès en lecture à copier le contenu**.<br /><br />Nom dans le portail Azure Classic : **Copier et extraire le contenu**<br /><br />Nom dans le portail Azure : **Copier (EXTRACT)**<br /><br />Nom dans les modèles AD RMS : **Extraire** <br /><br />Constante ou valeur API :`IPC_GENERIC_EXTRACT L"EXTRACT"`|
|Nom commun : **Afficher les droits** <br /><br />Encodage dans la stratégie : **VIEWRIGHTSDATA**|Permet à l’utilisateur d’afficher la stratégie appliquée au document.|Droits personnalisés Office : non implémenté.<br /><br />Nom dans le portail Azure Classic : **Afficher les droits affectés**<br /><br />Nom dans le portail Azure : **Afficher les droits (VIEWRIGHTSDATA)**.<br /><br />Nom dans les modèles AD RMS : **Afficher les droits** <br /><br />Constante ou valeur API :`IPC_READ_RIGHTS L"VIEWRIGHTSDATA"`|
|Nom commun : **Modifier les droits** <br /><br />Encodage dans la stratégie : **EDITRIGHTSDATA**|Permet à l’utilisateur de modifier la stratégie appliquée au document. Cela inclut notamment la suppression de la protection.|Droits personnalisés Office : non implémenté.<br /><br />Nom dans le portail Azure Classic : **Modifier les droits**<br /><br />Nom dans le portail Azure : **Modifier les droits (EDITRIGHTSDATA)**.<br /><br />Nom dans les modèles AD RMS : **Modifier les droits** <br /><br />Constante ou valeur API :`PC_WRITE_RIGHTS L"EDITRIGHTSDATA"`|
|Nom commun : **Autoriser les macros** <br /><br />Encodage dans la stratégie : **OBJMODEL**|Active l’option pour exécuter des macros ou effectuer d’autres accès à distance ou par programme au contenu d’un document.|Droits personnalisés Office : comme l’option de stratégie personnalisée **Autoriser l’accès par programme**. Ce n’est pas un paramètre par destinataire.<br /><br />Nom dans le portail Azure Classic : **Autoriser les macros**<br /><br />Nom dans le portail Azure : **Autoriser les macros (OBJMODEL)**<br /><br />Nom dans les modèles AD RMS : **Autoriser les macros** <br /><br />Constante ou valeur API : non implémenté.|

## <a name="rights-included-in-permissions-levels"></a>Droits inclus dans les niveaux d’autorisation

Certaines applications regroupent les droits d’utilisation dans des niveaux d’autorisation afin de faciliter la sélection de droits d’utilisation généralement utilisés ensemble. Ces niveaux d’autorisation permettent d’abstraire un niveau de complexité aux utilisateurs, pour qu’ils puissent choisir des options basées sur le rôle.  Par exemple, **Réviseur** et **Coauteur**. Bien que ces options montrent souvent un récapitulatif des droits aux utilisateurs, ils ne peuvent pas inclure tous les droits répertoriés dans le tableau précédent.

Utilisez le tableau suivant pour disposer d’une liste de ces niveaux d’autorisation et la liste complète des droits d’utilisation qu’ils contiennent. Les droits d’utilisation sont répertoriés par leur [nom commun](#usage-rights-and-descriptions).

|Niveau d’autorisation|Applications|Droits d’utilisation inclus|
|---------------------|----------------|---------------------------------|
|Visionneuse|Portail Azure Classic <br /><br />portail Azure<br /><br /> Applications de partage Rights Management pour Windows<br /><br />Client Azure Information Protection pour Windows|Afficher, Ouvrir, Lire ; Afficher les droits ; Répondre [[1]](#footnote-1); Répondre à tous [[1]](#footnote-1); Autoriser les Macros [[2]](#footnote-2)<br /><br />Remarque : Pour les e-mails, utilisez Réviseur plutôt que ce niveau d’autorisation pour vous assurer qu’une réponse à l’e-mail est reçue en tant qu’e-mail et non pas en tant que pièce jointe. Réviseur est également requis lorsque vous envoyez un e-mail à une autre organisation utilisant le client ou l’application web Outlook. Ou, pour les utilisateurs de votre organisation exempts de l’utilisation du service Azure Rights Management après l’implémentation des [contrôles d’intégration](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy).|
|Réviseur|Portail Azure Classic <br /><br />portail Azure<br /><br />Applications de partage Rights Management pour Windows<br /><br />Client Azure Information Protection pour Windows|Afficher, Ouvrir, Lire ; Enregistrer ; Modifier le contenu, Modifier ; Afficher les droits ; Répondre ; Répondre à tous [[3]](#footnote-3); Transférer [[3]](#footnote-3); Autoriser les Macros [[2]](#footnote-2)|
|Coauteur|Portail Azure Classic <br /><br />portail Azure<br /><br />Applications de partage Rights Management pour Windows<br /><br />Client Azure Information Protection pour Windows|Afficher, Ouvrir, Lire ; Enregistrer ; Modifier le contenu, Modifier ; Copier ; Afficher les droits ; Autoriser les Macros ; Enregistrer sous, Exporter [[4]](#footnote-4); Imprimer ; Répondre [[3]](#footnote-3); Répondre à tous [[3]](#footnote-3); Transférer [[3]](#footnote-3)|
|Copropriétaire|Portail Azure Classic <br /><br />portail Azure<br /><br />Applications de partage Rights Management pour Windows<br /><br />Client Azure Information Protection pour Windows|Afficher, Ouvrir, Lire ; Enregistrer ; Modifier le contenu, Modifier ; Copier ; Afficher les droits ; Modifier les droits ; Autoriser les Macros ; Enregistrer sous, Exporter ; Imprimer ; Répondre [[3]](#footnote-3); Répondre à tous [[3]](#footnote-3); Transférer [[3]](#footnote-3) ; Contrôle total|

----

###### <a name="footnote-1"></a>Note 1

Pas inclus dans le portail Azure.

###### <a name="footnote-2"></a>Note 2

Pour le client Azure Information Protection pour Windows, ce droit est actuellement requis pour la barre Information Protection dans les applications Office.

###### <a name="footnote-3"></a>Note 3
Non applicable pour le client Azure Information Protection pour Windows ou l’application de partage Rights Management pour Windows.

###### <a name="footnote-4"></a>Note 4
Pas inclus dans le portail Azure ou le client Azure Information Protection pour Windows.

## <a name="rights-included-in-the-default-templates"></a>Droits inclus dans les modèles par défaut
Le tableau suivant répertorie les droits d’utilisation inclus lorsque les modèles par défaut sont créés. Les droits d’utilisation sont répertoriés par leur [nom commun](#usage-rights-and-descriptions).

Ces modèles par défaut sont créés lorsque votre abonnement a été acheté, et les noms et droits d’utilisation peuvent être [modifiés](configure-policy-templates.md) dans le portail Azure. 

|Nom complet du modèle|Droits d’utilisation du 6 octobre 2017 à maintenant|Droits d’utilisation avant le 6 octobre 2017|
|----------------|--------------------|----------|
|\<*nom de l’organisation > - Affichage confidentiel uniquement* <br /><br />ou Gestionnaire de configuration<br /><br /> *Hautement confidentiel \ Tous les employés*|Afficher, Ouvrir, Lire ; Copier ; Afficher les droits ; Autoriser les Macros ; Imprimer ; Transférer ; Répondre ; Répondre à tous ; Enregistrer ; Modifier le contenu, Modifier|Afficher, Ouvrir, Lire|
|\<*nom de l’organisation > - Confidentiel* <br /><br />ou Gestionnaire de configuration <br /><br />*Confidentiel \ Tous les employés*|Afficher, Ouvrir, Lire ; Enregistrer sous, Exporter ; Copier ; Afficher les droits ; Modifier les droits ; Autoriser les Macros ; Imprimer ; Transférer ; Répondre ; Répondre à tous ; Enregistrer ; Modifier le contenu, Modifier ; Contrôle total|Afficher, Ouvrir, Lire ; Enregistrer sous, Exporter ; Modifier le contenu, Modifier ; Afficher les droits ; Autoriser les Macros ; Transférer ; Répondre ; Répondre à tous|

## <a name="do-not-forward-option-for-emails"></a>Option Ne pas transférer pour les e-mails

Les clients et services Exchange (par exemple, le client Outlook, l’application Outlook Web Access et les règles de transport Exchange) ont une option supplémentaire de protection des droits des informations pour les e-mails : **Ne pas transférer**. 

Même si cette option apparaît aux utilisateurs (et aux administrateurs Exchange) comme un modèle par défaut de Rights Management qu’ils peuvent sélectionner, **Ne pas transférer** n’est pas un modèle. Cela explique pourquoi vous ne la voyez pas dans le portail Azure lorsque vous affichez et gérez des modèles pour Azure Rights Management. Au lieu de cela, l’option **Ne pas transférer** est un ensemble de droits appliqués dynamiquement par les utilisateurs à leurs destinataires.

Lorsque l’option **Ne pas transférer** est appliquée à un e-mail, les destinataires ne peuvent pas le transférer, l’imprimer, faire une copie à partir de celui-ci, enregistrer des pièces jointes ou l’enregistrer sous un autre nom. Par exemple, dans le client Outlook, le bouton Transférer n’est pas disponible, les options de menu **Enregistrer sous**, **Enregistrer les pièces jointes**, et **Imprimer** ne sont pas disponibles, et vous ne pouvez pas ajouter ou modifier les destinataires dans le lignes **À**, **CC** ou **CCi**.

Il existe une distinction importante entre l’application de l’option **Ne pas transférer** et l’application d’un modèle qui n’accorde pas le droit de transfert à un e-mail : l’option **Ne pas transférer** utilise une liste dynamique d’utilisateurs autorisés basée sur les destinataires choisis par l’utilisateur de l’e-mail d’origine, tandis que les droits du modèle ont une liste statique d’utilisateurs autorisés, précédemment définie par l’administrateur. Quelle est la différence ? Prenons un exemple : 

Un utilisateur souhaite envoyer un e-mail à des personnes spécifiques du service marketing, contenant certaines informations à ne pas partager. Doit-il protéger l’e-mail avec un modèle restreignant les droits (affichage, réponse et enregistrement) au service marketing ?  Ou bien doit-il choisir l’option **Ne pas transférer** ? Les deux choix se traduiraient par le fait que les destinataires ne pourraient pas transférer l’e-mail. 

- S’il applique le modèle, les destinataires peuvent toujours partager les informations avec d’autres personnes du service marketing. Par exemple, un destinataire peut utiliser l’explorateur pour glisser et déposer l’e-mail vers un emplacement partagé ou un lecteur USB. Ainsi, toute personne du service marketing (et le propriétaire de l’e-mail) ayant accès à cet emplacement peut afficher les informations contenues dans l’e-mail.
 
- S’il applique l’option **Ne pas transférer**, les destinataires ne pourront pas partager les informations avec d’autres personnes du service marketing en déplaçant l’e-mail vers un autre emplacement. Dans ce scénario, seuls les destinataires d’origine (et le propriétaire de l’e-mail) seront en mesure d’afficher les informations contenues dans l’e-mail.

> [!NOTE] 
> Utilisez l’option **Ne pas transférer** quand il est important que seuls les destinataires choisis par l’expéditeur puissent consulter les informations contenues dans l’e-mail. Utilisez un modèle pour les e-mails afin de restreindre les droits à un groupe de personnes spécifié à l’avance par l’administrateur, indépendamment des destinataires choisis par l’expéditeur.

## <a name="rights-management-issuer-and-rights-management-owner"></a>L’émetteur Rights Management et le propriétaire Rights Management

Quand un document ou un e-mail est protégé à l’aide du service Azure Rights Management, le compte qui protège ce contenu devient automatiquement l’émetteur Rights Management pour ce contenu. Ce compte est enregistré avec le champ **issuer** dans les [journaux d’utilisation](log-analyze-usage.md#how-to-interpret-your-azure-rights-management-usage-logs). 

L’émetteur Rights Management se voit toujours accorder le droit d’utilisation Contrôle total pour le document ou l’e-mail, et en outre :

- Si les paramètres de protection incluent une date d’expiration, l’émetteur Rights Management peut toujours ouvrir et modifier le document ou l’e-mail après cette date.

- L’émetteur Rights Management peut toujours accéder au document ou à l’e-mail en mode hors connexion.

- L’émetteur Rights Management peut toujours ouvrir un document une fois qu’il est révoqué. 

Par défaut, ce compte est également le **propriétaire Rights Management** pour ce contenu, qui est le cas lorsqu’un utilisateur qui a créé le document ou l’e-mail instaure la protection. Mais il existe certains scénarios où un administrateur ou un service peut protéger du contenu pour le compte d’utilisateurs. Exemple :

- Un administrateur protège en bloc des fichiers sur un partage de fichiers : le compte d’administrateur dans Azure AD protège les documents pour les utilisateurs.

- Le connecteur Rights Management protège les documents Office dans un dossier de Windows Server : le compte de principal du service dans Azure AD qui est créé pour le connecteur RMS protège les documents pour les utilisateurs.

Dans ces scénarios, l’émetteur Rights Management peut affecter le propriétaire Rights Management à un autre compte à l’aide de kits de développement logiciel Azure Information Protection ou PowerShell. Par exemple, lorsque vous utilisez l’applet de commande Powershell [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) avec le client Azure Information Protection, vous pouvez spécifier le paramètre **OwnerEmail** afin d’affecter le propriétaire Rights Management à un autre compte. 

Lorsque l’émetteur Rights Management protège pour des utilisateurs, l’affectation du propriétaire Rights Management garantit que le propriétaire du document ou de l’e-mail d’origine a le même niveau de contrôle pour leur contenu protégé que s’ils avaient instauré la protection eux-mêmes. 

Par exemple, l’utilisateur qui a créé le document peut l’imprimer, même s’il est désormais protégé avec un modèle n’incluant pas le droit d’utilisation Imprimer. Le même utilisateur peut toujours accéder à son document, quel que soit le paramètre d’accès hors connexion ou la date d’expiration configuré dans ce modèle. En outre, étant donné que le propriétaire Rights Management possède le droit d’utilisation Contrôle total, cet utilisateur peut également protéger de nouveau le document pour autoriser l’accès à d’autres utilisateurs (l’utilisateur devient alors l’émetteur Rights Management ainsi que le propriétaire Rights Management), et cet utilisateur peut même supprimer la protection. Toutefois, seulement l’émetteur Rights Management peut suivre et révoquer un document.

Le propriétaire Rights Management pour un document ou un e-mail est enregistré avec le champ **owner-email** dans les [journaux d’utilisation](log-analyze-usage.md#how-to-interpret-your-azure-rights-management-usage-logs).

Notez que le propriétaire Rights Management est indépendant du propriétaire du système de fichiers Windows. Ce sont souvent les mêmes, mais ils peuvent être différents, même si vous n’utilisez pas les kits de développement logiciel ou PowerShell.

## <a name="rights-management-use-license"></a>Licence d’utilisation de Rights Management

Lorsqu’un utilisateur ouvre un document ou un e-mail protégé par Azure Rights Management, une licence d’utilisation de Rights Management pour ce contenu est accordée à l’utilisateur. Cette licence d’utilisation est un certificat contenant les droits d’utilisation de l’utilisateur pour le document ou l’e-mail ainsi que la clé de chiffrement utilisée pour chiffrer le contenu. La licence d’utilisation peut également contenir une date d’expiration, ainsi qu’une durée de validité.

Pendant la durée de la licence d’utilisation, l’utilisateur n’est pas de nouveau authentifié ou autorisé. Cela permet à l’utilisateur d’ouvrir le document ou l’e-mail protégé sans avoir besoin d’une connexion internet. Lorsque la période de validité de la licence d’utilisation a expiré, l’utilisateur devra de nouveau s’authentifier et recevoir une autorisation la prochaine fois qu’il accèdera au document ou à l’e-mail protégé. 

Lorsque les documents et e-mails sont protégés à l’aide d’une étiquette ou d’un modèle qui définit les paramètres de protection, vous pouvez modifier ces paramètres dans votre modèle ou votre étiquette sans avoir besoin de protéger de nouveau le contenu. Si un utilisateur a déjà accédé au contenu, les changements prennent effet une fois que sa licence d’utilisation est arrivée à expiration. Toutefois, lorsque des utilisateurs appliquent des autorisations personnalisées (également connues sous le nom de stratégie de droits ad-hoc) et que ces autorisations doivent être modifiées après la protection du document ou de l’e-mail, le contenu doit être de nouveau protégé avec les nouvelles autorisations. Des autorisations personnalisées pour un e-mail sont implémentées avec l’option Ne pas transférer.

La période de validité par défaut de la licence d’utilisation pour un client est de 30 jours et vous pouvez configurer cette valeur à l’aide de l’applet de commande PowerShell [Set-AadrmMaxUseLicenseValidityTime](/powershell/module/aadrm/set-aadrmmaxuselicensevaliditytime). Vous pouvez configurer un paramètre plus restrictif lorsque la protection est appliquée à l’aide d’une étiquette ou d’un modèle :

- Lorsque vous configurez une étiquette ou un modèle dans le portail Azure, la période de validité de la licence d’utilisation prend sa valeur à partir du paramètre **Autoriser l’accès hors connexion**. 
    
    Pour plus d’informations et de conseils pour la configuration de ce paramètre dans le portail Azure, consultez le tableau à l’étape 9 de l’article [Comment configurer une étiquette pour la protection de Rights Management](configure-policy-protection.md).

- Lorsque vous configurez un modèle à l’aide de PowerShell, la période de validité de la licence d’utilisation prend sa valeur à partir du paramètre *LicenseValidityDuration* dans les applets de commande [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty) et [Add-AadrmTemplate](/powershell/module/aadrm/add-aadrmtemplate).
    
    Pour plus d’informations et de conseils pour la configuration de ce paramètre à l’aide de PowerShell, consultez l’aide relative à chaque applet de commande.


## <a name="see-also"></a> Voir aussi
[Configuration et gestion des modèles pour Azure Information Protection](configure-policy-templates.md)

[Configuration de super utilisateurs pour Azure Rights Management et les services de découverte ou la récupération de données](configure-super-users.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

