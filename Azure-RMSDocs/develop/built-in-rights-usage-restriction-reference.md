---
title: 'Comment : utiliser les droits intégrés | Azure RMS'
description: Décrit les droits intégrés fournis par RMS SDK 4.2 et les restrictions d’utilisation qu’une application doit appliquer pour respecter ces droits.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 9142dd29-f1f4-4c2f-82ac-534f14b8bba1
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
experimental: true
experiment_id: priyamo-TableVsFlatList-20160805
ms.openlocfilehash: 337cb03e6350bafb96f0672f9225ebe613044ea4
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/19/2020
ms.locfileid: "95567972"
---
# <a name="how-to-use-built-in-rights"></a>Comment : utiliser les droits intégrés

Cette rubrique décrit les droits intégrés fournis par Microsoft Rights Management SDK 4.2 et les restrictions d’utilisation qu’une application doit appliquer pour respecter ces droits. Vous trouverez ci-après les différents droits intégrés (droits communs, droits sur les documents modifiables et droits sur les e-mails), suivis d’une description et des valeurs qu’ils acceptent par système d’exploitation.

**Remarque** : Pour le SDK Linux, consultez le fichier source *rights.h* pour obtenir plus d’informations.

## <a name="common-rights"></a>Droits communs

**All** : collection de tous les droits communs.
- Android : [CommonRights.All](/previous-versions/windows/desktop/msipcthin2/commonrights-class-java)
- iOS et OS X : [MSCommonRights](/previous-versions/windows/desktop/msipcthin2/mscommonrights-interface-objc) -User, Owner et View doivent implémenter **All**
- Windows Store et Windows Phone : [CommonRights.All</strong>](/previous-versions/windows/desktop/msipcthin2/commonrights-all)
- Linux : [CommonRights::All](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)

**Owner** : le droit owner accorde un contrôle total sur le contenu protégé.
- Android : [ <strong> CommonRights. Owner](/previous-versions/windows/desktop/msipcthin2/commonrights-class-java)
- iOS et OS X : [MSCommonRights owner](/previous-versions/windows/desktop/msipcthin2/mscommonrights-interface-objc)
- Windows Store et Windows Phone : [CommonRights.Owner](/previous-versions/windows/desktop/msipcthin2/commonrights-owner)
- Linux : [CommonRights::Owner](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)

**View** : droit d’afficher le contenu protégé. Quand ce droit est accordé, l’application permet généralement à l’utilisateur d’ouvrir et d’afficher le contenu protégé. Toutefois, l’utilisateur doit disposer de droits supplémentaires pour modifier, extraire, transférer ou enregistrer le contenu.

- Android : [CommonRights.View](/previous-versions/windows/desktop/msipcthin2/commonrights-class-java)
- iOS et OS X : [MSCommonRights view](/previous-versions/windows/desktop/msipcthin2/mscommonrights-interface-objc)
- Windows Store et Windows Phone : [CommonRights.View](/previous-versions/windows/desktop/msipcthin2/commonrights-view)
- Linux : [CommonRights::View](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)</li>

 

## <a name="editable-document-rights"></a>Droits sur les documents modifiables
**All** : collection contenant tous les droits sur les documents modifiables.
- Android : [EditableDocumentRights.All](/previous-versions/windows/desktop/msipcthin2/editabledocumentrights-class-java)
- iOS et OS X : [MSEditableDocumentRights all](/previous-versions/windows/desktop/msipcthin2/mseditabledocumentrights-interface-objc)
- Windows Store et Windows Phone : [EditableDocumentRights.All](/previous-versions/windows/desktop/msipcthin2/editabledocumentrights-all)
- Linux : [EditableDocumentRights::All](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Comment** : droit d’ajouter des commentaires au document.
- Android : [EditableDocumentRights.Comment](/previous-versions/windows/desktop/msipcthin2/editabledocumentrights-class-java)
- iOS et OS X : [MSEditableDocumentRights comment](/previous-versions/windows/desktop/msipcthin2/mseditabledocumentrights-interface-objc)
- Windows Store et Windows Phone : [EditableDocumentRights.Comment](/previous-versions/windows/desktop/msipcthin2/editabledocumentrights--comment)
- Linux : [EditableDocumentRights::Comment](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Edit** : Droit de modifier le contenu protégé et de l’enregistrer dans le même format protégé. Quand ce droit est accordé, l’application permet généralement à l’utilisateur de modifier le contenu protégé et de l’enregistrer dans le même fichier.
- Android : [EditableDocumentRights.Edit](/previous-versions/windows/desktop/msipcthin2/editabledocumentrights-class-java)
- iOS et OS X : [MSEditableDocumentRights edit](/previous-versions/windows/desktop/msipcthin2/mseditabledocumentrights-interface-objc)
- Windows Store et Windows Phone : [EditableDocumentRights.Edit](/previous-versions/windows/desktop/msipcthin2/editabledocumentrights-edit)
- Linux : [EditableDocumentRights::Edit](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Export** : droit d’extraire le contenu d’un format protégé et de le placer dans un autre format protégé par AD RMS. Quand ce droit est accordé, l’application permet généralement à l’utilisateur d’enregistrer le contenu protégé dans d’autres formats protégés par AD RMS (par exemple, si l’application implémente une fonctionnalité *Enregistrer sous*).

- Android : [EditableDocumentRights.Export](/previous-versions/windows/desktop/msipcthin2/editabledocumentrights-class-java)
- iOS et OS X : [MSEditableDocumentRights exportable](/previous-versions/windows/desktop/msipcthin2/mseditabledocumentrights-interface-objc)
- Windows Store et Windows Phone : [EditableDocumentRights.Export](/previous-versions/windows/desktop/msipcthin2/editabledocumentrights-export)
- Linux : [EditableDocumentRights::Export](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Extract** : Droit d’extraire le contenu d’un format protégé et de le placer dans un format non protégé. Quand ce droit est accordé, l’application permet généralement à l’utilisateur de copier et de coller les informations d’un contenu protégé. Si l’application implémente une fonctionnalité <em>Enregistrer sous</em>, elle peut également permettre à l’utilisateur d’enregistrer le contenu protégé dans des formats non protégés et dans d’autres formats protégés. Ce droit a la même valeur que le droit Extract pour les e-mails.

- Android : [EditableDocumentRights.Extract](/previous-versions/windows/desktop/msipcthin2/editabledocumentrights-class-java)
- iOS et OS X : [MSEditableDocumentRights extract](/previous-versions/windows/desktop/msipcthin2/mseditabledocumentrights-interface-objc)
- Windows Store et Windows Phone : [EditableDocumentRights.Extract](/previous-versions/windows/desktop/msipcthin2/editabledocumentrights-extract)
- Linux : [EditableDocumentRights::Extract](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Print** : Droit d’imprimer le contenu protégé. Quand ce droit est accordé, l’application permet généralement à l’utilisateur d’imprimer le contenu protégé. Ce droit a la même valeur que le droit Print pour les e-mails.

- Android : [EditableDocumentRights.Print](/previous-versions/windows/desktop/msipcthin2/editabledocumentrights-class-java)
- iOS et OS X : [MSEditableDocumentRights print](/previous-versions/windows/desktop/msipcthin2/mseditabledocumentrights-interface-objc)
- Windows Store et Windows Phone : [EditableDocumentRights.Print](/previous-versions/windows/desktop/msipcthin2/editabledocumentrights-print)
- Linux : [EditableDocumentRights::Print](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

 

## <a name="email-rights"></a>Droits sur les e-mails

**All** : Collection contenant tous les droits sur les e-mails.
- Android : [EmailRights.All](/previous-versions/windows/desktop/msipcthin2/emailrights-class-java)
- iOS et OS X : [MSEmailRights all](/previous-versions/windows/desktop/msipcthin2/msemailrights-interface-objc)
- Windows Store et Windows Phone : [EmailRights.All](/previous-versions/windows/desktop/msipcthin2/emailrights-all)
- Linux : [EmailRights::All](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Extract** : Droit d’extraire le contenu d’un format protégé et de le placer dans un format non protégé. Quand ce droit est accordé, l’application permet généralement au destinataire d’un e-mail de copier et de coller les informations d’un message protégé. Si l’application implémente une fonctionnalité <em>Enregistrer sous</em>, l’application peut également permettre au destinataire d’enregistrer le contenu protégé dans des formats non protégés et dans d’autres formats protégés. Ce droit a la même valeur que le droit Extract pour les documents modifiables.

- Android : [EmailRights.Extract](/previous-versions/windows/desktop/msipcthin2/emailrights-class-java)
- iOS et OS X : [MSEmailRights extract](/previous-versions/windows/desktop/msipcthin2/msemailrights-interface-objc)
- Windows Store et Windows Phone : [EmailRights.Extract</strong>](/previous-versions/windows/desktop/msipcthin2/emailrights-extract)
- Linux : [EmailRights::Extract](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Forward** : Droit de transférer un message protégé. Quand ce droit est accordé, l’application permet généralement au destinataire d’un e-mail de transférer un message protégé.
- Android : [<strong>EmailRights.Forward</strong>](/previous-versions/windows/desktop/msipcthin2/emailrights-class-java)
- iOS et OS X : [MSEmailRights forward](/previous-versions/windows/desktop/msipcthin2/msemailrights-interface-objc)
- Windows Store et Windows Phone : [EmailRights.Forward](/previous-versions/windows/desktop/msipcthin2/emailrights-forward)
- Linux : [EmailRights::Forward](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Print** : Droit d’imprimer le contenu protégé. Quand ce droit est accordé, l’application permet généralement au destinataire d’un e-mail d’imprimer un message protégé. Ce droit a la même valeur que le droit Print pour les documents modifiables.

- Android : [EmailRights.Print](/previous-versions/windows/desktop/msipcthin2/emailrights-class-java)
- iOS et OS X : [MSEmailRights print](/previous-versions/windows/desktop/msipcthin2/msemailrights-interface-objc)
- Windows Store et Windows Phone : [EmailRights.Print](/previous-versions/windows/desktop/msipcthin2/emailrights-print)
- Linux : [EmailRights::Print](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Reply** : Quand ce droit est accordé, l’application permet généralement au destinataire d’un e-mail de répondre à un message protégé et d’inclure une copie du message d’origine.

- Android : [EmailRights.Reply](/previous-versions/windows/desktop/msipcthin2/emailrights-class-java)
- iOS et OS X : [MSEmailRights reply](/previous-versions/windows/desktop/msipcthin2/msemailrights-interface-objc)
- Windows Store et Windows Phone : [EmailRights.Reply](/previous-versions/windows/desktop/msipcthin2/emailrights-reply)
- Linux : [EmailRights::Reply](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**ReplyAll** : Quand ce droit est accordé, l’application permet généralement au destinataire d’un e-mail de répondre à tous les destinataires d’un message protégé et d’inclure une copie du message d’origine.

- Android : [EmailRights.ReplyAll</strong>](/previous-versions/windows/desktop/msipcthin2/emailrights-class-java)
- iOS et OS X : [MSEmailRights replyAll](/previous-versions/windows/desktop/msipcthin2/msemailrights-interface-objc)
- Windows Store et Windows Phone : [EmailRights.ReplyAll](/previous-versions/windows/desktop/msipcthin2/emailrights-replyall)
- Linux : [EmailRights::ReplyAll](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)