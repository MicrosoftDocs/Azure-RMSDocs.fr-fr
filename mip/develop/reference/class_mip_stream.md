---
title: Flux de classe
description: 'Documente la classe Stream :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: b2c8be3d6997985b62933d40bf855e48a20ca928
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764335"
---
# <a name="class-stream"></a>Flux de classe 
Classe qui définit l’interface entre le SDK MIP et le contenu basé sur le flux de données (Stream).
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public int64_t Read(uint8_t* buffer, int64_t bufferLength)  |  Lire dans une mémoire tampon à partir du flux.
public int64_t Write(const uint8_t* buffer, int64_t bufferLength)  |  Écrire dans le flux à partir d’une mémoire tampon.
public bool Flush()  |  Vider le flux.
public void Seek(int64_t position)  |  Rechercher une position spécifique dans le flux.
public bool CanRead() const  |  Vérifier si le flux est accessible en lecture.
public bool CanWrite() const  |  Vérifier si le flux est accessible en écriture.
public int64_t Position()  |  Obtenir la position actuelle dans le flux.
public int64_t Size()  |  Obtenir la taille du contenu dans le flux.
public void Size(int64_t value)  |  Définir la taille du flux.
  
## <a name="members"></a>Membres
  
### <a name="read-function"></a>Read, fonction
Lire dans une mémoire tampon à partir du flux.

Paramètres :  
* **buffer** : pointeur vers une mémoire tampon 


* **bufferLength** : taille de la mémoire tampon. 



  
**Retourne** : nombre d’octets lus.
  
### <a name="write-function"></a>Write, fonction
Écrire dans le flux à partir d’une mémoire tampon.

Paramètres :  
* **buffer** : pointeur vers une mémoire tampon 


* **bufferLength** : taille de la mémoire tampon. 



  
**Retourne** : nombre d’octets écrits.
  
### <a name="flush-function"></a>Flush, fonction
Vider le flux.

  
**Retourne** : true en cas de réussite ; sinon, false.
  
### <a name="seek-function"></a>Seek (fonction)
Rechercher une position spécifique dans le flux.

Paramètres :  
* **position** : position à laquelle rechercher dans le flux.


  
### <a name="canread-function"></a>CanRead, fonction
Vérifier si le flux est accessible en lecture.

  
**Retourne** : true s’il est accessible en lecture ; sinon, false.
  
### <a name="canwrite-function"></a>CanWrite, fonction
Vérifier si le flux est accessible en écriture.

  
**Retourne** : true s’il est accessible en écriture ; sinon, false.
  
### <a name="position-function"></a>Position, fonction
Obtenir la position actuelle dans le flux.

  
**Retourne** : la position dans le flux.
  
### <a name="size-function"></a>Size, fonction
Obtenir la taille du contenu dans le flux.

  
**Retourne** : la taille du flux.
  
### <a name="size-function"></a>Size, fonction
Définir la taille du flux.

Paramètres :  
* **stream** : taille.

