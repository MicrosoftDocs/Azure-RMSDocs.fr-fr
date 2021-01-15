---
title: MetadataEntry de classe
description: 'Documente la classe metadataentry :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: dd758d49d0c207fe5e4c5eeb04bb63ba91174fcc
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98215185"
---
# <a name="class-metadataentry"></a>MetadataEntry de classe 
Classe d’abstraction pour l’entrée de métadonnées.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public MetadataEntry (const std :: String& clé, const std :: String& value, uint32_t version)  |  Au c’Tor pour une abstraction MetadataEntry.
public MetadataEntry (const std :: String& clé, const std :: String& valeur, const MetadataVersion& version)  |  Au c’Tor pour une abstraction MetadataEntry.
public MetadataEntry (const std :: String& clé, const std :: String& valeur)  |  Au c’Tor pour une abstraction MetadataEntry, version est définie à une valeur par défaut de 0.
public const std :: String& GetKey () const  |  Obtient la clé de l’entrée de métadonnées.
public const std :: String& GetValue () const  |  Obtient la valeur de l’entrée de métadonnées.
public MetadataVersion GetVersion () const  |  Obtient la version de l’entrée de métadonnées.
  
## <a name="members"></a>Membres
  
### <a name="metadataentry-function"></a>MetadataEntry fonction)
Au c’Tor pour une abstraction MetadataEntry.

Paramètres :  
* **clé**: entrée de clé de métadonnées. 


* **valeur**: entrée de valeur de métadonnées 


* **version**: valeur de la version des métadonnées


  
### <a name="metadataentry-function"></a>MetadataEntry fonction)
Au c’Tor pour une abstraction MetadataEntry.

Paramètres :  
* **clé**: entrée de clé de métadonnées. 


* **valeur**: entrée de valeur de métadonnées 


* **version**: valeur de la version des métadonnées


  
### <a name="metadataentry-function"></a>MetadataEntry fonction)
Au c’Tor pour une abstraction MetadataEntry, version est définie à une valeur par défaut de 0.

Paramètres :  
* **clé**: entrée de clé de métadonnées. 


* **valeur**: entrée de valeur de métadonnées


  
### <a name="getkey-function"></a>GetKey fonction)
Obtient la clé de l’entrée de métadonnées.

  
**Retourne**: clé d’entrée de métadonnées.
  
### <a name="getvalue-function"></a>GetValue, fonction
Obtient la valeur de l’entrée de métadonnées.

  
**Retourne**: valeur d’entrée de métadonnées.
  
### <a name="getversion-function"></a>GetVersion, fonction
Obtient la version de l’entrée de métadonnées.

  
**Retourne**: version d’entrée de métadonnées.