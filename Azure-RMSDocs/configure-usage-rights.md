---
title: Configurer les droits d’utilisation pour Azure Information Protection
description: Comprenez et identifiez les droits spécifiques qui sont utilisés quand vous protégez des fichiers ou des e-mails à l’aide de la protection Rights Management de Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/04/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 97ddde38-b91b-42a5-8eb4-3ce6ce15393d
ms.reviewer: esaggese
ms.subservice: azurerms
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 39fedde68cfe771d29e9fda1be4a9f2883cf1ede
ms.sourcegitcommit: 78c7ab80be7c292ea4bc62954a4e29c449e97439
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/13/2021
ms.locfileid: "98164247"
---
# <a name="configuring-usage-rights-for-azure-information-protection"></a>Configuration des droits d’utilisation pour Azure Information Protection

>***S’applique à** : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Concerne** : [Client d’étiquetage unifié AIP et client classique](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Pour fournir une expérience client unifiée et homogène, le **client classique Azure Information Protection** et la **gestion des étiquettes** dans le portail Azure seront **dépréciés** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.
> 
> Par souci d’exhaustivité, cet article contient des valeurs tirées du portail Azure Classic, qui n’est plus en service depuis le 8 janvier 2018.

Quand vous configurez des étiquettes de sensibilité ou des modèles de protection pour le chiffrement, vous sélectionnez les droits d’utilisation qui seront ensuite appliqués automatiquement lorsque l’étiquette ou le modèle est sélectionné par des utilisateurs, des administrateurs ou des services configurés. Par exemple, dans le portail Azure, vous pouvez sélectionner des rôles qui configurent un regroupement logique de droits d’utilisation, ou bien vous pouvez configurer les droits individuels. Les utilisateurs peuvent également sélectionner et appliquer les droits d’utilisation eux-mêmes.

Utilisez cet article pour vous aider à configurer les droits d’utilisation que vous souhaitez pour l’application que vous utilisez et pour comprendre comment ces droits sont conçus pour être interprétés par les applications. Toutefois, les applications peuvent varier dans la manière dont elles implémentent les droits. par conséquent, consultez toujours leur documentation et effectuez vos propres tests avec les applications que les utilisateurs utilisent pour vérifier le comportement avant le déploiement en production.


## <a name="usage-rights-and-descriptions"></a>Droits d’utilisation et descriptions
Le tableau suivant répertorie et décrit les droits d’utilisation pris en charge par Rights Management, ainsi que la façon dont ils sont utilisés et interprétés. Ils sont répertoriés par leur **nom commun**, généralement la façon dont ils sont affichés ou référencés, sous une forme plus conviviale que la valeur uniterme utilisée dans le code (la valeur **Encodage dans la stratégie**). 

Dans ce tableau :

- La **constante ou la valeur** de l’API est le nom du kit de développement logiciel (SDK) pour un appel d’API MSIPC, utilisé lorsque vous écrivez une application qui vérifie un droit d’utilisation, ou ajoute un droit d’utilisation à une stratégie.

- Le **Centre d’administration d’étiquetage** fait référence à l’emplacement où vous configurez les étiquettes de sensibilité et peut être soit le centre de conformité Microsoft 365, le Microsoft 365 Security Center, soit le centre de conformité Microsoft 365 Security &.

    Si vous disposez du client Classic, configurez vos étiquettes et vos stratégies d’étiquette dans la Portail Azure.


|Droits d’utilisation|Description|Implémentation|
|-------------------------------|---------------------------|-----------------|
|Nom commun : **Modifier le contenu, Modifier** <br /><br />Encodage dans la stratégie : **DOCEDIT**|Permet à l’utilisateur de modifier, réorganiser, mettre en forme ou filtrer le contenu dans l’application. Il n’accorde pas le droit d’enregistrer la copie modifiée.<br /><br />Dans Word, sauf si vous avez Office 365 ProPlus avec la version minimale [1807](/officeupdates/monthly-channel-2018#version-1807-july-25),ce droit n’est pas suffisant pour activer ou désactiver le **Suivi des modifications**, ni pour utiliser toutes les fonctionnalités de suivi des modifications en tant que réviseur. À la place, pour utiliser toutes les options de suivi des modifications, le droit suivant est requis : **Contrôle total**. |Droits personnalisés Office : dans le cadre des options **Modifier** et **Contrôle total**. <br /><br />Nom dans le portail Azure Classic : **Modifier le contenu**<br /><br />Nom dans le centre d’administration d’étiquetage et Portail Azure : **modifier le contenu, modifier (DOCEDIT)**<br /><br />Nom dans les modèles AD RMS : **Modifier** <br /><br />Constante ou valeur API : non applicable.|
|Nom commun : **Enregistrer** <br /><br />Encodage dans la stratégie : **EDIT**|Permet à l’utilisateur d’enregistrer le document à l’emplacement actuel.<br /><br />Dans les applications Office, ce droit permet également à l’utilisateur de modifier le document et de l’enregistrer sous un nouveau nom si le format de fichier sélectionné en mode natif prend en charge la protection Rights Management. La restriction de format de fichier empêche toute suppression éventuelle de la protection d’origine appliquée au fichier.|Droits personnalisés Office : dans le cadre des options **Modifier** et **Contrôle total**. <br /><br />Nom dans le portail Azure Classic : **Enregistrer le fichier**<br /><br />Nom dans le centre d’administration d’étiquetage et Portail Azure : **Enregistrer (modifier)**<br /><br />Nom dans les modèles AD RMS : **Enregistrer** <br /><br />Constante ou valeur API :`IPC_GENERIC_WRITE L"EDIT"`|
|Nom commun : **Commentaire** <br /><br />Encodage dans la stratégie : **COMMENT**|Active l’option d’ajout d’annotations ou de commentaires au contenu.<br /><br />Ce droit est disponible dans le SDK, il est disponible en tant que stratégie ad hoc dans les modules AzureInformationProtection et Protection RMS pour Windows PowerShell et il a été implémenté dans certaines applications d’éditeurs de logiciels. Toutefois, il n’est pas largement utilisé et n’est pas pris en charge par les applications Office.|Droits personnalisés Office : non implémenté. <br /><br />Nom dans le portail Azure Classic : non implémenté.<br /><br />Nom dans le centre d’administration d’étiquetage et Portail Azure : non implémenté.<br /><br />Nom dans les modèles AD RMS : non implémenté. <br /><br />Constante ou valeur API :`IPC_GENERIC_COMMENT L"COMMENT`|
|Nom commun : **Enregistrer sous, Exporter** <br /><br />Encodage dans la stratégie : **EXPORT**|Active l’option d’enregistrement du contenu sous un autre nom de fichier (Enregistrer sous). <br /><br />Pour le client Azure Information Protection, le fichier peut être enregistré sans protection, et aussi reprotégé avec de nouveaux paramètres et autorisations. Ces actions autorisées signifient qu’un utilisateur disposant de ce droit peut changer ou supprimer une étiquette Azure Information Protection dans un document ou un e-mail protégé. <br /><br />Ce droit permet également à l’utilisateur d’utiliser d’autres options d’exportation dans les applications, telles que **Envoyer à OneNote**.|Droits personnalisés Office : En relation avec l’option **Contrôle total**. <br /><br />Nom dans le portail Azure Classic : **Exporter le contenu (Enregistrer sous)** <br /><br />Nom dans le centre d’administration d’étiquetage et Portail Azure : **Enregistrer sous, exporter (exporter)**<br /><br />Nom dans les modèles AD RMS : **Exporter (Enregistrer sous)** <br /><br />Constante ou valeur API :`IPC_GENERIC_EXPORT L"EXPORT"`|
|Nom commun : **Transférer** <br /><br />Encodage dans la stratégie : **FORWARD**|Active l’option de transfert de message électronique et d’ajout de destinataires aux lignes **À** et **CC**. Ce droit ne s’applique pas aux documents, uniquement aux e-mails.<br /><br />Il n’autorise pas le redirecteur à accorder des droits à d’autres utilisateurs dans le cadre du transfert. <br /><br />Quand vous accordez ce droit, vous devez également accorder le droit **Modifier le contenu, Modifier** (nom commun) et le droit **Enregistrer** (nom commun) pour garantir que l’e-mail protégé n’est pas remis sous forme de pièce jointe. Spécifiez aussi ces droits quand vous envoyez un e-mail à une autre organisation qui utilise le client Outlook ou Outlook Web App. Ou, pour les utilisateurs de votre organisation qui sont exemptés de l’utilisation de la protection Rights Management, car vous avez implémenté des [contrôles d’intégration](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy).|Droits personnalisés Office : refusé lorsque vous utilisez la stratégie standard **Ne pas transférer**.<br /><br />Nom dans le portail Azure Classic : **Transférer**<br /><br />Nom dans le centre d’administration d’étiquetage et Portail Azure : **transférer (suivant)**<br /><br />Nom dans les modèles AD RMS : **Transférer** <br /><br />Constante ou valeur API :`IPC_EMAIL_FORWARD L"FORWARD"`|
|Nom commun : **Contrôle total** <br /><br />Encodage dans la stratégie : **OWNER**|Accorde tous les droits au document, toutes les actions disponibles peuvent être effectuées.<br /><br />Inclut la possibilité de supprimer la protection et de reprotéger un document. <br /><br />Notez que ce droit d’utilisation n’est pas le même que le [propriétaire Rights Management](#rights-management-issuer-and-rights-management-owner).|Droits personnalisés Office : comme l’option personnalisée **Contrôle total**.<br /><br />Nom dans le portail Azure Classic : **Contrôle total**<br /><br />Nom dans le centre d’administration d’étiquetage et Portail Azure : **contrôle total (propriétaire)**<br /><br />Nom dans les modèles AD RMS : **Contrôle total** <br /><br />Constante ou valeur API :`IPC_GENERIC_ALL L"OWNER"`|
|Nom commun : **Imprimer** <br /><br />Encodage dans la stratégie : **PRINT**|Active les options d’impression du contenu.|Droits personnalisés Office : comme l’option **imprimer le contenu** dans les autorisations personnalisées. Ce n’est pas un paramètre par destinataire.<br /><br />Nom dans le portail Azure Classic : **Imprimer**<br /><br />Nom dans le centre d’administration d’étiquetage et Portail Azure : **Imprimer (imprimer)**<br /><br />Nom dans les modèles AD RMS : **Imprimer** <br /><br />Constante ou valeur API :`IPC_GENERIC_PRINT L"PRINT"`|
|Nom commun : **Répondre** <br /><br />Encodage dans la stratégie : **REPLY**|Active l’option **Répondre** dans un client de messagerie, sans autoriser la modification des lignes **À** ou **CC**.<br /><br />Quand vous accordez ce droit, vous devez également accorder le droit **Modifier le contenu, Modifier** (nom commun) et le droit **Enregistrer** (nom commun) pour garantir que l’e-mail protégé n’est pas remis sous forme de pièce jointe. Spécifiez aussi ces droits quand vous envoyez un e-mail à une autre organisation qui utilise le client Outlook ou Outlook Web App. Ou, pour les utilisateurs de votre organisation qui sont exemptés de l’utilisation de la protection Rights Management, car vous avez implémenté des [contrôles d’intégration](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy).|Droits personnalisés Office : non applicable.<br /><br />Nom dans le portail Azure Classic : **Répondre**<br /><br />Nom dans le portail Azure Classic : **Répondre (REPLY)**<br /><br />Nom dans les modèles AD RMS : **Répondre** <br /><br />Constante ou valeur API :`IPC_EMAIL_REPLY`|
|Nom commun : **Répondre à tous** <br /><br />Encodage dans la stratégie : **REPLYALL**|Active l’option **Répondre à tous** dans un client de messagerie, mais ne permet pas à l’utilisateur d’ajouter des destinataires aux lignes **À** ou **CC**.<br /><br />Quand vous accordez ce droit, vous devez également accorder le droit **Modifier le contenu, Modifier** (nom commun) et le droit **Enregistrer** (nom commun) pour garantir que l’e-mail protégé n’est pas remis sous forme de pièce jointe. Spécifiez aussi ces droits quand vous envoyez un e-mail à une autre organisation qui utilise le client Outlook ou Outlook Web App. Ou, pour les utilisateurs de votre organisation qui sont exemptés de l’utilisation de la protection Rights Management, car vous avez implémenté des [contrôles d’intégration](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy).|Droits personnalisés Office : non applicable.<br /><br />Nom dans le portail Azure Classic : **Répondre à tous**<br /><br />Nom dans le centre d’administration d’étiquetage et Portail Azure : **répondre à tous (répondre à tous)**<br /><br />Nom dans les modèles AD RMS : **Répondre à tous** <br /><br />Constante ou valeur API :`IPC_EMAIL_REPLYALL L"REPLYALL"`|
|Nom commun : **Afficher, Ouvrir, Lire** <br /><br />Encodage dans la stratégie : **VIEW**|Permet à l’utilisateur d’ouvrir le document et de voir son contenu.<br /><br /> Dans Excel, ce droit n’est pas suffisant pour trier les données. Pour ce faire, le droit suivant est requis : **Modifier le contenu, Modifier**. Pour filtrer les données dans Excel, vous avez besoin des deux droits suivants : **Modifier le contenu, Modifier** et **Copier**.|Droits personnalisés Office : comme la stratégie personnalisée **Lire**, l’option **Afficher**.<br /><br />Nom dans le portail Azure Classic : **Afficher**<br /><br />Nom dans le centre d’administration d’étiquetage et Portail Azure : **afficher, ouvrir, lire (afficher)**<br /><br />Nom dans les modèles AD RMS : **Lecture** <br /><br />Constante ou valeur API :`IPC_GENERIC_READ L"VIEW"`|
|Nom commun : **Copier** <br /><br />Encodage dans la stratégie : **EXTRACT**|Active les options permettant de copier des données (y compris des captures d’écran) à partir du document dans ce même document ou dans un autre.<br /><br />Dans certaines applications, il permet également d’enregistrer le document entier dans un format non protégé.<br /><br />Dans Skype Entreprise et des applications de partage d’écran similaires, le présentateur doit avoir ce droit pour présenter correctement un document protégé. Si le présentateur ne dispose pas de ce droit, les participants ne peuvent pas afficher le document et il s’affiche en noir pour eux.|Droits personnalisés Office: comme l’option de stratégie personnalisée **Autoriser les utilisateurs disposant de l’accès en lecture à copier le contenu**.<br /><br />Nom dans le portail Azure Classic : **Copier et extraire le contenu**<br /><br />Nom dans le centre d’administration d’étiquetage et Portail Azure : **copier (extract)**<br /><br />Nom dans les modèles AD RMS : **Extraire** <br /><br />Constante ou valeur API :`IPC_GENERIC_EXTRACT L"EXTRACT"`|
|Nom commun : **Afficher les droits** <br /><br />Encodage dans la stratégie : **VIEWRIGHTSDATA**|Permet à l’utilisateur d’afficher la stratégie appliquée au document. <br /><br /> Non pris en charge par les applications Office ou les clients Azure Information Protection.|Droits personnalisés Office : non implémenté.<br /><br />Nom dans le portail Azure Classic : **Afficher les droits affectés**<br /><br />Nom dans le centre d’administration d’étiquetage et Portail Azure : **afficher les droits (VIEWRIGHTSDATA)**.<br /><br />Nom dans les modèles AD RMS : **Afficher les droits** <br /><br />Constante ou valeur API :`IPC_READ_RIGHTS L"VIEWRIGHTSDATA"`|
|Nom commun : **Modifier les droits** <br /><br />Encodage dans la stratégie : **EDITRIGHTSDATA**|Permet à l’utilisateur de modifier la stratégie appliquée au document. Cela inclut notamment la suppression de la protection. <br /><br /> Non pris en charge par les applications Office ou les clients Azure Information Protection.|Droits personnalisés Office : non implémenté.<br /><br />Nom dans le portail Azure Classic : **Modifier les droits**<br /><br />Nom dans le centre d’administration d’étiquetage et Portail Azure : **modifier les droits (EDITRIGHTSDATA)**.<br /><br />Nom dans les modèles AD RMS : **Modifier les droits** <br /><br />Constante ou valeur API :`PC_WRITE_RIGHTS L"EDITRIGHTSDATA"`|
|Nom commun : **Autoriser les macros** <br /><br />Encodage dans la stratégie : **OBJMODEL**|Active l’option pour exécuter des macros ou effectuer d’autres accès à distance ou par programme au contenu d’un document.|Droits personnalisés Office : comme l’option de stratégie personnalisée **Autoriser l’accès par programme**. Ce n’est pas un paramètre par destinataire.<br /><br />Nom dans le portail Azure Classic : **Autoriser les macros**<br /><br />Nom dans le centre d’administration d’étiquetage et Portail Azure : **autoriser les macros (OBJMODEL)**<br /><br />Nom dans les modèles AD RMS : **Autoriser les macros** <br /><br />Constante ou valeur API : non implémenté.|

## <a name="rights-included-in-permissions-levels"></a>Droits inclus dans les niveaux d’autorisation

Certaines applications regroupent les droits d’utilisation dans des niveaux d’autorisation afin de faciliter la sélection de droits d’utilisation généralement utilisés ensemble. Ces niveaux d’autorisation permettent d’abstraire un niveau de complexité aux utilisateurs, pour qu’ils puissent choisir des options basées sur le rôle.  Par exemple, **Réviseur** et **Coauteur**. Bien que ces options montrent souvent un récapitulatif des droits aux utilisateurs, ils ne peuvent pas inclure tous les droits répertoriés dans le tableau précédent.

Utilisez le tableau suivant pour disposer d’une liste de ces niveaux d’autorisation et la liste complète des droits d’utilisation qu’ils contiennent. Les droits d’utilisation sont répertoriés par leur [nom commun](#usage-rights-and-descriptions).

|Niveau d’autorisation|Applications|Droits d’utilisation inclus|
|---------------------|----------------|---------------------------------|
|Visionneuse|Portail Azure Classic <br /><br />Portail Azure<br /><br />Client Azure Information Protection pour Windows|Afficher, Ouvrir, Lire ; Afficher les droits ; Répondre [[1]](#footnote-1); Répondre à tous [[1]](#footnote-1); Autoriser les Macros [[2]](#footnote-2)<br /><br />Remarque : Pour les e-mails, utilisez Réviseur plutôt que ce niveau d’autorisation pour vous assurer qu’une réponse à l’e-mail est reçue en tant qu’e-mail et non pas en tant que pièce jointe. Réviseur est également requis lorsque vous envoyez un e-mail à une autre organisation utilisant le client ou l’application web Outlook. Ou, pour les utilisateurs de votre organisation exempts de l’utilisation du service Azure Rights Management après l’implémentation des [contrôles d’intégration](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy).|
|Réviseur|Portail Azure Classic <br /><br />Portail Azure<br /><br />Client Azure Information Protection pour Windows|Afficher, Ouvrir, Lire ; Enregistrer ; Modifier le contenu, Modifier ; Afficher les droits ; Répondre ; Répondre à tous [[3]](#footnote-3); Transférer [[3]](#footnote-3); Autoriser les Macros [[2]](#footnote-2)|
|Coauteur|Portail Azure Classic <br /><br />Portail Azure<br /><br />Client Azure Information Protection pour Windows|Afficher, Ouvrir, Lire ; Enregistrer ; Modifier le contenu, Modifier ; Copier ; Afficher les droits ; Autoriser les Macros ; Enregistrer sous, Exporter [[4]](#footnote-4); Imprimer ; Répondre [[3]](#footnote-3); Répondre à tous [[3]](#footnote-3); Transférer [[3]](#footnote-3)|
|Copropriétaire|Portail Azure Classic <br /><br />Portail Azure<br /><br />Client Azure Information Protection pour Windows|Afficher, Ouvrir, Lire ; Enregistrer ; Modifier le contenu, Modifier ; Copier ; Afficher les droits ; Modifier les droits ; Autoriser les Macros ; Enregistrer sous, Exporter ; Imprimer ; Répondre [[3]](#footnote-3); Répondre à tous [[3]](#footnote-3); Transférer [[3]](#footnote-3) ; Contrôle total|

----

###### <a name="footnote-1"></a>Note 1

Non inclus dans le centre d’administration d’étiquetage ou Portail Azure.

###### <a name="footnote-2"></a>Note 2

Pour le client Azure Information Protection pour Windows, ce droit est requis pour la barre de Information Protection dans les applications Office.

###### <a name="footnote-3"></a>Note 3
Non applicable dans le client Azure Information Protection pour Windows.

###### <a name="footnote-4"></a>Note 4
Non inclus dans le centre d’administration d’étiquetage, le Portail Azure ou le client Azure Information Protection pour Windows.

## <a name="do-not-forward-option-for-emails"></a>Option Ne pas transférer pour les e-mails

Les clients et services Exchange (par exemple, le client Outlook, Outlook sur le web, les règles de flux de courrier Exchange et les actions de protection contre la perte de données pour Exchange) disposent d’une option de protection des droits d’information supplémentaire pour les e-mails : **Ne pas transférer**. 

Même si cette option apparaît aux utilisateurs (et aux administrateurs Exchange) comme un modèle par défaut de Rights Management qu’ils peuvent sélectionner, **Ne pas transférer** n’est pas un modèle. Cela explique pourquoi vous ne pouvez pas la voir dans le portail Azure quand vous affichez et gérez les modèles de protection. L’option **Ne pas transférer** correspond plutôt à un ensemble de droits d’utilisation appliqué dynamiquement par les utilisateurs à leurs destinataires.

Lorsque l’option **Ne pas transférer** est appliquée à un e-mail, cet e-mail est chiffré et les destinataires doivent être authentifiés. Ils ne peuvent pas le transférer, l’imprimer ou le copier. Par exemple, dans le client Outlook, le bouton Transférer n’est pas accessible. Les options de menu **Enregistrer sous** et **Imprimer** ne sont pas disponibles non plus. Il n’est pas possible d’ajouter ou de modifier les destinataires dans les zones **À**, **Cc** et **Cci**.

Les [documents Office](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM) non protégés qui sont joints à l’e-mail héritent automatiquement des mêmes restrictions. Les droits d’utilisation appliqués à ces documents sont **Modifier le contenu, Modifier** ; **Enregistrer** ; **Afficher, Ouvrir, Lire** et **Autoriser les macros**. Si vous souhaitez des droits d’utilisation différents pour une pièce jointe ou si votre pièce jointe n’est pas un document Office prenant en charge cette protection héritée, protégez le fichier avant de le joindre à l’e-mail. Vous pouvez alors affecter les droits d’utilisation spécifiques dont vous avez besoin pour le fichier. 

### <a name="difference-between-do-not-forward-and-not-granting-the-forward-usage-right"></a>Différence entre l’option Ne pas transférer et le fait de ne pas accorder le droit d’utilisation Transférer

Il existe une distinction importante entre l’application de l’option **Ne pas transférer** et celle d’un modèle qui n’accorde pas le droit d’utilisation **Transférer** à un e-mail : l’option **Ne pas transférer** utilise une liste dynamique des utilisateurs autorisés qui se base sur les destinataires choisis par l’utilisateur dans l’e-mail d’origine, tandis que les droits du modèle ont une liste statique d’utilisateurs autorisés que l’administrateur a spécifiés au préalable. Quelle est la différence ? Prenons un exemple : 

Un utilisateur souhaite envoyer un e-mail à des personnes spécifiques du service marketing, contenant certaines informations à ne pas partager. Doit-il protéger l’e-mail avec un modèle restreignant les droits (affichage, réponse et enregistrement) au service marketing ?  Ou bien doit-il choisir l’option **Ne pas transférer** ? Les deux choix se traduiraient par le fait que les destinataires ne pourraient pas transférer l’e-mail. 

- S’il applique le modèle, les destinataires peuvent toujours partager les informations avec d’autres personnes du service marketing. Par exemple, un destinataire peut utiliser l’explorateur pour glisser et déposer l’e-mail vers un emplacement partagé ou un lecteur USB. Ainsi, toute personne du service marketing (et le propriétaire de l’e-mail) ayant accès à cet emplacement peut afficher les informations contenues dans l’e-mail.
 
- S’il applique l’option **Ne pas transférer**, les destinataires ne pourront pas partager les informations avec d’autres personnes du service marketing en déplaçant l’e-mail vers un autre emplacement. Dans ce scénario, seuls les destinataires d’origine (et le propriétaire de l’e-mail) seront en mesure d’afficher les informations contenues dans l’e-mail.

> [!NOTE] 
> Utilisez l’option **Ne pas transférer** quand il est important que seuls les destinataires choisis par l’expéditeur puissent consulter les informations contenues dans l’e-mail. Utilisez un modèle pour les e-mails afin de restreindre les droits à un groupe de personnes spécifié à l’avance par l’administrateur, indépendamment des destinataires choisis par l’expéditeur.

## <a name="encrypt-only-option-for-emails"></a>Option de chiffrement uniquement pour les e-mails

Quand Exchange Online utilise les nouvelles fonctionnalités de chiffrement de messages Office 365, une nouvelle option **de chiffrement de courrier électronique devient** disponible pour chiffrer les données sans restrictions supplémentaires.

Cette option est disponible pour les locataires qui utilisent Exchange Online et qui peuvent être sélectionnées comme suit :

- **Dans Outlook sur le Web**
- **Comme une autre option de protection des droits** pour une règle de courrier
- **En tant qu’action DLP d’Office 365**
- **À partir d’Outlook**, pour les versions listées dans le [tableau des versions prises en charge pour les applications Microsoft 365es par canal de mise à jour](/officeupdates/update-history-microsoft365-apps-by-date), lorsque vous avez [Microsoft 365 des applications qui prennent en charge Azure RMS](requirements-applications.md#windows-computers-for-information-rights-management-irm). 

Pour plus d’informations sur l’option chiffrer uniquement, consultez l’annonce de blog suivante de l’équipe Office : [chiffrement du déploiement uniquement dans le chiffrement de messages Office 365](https://aka.ms/omefeb2018).

Lorsque cette option est sélectionnée, l’e-mail est chiffré et les destinataires doivent être authentifiés. Ensuite, les destinataires ont tous les droits d’utilisation, à l’exception de **Enregistrer sous, Exporter** et de **Contrôle total**. Cette combinaison de droits d’utilisation signifie que les destinataires n’ont aucune restriction, mis à part qu’ils ne peuvent pas supprimer la protection. Par exemple, un destinataire peut copier à partir de l’e-mail, l’imprimer et le transférer. 

De façon similaire, par défaut, les [documents Office](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM) non protégés qui sont joints à l’e-mail héritent des mêmes autorisations. Ces documents sont automatiquement protégés et, quand ils sont téléchargés, ils peuvent être enregistrés, modifiés, copiés et imprimés à partir des applications Office par les destinataires. Lorsque le document est enregistré par un destinataire, il peut être enregistré sous un nouveau nom et même dans un format différent. Toutefois, seuls les formats de fichier qui prennent en charge la protection sont disponibles, de sorte que le document ne peut pas être enregistré sans la protection d’origine. Si vous souhaitez des droits d’utilisation différents pour une pièce jointe ou si votre pièce jointe n’est pas un document Office prenant en charge cette protection héritée, protégez le fichier avant de le joindre à l’e-mail. Vous pouvez alors affecter les droits d’utilisation spécifiques dont vous avez besoin pour le fichier.

Vous pouvez aussi modifier cet héritage de la protection des documents en spécifiant `Set-IRMConfiguration -DecryptAttachmentForEncryptOnly $true` avec [Exchange Online PowerShell](/powershell/exchange/exchange-online/connect-to-exchange-online-powershell/connect-to-exchange-online-powershell). Utilisez cette configuration quand vous n’avez pas besoin de conserver la protection d’origine pour le document une fois que l’utilisateur est authentifié. Quand les destinataires ouvrent l’e-mail, le document n’est pas protégé.

Si vous n’avez pas besoin qu’un document joint conserve la protection d’origine, consultez [Sécuriser la collaboration sur les documents à l’aide d’Azure Information Protection](secure-collaboration-documents.md).

Remarque : Si vous voyez des références à **DecryptAttachmentFromPortal**, ce paramètre est désormais déconseillé pour [Set-IRMConfiguration](/powershell/module/exchange/encryption-and-certificates/set-irmconfiguration). Sauf si vous avez précédemment défini ce paramètre, il n’est pas disponible.

## <a name="automatically-encrypt-pdf-documents-with-exchange-online"></a>Chiffrer automatiquement les documents PDF avec Exchange Online

Quand Exchange Online utilise les nouvelles fonctionnalités de chiffrement de messages Office 365, vous pouvez chiffrer automatiquement les documents PDF non protégés lorsqu’ils sont joints à un message électronique chiffré. Le document hérite des mêmes autorisations que celles du message électronique. Pour activer cette configuration, définissez **EnablePdfEncryption $true** avec [Set-IRMConfiguration](/powershell/module/exchange/encryption-and-certificates/set-irmconfiguration).

Les destinataires qui n’ont pas encore de lecteur installé et qui prend en charge la norme ISO pour le chiffrement PDF peuvent installer l’un des lecteurs listés dans les [lecteurs PDF qui prennent en charge Microsoft information protection](./rms-client/protected-pdf-readers.md). Les destinataires peuvent également lire le document PDF protégé dans le portail OME.

## <a name="rights-management-issuer-and-rights-management-owner"></a>L’émetteur Rights Management et le propriétaire Rights Management

Quand un document ou un e-mail est protégé à l’aide du service Azure Rights Management, le compte qui protège ce contenu devient automatiquement l’émetteur Rights Management pour ce contenu. Ce compte est enregistré avec le champ **issuer** dans les [journaux d’utilisation](log-analyze-usage.md#how-to-interpret-your-usage-logs). 

L’émetteur Rights Management se voit toujours accorder le droit d’utilisation Contrôle total pour le document ou l’e-mail, et en outre :

- Si les paramètres de protection incluent une date d’expiration, l’émetteur Rights Management peut toujours ouvrir et modifier le document ou l’e-mail après cette date.

- L’émetteur Rights Management peut toujours accéder au document ou à l’e-mail en mode hors connexion.

- L’émetteur Rights Management peut toujours ouvrir un document une fois qu’il est révoqué. 

Par défaut, ce compte est également le **propriétaire Rights Management** pour ce contenu, qui est le cas lorsqu’un utilisateur qui a créé le document ou l’e-mail instaure la protection. Mais il existe certains scénarios où un administrateur ou un service peut protéger du contenu pour le compte d’utilisateurs. Par exemple :

- Un administrateur protège en bloc des fichiers sur un partage de fichiers : le compte d’administrateur dans Azure AD protège les documents pour les utilisateurs.

- Le connecteur Rights Management protège les documents Office dans un dossier de Windows Server : le compte de principal du service dans Azure AD qui est créé pour le connecteur RMS protège les documents pour les utilisateurs.

Dans ces scénarios, l’émetteur Rights Management peut affecter le propriétaire Rights Management à un autre compte à l’aide de kits de développement logiciel Azure Information Protection ou PowerShell. Par exemple, lorsque vous utilisez l’applet de commande Powershell [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) avec le client Azure Information Protection, vous pouvez spécifier le paramètre **OwnerEmail** afin d’affecter le propriétaire Rights Management à un autre compte. 

Lorsque l’émetteur Rights Management protège pour des utilisateurs, l’affectation du propriétaire Rights Management garantit que le propriétaire du document ou de l’e-mail d’origine a le même niveau de contrôle pour leur contenu protégé que s’ils avaient instauré la protection eux-mêmes. 

Par exemple, l’utilisateur qui a créé le document peut l’imprimer, même s’il est désormais protégé avec un modèle n’incluant pas le droit d’utilisation Imprimer. Le même utilisateur peut toujours accéder à son document, quel que soit le paramètre d’accès hors connexion ou la date d’expiration configuré dans ce modèle. En outre, étant donné que le propriétaire Rights Management possède le droit d’utilisation Contrôle total, cet utilisateur peut également protéger de nouveau le document pour autoriser l’accès à d’autres utilisateurs (l’utilisateur devient alors l’émetteur Rights Management ainsi que le propriétaire Rights Management), et cet utilisateur peut même supprimer la protection. Toutefois, seulement l’émetteur Rights Management peut suivre et révoquer un document.

Le propriétaire Rights Management pour un document ou un e-mail est enregistré avec le champ **owner-email** dans les [journaux d’utilisation](log-analyze-usage.md#how-to-interpret-your-usage-logs).

Notez que le propriétaire Rights Management est indépendant du propriétaire du système de fichiers Windows. Ce sont souvent les mêmes, mais ils peuvent être différents, même si vous n’utilisez pas les kits de développement logiciel ou PowerShell.

## <a name="rights-management-use-license"></a>Licence d’utilisation de Rights Management

Lorsqu’un utilisateur ouvre un document ou un e-mail protégé par Azure Rights Management, une licence d’utilisation de Rights Management pour ce contenu est accordée à l’utilisateur. Cette licence d’utilisation est un certificat contenant les droits d’utilisation de l’utilisateur pour le document ou l’e-mail ainsi que la clé de chiffrement utilisée pour chiffrer le contenu. La licence d’utilisation peut également contenir une date d’expiration, ainsi qu’une durée de validité.

Un utilisateur doit disposer d’une licence d’utilisation valide pour ouvrir le contenu en plus de son certificat de compte de droits (RAC), certificat accordé quand [l’environnement utilisateur est initialisé](how-does-it-work.md#initializing-the-user-environment), puis renouvelé tous les 31 jours.

Pendant la durée de la licence d’utilisation, l’utilisateur n’est ni réauthentifié ni réautorisé pour le contenu. Cela permet à l’utilisateur de continuer à ouvrir le document ou l’e-mail protégé sans connexion Internet. Au terme de la période de validité de la licence d’utilisation, l’utilisateur doit être réauthentifié et réautorisé s’il souhaite accéder au document ou à l’e-mail protégé. 

Lorsque les documents et e-mails sont protégés à l’aide d’une étiquette ou d’un modèle qui définit les paramètres de protection, vous pouvez modifier ces paramètres dans votre modèle ou votre étiquette sans avoir besoin de protéger de nouveau le contenu. Si un utilisateur a déjà accédé au contenu, les changements prennent effet une fois que sa licence d’utilisation est arrivée à expiration. Toutefois, lorsque des utilisateurs appliquent des autorisations personnalisées (également connues sous le nom de stratégie de droits ad-hoc) et que ces autorisations doivent être modifiées après la protection du document ou de l’e-mail, le contenu doit être de nouveau protégé avec les nouvelles autorisations. Des autorisations personnalisées pour un e-mail sont implémentées avec l’option Ne pas transférer.

La période de validité de la licence d’utilisation par défaut pour un locataire est de 30 jours. vous pouvez configurer cette valeur à l’aide de l’applet de commande PowerShell [Set-AipServiceMaxUseLicenseValidityTime](/powershell/module/aipservice/set-aipservicemaxuselicensevaliditytime). Vous pouvez configurer un paramètre plus restrictif lorsque la protection est appliquée à l’aide d’une étiquette ou d’un modèle :

- Lorsque vous configurez une étiquette ou un modèle dans le portail Azure, la période de validité de la licence d’utilisation prend sa valeur à partir du paramètre **Autoriser l’accès hors connexion**. 
    
    Pour plus d’informations et de conseils sur la configuration de ce paramètre dans le portail Azure, consultez le tableau [Informations sur les paramètres de protection](configure-policy-protection.md#information-about-the-protection-settings) dans les instructions relatives à la configuration d’une étiquette pour la protection Rights Management.

- Quand vous configurez un modèle à l’aide de PowerShell, la période de validité de la licence d’utilisation prend sa valeur du paramètre *LicenseValidityDuration* dans les applets de commande [Set-AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty) et [Add-AipServiceTemplate](/powershell/module/aipservice/add-aipservicetemplate) .
    
    Pour plus d’informations et de conseils pour la configuration de ce paramètre à l’aide de PowerShell, consultez l’aide relative à chaque applet de commande.

## <a name="rights-included-in-the-default-templates"></a>Droits inclus dans les modèles par défaut

**Concerne**: client classique AIP uniquement

Le tableau suivant répertorie les droits d’utilisation inclus lorsque les modèles par défaut sont créés. Les droits d’utilisation sont répertoriés par leur [nom commun](#usage-rights-and-descriptions).

Ces modèles par défaut sont créés lors de l’achat de votre abonnement, et les noms et les droits d’utilisation peuvent être [modifiés](configure-policy-templates.md) dans la portail Azure et avec [PowerShell](/powershell/module/aipservice/set-aipservicetemplateproperty). 

|Nom complet du modèle|Droits d’utilisation du 6 octobre 2017 à maintenant|Droits d’utilisation avant le 6 octobre 2017|
|----------------|--------------------|----------|
|\<*organization name> -Affichage confidentiel uniquement * <br /><br />or<br /><br /> *Hautement confidentiel \ Tous les employés*|Afficher, Ouvrir, Lire ; Copier ; Afficher les droits ; Autoriser les Macros ; Imprimer ; Transférer ; Répondre ; Répondre à tous ; Enregistrer ; Modifier le contenu, Modifier|Afficher, Ouvrir, Lire|
|\<*organization name>Confidentiel <br /><br />or <br /><br />*Confidentiel \ Tous les employés*|Afficher, Ouvrir, Lire ; Enregistrer sous, Exporter ; Copier ; Afficher les droits ; Modifier les droits ; Autoriser les Macros ; Imprimer ; Transférer ; Répondre ; Répondre à tous ; Enregistrer ; Modifier le contenu, Modifier ; Contrôle total|Afficher, Ouvrir, Lire ; Enregistrer sous, Exporter ; Modifier le contenu, Modifier ; Afficher les droits ; Autoriser les Macros ; Transférer ; Répondre ; Répondre à tous|

## <a name="see-also"></a>Voir aussi
[Configuration et gestion des modèles pour Azure Information Protection](configure-policy-templates.md)

[Configuration de super utilisateurs pour Azure Information Protection ainsi que pour les services de découverte ou la récupération des données](configure-super-users.md)