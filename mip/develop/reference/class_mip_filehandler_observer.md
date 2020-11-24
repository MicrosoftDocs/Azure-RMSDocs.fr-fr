---
title: 'classe FileHandler :: observer'
description: 'Documente la classe fileHandler :: observer du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: d469271718d422216f6eaad905e60cd82e7f1244
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566950"
---
# <a name="class-filehandlerobserver"></a>classe FileHandler :: observer 
Interface Observer permettant aux clients d’obtenir les notifications des événements liés au gestionnaire de fichiers.
Toutes les erreurs héritent de mip::Error. Le client ne doit pas rappeler le moteur sur le thread qui appelle l’observateur.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public virtual void OnCreateFileHandlerSuccess(const std::shared_ptr\<FileHandler\>& fileHandler, const std::shared_ptr\<void\>& context)  |  Appelé en cas de création réussie du gestionnaire.
public virtual void OnCreateFileHandlerFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Appelé en cas d’échec de la création du gestionnaire.
public virtual void OnClassifySuccess (const std :: Vector \<std::shared_ptr\<Action\> \>& actions, const std :: shared_ptr \<void\>& Context)  |  Appelé lorsque la classification est réussie.
public virtual void OnClassifyFailure (const std :: exception_ptr& erreur, const std :: shared_ptr \<void\>& contexte)  |  Appelé lorsque la classification a échoué.
public virtual void OnGetDecryptedTemporaryFileSuccess (const std :: String& decryptedFilePath, const std :: shared_ptr \<void\>& Context)  |  Appelée lors de la réussite du fichier temporaire déchiffré.
public virtual void OnGetDecryptedTemporaryFileFailure (const std :: exception_ptr& erreur, const std :: shared_ptr \<void\>& contexte)  |  Appelée lors de l’échec de l’obtention du fichier temporaire déchiffré.
public virtual void OnGetDecryptedTemporaryStreamSuccess (const std :: shared_ptr \<Stream\>& decryptedStream, const std :: shared_ptr \<void\>& Context)  |  Appelée lors de la réussite du flux temporaire déchiffré.
public virtual void OnGetDecryptedTemporaryStreamFailure (const std :: exception_ptr& erreur, const std :: shared_ptr \<void\>& contexte)  |  Appelé lors de l’échec de l’obtention du flux de déchiffrement temporaire.
public virtual void OnCommitSuccess(bool committed, const std::shared_ptr\<void\>& context)  |  Appelé quand la validation des modifications du fichier a réussi.
public virtual void OnCommitFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Appelé en cas d’échec de la validation des modifications du fichier.
public virtual void OnInspectSuccess (const std :: shared_ptr \<FileInspector\>& fileInspector, const std :: shared_ptr \<void\>& Context)  |  Appelé lorsque l’inspection est réussie.
public virtual void OnInspectFailure (const std :: exception_ptr& erreur, const std :: shared_ptr \<void\>& contexte)  |  Appelé lorsque l’inspection a échoué.
  
## <a name="members"></a>Membres
  
### <a name="oncreatefilehandlersuccess-function"></a>OnCreateFileHandlerSuccess fonction)
Appelé en cas de création réussie du gestionnaire.
  
### <a name="oncreatefilehandlerfailure-function"></a>OnCreateFileHandlerFailure fonction)
Appelé en cas d’échec de la création du gestionnaire.
  
### <a name="onclassifysuccess-function"></a>OnClassifySuccess fonction)
Appelé lorsque la classification est réussie.
  
### <a name="onclassifyfailure-function"></a>OnClassifyFailure fonction)
Appelé lorsque la classification a échoué.
  
### <a name="ongetdecryptedtemporaryfilesuccess-function"></a>OnGetDecryptedTemporaryFileSuccess fonction)
Appelée lors de la réussite du fichier temporaire déchiffré.
  
### <a name="ongetdecryptedtemporaryfilefailure-function"></a>OnGetDecryptedTemporaryFileFailure fonction)
Appelée lors de l’échec de l’obtention du fichier temporaire déchiffré.
  
### <a name="ongetdecryptedtemporarystreamsuccess-function"></a>OnGetDecryptedTemporaryStreamSuccess fonction)
Appelée lors de la réussite du flux temporaire déchiffré.
  
### <a name="ongetdecryptedtemporarystreamfailure-function"></a>OnGetDecryptedTemporaryStreamFailure fonction)
Appelé lors de l’échec de l’obtention du flux de déchiffrement temporaire.
  
### <a name="oncommitsuccess-function"></a>OnCommitSuccess fonction)
Appelé quand la validation des modifications du fichier a réussi.
  
### <a name="oncommitfailure-function"></a>OnCommitFailure fonction)
Appelé en cas d’échec de la validation des modifications du fichier.
  
### <a name="oninspectsuccess-function"></a>OnInspectSuccess fonction)
Appelé lorsque l’inspection est réussie.
  
### <a name="oninspectfailure-function"></a>OnInspectFailure fonction)
Appelé lorsque l’inspection a échoué.