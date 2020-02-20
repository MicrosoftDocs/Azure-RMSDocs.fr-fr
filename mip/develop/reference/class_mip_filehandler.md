---
title: mip::FileHandler, classe
description: 'Documente la classe MIP :: fileHandler du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 52c28c1763fc3e7513f98a23a18cb6c91e0ed508
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77488736"
---
# <a name="class-mipfilehandler"></a>mip::FileHandler, classe 
Interface pour toutes les fonctions de gestion de fichiers.
  
## <a name="summary"></a>Résumé
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
public void CommitAsync (const std :: String & outputFilePath, const std :: shared_ptr\<void\>contexte &) | Écrit les modifications dans le fichier spécifié par le paramètre \|outputFilePath\ |  .
public void CommitAsync (const std :: shared_ptr\<flux\>& outputStream, const std :: shared_ptr\<void\>contexte &) | Écrit les modifications dans le flux spécifié par le paramètre \|outputStream\ |  .
public bool IsModified ()  |  Vérifie s’il existe des modifications à valider dans le fichier.
public void GetDecryptedTemporaryFileAsync (const std :: shared_ptr\<void\>& Context)  |  Retourne un chemin d’accès à un fichier temporaire (qui sera supprimé si possible), représentant le contenu déchiffré.
public void GetDecryptedTemporaryStreamAsync (const std :: shared_ptr\<void\>& Context)  |  Retourne un flux représentant le contenu déchiffré.
public void NotifyCommitSuccessful (const std :: String & actualFilePath)  |  À appeler quand les modifications ont été validées sur le disque.
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