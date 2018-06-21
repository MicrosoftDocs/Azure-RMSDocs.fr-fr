# <a name="class-mipstream"></a>mip::Stream, classe 
Classe qui définit l’interface entre le SDK MIP et le contenu basé sur le flux de données (Stream).
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public int64_t Read(uint8_t* buffer, int64_t bufferLength)  |  Lire dans une mémoire tampon à partir du flux.
 public int64_t Write(const uint8_t* buffer, int64_t bufferLength)  |  Écrire dans le flux à partir d’une mémoire tampon.
 public bool Flush()  |  Vider le flux.
 public void Seek(uint64_t position)  |  Rechercher une position spécifique dans le flux.
 public bool CanRead() const  |  Vérifier si le flux est accessible en lecture.
 public bool CanWrite() const  |  Vérifier si le flux est accessible en écriture.
 public uint64_t Position()  |  Obtenir la position actuelle dans le flux.
 public uint64_t Size()  |  Obtenir la taille du contenu dans le flux.
 public void Size(uint64_t value)  |  Définir la taille du flux.
public std::shared_ptr<Stream> Clone()  |  Cloner le flux.
  
## <a name="members"></a>Membres
  
### <a name="read"></a>Lire
Lire dans une mémoire tampon à partir du flux.

Paramètres :  
* **buffer** : pointeur vers une mémoire tampon 


* **bufferLength** : taille de la mémoire tampon. 



  
**Retourne** : le nombre d’octets réellement lus.
  
### <a name="write"></a>Écrire
Écrire dans le flux à partir d’une mémoire tampon.

Paramètres :  
* **buffer** : pointeur vers une mémoire tampon 


* **bufferLength** : taille de la mémoire tampon. 



  
**Retourne** : le nombre d’octets réellement lus.
  
### <a name="flush"></a>Purge
Vider le flux.

  
**Retourne** : true en cas de réussite ; sinon, false.
  
### <a name="seek"></a>Seek
Rechercher une position spécifique dans le flux.

Paramètres :  
* **position** : position à laquelle rechercher dans le flux.


  
### <a name="canread"></a>CanRead
Vérifier si le flux est accessible en lecture.

  
**Retourne** : true s’il est accessible en lecture ; sinon, false.
  
### <a name="canwrite"></a>CanWrite
Vérifier si le flux est accessible en écriture.

  
**Retourne** : true s’il est accessible en écriture ; sinon, false.
  
### <a name="position"></a>Position
Obtenir la position actuelle dans le flux.

  
**Retourne** : la position dans le flux.
  
### <a name="size"></a>Size
Obtenir la taille du contenu dans le flux.

  
**Retourne** : la taille du flux.
  
### <a name="size"></a>Size
Définir la taille du flux.

Paramètres :  
* **stream** : taille.


  
### <a name="stream"></a>Flux
Cloner le flux.

  
**Retourne** : le nouveau flux.