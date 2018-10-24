---
title: mip FileHandler Observer, classe
description: Informations de référence pour la classe mip FileHandler Observer
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a587107afc2b8963d64c31ad47af81761bf2b9f8
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446164"
---
# <a name="class-mipfilehandlerobserver"></a>mip::FileHandler::Observer, classe 
Interface [Observer](class_mip_filehandler_observer.md) permettant aux clients d’obtenir les notifications des événements liés au gestionnaire de fichiers.
Toutes les erreurs héritent de [mip::Error](class_mip_error.md). Le client ne doit pas rappeler le moteur sur le thread qui appelle l’observateur.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public virtual void OnCreateFileHandlerSuccess(const std::shared_ptr<FileHandler>& fileHandler, const std::shared_ptr<void>& context)  |  Appelé en cas de création réussie du gestionnaire.
public virtual void OnCreateFileHandlerFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Appelé en cas d’échec de la création du gestionnaire.
public virtual void OnGetLabelSuccess(const std::shared_ptr<ContentLabel>& label, const std::shared_ptr<void>& context)  |  Appelé en cas de récupération réussie de l’étiquette.
public virtual void OnGetLabelFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Appelé en cas d’échec de la récupération de l’étiquette.
public virtual void OnGetProtectionSuccess(const std::shared_ptr<ProtectionHandler>& protectionHandler, const std::shared_ptr<void>& context)  |  Appelé en cas de récupération réussie de la stratégie de protection.
public virtual void OnGetProtectionFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Appelé en cas d’échec de la récupération de la stratégie de protection.
public virtual void OnCommitSuccess(bool committed, const std::shared_ptr<void>& context)  |  Appelé quand la validation des modifications du fichier a réussi.
public virtual void OnCommitFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Appelé en cas d’échec de la validation des modifications du fichier.
  
## <a name="members"></a>Membres
  
### <a name="oncreatefilehandlersuccess"></a>OnCreateFileHandlerSuccess
Appelé en cas de création réussie du gestionnaire.
  
### <a name="oncreatefilehandlerfailure"></a>OnCreateFileHandlerFailure
Appelé en cas d’échec de la création du gestionnaire.
  
### <a name="ongetlabelsuccess"></a>OnGetLabelSuccess
Appelé en cas de récupération réussie de l’étiquette.
  
### <a name="ongetlabelfailure"></a>OnGetLabelFailure
Appelé en cas d’échec de la récupération de l’étiquette.
  
### <a name="ongetprotectionsuccess"></a>OnGetProtectionSuccess
Appelé en cas de récupération réussie de la stratégie de protection.
  
### <a name="ongetprotectionfailure"></a>OnGetProtectionFailure
Appelé en cas d’échec de la récupération de la stratégie de protection.
  
### <a name="oncommitsuccess"></a>OnCommitSuccess
Appelé quand la validation des modifications du fichier a réussi.
  
### <a name="oncommitfailure"></a>OnCommitFailure
Appelé en cas d’échec de la validation des modifications du fichier.