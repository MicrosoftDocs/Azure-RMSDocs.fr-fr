---
title: mip::FileHandler, classe
description: Décrit la classe mip::filehandler de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: ee0545346eef2c143946496f56af77b7081b1e06
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "60184652"
---
# <a name="class-mipfilehandler"></a>mip::FileHandler, classe 
Interface pour toutes les fonctions de gestion de fichiers.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::shared_ptr\<ContentLabel\> GetLabel()  |  Démarre la récupération de l’étiquette de sensibilité à partir du fichier.
public std::shared_ptr\<ProtectionHandler\> GetProtection()  |  Démarre la récupération de la stratégie de protection à partir du fichier.
public ClassifyAsync void (const std::shared_ptr\<void\>& contexte)  |  Exécute les règles dans le gestionnaire et retourne la liste des actions à exécuter.
public void SetLabel(const std::string& labelId, const LabelingOptions& labelingOptions)  |  Définit l’étiquette de sensibilité sur le fichier.
public void DeleteLabel(const LabelingOptions& labelingOptions)  |  Supprime l’étiquette de sensibilité du fichier.
publique SetProtection void (const std::shared_ptr\<ProtectionDescriptor\>& protectionDescriptor)  |  Définit des autorisations personnalisées ou basées sur un modèle (en fonction de protectionDescriptor->GetProtectionType) pour le fichier.
public void SetProtection(const std::vector\<uint8_t\>& serializedPublishingLicense, const std::vector\<uint8_t\>& serializedProtectionInfo)  |  Définit des autorisations personnalisées ou basées sur modèle (en fonction de serializedPublishingLicense et serializedProtectionInfo) au fichier.
public void RemoveProtection()  |  Supprime la protection du fichier. Si le fichier porte une étiquette, celle-ci est perdue.
public void CommitAsync(const std::string& outputFilePath, const std::shared_ptr\<void\>& context) | Écrit les modifications dans le fichier spécifié par le paramètre \|outputFilePath\ |  .
public void CommitAsync(const std::shared_ptr\<Stream\>& outputStream, const std::shared_ptr\<void\>& context) | Écrit les modifications dans le flux spécifié par le paramètre \|outputStream\ |  .
public void GetDecryptedTemporaryFileAsync(const std::shared_ptr\<void\>& context)  |  Retourne un chemin d’accès dans un fichier temporaire (qui est supprimé si possible) - qui représente le contenu déchiffré.
public void NotifyCommitSuccessful(const std::string& actualFilePath)  |  À appeler quand les modifications ont été validées sur le disque.
public std::string GetOutputFileName()  |  Détermine le nom et l’extension du fichier de sortie en fonction du nom du fichier d’origine et des modifications cumulées.
  
## <a name="members"></a>Membres
  
### <a name="getlabel-function"></a>GetLabel (fonction)
Démarre la récupération de l’étiquette de sensibilité à partir du fichier.
  
### <a name="getprotection-function"></a>GetProtection (fonction)
Démarre la récupération de la stratégie de protection à partir du fichier.
  
### <a name="classifyasync-function"></a>ClassifyAsync (fonction)
Exécute les règles dans le gestionnaire et retourne la liste des actions à exécuter.

  
**Retourne**: Liste des actions qui doivent être appliquées sur le contenu.
  
### <a name="setlabel-function"></a>SetLabel (fonction)
Définit l’étiquette de sensibilité sur le fichier.
Les modifications ne sont pas écrites dans le fichier tant que CommitAsync n’est pas appelé. La méthode Privileged et Auto permet à l’API de substituer une étiquette existante. Lève [JustificationRequiredError](class_mip_justificationrequirederror.md) quand la définition de l’étiquette nécessite une justification de l’opération (via le paramètre labelingOptions).
  
### <a name="deletelabel-function"></a>DeleteLabel (fonction)
Supprime l’étiquette de sensibilité du fichier.
Les modifications ne sont pas écrites dans le fichier tant que CommitAsync n’est pas appelé. La méthode Privileged et Auto permet à l’API de substituer une étiquette existante. Lève [JustificationRequiredError](class_mip_justificationrequirederror.md) quand la définition de l’étiquette nécessite une justification de l’opération (via le paramètre labelingOptions).
  
### <a name="setprotection-function"></a>SetProtection (fonction)
Définit des autorisations personnalisées ou basées sur un modèle (en fonction de protectionDescriptor->GetProtectionType) pour le fichier.
Les modifications ne sont pas écrites dans le fichier tant que CommitAsync n’est pas appelé.
  
### <a name="setprotection-function"></a>SetProtection (fonction)
Définit des autorisations personnalisées ou basées sur modèle (en fonction de serializedPublishingLicense et serializedProtectionInfo) au fichier.
Les modifications ne sont pas écrites dans le fichier tant que CommitAsync n’est pas appelé.
  
### <a name="removeprotection-function"></a>RemoveProtection (fonction)
Supprime la protection du fichier. Si le fichier porte une étiquette, celle-ci est perdue.
Les modifications ne sont pas écrites dans le fichier tant que CommitAsync n’est pas appelé.
  
### <a name="commitasync-function"></a>CommitAsync (fonction)
Écrit les modifications dans le fichier spécifié par le paramètre |outputFilePath|.
[FileHandler::Observer](class_mip_filehandler_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="commitasync-function"></a>CommitAsync (fonction)
Écrit les modifications dans le flux spécifié par le paramètre |outputStream|.
[FileHandler::Observer](class_mip_filehandler_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="getdecryptedtemporaryfileasync-function"></a>GetDecryptedTemporaryFileAsync function
Retourne un chemin d’accès dans un fichier temporaire (qui est supprimé si possible) - qui représente le contenu déchiffré.
[FileHandler::Observer](class_mip_filehandler_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="notifycommitsuccessful-function"></a>NotifyCommitSuccessful (fonction)
À appeler quand les modifications ont été validées sur le disque.

Paramètres :  
* **actualFilePath**: Le chemin d’accès de fichier réel du fichier de sortie 


Déclenche un événement d’audit
  
### <a name="getoutputfilename-function"></a>GetOutputFileName function
Détermine le nom et l’extension du fichier de sortie en fonction du nom du fichier d’origine et des modifications cumulées.