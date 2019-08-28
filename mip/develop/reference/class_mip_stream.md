---
title: mip::Stream, classe
description: 'Documente la classe MIP:: Stream du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: c799708931103c595ce1ad66a41accb9f0dcfc85
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70056841"
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
  
### <a name="read-function"></a>Read, fonction
Lire dans une mémoire tampon à partir du flux.

Paramètres :  
* **buffer** : pointeur vers une mémoire tampon 


* **bufferLength** : taille de la mémoire tampon. 



  
**Retourne**: Nombre d’octets lus.
  
### <a name="write-function"></a>Write, fonction
Écrire dans le flux à partir d’une mémoire tampon.

Paramètres :  
* **buffer** : pointeur vers une mémoire tampon 


* **bufferLength** : taille de la mémoire tampon. 



  
**Retourne**: Nombre d’octets écrits.
  
### <a name="flush-function"></a>Flush, fonction
Vider le flux.

  
**Retourne**: True en cas de réussite, sinon false.
  
### <a name="seek-function"></a>Seek, fonction
Rechercher une position spécifique dans le flux.

Paramètres :  
* **position** : position à laquelle rechercher dans le flux.


  
### <a name="canread-function"></a>CanRead, fonction
Vérifier si le flux est accessible en lecture.

  
**Retourne**: True si readed else est false.
  
### <a name="canwrite-function"></a>CanWrite, fonction
Vérifier si le flux est accessible en écriture.

  
**Retourne**: True s’il est accessible en écriture. sinon, false.
  
### <a name="position-function"></a>Position, fonction
Obtenir la position actuelle dans le flux.

  
**Retourne**: Position dans le flux.
  
### <a name="size-function"></a>Size, fonction
Obtenir la taille du contenu dans le flux.

  
**Retourne**: Taille du flux.
  
### <a name="size-function"></a>Size, fonction
Définir la taille du flux.

Paramètres :  
* **stream** : taille.

