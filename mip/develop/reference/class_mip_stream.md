---
title: mip::Stream, classe
description: Décrit la classe mip::stream de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 1987aea2e90a3ded3a55f509e3d49a689d361c62
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "60185111"
---
# <a name="class-mipstream"></a>mip::Stream, classe 
Classe qui définit l’interface entre le SDK MIP et le contenu basé sur le flux de données (Stream).
  
## <a name="summary"></a>Récapitulatif
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
  
### <a name="read-function"></a>Read (fonction)
Lire dans une mémoire tampon à partir du flux.

Paramètres :  
* **buffer** : pointeur vers une mémoire tampon 


* **bufferLength** : taille de la mémoire tampon. 



  
**Retourne**: Nombre d’octets lus.
  
### <a name="write-function"></a>Écrire (fonction)
Écrire dans le flux à partir d’une mémoire tampon.

Paramètres :  
* **buffer** : pointeur vers une mémoire tampon 


* **bufferLength** : taille de la mémoire tampon. 



  
**Retourne**: Nombre d’octets écrits.
  
### <a name="flush-function"></a>Flush (fonction)
Vider le flux.

  
**Retourne**: True si l’opération réussit ; sinon, false.
  
### <a name="seek-function"></a>Seek (fonction)
Rechercher une position spécifique dans le flux.

Paramètres :  
* **position** : position à laquelle rechercher dans le flux.


  
### <a name="canread-function"></a>CanRead (fonction)
Vérifier si le flux est accessible en lecture.

  
**Retourne**: True si elle est lisible ; sinon, false.
  
### <a name="canwrite-function"></a>CanWrite (fonction)
Vérifier si le flux est accessible en écriture.

  
**Retourne**: True si elle est accessible en écriture ; sinon, false.
  
### <a name="position-function"></a>Position, fonction
Obtenir la position actuelle dans le flux.

  
**Retourne**: Position dans le flux.
  
### <a name="size-function"></a>Fonction de la taille
Obtenir la taille du contenu dans le flux.

  
**Retourne**: La taille du flux.
  
### <a name="size-function"></a>Fonction de la taille
Définir la taille du flux.

Paramètres :  
* **stream** : taille.

