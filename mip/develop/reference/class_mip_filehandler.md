---
title: FileHandler de classe
description: 'Documente la classe fileHandler :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: fe04fd0303d5f5717690206760125932826f4708
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763168"
---
# <a name="class-filehandler"></a>FileHandler de classe 
Interface pour toutes les fonctions de gestion de fichiers.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std :: shared_ptr\<ContentLabel\> getLabel ()  |  Démarre la récupération de l’étiquette de sensibilité à partir du fichier.
public std :: shared_ptr\<ProtectionHandler\> GetProtection ()  |  Démarre la récupération de la stratégie de protection à partir du fichier.
public void ClassifyAsync (const std :: shared_ptr\<void\>& Context)  |  Exécute les règles dans le gestionnaire et retourne la liste des actions à exécuter.
public void InspectAsync (const std :: shared_ptr\<void\>& Context)  |  Crée un objet d’inspecteur de fichier, utilisé pour récupérer le contenu d’un fichier à partir de formats de fichiers compatibles.
public void SetLabel (const std :: shared_ptr\<étiquette\>& étiquette, const LabelingOptions& LabelingOptions, const ProtectionSettings& ProtectionSettings)  |  Définit l’étiquette de sensibilité sur le fichier.
public void DeleteLabel(const LabelingOptions& labelingOptions)  |  Supprime l’étiquette de sensibilité du fichier.
public void SetProtection (const std :: shared_ptr\<protectionDescriptor\>& ProtectionDescriptor, const ProtectionSettings& ProtectionSettings)  |  Définit des autorisations personnalisées ou basées sur un modèle (en fonction de protectionDescriptor->GetProtectionType) pour le fichier.
public void SetProtection (const std :: shared_ptr\<protectionHandler\>& ProtectionHandler)  |  Définit la protection d’un document à l’aide d’un gestionnaire de protection existant.
public void RemoveProtection()  |  Supprime la protection du fichier. Si le format de fichier d’origine ne prend pas en charge l’étiquetage, l’étiquette sera perdue lorsque la protection sera supprimée. Lorsque le format natif prend en charge l’étiquetage, les métadonnées d’étiquette sont conservées.
public void CommitAsync (const std :: String& outputFilePath, const std :: shared_ptr\<void\>& Context) | Écrit les modifications dans le fichier spécifié par le paramètre \|outputFilePath\ |  paramètre.
public void CommitAsync (const std :: shared_ptr\<flux\>& OutputStream, const std :: shared_ptr\<void\>& Context) | Écrit les modifications dans le flux spécifié par le paramètre \|outputStream\ |  paramètre.
public bool IsModified ()  |  Vérifie s’il existe des modifications à valider dans le fichier.
public void GetDecryptedTemporaryFileAsync (const std :: shared_ptr\<void\>& Context)  |  Retourne un chemin d’accès à un fichier temporaire (qui sera supprimé si possible), représentant le contenu déchiffré.
public void GetDecryptedTemporaryStreamAsync (const std :: shared_ptr\<void\>& Context)  |  Retourne un flux représentant le contenu déchiffré.
public void NotifyCommitSuccessful (const std :: String& actualFilePath)  |  À appeler quand les modifications ont été validées sur le disque.
public std::string GetOutputFileName()  |  Détermine le nom et l’extension du fichier de sortie en fonction du nom du fichier d’origine et des modifications cumulées.
  
## <a name="members"></a>Membres
  
### <a name="getlabel-function"></a>GetLabel fonction)
Démarre la récupération de l’étiquette de sensibilité à partir du fichier.
  
### <a name="getprotection-function"></a>GetProtection fonction)
Démarre la récupération de la stratégie de protection à partir du fichier.
  
### <a name="classifyasync-function"></a>ClassifyAsync fonction)
Exécute les règles dans le gestionnaire et retourne la liste des actions à exécuter.

  
**Retourne** : une liste des actions à appliquer au contenu.
  
### <a name="inspectasync-function"></a>InspectAsync fonction)
Crée un objet d’inspecteur de fichier, utilisé pour récupérer le contenu d’un fichier à partir de formats de fichiers compatibles.

  
**Retourne**: un inspecteur de fichier.
  
### <a name="setlabel-function"></a>SetLabel fonction)
Définit l’étiquette de sensibilité sur le fichier.
Les modifications ne sont pas écrites dans le fichier tant que CommitAsync n’est pas appelé. La méthode Privileged et Auto permet à l’API de substituer une étiquette existante. Lève [JustificationRequiredError](class_mip_justificationrequirederror.md) quand la définition de l’étiquette nécessite une justification de l’opération (via le paramètre labelingOptions).
  
### <a name="deletelabel-function"></a>DeleteLabel fonction)
Supprime l’étiquette de sensibilité du fichier.
Les modifications ne sont pas écrites dans le fichier tant que CommitAsync n’est pas appelé. La méthode Privileged et Auto permet à l’API de substituer une étiquette existante. Lève JustificationRequiredError quand la définition de l’étiquette nécessite une justification de l’opération (via le paramètre labelingOptions).
  
### <a name="setprotection-function"></a>SetProtection fonction)
Définit des autorisations personnalisées ou basées sur un modèle (en fonction de protectionDescriptor->GetProtectionType) pour le fichier.
Les modifications ne sont pas écrites dans le fichier tant que CommitAsync n’est pas appelé.
  
### <a name="setprotection-function"></a>SetProtection fonction)
Définit la protection d’un document à l’aide d’un gestionnaire de protection existant.
Les modifications ne sont pas écrites dans le fichier tant que CommitAsync n’est pas appelé.
  
### <a name="removeprotection-function"></a>RemoveProtection fonction)
Supprime la protection du fichier. Si le format de fichier d’origine ne prend pas en charge l’étiquetage, l’étiquette sera perdue lorsque la protection sera supprimée. Lorsque le format natif prend en charge l’étiquetage, les métadonnées d’étiquette sont conservées.
Les modifications ne sont pas écrites dans le fichier tant que CommitAsync n’est pas appelé.
  
### <a name="commitasync-function"></a>CommitAsync fonction)
Écrit les modifications dans le fichier spécifié par le paramètre |outputFilePath|.
FileHandler::Observer est appelé en cas de réussite ou d’échec.
  
### <a name="commitasync-function"></a>CommitAsync fonction)
Écrit les modifications dans le flux spécifié par le paramètre |outputStream|.
FileHandler::Observer est appelé en cas de réussite ou d’échec.
  
### <a name="ismodified-function"></a>IsModified fonction)
Vérifie s’il existe des modifications à valider dans le fichier.
Les modifications ne sont pas écrites dans le fichier tant que CommitAsync n’est pas appelé.
  
### <a name="getdecryptedtemporaryfileasync-function"></a>GetDecryptedTemporaryFileAsync fonction)
Retourne un chemin d’accès à un fichier temporaire (qui sera supprimé si possible), représentant le contenu déchiffré.
FileHandler::Observer est appelé en cas de réussite ou d’échec.
  
### <a name="getdecryptedtemporarystreamasync-function"></a>GetDecryptedTemporaryStreamAsync fonction)
Retourne un flux représentant le contenu déchiffré.
FileHandler::Observer est appelé en cas de réussite ou d’échec.
  
### <a name="notifycommitsuccessful-function"></a>NotifyCommitSuccessful fonction)
À appeler quand les modifications ont été validées sur le disque.

Paramètres :  
* **actualFilePath**: chemin d’accès réel du fichier de sortie 


Déclenche un événement d’audit
  
### <a name="getoutputfilename-function"></a>GetOutputFileName fonction)
Détermine le nom et l’extension du fichier de sortie en fonction du nom du fichier d’origine et des modifications cumulées.