# <a name="class-mipistream"></a>mip::IStream, classe 
Interface de base pour les flux protégés.
Portée à partir de Windows::Storage::Streams::IRandomAccessStream::IRandomAccessStream et Windows::Storage::Streams::FileRandomAccessStream::FileRandomAccessStream. [https://msdn.microsoft.com/en-us/library/windows/apps/windows.storage.streams.irandomaccessstream.aspx](https://msdn.microsoft.com/en-us/library/windows/apps/windows.storage.streams.irandomaccessstream.aspx)[https://msdn.microsoft.com/en-us/library/windows/apps/windows.storage.streams.filerandomaccessstream.aspx](https://msdn.microsoft.com/en-us/library/windows/apps/windows.storage.streams.filerandomaccessstream.aspx)
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::shared_future<int64_t> ReadAsync(uint8_t* pbBuffer, int64_t cbBuffer, int64_t cbOffset, std::launch launchType)  |  Lit un bloc de données à partir d’un flux de manière asynchrone.
public std::shared_future<int64_t> WriteAsync(const uint8_t* cpbBuffer, int64_t cbBuffer, int64_t cbOffset, std::launch launchType)  |  Écrit un bloc de données dans un flux de manière asynchrone.
public std::future<bool> FlushAsync(std::launch launchType)  |  Vide la mémoire tampon du flux de sortie de manière asynchrone.
public int64_t Read(uint8_t* pbBuffer, int64_t cbBuffer)  |  Lit un bloc de données à partir d’un flux de manière synchrone.
public int64_t Write(const uint8_t* cpbBuffer, int64_t cbBuffer)  |  Écrit un bloc de données dans un flux de manière synchrone.
public bool Flush()  |  Vide la mémoire tampon du flux de sortie de manière synchrone.
public SharedStream Clone()  |  Clone le flux.
public void Seek(uint64_t u64Position)  |  Recherche une position dans le flux.
public bool CanRead() const  |  Obtient une valeur déterminant si le flux peut être lu.
public bool CanWrite() const  |  Obtient une valeur déterminant si le flux peut être écrit.
public uint64_t Position()  |  Obtient la position actuelle du flux à partir du début (en octets)
public uint64_t Size()  |  Obtient la taille du flux (en octets)
public void Size(uint64_t u64Value)  |  Définit la taille du flux (en octets)
public inline virtual std::vector<uint8_t> Read(uint64_t u64size)  |  Lit un bloc de données à partir d’un flux de manière synchrone.
  
## <a name="members"></a>Membres
  
### <a name="readasync"></a>ReadAsync
Lit un bloc de données à partir d’un flux de manière asynchrone.
  
#### <a name="parameters"></a>Paramètres
* pbBuffer : mémoire tampon dans laquelle le flux doit être lu 
* cbBuffer : taille de la mémoire tampon 
* cbOffset : décalage à partir du début du flux d’entrée où la lecture doit commencer 
* launchType : type de lancement asynchrone
  
#### <a name="returns"></a>Returns
future asynchrone contenant le nombre réel d’octets lus. Assurez-vous que la mémoire tampon existe jusqu’à ce que le résultat soit récupéré à partir de std::future
  
### <a name="writeasync"></a>WriteAsync
Écrit un bloc de données dans un flux de manière asynchrone.
  
#### <a name="parameters"></a>Paramètres
* cpbBuffer : mémoire tampon de données à écrire 
* cbBuffer : taille de la mémoire tampon 
* cbOffset : décalage à partir du début du flux de sortie où l’écriture doit commencer 
* launchType : type de lancement asynchrone
  
#### <a name="returns"></a>Returns
future asynchrone contenant le nombre réel d’octets écrits. Assurez-vous que la mémoire tampon existe jusqu’à ce que le résultat soit récupéré à partir de std::future
  
### <a name="flushasync"></a>FlushAsync
Vide la mémoire tampon du flux de sortie de manière asynchrone.
  
#### <a name="parameters"></a>Paramètres
* launchType : type de lancement asynchrone
  
#### <a name="returns"></a>Returns
future asynchrone contenant une valeur indiquant si le vidage a réussi
  
### <a name="read"></a>Lire
Lit un bloc de données à partir d’un flux de manière synchrone.
  
#### <a name="parameters"></a>Paramètres
* pbBuffer : mémoire tampon dans laquelle le flux doit être lu 
* cbBuffer : taille de la mémoire tampon
  
#### <a name="returns"></a>Returns
Nombre réel d’octets lus
  
### <a name="write"></a>Écrire
Écrit un bloc de données dans un flux de manière synchrone.
  
#### <a name="parameters"></a>Paramètres
* cpbBuffer : mémoire tampon de données à écrire 
* cbBuffer : taille de la mémoire tampon
  
#### <a name="returns"></a>Returns
Nombre réel d’octets écrits
  
### <a name="flush"></a>Purge
Vide la mémoire tampon du flux de sortie de manière synchrone.
  
#### <a name="returns"></a>Returns
Une valeur indiquant si le vidage a réussi
  
### <a name="sharedstream"></a>SharedStream
Clone le flux.
  
#### <a name="returns"></a>Returns
Flux cloné
  
### <a name="seek"></a>Seek
Recherche une position dans le flux.
  
#### <a name="parameters"></a>Paramètres
* u64Position : décalage d’octet à partir du début du flux
  
### <a name="canread"></a>CanRead
Obtient une valeur déterminant si le flux peut être lu.
  
#### <a name="returns"></a>Returns
Une valeur déterminant si le flux peut être lu
  
### <a name="canwrite"></a>CanWrite
Obtient une valeur déterminant si le flux peut être écrit.
  
#### <a name="returns"></a>Returns
Une valeur déterminant si le flux peut être écrit
  
### <a name="position"></a>Position
Obtient la position actuelle du flux à partir du début (en octets)
  
#### <a name="returns"></a>Returns
Position actuelle du flux à partir du début (en octets)
  
### <a name="size"></a>Size
Obtient la taille du flux (en octets)
  
#### <a name="returns"></a>Returns
Taille du flux (en octets)
  
### <a name="size"></a>Size
Définit la taille du flux (en octets)
  
#### <a name="parameters"></a>Paramètres
* u64Value : taille du flux (en octets)
  
### <a name="read"></a>Lire
Lit un bloc de données à partir d’un flux de manière synchrone.
  
#### <a name="parameters"></a>Paramètres
* u64size : taille des données à lire (en octets)
  
#### <a name="returns"></a>Returns
Vecteur des données réellement lues