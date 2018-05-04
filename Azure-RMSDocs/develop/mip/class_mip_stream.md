# <a name="class-mipstream"></a>mip::Stream, classe 
Classe qui définit l’interface entre le mip sdk et le contenu basé sur le flux de données (Stream).
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public int64_t Read | Lire dans une mémoire tampon à partir du flux.
public int64_t Write | Écrire dans le flux à partir d’une mémoire tampon.
public bool Flush | Vider le flux.
public void Seek | Rechercher une position spécifique dans le flux.
public bool CanRead | Vérifier si le flux est accessible en lecture.
public bool CanWrite | Vérifier si le flux est accessible en écriture.
public uint64_t Position | Obtenir la position actuelle dans le flux.
public uint64_t Size | Obtenir la taille du contenu dans le flux.
public void Size | Définir la taille du flux.
public std::shared_ptr< Stream > Clone | Cloner le flux.
## <a name="members"></a>Membres
### <a name="read"></a>Lire
Lire dans une mémoire tampon à partir du flux.
#### <a name="parameters"></a>Paramètres
* buffer : pointeur vers une mémoire tampon 
* bufferLength : taille de la mémoire tampon. 
#### <a name="returns"></a>Returns
le nombre d’octets lus.
### <a name="write"></a>Écrire
Écrire dans le flux à partir d’une mémoire tampon.
#### <a name="parameters"></a>Paramètres
* buffer : pointeur vers une mémoire tampon 
* bufferLength : taille de la mémoire tampon. 
#### <a name="returns"></a>Returns
le nombre d’octets lus.
### <a name="flush"></a>Purge
Vider le flux.
#### <a name="returns"></a>Returns
true en cas de réussite ; sinon, false.
### <a name="seek"></a>Seek
Rechercher une position spécifique dans le flux.
#### <a name="parameters"></a>Paramètres
* position : position à rechercher dans le flux.
### <a name="canread"></a>CanRead
Vérifier si le flux est accessible en lecture.
#### <a name="returns"></a>Returns
true s’il est accessible en lecture ; sinon, false.
### <a name="canwrite"></a>CanWrite
Vérifier si le flux est accessible en écriture.
#### <a name="returns"></a>Returns
true s’il est accessible en écriture ; sinon, false.
### <a name="position"></a>Position
Obtenir la position actuelle dans le flux.
#### <a name="returns"></a>Returns
la position dans le flux.
### <a name="size"></a>Size
Obtenir la taille du contenu dans le flux.
#### <a name="returns"></a>Returns
la taille du flux.
### <a name="size"></a>Size
Définir la taille du flux.
#### <a name="parameters"></a>Paramètres
* stream size : taille du flux.
### <a name="stream"></a>Flux
Cloner le flux.
#### <a name="returns"></a>Returns
le nouveau flux.