---
title: MetadataEntry de classe
description: 'Documente la classe metadataentry :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: c9c1c8f9683ebb4be079f1817aa92a71e72005ca
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81766505"
---
# <a name="class-metadataentry"></a>MetadataEntry de classe 
Classe d’abstraction pour l’entrée de métadonnées.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public MetadataEntry (const std :: String& clé, const std :: String& valeur, unsigned int version)  |  Au c’Tor pour une abstraction MetadataEntry.
public MetadataEntry (const std :: String& clé, const std :: String& valeur)  |  Au c’Tor pour une abstraction MetadataEntry, version est définie à une valeur par défaut de 0.
public const std :: String& GetKey () const  |  Obtient la clé de l’entrée de métadonnées.
public const std :: String& GetValue () const  |  Obtient la valeur de l’entrée de métadonnées.
public unsigned int GetVersion () const  |  Obtient la version de l’entrée de métadonnées.
  
## <a name="members"></a>Membres
  
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