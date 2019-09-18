---
title: mip::FileHandler, classe
description: 'Documente la classe MIP :: fileHandler du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: f7ffac2409b23c3f1a9c426f8151804b538d47c4
ms.sourcegitcommit: 9cedac6569f3a33a22a721da27074a438b1a7882
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71070642"
---
# <a name="class-mipfilehandler"></a>mip::FileHandler, classe 
Interface pour toutes les fonctions de gestion de fichiers.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std :: shared_ptr\<ContentLabel\> getLabel ()  |  Démarre la récupération de l’étiquette de sensibilité à partir du fichier.
public std :: shared_ptr\<ProtectionHandler\> GetProtection ()  |  Démarre la récupération de la stratégie de protection à partir du fichier.
public void ClassifyAsync (const std :: shared_ptr\<void\>& Context)  |  Exécute les règles dans le gestionnaire et retourne la liste des actions à exécuter.
public void InspectAsync (const std :: shared_ptr\<void\>& Context)  |  Crée un objet d’inspecteur de fichier, utilisé pour récupérer le contenu d’un fichier à partir de formats de fichiers compatibles.
public void setLabel (const std :: shared_ptr\<étiquette\>& label, const LabelingOptions & LabelingOptions, const ProtectionSettings & ProtectionSettings)  |  Définit l’étiquette de sensibilité sur le fichier.
public void DeleteLabel(const LabelingOptions& labelingOptions)  |  Supprime l’étiquette de sensibilité du fichier.
public void SetProtection (const std :: shared_ptr\<ProtectionDescriptor\>& ProtectionDescriptor, const ProtectionSettings & ProtectionSettings)  |  Définit des autorisations personnalisées ou basées sur un modèle (en fonction de protectionDescriptor->GetProtectionType) pour le fichier.
public void RemoveProtection()  |  Supprime la protection du fichier. Si le fichier porte une étiquette, celle-ci est perdue.
public void CommitAsync(const std::string& outputFilePath, const std::shared_ptr\<void\>& context) | Écrit les modifications dans le fichier spécifié par le paramètre \|outputFilePath\ |  .
public void CommitAsync (const std :: shared_ptr\<flux\>& OutputStream, const std :: shared_ptr\<void\>& Context) | Écrit les modifications dans le flux spécifié par le paramètre \|outputStream\ |  .
public void GetDecryptedTemporaryFileAsync (const std :: shared_ptr\<void\>& Context)  |  Retourne un chemin d’accès à un fichier temporaire (qui sera supprimé si possible), représentant le contenu déchiffré.
public void GetDecryptedTemporaryStreamAsync (const std :: shared_ptr\<void\>& Context)  |  Retourne un flux représentant le contenu déchiffré.
public void NotifyCommitSuccessful (const std :: String & actualFilePath)  |  À appeler quand les modifications ont été validées sur le disque.
public std::string GetOutputFileName()  |  Détermine le nom et l’extension du fichier de sortie en fonction du nom du fichier d’origine et des modifications cumulées.
public static bool IsProtected (const std :: String & FilePath, const std :: shared_ptr<MipContext>& mipContext) | Vérifie si un fichier est protégé ou non.
public static FILE_API std :: Vector&lt;uint8_t&gt; _ _ cdecl Mip :: fileHandler :: GetSerializedPublishingLicense | Retourne la licence de publication si le fichier en contient.
## <a name="members"></a>Membres
  
### <a name="getlabel-function"></a>GetLabel fonction)
Démarre la récupération de l’étiquette de sensibilité à partir du fichier.
  
### <a name="getprotection-function"></a>GetProtection fonction)
Démarre la récupération de la stratégie de protection à partir du fichier.
  
### <a name="classifyasync-function"></a>ClassifyAsync fonction)
Exécute les règles dans le gestionnaire et retourne la liste des actions à exécuter.

  
**Retourne**: Liste des actions qui doivent être appliquées au contenu.
  
### <a name="inspectasync-function"></a>InspectAsync fonction)
Crée un objet d’inspecteur de fichier, utilisé pour récupérer le contenu d’un fichier à partir de formats de fichiers compatibles.

  
**Retourne**: Inspecteur de fichier.
  
### <a name="setlabel-function"></a>SetLabel fonction)
Définit l’étiquette de sensibilité sur le fichier.
Les modifications ne sont pas écrites dans le fichier tant que CommitAsync n’est pas appelé. La méthode Privileged et Auto permet à l’API de substituer une étiquette existante. Lève [JustificationRequiredError](class_mip_justificationrequirederror.md) quand la définition de l’étiquette nécessite une justification de l’opération (via le paramètre labelingOptions).
  
### <a name="deletelabel-function"></a>DeleteLabel fonction)
Supprime l’étiquette de sensibilité du fichier.
Les modifications ne sont pas écrites dans le fichier tant que CommitAsync n’est pas appelé. La méthode Privileged et Auto permet à l’API de substituer une étiquette existante. Lève [JustificationRequiredError](class_mip_justificationrequirederror.md) quand la définition de l’étiquette nécessite une justification de l’opération (via le paramètre labelingOptions).
  
### <a name="setprotection-function"></a>SetProtection fonction)
Définit des autorisations personnalisées ou basées sur un modèle (en fonction de protectionDescriptor->GetProtectionType) pour le fichier.
Les modifications ne sont pas écrites dans le fichier tant que CommitAsync n’est pas appelé.
  
### <a name="removeprotection-function"></a>RemoveProtection fonction)
Supprime la protection du fichier. Si le fichier porte une étiquette, celle-ci est perdue.
Les modifications ne sont pas écrites dans le fichier tant que CommitAsync n’est pas appelé.
  
### <a name="commitasync-function"></a>CommitAsync fonction)
Écrit les modifications dans le fichier spécifié par le paramètre |outputFilePath|.
[FileHandler::Observer](class_mip_filehandler_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="commitasync-function"></a>CommitAsync fonction)
Écrit les modifications dans le flux spécifié par le paramètre |outputStream|.
[FileHandler::Observer](class_mip_filehandler_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="getdecryptedtemporaryfileasync-function"></a>GetDecryptedTemporaryFileAsync fonction)
Retourne un chemin d’accès à un fichier temporaire (qui sera supprimé si possible), représentant le contenu déchiffré.
[FileHandler::Observer](class_mip_filehandler_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="getdecryptedtemporarystreamasync-function"></a>GetDecryptedTemporaryStreamAsync fonction)
Retourne un flux représentant le contenu déchiffré.
[FileHandler::Observer](class_mip_filehandler_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="notifycommitsuccessful-function"></a>NotifyCommitSuccessful fonction)
À appeler quand les modifications ont été validées sur le disque.

Paramètres :  
* **actualFilePath**: Chemin d’accès réel du fichier de sortie 


Déclenche un événement d’audit
  
### <a name="getoutputfilename-function"></a>GetOutputFileName fonction)
Détermine le nom et l’extension du fichier de sortie en fonction du nom du fichier d’origine et des modifications cumulées.

### <a name="isprotected-function"></a>IsProtected fonction)
Vérifie si un fichier est protégé ou non.


### <a name="getserializedpublishinglicense-function"></a>GetSerializedPublishingLicense fonction)
Retourne la licence de publication si le fichier en contient.
