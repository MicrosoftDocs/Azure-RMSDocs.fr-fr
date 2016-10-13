---
title: "Comment : utiliser les droits intégrés | Azure RMS"
description: "Décrit les droits intégrés fournis par RMS SDK 4.2 et les restrictions d’utilisation qu’une application doit suivre pour respecter ces droits."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 9142dd29-f1f4-4c2f-82ac-534f14b8bba1
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
experiment_id: priyamo-TableVsFlatList-20160805
translationtype: Human Translation
ms.sourcegitcommit: b4abffcbe6e49ea25f3cf493a1e68fcd6ea25b26
ms.openlocfilehash: a8a513260dde6047c95c52c48217b7b4d8466cbc


---

# Comment : utiliser les droits intégrés

Cette rubrique décrit les droits intégrés fournis par Microsoft Rights Management SDK 4.2 et les restrictions d’utilisation qu’une application doit suivre pour respecter ces droits. Le tableau suivant recense les différents droits intégrés (droits communs, droits sur les documents modifiables et droits sur les e-mails), suivis d’une description et des valeurs qu’ils acceptent par système d’exploitation.

**Remarque** : Pour le SDK Linux, consultez le fichier source *rights.h* pour obtenir plus d’informations.

## Droits communs ##

| Droit | Description | Android | iOS et OSX | Windows Store et Windows Phone | Linux |
|-------|-------------|---------|-------------|---------------------------------|-------|
| **All** | Collection de tous les droits communs. | [CommonRights.All](/information-protection/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_ALL) | [MSCommonRights owner](/information-protection/sdk/4.2/api/iOS/mscommonrights#msipcthin2_mscommonrights_interface_objc___NSString__owner_)| [CommonRights.All</strong>](/information-protection/sdk/4.2/api/winrt/commonrights#msipcthin2_commonrights)| [CommonRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)|
| **Owner**| Accorde un contrôle total sur le contenu protégé. |  [CommonRights.Owner](/information-protection/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_Owner) |[MSCommonRights owner](/information-protection/sdk/4.2/api/iOS/mscommonrights#msipcthin2_mscommonrights_interface_objc___NSString__owner_) |[CommonRights.Owner](/information-protection/sdk/4.2/api/winrt/commonrights#msipcthin2_commonrights_owner) |  [CommonRights::Owner](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)|
| **View** | Droit d’afficher le contenu protégé. Quand ce droit est accordé, l’application permet généralement à l’utilisateur d’ouvrir et d’afficher le contenu protégé. Toutefois, l’utilisateur doit disposer de droits supplémentaires pour modifier, extraire, transférer ou enregistrer le contenu. |  [CommonRights.View](/information-protection/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_View) | [MSCommonRights view](/information-protection/sdk/4.2/api/iOS/mscommonrights#msipcthin2_mscommonrights_interface_objc___NSString__owner_)|[CommonRights.View](/information-protection/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_View) | [CommonRights::View](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html) |


## Droits sur les documents modifiables ##

| Droit | Description | Android | iOS et OSX | Windows Store et Windows Phone | Linux |
|-------|-------------|---------|-------------|---------------------------------|-------|
| **All** | Collection contenant tous les droits sur les documents modifiables.| [EditableDocumentRights.All](/information-protection/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_ALL) | [MSEditableDocumentRights all](/information-protection/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc) | [EditableDocumentRights.All](/information-protection/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_all) |[EditableDocumentRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)|
| **Comment** | Droit d’ajouter des commentaires au document. | [EditableDocumentRights.Comment](/information-protection/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Comment)|[MSEditableDocumentRights comment](/information-protection/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc) |[EditableDocumentRights.Comment](/information-protection/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights__comment)| [EditableDocumentRights::Comment](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)|
| **Edit** | Droit de modifier le contenu protégé et de l’enregistrer dans le même format protégé. Quand ce droit est accordé, l’application permet généralement à l’utilisateur de modifier le contenu protégé et de l’enregistrer dans le même fichier. | [EditableDocumentRights.Edit](/information-protection/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Edit) | [MSEditableDocumentRights edit](/information-protection/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc) | [EditableDocumentRights.Edit](/information-protection/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_edit) | [EditableDocumentRights::Edit](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html) |
| **Export** | Droit d’extraire le contenu d’un format protégé et de le placer dans un autre format protégé par AD RMS. Quand ce droit est accordé, l’application permet généralement à l’utilisateur d’enregistrer le contenu protégé dans d’autres formats protégés par AD RMS (par exemple, si l’application implémente une fonctionnalité *Enregistrer sous*). | [EditableDocumentRights.Export](/information-protection/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Export) | [MSEditableDocumentRights exportable](/information-protection/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc) |[EditableDocumentRights.Export](/information-protection/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_export) | [EditableDocumentRights::Export](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)|
| **Extract** | Droit d’extraire le contenu d’un format protégé et de le placer dans un format non protégé. Quand ce droit est accordé, l’application permet généralement à l’utilisateur de copier et de coller les informations d’un contenu protégé. Si l’application implémente une fonctionnalité <em>Enregistrer sous</em>, elle peut également permettre à l’utilisateur d’enregistrer le contenu protégé dans des formats non protégés et dans d’autres formats protégés. Ce droit a la même valeur que le droit Extract pour les e-mails. |  [EditableDocumentRights.Extract](/information-protection/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Extract) |[MSEditableDocumentRights extract](/information-protection/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc) | [EditableDocumentRights.Extract](/information-protection/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_extract) |  [EditableDocumentRights::Extract](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)|
| **Print** | Droit d’imprimer le contenu protégé. Quand ce droit est accordé, l’application permet généralement à l’utilisateur d’imprimer le contenu protégé. Ce droit a la même valeur que le droit Print pour les e-mails. | [EditableDocumentRights.Print](/information-protection/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Print) |  [MSEditableDocumentRights print](/information-protection/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)| [EditableDocumentRights.Print](/information-protection/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_print) | [EditableDocumentRights::Print](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)|
 

## Droits sur les e-mails ##

| Droit | Description | Android | iOS et OSX | Windows Store et Windows Phone | Linux |
|-------|-------------|---------|-------------|---------------------------------|-------|
| **All** |Collection contenant tous les droits sur les e-mails. |  [EmailRights.All](/information-protection/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_ALL) | [MSEmailRights all](/information-protection/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc) | [EmailRights.All](/information-protection/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_all)|[EmailRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)|
| **Extract** | Droit d’extraire le contenu d’un format protégé et de le placer dans un format non protégé. Quand ce droit est accordé, l’application permet généralement au destinataire d’un e-mail de copier et de coller les informations d’un message protégé. Si l’application implémente une fonctionnalité <em>Enregistrer sous</em>, l’application peut également permettre au destinataire d’enregistrer le contenu protégé dans des formats non protégés et dans d’autres formats protégés. Ce droit a la même valeur que le droit Extract pour les documents modifiables. | [EmailRights.Extract](/information-protection/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Extract) | [MSEmailRights extract](/information-protection/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc) | [EmailRights.Extract</strong>](/information-protection/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_extract) | [EmailRights::Extract](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html) |
|**Forward**| Droit de transférer un message protégé. Quand ce droit est accordé, l’application permet généralement au destinataire d’un e-mail de transférer un message protégé.| [<strong>EmailRights.Forward</strong>](/information-protection/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Forward) | [MSEmailRights forward](/information-protection/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc) | [EmailRights.Forward](/information-protection/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_forward) | [EmailRights::Forward](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html) |
|**Print** | Droit d’imprimer le contenu protégé. Quand ce droit est accordé, l’application permet généralement au destinataire d’un e-mail d’imprimer un message protégé. Ce droit a la même valeur que le droit Print pour les documents modifiables. | [EmailRights.Print](/information-protection/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Print) |[MSEmailRights print](/information-protection/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc) | [EmailRights.Print](/information-protection/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_print) | [EmailRights::Print](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)|
| **Reply** | Quand ce droit est accordé, l’application permet généralement au destinataire d’un e-mail de répondre à un message protégé et d’inclure une copie du message d’origine. | [EmailRights.Reply](/information-protection/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Reply) | [MSEmailRights reply](/information-protection/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc) | [EmailRights.Reply](/information-protection/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_reply) | [EmailRights::Reply](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)|
| **ReplyAll** | Quand ce droit est accordé, l’application permet généralement au destinataire d’un e-mail de répondre à tous les destinataires d’un message protégé et d’inclure une copie du message d’origine. | [EmailRights.ReplyAll</strong>](/information-protection/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_ReplyAll) | [MSEmailRights replyAll](/information-protection/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc) | [EmailRights.ReplyAll](/information-protection/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_replyall) | [EmailRights::ReplyAll](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)|



<!--HONumber=Sep16_HO5-->


