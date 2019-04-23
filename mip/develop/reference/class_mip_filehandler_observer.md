---
title: mip::FileHandler::Observer, classe
description: Décrit la classe mip::filehandler de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 4204bd17abe756c42c672a1cda17706b59600795
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "60184686"
---
# <a name="class-mipfilehandlerobserver"></a>mip::FileHandler::Observer, classe 
Interface [Observer](class_mip_filehandler_observer.md) permettant aux clients d’obtenir les notifications des événements liés au gestionnaire de fichiers.
Toutes les erreurs héritent de [mip::Error](class_mip_error.md). Le client ne doit pas rappeler le moteur sur le thread qui appelle l’observateur.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public OnCreateFileHandlerSuccess void virtuel (const std::shared_ptr\<FileHandler\>& Gestionnaire de fichiers, const std::shared_ptr\<void\>& contexte)  |  Appelé en cas de création réussie du gestionnaire.
public OnCreateFileHandlerFailure void virtuel (std::exception_ptr const & erreur, const std::shared_ptr\<void\>& contexte)  |  Appelé en cas d’échec de la création du gestionnaire.
public OnClassifySuccess void virtuel (const std::vector\<std::shared_ptr\<Action\>\>& actions, const std::shared_ptr\<void\>& contexte)  |  Appelée lorsque classer de réussite.
public OnClassifyFailure void virtuel (std::exception_ptr const & erreur, const std::shared_ptr\<void\>& contexte)  |  Appelée lorsque classifier a échoué.
public virtual void OnGetDecryptedTemporaryFileSuccess(const std::string& decryptedFilePath, const std::shared_ptr\<void\>& context)  |  Appelé lors de l’obtention de la réussite d’un fichier temporaire déchiffré.
public OnGetDecryptedTemporaryFileFailure void virtuel (std::exception_ptr const & erreur, const std::shared_ptr\<void\>& contexte)  |  Appelé lors de l’obtention du fichier temporaire déchiffré a échoué.
public OnCommitSuccess void virtuel (bool validée, const std::shared_ptr\<void\>& contexte)  |  Appelé quand la validation des modifications du fichier a réussi.
public OnCommitFailure void virtuel (std::exception_ptr const & erreur, const std::shared_ptr\<void\>& contexte)  |  Appelé en cas d’échec de la validation des modifications du fichier.
  
## <a name="members"></a>Membres
  
### <a name="oncreatefilehandlersuccess-function"></a>OnCreateFileHandlerSuccess (fonction)
Appelé en cas de création réussie du gestionnaire.
  
### <a name="oncreatefilehandlerfailure-function"></a>OnCreateFileHandlerFailure (fonction)
Appelé en cas d’échec de la création du gestionnaire.
  
### <a name="onclassifysuccess-function"></a>OnClassifySuccess (fonction)
Appelée lorsque classer de réussite.
  
### <a name="onclassifyfailure-function"></a>OnClassifyFailure (fonction)
Appelée lorsque classifier a échoué.
  
### <a name="ongetdecryptedtemporaryfilesuccess-function"></a>OnGetDecryptedTemporaryFileSuccess (fonction)
Appelé lors de l’obtention de la réussite d’un fichier temporaire déchiffré.
  
### <a name="ongetdecryptedtemporaryfilefailure-function"></a>OnGetDecryptedTemporaryFileFailure function
Appelé lors de l’obtention du fichier temporaire déchiffré a échoué.
  
### <a name="oncommitsuccess-function"></a>OnCommitSuccess (fonction)
Appelé quand la validation des modifications du fichier a réussi.
  
### <a name="oncommitfailure-function"></a>OnCommitFailure (fonction)
Appelé en cas d’échec de la validation des modifications du fichier.