---
title: 'Comment : utiliser les droits intégrés | Azure RMS'
description: Décrit les droits intégrés fournis par RMS SDK 4.2 et les restrictions d’utilisation qu’une application doit suivre pour respecter ces droits.
keywords: ''
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 9142dd29-f1f4-4c2f-82ac-534f14b8bba1
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 3340b1c1f3c4495db9092ed741049f50d64596cb
ms.sourcegitcommit: 93124ef58e471277c7793130f1a82af33dabcea9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/11/2018
ms.locfileid: "27765664"
---
# <a name="how-to-use-built-in-rights"></a>Comment : utiliser les droits intégrés

Cette rubrique décrit les droits intégrés fournis par Microsoft Rights Management SDK 4.2 et les restrictions d’utilisation qu’une application doit suivre pour respecter ces droits. Vous trouverez ci-après les différents droits intégrés (droits communs, droits sur les documents modifiables et droits sur les e-mails), suivis d’une description et des valeurs qu’ils acceptent par système d’exploitation.

**Remarque** : Pour le SDK Linux, consultez le fichier source *rights.h* pour obtenir plus d’informations.

## <a name="common-rights"></a>Droits communs

**All** : collection de tous les droits communs.
- Android : [CommonRights.All](https://msdn.microsoft.com/library/dn758258.aspx)
- iOS et OS X : [MSCommonRights](https://msdn.microsoft.com/library/dn758314.aspx) -User, Owner et View doivent implémenter **All**
- Windows Store et Windows Phone : [CommonRights.All</strong>](https://msdn.microsoft.com/library/microsoft.rightsmanagement.commonrights.all.aspx)
- Linux : [CommonRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)

**Owner** : Le droit Owner accorde un contrôle total sur le contenu protégé.
- Android : [<strong>CommonRights.Owner](https://msdn.microsoft.com/library/dn758258.aspx)
- iOS et OS X : [MSCommonRights owner](https://msdn.microsoft.com/library/dn758314.aspx)
- Windows Store et Windows Phone : [CommonRights.Owner](https://msdn.microsoft.com/library/microsoft.rightsmanagement.commonrights.owner.aspx)
- Linux : [CommonRights::Owner](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)

**View** : droit d’afficher le contenu protégé. Quand ce droit est accordé, l’application permet généralement à l’utilisateur d’ouvrir et d’afficher le contenu protégé. Toutefois, l’utilisateur doit disposer de droits supplémentaires pour modifier, extraire, transférer ou enregistrer le contenu.

- Android : [CommonRights.View](https://msdn.microsoft.com/library/dn758258.aspx)
- iOS et OS X : [MSCommonRights view](https://msdn.microsoft.com/library/dn758314.aspx)
- Windows Store et Windows Phone : [CommonRights.View](https://msdn.microsoft.com/library/microsoft.rightsmanagement.commonrights.view.aspx)
- Linux : [CommonRights::View](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)</li>

 

## <a name="editable-document-rights"></a>Droits sur les documents modifiables
**All** : collection contenant tous les droits sur les documents modifiables.
- Android : [EditableDocumentRights.All](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS et OS X : [MSEditableDocumentRights all](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows Store et Windows Phone : [EditableDocumentRights.All](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.all.aspx)
- Linux : [EditableDocumentRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Comment** : droit d’ajouter des commentaires au document.
- Android : [EditableDocumentRights.Comment](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS et OS X : [MSEditableDocumentRights comment](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows Store et Windows Phone : [EditableDocumentRights.Comment](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.comment.aspx)
- Linux : [EditableDocumentRights::Comment](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Edit** : Droit de modifier le contenu protégé et de l’enregistrer dans le même format protégé. Quand ce droit est accordé, l’application permet généralement à l’utilisateur de modifier le contenu protégé et de l’enregistrer dans le même fichier.
- Android : [EditableDocumentRights.Edit](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS et OS X : [MSEditableDocumentRights edit](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows Store et Windows Phone : [EditableDocumentRights.Edit](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.edit.aspx)
- Linux : [EditableDocumentRights::Edit](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Export** : droit d’extraire le contenu d’un format protégé et de le placer dans un autre format protégé par AD RMS. Quand ce droit est accordé, l’application permet généralement à l’utilisateur d’enregistrer le contenu protégé dans d’autres formats protégés par AD RMS (par exemple, si l’application implémente une fonctionnalité *Enregistrer sous*).

- Android : [EditableDocumentRights.Export](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS et OS X : [MSEditableDocumentRights exportable](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows Store et Windows Phone : [EditableDocumentRights.Export](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.export.aspx)
- Linux : [EditableDocumentRights::Export](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Extract** : Droit d’extraire le contenu d’un format protégé et de le placer dans un format non protégé. Quand ce droit est accordé, l’application permet généralement à l’utilisateur de copier et de coller les informations d’un contenu protégé. Si l’application implémente une fonctionnalité <em>Enregistrer sous</em>, elle peut également permettre à l’utilisateur d’enregistrer le contenu protégé dans des formats non protégés et dans d’autres formats protégés. Ce droit a la même valeur que le droit Extract pour les e-mails.

- Android : [EditableDocumentRights.Extract](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS et OS X : [MSEditableDocumentRights extract](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows Store et Windows Phone : [EditableDocumentRights.Extract](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.extract.aspx)
- Linux : [EditableDocumentRights::Extract](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Print** : Droit d’imprimer le contenu protégé. Quand ce droit est accordé, l’application permet généralement à l’utilisateur d’imprimer le contenu protégé. Ce droit a la même valeur que le droit Print pour les e-mails.

- Android : [EditableDocumentRights.Print](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS et OS X : [MSEditableDocumentRights print](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows Store et Windows Phone : [EditableDocumentRights.Print](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.print.aspx)
- Linux : [EditableDocumentRights::Print](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

 

## <a name="email-rights"></a>Droits sur les e-mails

**All** : Collection contenant tous les droits sur les e-mails.
- Android : [EmailRights.All](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS et OS X : [MSEmailRights all](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows Store et Windows Phone : [EmailRights.All](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.all.aspx)
- Linux : [EmailRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Extract** : Droit d’extraire le contenu d’un format protégé et de le placer dans un format non protégé. Quand ce droit est accordé, l’application permet généralement au destinataire d’un e-mail de copier et de coller les informations d’un message protégé. Si l’application implémente une fonctionnalité <em>Enregistrer sous</em>, l’application peut également permettre au destinataire d’enregistrer le contenu protégé dans des formats non protégés et dans d’autres formats protégés. Ce droit a la même valeur que le droit Extract pour les documents modifiables.

- Android : [EmailRights.Extract](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS et OS X : [MSEmailRights extract](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows Store et Windows Phone : [EmailRights.Extract</strong>](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.extract.aspx)
- Linux : [EmailRights::Extract](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Forward** : Droit de transférer un message protégé. Quand ce droit est accordé, l’application permet généralement au destinataire d’un e-mail de transférer un message protégé.
- Android : [<strong>EmailRights.Forward</strong>](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS et OS X : [MSEmailRights forward](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows Store et Windows Phone : [EmailRights.Forward](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.forward.aspx)
- Linux : [EmailRights::Forward](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Print** : Droit d’imprimer le contenu protégé. Quand ce droit est accordé, l’application permet généralement au destinataire d’un e-mail d’imprimer un message protégé. Ce droit a la même valeur que le droit Print pour les documents modifiables.

- Android : [EmailRights.Print](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS et OS X : [MSEmailRights print](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows Store et Windows Phone : [EmailRights.Print](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.print.aspx)
- Linux : [EmailRights::Print](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Reply** : Quand ce droit est accordé, l’application permet généralement au destinataire d’un e-mail de répondre à un message protégé et d’inclure une copie du message d’origine.

- Android : [EmailRights.Reply](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS et OS X : [MSEmailRights reply](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows Store et Windows Phone : [EmailRights.Reply](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.reply.aspx)
- Linux : [EmailRights::Reply](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**ReplyAll** : Quand ce droit est accordé, l’application permet généralement au destinataire d’un e-mail de répondre à tous les destinataires d’un message protégé et d’inclure une copie du message d’origine.

- Android : [EmailRights.ReplyAll</strong>](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS et OS X : [MSEmailRights replyAll](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows Store et Windows Phone : [EmailRights.ReplyAll](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.replyall.aspx)
- Linux : [EmailRights::ReplyAll](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]