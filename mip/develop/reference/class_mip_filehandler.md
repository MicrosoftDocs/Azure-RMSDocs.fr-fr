---
title: mip::FileHandler, classe
description: 'Documente la classe MIP :: fileHandler du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: b2a6e3cd6de886c3e3983442a1ec7185b688b662
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "73558842"
---
# <a name="class-mipfilehandler"></a>mip::FileHandler, classe 
Interface pour toutes les fonctions de gestion de fichiers.
  
## <a name="summary"></a>Table des matières
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std :: shared_ptr\<ContentLabel\> GetLabel ()  |  Démarre la récupération de l’étiquette de sensibilité à partir du fichier.
public std :: shared_ptr\<ProtectionHandler\> GetProtection ()  |  Démarre la récupération de la stratégie de protection à partir du fichier.
public void ClassifyAsync (const std :: shared_ptr\<void\>& Context)  |  Exécute les règles dans le gestionnaire et retourne la liste des actions à exécuter.
public void InspectAsync (const std :: shared_ptr\<void\>& Context)  |  Crée un objet d’inspecteur de fichier, utilisé pour récupérer le contenu d’un fichier à partir de formats de fichiers compatibles.
public void SetLabel (const std :: shared_ptr\<étiquette\>& étiquette, const LabelingOptions & labelingOptions, const ProtectionSettings & protectionSettings)  |  Définit l’étiquette de sensibilité sur le fichier.
public void DeleteLabel(const LabelingOptions& labelingOptions)  |  Supprime l’étiquette de sensibilité du fichier.
public void SetProtection (const std :: shared_ptr\<ProtectionDescriptor\>& protectionDescriptor, const ProtectionSettings & protectionSettings)  |  Définit des autorisations personnalisées ou basées sur un modèle (en fonction de protectionDescriptor->GetProtectionType) pour le fichier.
public void SetProtection (const std :: shared_ptr\<ProtectionHandler\>& protectionHandler)  |  Définit la protection d’un document à l’aide d’un gestionnaire de protection existant.
public void RemoveProtection()  |  Supprime la protection du fichier. Si le fichier porte une étiquette, celle-ci est perdue.
public void CommitAsync(const std::string& outputFilePath, const std::shared_ptr\<void\>& context) | Écrit les modifications dans le fichier spécifié par le paramètre \|outputFilePath\ |  .
public void CommitAsync (const std :: shared_ptr\<flux\>& outputStream, const std :: shared_ptr\<void\>contexte &) | Écrit les modifications dans le flux spécifié par le paramètre \|outputStream\ |  .
public bool IsModified ()  |  Vérifie s’il existe des modifications à valider dans le fichier.
public void GetDecryptedTemporaryFileAsync (const std :: shared_ptr\<void\>& Context)  |  Retourne un chemin d’accès à un fichier temporaire (qui sera supprimé si possible), représentant le contenu déchiffré.
public void GetDecryptedTemporaryStreamAsync (const std :: shared_ptr\<void\>& Context)  |  Retourne un flux représentant le contenu déchiffré.
public void NotifyCommitSuccessful (const std :: String & actualFilePath)  |  À appeler quand les modifications ont été validées sur le disque.
public std::string GetOutputFileName()  |  Détermine le nom et l’extension du fichier de sortie en fonction du nom du fichier d’origine et des modifications cumulées.
public static bool IsProtected (const std :: String & filePath, const std :: shared_ptr<MipContext>& mipContext) | Vérifie si un fichier est protégé ou non.
public static FILE_API std :: Vector&lt;uint8_t&gt; __CDECL MIP :: FileHandler :: GetSerializedPublishingLicense | Retourne la licence de publication si le fichier en contient.

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
Les modifications ne sont pas écrites dans le fichier tant que CommitAsync n’est pas appelé. La méthode Privileged et auto permet à l’API de remplacer n’importe quelle étiquette existante lève JustificationRequiredError quand la définition de l’étiquette nécessite que l’opération soit justifiée (via le paramètre labelingOptions).
  
### <a name="deletelabel-function"></a>DeleteLabel fonction)
Supprime l’étiquette de sensibilité du fichier.
Les modifications ne sont pas écrites dans le fichier tant que CommitAsync n’est pas appelé. La méthode Privileged et auto permet à l’API de remplacer n’importe quelle étiquette existante lève JustificationRequiredError quand la définition de l’étiquette nécessite que l’opération soit justifiée (via le paramètre labelingOptions).
  
### <a name="setprotection-function"></a>SetProtection fonction)
Définit des autorisations personnalisées ou basées sur un modèle (en fonction de protectionDescriptor->GetProtectionType) pour le fichier.
Les modifications ne sont pas écrites dans le fichier tant que CommitAsync n’est pas appelé.
  
### <a name="setprotection-function"></a>SetProtection fonction)
Définit la protection d’un document à l’aide d’un gestionnaire de protection existant.
Les modifications ne sont pas écrites dans le fichier tant que CommitAsync n’est pas appelé.
  
### <a name="removeprotection-function"></a>RemoveProtection fonction)
Supprime la protection du fichier. Si le fichier porte une étiquette, celle-ci est perdue.
Les modifications ne sont pas écrites dans le fichier tant que CommitAsync n’est pas appelé.
  
### <a name="commitasync-function"></a>CommitAsync fonction)
Écrit les modifications dans le fichier spécifié par le paramètre |outputFilePath|.
FileHandler :: observer est appelé en cas de réussite ou d’échec.
  
### <a name="commitasync-function"></a>CommitAsync fonction)
Écrit les modifications dans le flux spécifié par le paramètre |outputStream|.
FileHandler :: observer est appelé en cas de réussite ou d’échec.
  
### <a name="ismodified-function"></a>IsModified fonction)
Vérifie s’il existe des modifications à valider dans le fichier.
Les modifications ne sont pas écrites dans le fichier tant que CommitAsync n’est pas appelé.
  
### <a name="getdecryptedtemporaryfileasync-function"></a>GetDecryptedTemporaryFileAsync fonction)
Retourne un chemin d’accès à un fichier temporaire (qui sera supprimé si possible), représentant le contenu déchiffré.
FileHandler :: observer est appelé en cas de réussite ou d’échec.
  
### <a name="getdecryptedtemporarystreamasync-function"></a>GetDecryptedTemporaryStreamAsync fonction)
Retourne un flux représentant le contenu déchiffré.
FileHandler :: observer est appelé en cas de réussite ou d’échec.
  
### <a name="notifycommitsuccessful-function"></a>NotifyCommitSuccessful fonction)
À appeler quand les modifications ont été validées sur le disque.

Paramètres :  
* **actualFilePath**: chemin d’accès réel du fichier de sortie 


Déclenche un événement d’audit
  
### <a name="getoutputfilename-function"></a>GetOutputFileName fonction)
Détermine le nom et l’extension du fichier de sortie en fonction du nom du fichier d’origine et des modifications cumulées.

### <a name="isprotected-function"></a>IsProtected fonction)
Vérifie si un fichier est protégé ou non.

### <a name="getserializedpublishinglicense-function"></a>GetSerializedPublishingLicense fonction)
Retourne la licence de publication si le fichier en contient.