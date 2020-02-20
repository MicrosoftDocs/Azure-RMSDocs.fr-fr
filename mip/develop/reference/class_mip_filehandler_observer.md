---
title: mip::FileHandler::Observer, classe
description: 'Documente la classe MIP :: fileHandler du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 86043ab5fdcc22884ce3c483d43947d46e51ac9c
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490011"
---
# <a name="class-mipfilehandlerobserver"></a>mip::FileHandler::Observer, classe 
Interface observer permettant aux clients d’obtenir des événements de notification liés au gestionnaire de fichiers.
Toutes les erreurs héritent de MIP :: Error. Le client ne doit pas rappeler le moteur sur le thread qui appelle l’observateur.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public virtual void OnCreateFileHandlerSuccess (const std :: shared_ptr\<FileHandler\>& fileHandler, const std :: shared_ptr\<void\>contexte &)  |  Appelé en cas de création réussie du gestionnaire.
public virtual void OnCreateFileHandlerFailure (const std :: exception_ptr & erreur, const std :: shared_ptr\<void\>contexte &)  |  Appelé en cas d’échec de la création du gestionnaire.
public virtual void OnClassifySuccess (const std :: Vector\<std :: shared_ptr\<action\>\>& actions, const std :: shared_ptr\<void\>& contexte)  |  Appelé lorsque la classification est réussie.
public virtual void OnClassifyFailure (const std :: exception_ptr & erreur, const std :: shared_ptr\<void\>contexte &)  |  Appelé lorsque la classification a échoué.
public virtual void OnGetDecryptedTemporaryFileSuccess (const std :: String & decryptedFilePath, const std :: shared_ptr\<void\>contexte &)  |  Appelée lors de la réussite du fichier temporaire déchiffré.
public virtual void OnGetDecryptedTemporaryFileFailure (const std :: exception_ptr & erreur, const std :: shared_ptr\<void\>contexte &)  |  Appelée lors de l’échec de l’obtention du fichier temporaire déchiffré.
public virtual void OnGetDecryptedTemporaryStreamSuccess (const std :: shared_ptr\<flux\>& decryptedStream, const std :: shared_ptr\<void\>& contexte)  |  Appelée lors de la réussite du flux temporaire déchiffré.
public virtual void OnGetDecryptedTemporaryStreamFailure (const std :: exception_ptr & erreur, const std :: shared_ptr\<void\>contexte &)  |  Appelé lors de l’échec de l’obtention du flux de déchiffrement temporaire.
public virtual void OnCommitSuccess (bool validée, const std :: shared_ptr\<void\>& Context)  |  Appelé quand la validation des modifications du fichier a réussi.
public virtual void OnCommitFailure (const std :: exception_ptr & erreur, const std :: shared_ptr\<void\>contexte &)  |  Appelé en cas d’échec de la validation des modifications du fichier.
public virtual void OnInspectSuccess (const std :: shared_ptr\<FileInspector\>& fileInspector, const std :: shared_ptr\<void\>contexte &)  |  Appelé lorsque l’inspection est réussie.
public virtual void OnInspectFailure (const std :: exception_ptr & erreur, const std :: shared_ptr\<void\>contexte &)  |  Appelé lorsque l’inspection a échoué.
  
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