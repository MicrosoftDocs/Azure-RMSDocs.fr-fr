---
# required metadata

title: Exemples de code Linux | Azure RMS
description: Cette rubrique présente les éléments de code et les scénarios importants pour la version Linux du Kit RMS SDK.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 11acef4b-67f8-4e45-a0e7-d9310213b5f9

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿# Exemples de code Linux

Cette rubrique présente les éléments de code et les scénarios importants pour la version Linux du Kit RMS SDK.

Les extraits de code ci-dessous sont tirés des exemples d’applications *rms\_sample* et *rmsauth\_sample*. Pour plus d’informations, consultez [samples](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples) dans le dépôt GitHub.

-   [**Scénario** : Accéder aux informations de stratégie de protection à partir d’un fichier protégé](#scenario__access_protection_policy_information_from_a___protected_file)
-   [**Scénario** : Créer un fichier protégé à l’aide d’un modèle](#scenario__create_a_new_protected_file_using_a_template)
-   [**Scénario** : Protéger un fichier à l’aide de la protection personnalisée](#scenario__protect_a_file_using_custom_protection)
-   [WorkerThread - méthode prise en charge](#workerthread_-_a_supporting_method)
-   [**Scénario** : Authentification RMS](#scenario__rms_authentication)

## Scénario : Accéder aux informations de stratégie de protection à partir d’un fichier protégé

**Ouvre et lit un fichier protégé RMS**
**Source** : [rms\_sample/mainwindow.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**Description** : Après obtention d’un nom de fichier auprès de l’utilisateur, lecture des certificats (voir *MainWindow::addCertificates*), configuration du rappel d’autorisation avec l’ID client et l’URL de redirection, appel de *ConvertFromPFile* (voir l’exemple de code suivant), puis lecture de la description, de la date de validité du contenu et du nom de la stratégie de protection.

**C++** :

    void MainWindow::ConvertFromPFILE(const string&amp; fileIn,
        const string&amp; clientId,
        const string&amp; redirectUrl,
        const string&amp; clientEmail) 
    {
    // add trusted certificates using HttpHelpers of RMS and Auth SDKs
    addCertificates();
    
    // create shared in/out streams
    auto inFile = make_shared&lt;ifstream&gt;(
    fileIn, ios_base::in | ios_base::binary);
    
    if (!inFile-&gt;is_open()) {
     AddLog(&quot;ERROR: Failed to open &quot;, fileIn.c_str());
    return;
    }
    
    string fileOut;
    
    // generate output filename
    auto pos = fileIn.find_last_of(&#39;.&#39;);
    
    if (pos != string::npos) {
     fileOut = fileIn.substr(0, pos);
    }
    
     // create streams
    auto outFile = make_shared&lt;fstream&gt;(
    fileOut, ios_base::in | ios_base::out | ios_base::trunc | ios_base::binary);
    
    if (!outFile-&gt;is_open()) {
     AddLog(&quot;ERROR: Failed to open &quot;, fileOut.c_str());
     return;
      }
    
    try
    {
    // create authentication context
    AuthCallback auth(clientId, redirectUrl);
    
    // process convertion
    auto pfs = PFileConverter::ConvertFromPFile(
      clientEmail,
      inFile,
      outFile,
      auth,
      this-&gt;consent);
    
    AddLog(&quot;Successfully converted to &quot;, fileOut.c_str());
    }
    catch (const rmsauth::Exception&amp; e)
    {
    AddLog(&quot;ERROR: &quot;, e.error().c_str());
    }
    catch (const rmscore::exceptions::RMSException&amp; e) {
    AddLog(&quot;ERROR: &quot;, e.what());
    }
    inFile-&gt;close();
    outFile-&gt;close();
    }

**Créer un flux de fichier protégé**
**Source** : [rms\_sample/pfileconverter.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**Description** : Cette méthode crée un flux de fichier protégé à partir du flux de sauvegarde passé par le biais de la méthode du SDK, *ProtectedFileStream::Aquire*, qui est ensuite retourné à l’appelant.

**C++** :

    shared_ptr&lt;GetProtectedFileStreamResult&gt;PFileConverter::ConvertFromPFile(
    const string           &amp; userId,
    shared_ptr&lt;istream&gt;      inStream,
    shared_ptr&lt;iostream&gt;     outStream,
    IAuthenticationCallback&amp; auth,
    IConsentCallback       &amp; consent)
    {
    auto inIStream = rmscrypto::api::CreateStreamFromStdStream(inStream);
    
    auto fsResult = ProtectedFileStream::Acquire(
    inIStream,
    userId,
    auth,
    consent,
    POL_None,
    static_cast&lt;ResponseCacheFlags&gt;(RESPONSE_CACHE_INMEMORY
                                    | RESPONSE_CACHE_ONDISK));
    
    if ((fsResult.get() != nullptr) &amp;&amp; (fsResult-&gt;m_status == Success) &amp;&amp;
      (fsResult-&gt;m_stream != nullptr)) {
    auto pfs = fsResult-&gt;m_stream;
    
    // preparing
    readPosition  = 0;
    writePosition = 0;
    totalSize     = pfs-&gt;Size();
    
    // start threads
    for (size_t i = 0; i &lt; THREADS_NUM; ++i) {
      threadPool.push_back(thread(WorkerThread,
                                  static_pointer_cast&lt;iostream&gt;(outStream), pfs,
                                  false));
    }
    
    for (thread&amp; t: threadPool) {
      if (t.joinable()) {
        t.join();
      }
    }
    }
      return fsResult;
    }

## Scénario : Créer un fichier protégé à l’aide d’un modèle

**Protège un fichier avec un modèle sélectionné par l’utilisateur**
**Source** : [rms\_sample/mainwindow.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**Description** : Après obtention d’un nom de fichier auprès de l’utilisateur, lecture des certificats (voir *MainWindow::addCertificates*) et configuration du rappel d’autorisation avec l’ID client et l’URL de redirection, le fichier sélectionné est protégé en appelant *ConvertToPFileTemplates* (voir l’exemple de code suivant).

**C++** :

    void MainWindow::ConvertToPFILEUsingTemplates(const string&amp; fileIn,
                                              const string&amp; clientId,
                                              const string&amp; redirectUrl,
                                              const string&amp; clientEmail) 
    {
    // generate output filename
    string fileOut = fileIn + &quot;.pfile&quot;;
    
    // add trusted certificates using HttpHelpers of RMS and Auth SDKs
    addCertificates();
    
    // create shared in/out streams
    auto inFile = make_shared&lt;ifstream&gt;(
    fileIn, ios_base::in | ios_base::binary);
    auto outFile = make_shared&lt;fstream&gt;(
    fileOut, ios_base::in | ios_base::out | ios_base::trunc | ios_base::binary);
    
    if (!inFile-&gt;is_open()) {
    AddLog(&quot;ERROR: Failed to open &quot;, fileIn.c_str());
    return;
    }
    
    if (!outFile-&gt;is_open()) {
    AddLog(&quot;ERROR: Failed to open &quot;, fileOut.c_str());
    return;
    }
    
    // find file extension
    string fileExt;
    auto   pos = fileIn.find_last_of(&#39;.&#39;);
    
    if (pos != string::npos) {
    fileExt = fileIn.substr(pos);
    }
    
    try {
    // create authentication callback
    AuthCallback auth(clientId, redirectUrl);
    
    // process convertion
    PFileConverter::ConvertToPFileTemplates(
      clientEmail, inFile, fileExt, outFile, auth,
      this-&gt;consent, this-&gt;templates);
    
    AddLog(&quot;Successfully converted to &quot;, fileOut.c_str());
    }
   catch (const rmsauth::Exception&amp; e) {
    AddLog(&quot;ERROR: &quot;, e.error().c_str());
    outFile-&gt;close();
    remove(fileOut.c_str());
    }
    catch (const rmscore::exceptions::RMSException&amp; e) {
    AddLog(&quot;ERROR: &quot;, e.what());
    
    outFile-&gt;close();
    remove(fileOut.c_str());
    }
    inFile-&gt;close();
    outFile-&gt;close();
    }


**Protège un fichier à l’aide d’une stratégie créée à partir d’un modèle**
**Source** : [rms\_sample/pfileconverter.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**Description**: Une liste de modèles associés à l’utilisateur est récupérée et le modèle sélectionné est ensuite utilisé pour créer une stratégie qui, à son tour, est utilisée pour protéger le fichier.

**C++** :

    void PFileConverter::ConvertToPFileTemplates(const string           &amp; userId,
                                             shared_ptr&lt;istream&gt;      inStream,
                                             const string           &amp; fileExt,
                                             std::shared_ptr&lt;iostream&gt;outStream,
                                             IAuthenticationCallback&amp; auth,
                                             IConsentCallback&amp; /*consent*/,
                                             ITemplatesCallback     &amp; templ)
    {
    auto templates = TemplateDescriptor::GetTemplateList(userId, auth);
    
    rmscore::modernapi::AppDataHashMap signedData;
    
    size_t pos = templ.SelectTemplate(templates);
    
    if (pos &lt; templates.size()) {
    auto policy = UserPolicy::CreateFromTemplateDescriptor(
      templates[pos],
      userId,
      auth,
      USER_AllowAuditedExtraction,
      signedData);
   
    ConvertToPFileUsingPolicy(policy, inStream, fileExt, outStream);
    }
    }

**Protège un fichier conformément à une stratégie**
**Source** : [rms\_sample/pfileconverter.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**Description**: Créer un flux de fichier protégé à l’aide de la stratégie donnée, puis protéger ce fichier.

**C++** :

    void PFileConverter::ConvertToPFileUsingPolicy(shared_ptr&lt;UserPolicy&gt;   policy,
                                               shared_ptr&lt;istream&gt;      inStream,
                                               const string           &amp; fileExt,
                                               std::shared_ptr&lt;iostream&gt;outStream)
    {
    if (policy.get() != nullptr) {
    auto outIStream = rmscrypto::api::CreateStreamFromStdStream(outStream);
    auto pStream    = ProtectedFileStream::Create(policy, outIStream, fileExt);
    
    // preparing
    readPosition  = 0;
    writePosition = pStream-&gt;Size();
    
    inStream-&gt;seekg(0, ios::end);
    totalSize = inStream-&gt;tellg();
    
    // start threads
    for (size_t i = 0; i &lt; THREADS_NUM; ++i) {
      threadPool.push_back(thread(WorkerThread,
                                  static_pointer_cast&lt;iostream&gt;(inStream),
                                  pStream,
                                  true));
    }
    
    for (thread&amp; t: threadPool) {
      if (t.joinable()) {
        t.join();
      }
    }
    
    pStream-&gt;Flush();
    }
    


## Scénario : Protéger un fichier à l’aide de la protection personnalisée

**Protège un fichier à l’aide de la protection personnalisée**
**Source** : [rms\_sample/mainwindow.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**Description** : Après obtention d’un nom de fichier auprès de l’utilisateur, lecture des certificats (voir *MainWindow::addCertificates*), collecte des informations sur les droits auprès de l’utilisateur et configuration du rappel d’autorisation avec l’ID client et l’URL de redirection, le fichier sélectionné est protégé en appelant *ConvertToPFileTemplates* (voir l’exemple de code suivant).

**C++** :

    void MainWindow::ConvertToPFILEUsingRights(const string            &amp; fileIn,
                                           const vector&lt;UserRights&gt;&amp; userRights,
                                           const string            &amp; clientId,
                                           const string            &amp; redirectUrl,
                                           const string            &amp; clientEmail)
    {
    // generate output filename
    string fileOut = fileIn + &quot;.pfile&quot;;
    
    // add trusted certificates using HttpHelpers of RMS and Auth SDKs
    addCertificates();
    
    // create shared in/out streams
    auto inFile = make_shared&lt;ifstream&gt;(
    fileIn, ios_base::in | ios_base::binary);
    auto outFile = make_shared&lt;fstream&gt;(
    fileOut, ios_base::in | ios_base::out | ios_base::trunc | ios_base::binary);
    
    if (!inFile-&gt;is_open()) {
    AddLog(&quot;ERROR: Failed to open &quot;, fileIn.c_str());
    return;
    }
    
    if (!outFile-&gt;is_open()) {
    AddLog(&quot;ERROR: Failed to open &quot;, fileOut.c_str());
    return;
    }
    
    // find file extension
    string fileExt;
    auto   pos = fileIn.find_last_of(&#39;.&#39;);
    
    if (pos != string::npos) {
    fileExt = fileIn.substr(pos);
    }
    
    // is anything to add
    if (userRights.size() == 0) {
    AddLog(&quot;ERROR: &quot;, &quot;Please fill email and check rights&quot;);
    return;
    }
    
    
    try {
    // create authentication callback
    AuthCallback auth(clientId, redirectUrl);
    
    // process convertion
    PFileConverter::ConvertToPFilePredefinedRights(
      clientEmail,
      inFile,
      fileExt,
      outFile,
      auth,
      this-&gt;consent,
      userRights);
    
    AddLog(&quot;Successfully converted to &quot;, fileOut.c_str());
    }
    catch (const rmsauth::Exception&amp; e) {
    AddLog(&quot;ERROR: &quot;, e.error().c_str());
    
    outFile-&gt;close();
    remove(fileOut.c_str());
    }
    catch (const rmscore::exceptions::RMSException&amp; e) {
    AddLog(&quot;ERROR: &quot;, e.what());
    
    outFile-&gt;close();
    remove(fileOut.c_str());
    }
    inFile-&gt;close();
    outFile-&gt;close();
    }


**Crée une stratégie de protection en fonction des droits de l’utilisateur sélectionnés**
**Source** : [rms\_sample/pfileconverter.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**Description** : Créer un descripteur de stratégie et le remplir avec les informations sur les droits de l’utilisateur, puis utiliser le descripteur de stratégie pour créer une stratégie utilisateur. Cette stratégie est utilisée pour protéger le fichier sélectionné par le biais d’un appel à *ConvertToPFileUsingPolicy* (voir la description fournie dans une section précédente de cette rubrique).

**C++** :

    void PFileConverter::ConvertToPFilePredefinedRights(
    const string            &amp; userId,
    shared_ptr&lt;istream&gt;       inStream,
    const string            &amp; fileExt,
    shared_ptr&lt;iostream&gt;      outStream,
    IAuthenticationCallback &amp; auth,
    IConsentCallback&amp; /*consent*/,
    const vector&lt;UserRights&gt;&amp; userRights)
    {
    auto endValidation = chrono::system_clock::now() + chrono::hours(48);
    
    
    PolicyDescriptor desc(userRights);
    
    desc.Referrer(make_shared&lt;string&gt;(&quot;https://client.test.app&quot;));
    desc.ContentValidUntil(endValidation);
    desc.AllowOfflineAccess(false);
    desc.Name(&quot;Test Name&quot;);
    desc.Description(&quot;Test Description&quot;);
    
    auto policy = UserPolicy::Create(desc, userId, auth,
                                   USER_AllowAuditedExtraction);
    ConvertToPFileUsingPolicy(policy, inStream, fileExt, outStream);
    

## WorkerThread - méthode prise en charge


La méthode *WorkerThread()* est appelée par deux des exemples de scénarios précédents (**Créer un flux de fichier protégé** et **Protège un fichier conformément à une stratégie**) de la manière suivante :

**C++** :

    threadPool.push_back(thread(WorkerThread,
                                  static_pointer_cast&lt;iostream&gt;(outStream), pfs,
                                  false));


**Méthode de prise en charge, WorkerThread()**

**C++** :

    static mutex   threadLocker;
    static int64_t totalSize     = 0;
    static int64_t readPosition  = 0;
    static int64_t writePosition = 0;
    static vector&lt;thread&gt; threadPool;
    
    static void WorkerThread(shared_ptr&lt;iostream&gt;           stdStream,
                         shared_ptr&lt;ProtectedFileStream&gt;pStream,
                         bool                           modeWrite) {
    vector&lt;uint8_t&gt; buffer(4096);
    int64_t bufferSize = static_cast&lt;int64_t&gt;(buffer.size());
    
    while (totalSize - readPosition &gt; 0) {
    // lock
    threadLocker.lock();
    
    // check remain
    if (totalSize - readPosition &lt;= 0) {
      threadLocker.unlock();
      return;
    }
    
    // get read/write offset
    int64_t offsetRead  = readPosition;
    int64_t offsetWrite = writePosition;
    int64_t toProcess   = min(bufferSize, totalSize - readPosition);
    readPosition  += toProcess;
    writePosition += toProcess;
    
    // no need to lock more
    threadLocker.unlock();
    
    if (modeWrite) {
      // stdStream is not thread safe!!!
      try {
        threadLocker.lock();
    
        stdStream-&gt;seekg(offsetRead);
        stdStream-&gt;read(reinterpret_cast&lt;char *&gt;(&amp;buffer[0]), toProcess);
        threadLocker.unlock();
        auto written =
          pStream-&gt;WriteAsync(
            buffer.data(), toProcess, offsetWrite, std::launch::deferred).get();
    
        if (written != toProcess) {
          throw rmscore::exceptions::RMSStreamException(&quot;Error while writing data&quot;);
        }
      }
      catch (exception&amp; e) {
        qDebug() &lt;&lt; &quot;Exception: &quot; &lt;&lt; e.what();
      }
    } else {
      auto read =
        pStream-&gt;ReadAsync(&amp;buffer[0],
                           toProcess,
                           offsetRead,
                           std::launch::deferred).get();
    
      if (read == 0) {
        break;
      }
    
      try {
        // stdStream is not thread safe!!!
        threadLocker.lock();
    
        // seek to write
        stdStream-&gt;seekp(offsetWrite);
        stdStream-&gt;write(reinterpret_cast&lt;const char *&gt;(buffer.data()), read);
        threadLocker.unlock();
      }
      catch (exception&amp; e) {
        qDebug() &lt;&lt; &quot;Exception: &quot; &lt;&lt; e.what();
      }
    }
    }
    }


## Scénario : Authentification RMS

Les exemples suivants montrent deux approches d’authentification : obtention d’un jeton oAuth2 d’authentification Azure avec interface utilisateur et sans interface utilisateur.
**Acquisition de jeton d’authentification oAuth2 avec l’interface utilisateur**
**Source** : [rmsauth\_sample/mainwindow.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rmsauth_sample)

**Étape 1** : Créer un point partagé de l’objet **rmsauth::FileCache**
Description : Vous pouvez définir le chemin du cache ou utiliser la valeur par défaut.

**C++** :

    auto FileCachePtr = std::make_shared&lt; rmsauth::FileCache&gt;();


**Étape 2** : Créer l’objet **rmsauth::AuthenticationContext**
Description : Spécifier l’*URI d’autorité* Azure et l’objet *FileCache*.

**C++** :

    AuthenticationContext authContext(
                              std::string(“https://sts.aadrm.com/_sts/oauth/authorize”),
                              AuthorityValidationType::False,
                              FileCachePtr);


**Étape 3** : Appeler la méthode **acquireToken** de l’objet **authContext** et spécifier les paramètres suivants :
Description :

-   *Ressource demandée* : Ressource protégée à laquelle vous souhaitez accéder
-   *ID du client unique* : Généralement un GUID
-   *URI de redirection* : URI qui sera réadressé après récupération du jeton d’authentification
-   *Comportement de l’invite d’authentification* : Si vous définissez **PromptBehavior::Auto**, la bibliothèque essaie d’utiliser le cache et d’actualiser le jeton si nécessaire
-   *ID d’utilisateur* : Nom d’utilisateur affiché dans la fenêtre d’invite

**C++** :

    auto result = authContext.acquireToken(
                std::string(“api.aadrm.com”),
                std::string(“4a63455a-cfa1-4ac6-bd2e-0d046cf1c3f7”),
                std::string(“https://client.test.app”),
                PromptBehavior::Auto,
                std::string(“john.smith@msopentechtest01.onmicrosoft.com”));


**Étape 4** : Obtenir le jeton d’accès à partir du résultat
Description : Appeler la méthode **result-&gt; accessToken()**

**Remarque**  Toutes les méthodes de bibliothèque d’authentification peuvent lever **rmsauth::Exception**

 
**Acquisition de jeton d’authentification oAuth2 sans interface utilisateur**
**Source** : [rmsauth\_sample/mainwindow.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rmsauth_sample)

**Étape 1** : Créer un point partagé de l’objet **rmsauth::FileCache**
Description : Vous pouvez définir le chemin du cache ou utiliser la valeur par défaut

**C++** :

    auto FileCachePtr = std::make_shared&lt; rmsauth::FileCache&gt;();


**Étape 2** : Créer l’objet **UserCredential**
Description : Spécifier la *connexion utilisateur* et le *mot de passe*

**C++** :

    auto userCred = std::make_shared&lt;UserCredential&gt;(&quot;john.smith@msopentechtest01.onmicrosoft.com&quot;,
                                                 &quot;SomePass&quot;);


**Étape 3** : Créer l’objet **rmsauth::AuthenticationContext**
Description : Spécifier l’*URI d’autorité* Azure et l’objet *FileCache*

**C++** :

    AuthenticationContext authContext(
                        std::string(“https://sts.aadrm.com/_sts/oauth/authorize”),
                        AuthorityValidationType::False,
                        FileCachePtr);


**Étape 4** : Appeler la méthode **acquireToken** de **authContext** et spécifier les paramètres :
-   *Ressource demandée* : Ressource protégée à laquelle vous souhaitez accéder
-   *ID du client unique* : Généralement un GUID
-   *Informations d’identification de l’utilisateur* : passer l’objet créé

**C++** :

    auto result = authContext.acquireToken(
                std::string(“api.aadrm.com”),
                std::string(“4a63455a-cfa1-4ac6-bd2e-0d046cf1c3f7”),
                userCred);


**Étape 5** : Obtenir le jeton d’accès à partir du résultat
Description : Appeler la méthode **result-&gt; accessToken()**

**Remarque**  Toutes les méthodes de bibliothèque d’authentification peuvent lever **rmsauth::Exception**



<!--HONumber=Apr16_HO3-->

