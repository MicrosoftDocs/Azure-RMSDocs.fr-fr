---
title: "Comment : utiliser les droits intégrés | Azure RMS"
description: "Décrit les droits intégrés fournis par RMS SDK 4.2 et les restrictions d’utilisation qu’une application doit suivre pour respecter ces droits."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 9142dd29-f1f4-4c2f-82ac-534f14b8bba1
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 79e58b8092ea7cb057229d4c464d79f3694296e6
ms.openlocfilehash: 4a5c1a0b420b9db20cca237e2170b6479c565ee6


---

# Comment : utiliser les droits intégrés

Cette rubrique décrit les droits intégrés fournis par Microsoft Rights Management SDK 4.2 et les restrictions d’utilisation qu’une application doit suivre pour respecter ces droits. Vous trouverez ci-après les différents droits intégrés (droits communs, droits sur les documents modifiables et droits sur les e-mails), suivis d’une description et des valeurs qu’ils acceptent par système d’exploitation.

**Remarque** : Pour le SDK Linux, consultez le fichier source *rights.h* pour obtenir plus d’informations.

## Droits communs ##

**All** : collection de tous les droits communs.
- Android : [CommonRights.All](/rights-management/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_ALL)
- iOS et OS X : [MSCommonRights owner](/rights-management/sdk/4.2/api/iOS/mscommonrights#msipcthin2_mscommonrights_interface_objc___NSString__owner_)
- Windows Store et Windows Phone : [CommonRights.All</strong>](/rights-management/sdk/4.2/api/winrt/commonrights#msipcthin2_commonrights)
- Linux : [CommonRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)

** Owner ** : Le droit Owner accorde un contrôle total sur le contenu protégé.
- Android : [<strong>CommonRights.Owner](/rights-management/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_Owner)
- iOS et OS X : [MSCommonRights owner](/rights-management/sdk/4.2/api/iOS/mscommonrights#msipcthin2_mscommonrights_interface_objc___NSString__owner_)
- Windows Store et Windows Phone : [CommonRights.Owner](/rights-management/sdk/4.2/api/winrt/commonrights#msipcthin2_commonrights_owner)
- Linux : [CommonRights::Owner](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)

**View** : droit d’afficher le contenu protégé. Quand ce droit est accordé, l’application permet généralement à l’utilisateur d’ouvrir et d’afficher le contenu protégé. Toutefois, l’utilisateur doit disposer de droits supplémentaires pour modifier, extraire, transférer ou enregistrer le contenu.

- Android : [CommonRights.View](/rights-management/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_View)
- iOS et OS X : [MSCommonRights view](/rights-management/sdk/4.2/api/iOS/mscommonrights#msipcthin2_mscommonrights_interface_objc___NSString__owner_)
- Windows Store et Windows Phone : [CommonRights.View](/rights-management/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_View)
- Linux : [CommonRights::View](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)</li>

 

## Droits sur les documents modifiables ##
**All** : collection contenant tous les droits sur les documents modifiables.
- Android : [EditableDocumentRights.All](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_ALL)
- iOS et OS X : [MSEditableDocumentRights all](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Windows Store et Windows Phone : [EditableDocumentRights.All](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_all)
- Linux : [EditableDocumentRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Comment** : droit d’ajouter des commentaires au document.
- Android : [EditableDocumentRights.Comment](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Comment)
- iOS et OS X : [MSEditableDocumentRights comment](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Windows Store et Windows Phone : [EditableDocumentRights.Comment](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights__comment)
- Linux : [EditableDocumentRights::Comment](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Edit** : Droit de modifier le contenu protégé et de l’enregistrer dans le même format protégé. Quand ce droit est accordé, l’application permet généralement à l’utilisateur de modifier le contenu protégé et de l’enregistrer dans le même fichier.
- Android : [EditableDocumentRights.Edit](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Edit)
- iOS et OS X : [MSEditableDocumentRights edit](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Windows Store et Windows Phone : [EditableDocumentRights.Edit](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_edit)
- Linux : [EditableDocumentRights::Edit](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Export** : droit d’extraire le contenu d’un format protégé et de le placer dans un autre format protégé par AD RMS. Quand ce droit est accordé, l’application permet généralement à l’utilisateur d’enregistrer le contenu protégé dans d’autres formats protégés par AD RMS (par exemple, si l’application implémente une fonctionnalité *Enregistrer sous*).

- Android : [EditableDocumentRights.Export](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Export)
- iOS et OS X : [MSEditableDocumentRights exportable](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Windows Store et Windows Phone : [EditableDocumentRights.Export](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_export)
- Linux : [EditableDocumentRights::Export](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Extract** : Droit d’extraire le contenu d’un format protégé et de le placer dans un format non protégé. Quand ce droit est accordé, l’application permet généralement à l’utilisateur de copier et de coller les informations d’un contenu protégé. Si l’application implémente une fonctionnalité <em>Enregistrer sous</em>, elle peut également permettre à l’utilisateur d’enregistrer le contenu protégé dans des formats non protégés et dans d’autres formats protégés. Ce droit a la même valeur que le droit Extract pour les e-mails.

- Android : [EditableDocumentRights.Extract](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Extract)
- iOS et OS X : [MSEditableDocumentRights extract](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Windows Store et Windows Phone : [EditableDocumentRights.Extract](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_extract)
- Linux : [EditableDocumentRights::Extract](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Print** : Droit d’imprimer le contenu protégé. Quand ce droit est accordé, l’application permet généralement à l’utilisateur d’imprimer le contenu protégé. Ce droit a la même valeur que le droit Print pour les e-mails.

- Android : [EditableDocumentRights.Print](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Print)
- iOS et OS X : [MSEditableDocumentRights print](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Windows Store et Windows Phone : [EditableDocumentRights.Print](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_print)
- Linux : [EditableDocumentRights::Print](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

 

## Droits sur les e-mails ##

**All** : Collection contenant tous les droits sur les e-mails.
- Android : [EmailRights.All](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_ALL)
- iOS et OS X : [MSEmailRights all](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Windows Store et Windows Phone : [EmailRights.All](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_all)
- Linux : [EmailRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Extract** : Droit d’extraire le contenu d’un format protégé et de le placer dans un format non protégé. Quand ce droit est accordé, l’application permet généralement au destinataire d’un e-mail de copier et de coller les informations d’un message protégé. Si l’application implémente une fonctionnalité <em>Enregistrer sous</em>, l’application peut également permettre au destinataire d’enregistrer le contenu protégé dans des formats non protégés et dans d’autres formats protégés. Ce droit a la même valeur que le droit Extract pour les documents modifiables.

- Android : [EmailRights.Extract](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Extract)
- iOS et OS X : [MSEmailRights extract](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Windows Store et Windows Phone : [EmailRights.Extract</strong>](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_extract)
- Linux : [EmailRights::Extract](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Forward** : Droit de transférer un message protégé. Quand ce droit est accordé, l’application permet généralement au destinataire d’un e-mail de transférer un message protégé.
- Android : [<strong>EmailRights.Forward</strong>](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Forward)
- iOS et OS X : [MSEmailRights forward](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Windows Store et Windows Phone : [EmailRights.Forward](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_forward)
- Linux : [EmailRights::Forward](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Print** : Droit d’imprimer le contenu protégé. Quand ce droit est accordé, l’application permet généralement au destinataire d’un e-mail d’imprimer un message protégé. Ce droit a la même valeur que le droit Print pour les documents modifiables.

- Android : [EmailRights.Print](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Print)
- iOS et OS X : [MSEmailRights print](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Windows Store et Windows Phone : [EmailRights.Print](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_print)
- Linux : [EmailRights::Print](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Reply** : Quand ce droit est accordé, l’application permet généralement au destinataire d’un e-mail de répondre à un message protégé et d’inclure une copie du message d’origine.

- Android : [EmailRights.Reply](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Reply)
- iOS et OS X : [MSEmailRights reply](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Windows Store et Windows Phone : [EmailRights.Reply](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_reply)
- Linux : [EmailRights::Reply](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**ReplyAll** : Quand ce droit est accordé, l’application permet généralement au destinataire d’un e-mail de répondre à tous les destinataires d’un message protégé et d’inclure une copie du message d’origine.

- Android : [EmailRights.ReplyAll</strong>](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_ReplyAll)
- iOS et OS X : [MSEmailRights replyAll](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Windows Store et Windows Phone : [EmailRights.ReplyAll](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_replyall)
- Linux : [EmailRights::ReplyAll](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

 

 

 



<!--HONumber=Jul16_HO3-->


