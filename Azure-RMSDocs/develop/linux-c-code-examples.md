---
title: Exemples de code Linux | Azure RMS
description: Cette rubrique présente les éléments de code et les scénarios importants pour la version Linux du Kit RMS SDK.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 0F7714CA-1D3E-4846-B187-739825B7DE26
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: b3336297309d98245814a0d31c87f9eca4501ddb
ms.sourcegitcommit: 84b45c949d85a7291c088a050d2a66d356fc9af2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/24/2020
ms.locfileid: "87135729"
---
# <a name="linux-code-examples"></a>Exemples de code Linux

[!INCLUDE [deprecation notice](../includes/deprecation-warning.md)]

Cette rubrique présente les éléments de code et les scénarios importants pour la version Linux du Kit RMS SDK.

Les extraits de code ci-dessous sont tirés des exemples d’applications, de *RMS \_ Sample* et *rmsauth \_ *. Pour plus d’informations, consultez [samples](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples) dans le dépôt GitHub.

## <a name="scenario-access-protection-policy-information-from-a-protected-file"></a>Scénario : Accéder aux informations de stratégie de protection à partir d’un fichier protégé

**Ouvre et lit un fichier** 
 protégé par RMS **Source**: [RMS \_ Sample/MainWindow. cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**Description** : Après obtention d’un nom de fichier auprès de l’utilisateur, lecture des certificats (voir *MainWindow::addCertificates*), configuration du rappel d’autorisation avec l’ID client et l’URL de redirection, appel de *ConvertFromPFile* (voir l’exemple de code suivant), puis lecture de la description, de la date de validité du contenu et du nom de la stratégie de protection.

**C++**:

  ```cpp
    void MainWindow::ConvertFromPFILE(const string& fileIn,
        const string& clientId,
        const string& redirectUrl,
        const string& clientEmail) 
    {
    // add trusted certificates using HttpHelpers of RMS and Auth SDKs
    addCertificates();
    
    // create shared in/out streams
    auto inFile = make_shared<ifstream>(
    fileIn, ios_base::in | ios_base::binary);
    
    if (!inFile->is_open()) {
     AddLog("ERROR: Failed to open ", fileIn.c_str());
    return;
    }
    
    string fileOut;
    
    // generate output filename
    auto pos = fileIn.find_last_of('.');
    
    if (pos != string::npos) {
     fileOut = fileIn.substr(0, pos);
    }
    
     // create streams
    auto outFile = make_shared<fstream>(
    fileOut, ios_base::in | ios_base::out | ios_base::trunc | ios_base::binary);
    
    if (!outFile->is_open()) {
     AddLog("ERROR: Failed to open ", fileOut.c_str());
     return;
      }
    
    try
    {
    // create authentication context
    AuthCallback auth(clientId, redirectUrl);
    
    // process conversion
    auto pfs = PFileConverter::ConvertFromPFile(
      clientEmail,
      inFile,
      outFile,
      auth,
      this->consent);
    
    AddLog("Successfully converted to ", fileOut.c_str());
    }
    catch (const rmsauth::Exception& e)
    {
    AddLog("ERROR: ", e.error().c_str());
    }
    catch (const rmscore::exceptions::RMSException& e) {
    AddLog("ERROR: ", e.what());
    }
    inFile->close();
    outFile->close();
    }
  ```

**Créer un flux** 
 de fichier protégé **Source**: [RMS \_ Sample/pfileconverter. cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**Description**: cette méthode crée un flux de fichier protégé à partir du flux de sauvegarde passé via la méthode SDK, *ProtectedFileStream :: Acquire*, qui est ensuite retournée à l’appelant.

**C++**:

  ```cpp
    shared_ptr<GetProtectedFileStreamResult>PFileConverter::ConvertFromPFile(
    const string           & userId,
    shared_ptr<istream>      inStream,
    shared_ptr<iostream>     outStream,
    IAuthenticationCallback& auth,
    IConsentCallback       & consent)
    {
    auto inIStream = rmscrypto::api::CreateStreamFromStdStream(inStream);
    
    auto fsResult = ProtectedFileStream::Acquire(
    inIStream,
    userId,
    auth,
    consent,
    POL_None,
    static_cast<ResponseCacheFlags>(RESPONSE_CACHE_INMEMORY
                                    | RESPONSE_CACHE_ONDISK));
    
    if ((fsResult.get() != nullptr) && (fsResult->m_status == Success) &&
      (fsResult->m_stream != nullptr)) {
    auto pfs = fsResult->m_stream;
    
    // preparing
    readPosition  = 0;
    writePosition = 0;
    totalSize     = pfs->Size();
    
    // start threads
    for (size_t i = 0; i < THREADS_NUM; ++i) {
      threadPool.push_back(thread(WorkerThread,
                                  static_pointer_cast<iostream>(outStream), pfs,
                                  false));
    }
    
    for (thread& t: threadPool) {
      if (t.joinable()) {
        t.join();
      }
    }
    }
      return fsResult;
    }
  ```

## <a name="scenario-create-a-new-protected-file-using-a-template"></a>Scénario : Créer un fichier protégé à l’aide d’un modèle

**Protège un fichier avec un modèle** 
 sélectionné par l’utilisateur **Source**: [RMS \_ Sample/MainWindow. cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**Description** : Après obtention d’un nom de fichier auprès de l’utilisateur, lecture des certificats (voir *MainWindow::addCertificates*) et configuration du rappel d’autorisation avec l’ID client et l’URL de redirection, le fichier sélectionné est protégé en appelant *ConvertToPFileTemplates* (voir l’exemple de code suivant).

**C++**:

  ```cpp
    void MainWindow::ConvertToPFILEUsingTemplates(const string& fileIn,
                                              const string& clientId,
                                              const string& redirectUrl,
                                              const string& clientEmail) 
    {
    // generate output filename
    string fileOut = fileIn + ".pfile";
    
    // add trusted certificates using HttpHelpers of RMS and Auth SDKs
    addCertificates();
    
    // create shared in/out streams
    auto inFile = make_shared<ifstream>(
    fileIn, ios_base::in | ios_base::binary);
    auto outFile = make_shared<fstream>(
    fileOut, ios_base::in | ios_base::out | ios_base::trunc | ios_base::binary);
    
    if (!inFile->is_open()) {
    AddLog("ERROR: Failed to open ", fileIn.c_str());
    return;
    }
    
    if (!outFile->is_open()) {
    AddLog("ERROR: Failed to open ", fileOut.c_str());
    return;
    }
    
    // find file extension
    string fileExt;
    auto   pos = fileIn.find_last_of('.');
    
    if (pos != string::npos) {
    fileExt = fileIn.substr(pos);
    }
    
    try {
    // create authentication callback
    AuthCallback auth(clientId, redirectUrl);
    
    // process conversion
    PFileConverter::ConvertToPFileTemplates(
      clientEmail, inFile, fileExt, outFile, auth,
      this->consent, this->templates);
    
    AddLog("Successfully converted to ", fileOut.c_str());
    }
   catch (const rmsauth::Exception& e) {
    AddLog("ERROR: ", e.error().c_str());
    outFile->close();
    remove(fileOut.c_str());
    }
    catch (const rmscore::exceptions::RMSException& e) {
    AddLog("ERROR: ", e.what());
    
    outFile->close();
    remove(fileOut.c_str());
    }
    inFile->close();
    outFile->close();
    }
  ```


**Protège un fichier à l’aide d’une stratégie créée à partir d’un modèle** 
 **Source**: [RMS \_ Sample/pfileconverter. cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**Description**: Une liste de modèles associés à l’utilisateur est récupérée et le modèle sélectionné est ensuite utilisé pour créer une stratégie qui, à son tour, est utilisée pour protéger le fichier.

**C++**:

  ```cpp
    void PFileConverter::ConvertToPFileTemplates(const string           & userId,
                                             shared_ptr<istream>      inStream,
                                             const string           & fileExt,
                                             std::shared_ptr<iostream>outStream,
                                             IAuthenticationCallback& auth,
                                             IConsentCallback& /*consent*/,
                                             ITemplatesCallback     & templ)
    {
    auto templates = TemplateDescriptor::GetTemplateList(userId, auth);
    
    rmscore::modernapi::AppDataHashMap signedData;
    
    size_t pos = templ.SelectTemplate(templates);
    
    if (pos < templates.size()) {
    auto policy = UserPolicy::CreateFromTemplateDescriptor(
      templates[pos],
      userId,
      auth,
      USER_AllowAuditedExtraction,
      signedData);
   
    ConvertToPFileUsingPolicy(policy, inStream, fileExt, outStream);
    }
    }
  ```

**Protège un fichier à partir d’une stratégie** 
 **Source**: [RMS \_ Sample/pfileconverter. cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**Description**: Créer un flux de fichier protégé à l’aide de la stratégie donnée, puis protéger ce fichier.

**C++**:

  ```cpp
    void PFileConverter::ConvertToPFileUsingPolicy(shared_ptr<UserPolicy>   policy,
                                               shared_ptr<istream>      inStream,
                                               const string           & fileExt,
                                               std::shared_ptr<iostream>outStream)
    {
    if (policy.get() != nullptr) {
    auto outIStream = rmscrypto::api::CreateStreamFromStdStream(outStream);
    auto pStream    = ProtectedFileStream::Create(policy, outIStream, fileExt);
    
    // preparing
    readPosition  = 0;
    writePosition = pStream->Size();
    
    inStream->seekg(0, ios::end);
    totalSize = inStream->tellg();
    
    // start threads
    for (size_t i = 0; i < THREADS_NUM; ++i) {
      threadPool.push_back(thread(WorkerThread,
                                  static_pointer_cast<iostream>(inStream),
                                  pStream,
                                  true));
    }
    
    for (thread& t: threadPool) {
      if (t.joinable()) {
        t.join();
      }
    }
    
    pStream->Flush();
    }
  ```


## <a name="scenario-protect-a-file-using-custom-protection"></a>Scénario : Protéger un fichier à l’aide de la protection personnalisée

**Protège un fichier à l’aide de la protection personnalisée** 
 **Source**: [RMS \_ Sample/MainWindow. cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**Description** : Après obtention d’un nom de fichier auprès de l’utilisateur, lecture des certificats (voir *MainWindow::addCertificates*), collecte des informations sur les droits auprès de l’utilisateur et configuration du rappel d’autorisation avec l’ID client et l’URL de redirection, le fichier sélectionné est protégé en appelant *ConvertToPFileTemplates* (voir l’exemple de code suivant).

**C++**:

  ```cpp
    void MainWindow::ConvertToPFILEUsingRights(const string            & fileIn,
                                           const vector<UserRights>& userRights,
                                           const string            & clientId,
                                           const string            & redirectUrl,
                                           const string            & clientEmail)
    {
    // generate output filename
    string fileOut = fileIn + ".pfile";
    
    // add trusted certificates using HttpHelpers of RMS and Auth SDKs
    addCertificates();
    
    // create shared in/out streams
    auto inFile = make_shared<ifstream>(
    fileIn, ios_base::in | ios_base::binary);
    auto outFile = make_shared<fstream>(
    fileOut, ios_base::in | ios_base::out | ios_base::trunc | ios_base::binary);
    
    if (!inFile->is_open()) {
    AddLog("ERROR: Failed to open ", fileIn.c_str());
    return;
    }
    
    if (!outFile->is_open()) {
    AddLog("ERROR: Failed to open ", fileOut.c_str());
    return;
    }
    
    // find file extension
    string fileExt;
    auto   pos = fileIn.find_last_of('.');
    
    if (pos != string::npos) {
    fileExt = fileIn.substr(pos);
    }
    
    // is anything to add
    if (userRights.size() == 0) {
    AddLog("ERROR: ", "Please fill email and check rights");
    return;
    }
    
    
    try {
    // create authentication callback
    AuthCallback auth(clientId, redirectUrl);
    
    // process conversion
    PFileConverter::ConvertToPFilePredefinedRights(
      clientEmail,
      inFile,
      fileExt,
      outFile,
      auth,
      this->consent,
      userRights);
    
    AddLog("Successfully converted to ", fileOut.c_str());
    }
    catch (const rmsauth::Exception& e) {
    AddLog("ERROR: ", e.error().c_str());
    
    outFile->close();
    remove(fileOut.c_str());
    }
    catch (const rmscore::exceptions::RMSException& e) {
    AddLog("ERROR: ", e.what());
    
    outFile->close();
    remove(fileOut.c_str());
    }
    inFile->close();
    outFile->close();
    }
  ```


**Crée une stratégie de protection donnant aux utilisateurs les droits sélectionnés** 
 **Source**: [RMS \_ Sample/pfileconverter. cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**Description** : Créer un descripteur de stratégie et le remplir avec les informations sur les droits de l’utilisateur, puis utiliser le descripteur de stratégie pour créer une stratégie utilisateur. Cette stratégie est utilisée pour protéger le fichier sélectionné par le biais d’un appel à *ConvertToPFileUsingPolicy* (voir la description fournie dans une section précédente de cette rubrique).

**C++**:

  ```cpp
    void PFileConverter::ConvertToPFilePredefinedRights(
    const string            & userId,
    shared_ptr<istream>       inStream,
    const string            & fileExt,
    shared_ptr<iostream>      outStream,
    IAuthenticationCallback & auth,
    IConsentCallback& /*consent*/,
    const vector<UserRights>& userRights)
    {
    auto endValidation = chrono::system_clock::now() + chrono::hours(48);
    
    
    PolicyDescriptor desc(userRights);
    
    desc.Referrer(make_shared<string>("https://client.test.app"));
    desc.ContentValidUntil(endValidation);
    desc.AllowOfflineAccess(false);
    desc.Name("Test Name");
    desc.Description("Test Description");
    
    auto policy = UserPolicy::Create(desc, userId, auth,
                                   USER_AllowAuditedExtraction);
    ConvertToPFileUsingPolicy(policy, inStream, fileExt, outStream);
  ```
    

## <a name="workerthread---a-supporting-method"></a>WorkerThread - méthode prise en charge


La méthode *WorkerThread()* est appelée par deux des exemples de scénarios précédents (**Créer un flux de fichier protégé** et **Protège un fichier conformément à une stratégie**) de la manière suivante :

**C++**:

  ```cpp
    threadPool.push_back(thread(WorkerThread,
                                  static_pointer_cast<iostream>(outStream), pfs,
                                  false));
  ```


**Méthode de prise en charge, WorkerThread()**

**C++**:

  ```cpp
    static mutex   threadLocker;
    static int64_t totalSize     = 0;
    static int64_t readPosition  = 0;
    static int64_t writePosition = 0;
    static vector<thread> threadPool;
    
    static void WorkerThread(shared_ptr<iostream>           stdStream,
                         shared_ptr<ProtectedFileStream>pStream,
                         bool                           modeWrite) {
    vector<uint8_t> buffer(4096);
    int64_t bufferSize = static_cast<int64_t>(buffer.size());
    
    while (totalSize - readPosition > 0) {
    // lock
    threadLocker.lock();
    
    // check remain
    if (totalSize - readPosition <= 0) {
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
    
        stdStream->seekg(offsetRead);
        stdStream->read(reinterpret_cast<char *>(&buffer[0]), toProcess);
        threadLocker.unlock();
        auto written =
          pStream->WriteAsync(
            buffer.data(), toProcess, offsetWrite, std::launch::deferred).get();
    
        if (written != toProcess) {
          throw rmscore::exceptions::RMSStreamException("Error while writing data");
        }
      }
      catch (exception& e) {
        qDebug() << "Exception: " << e.what();
      }
    } else {
      auto read =
        pStream->ReadAsync(&buffer[0],
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
        stdStream->seekp(offsetWrite);
        stdStream->write(reinterpret_cast<const char *>(buffer.data()), read);
        threadLocker.unlock();
      }
      catch (exception& e) {
        qDebug() << "Exception: " << e.what();
      }
    }
    }
    }
  ```


## <a name="scenario-rms-authentication"></a>Scénario : Authentification RMS

Les exemples suivants montrent deux approches d’authentification : obtention d’un jeton oAuth2 d’authentification Azure avec interface utilisateur et sans interface utilisateur.
**Acquisition du jeton d’authentification oAuth2 avec l’interface utilisateur** 
 **Source**: [rmsauth \_ Sample/MainWindow. cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rmsauth_sample)

**Étape 1**: créer un point partagé de l’objet **Rmsauth :: FileCache** .
Description : Vous pouvez définir le chemin du cache ou utiliser la valeur par défaut.

**C++**:

  ```cpp
    auto FileCachePtr = std::make_shared< rmsauth::FileCache>();
  ```


**Étape 2** : Créer l’objet **rmsauth::AuthenticationContext** Description : Spécifier l’*URI d’autorité* Azure et l’objet *FileCache*.

**C++**:

  ```cpp
    AuthenticationContext authContext(
                              std::string("https://sts.aadrm.com/_sts/oauth/authorize"),
                              AuthorityValidationType::False,
                              FileCachePtr);
  ```


**Étape 3**: appelez la méthode **acquireToken** de l’objet **authContext** et spécifiez les paramètres suivants : Description :

-   *Ressource demandée* : Ressource protégée à laquelle vous souhaitez accéder
-   *ID du client unique* : Généralement un GUID
-   *URI de redirection* : URI qui sera réadressé après récupération du jeton d’authentification
-   *Comportement de l’invite d’authentification* : Si vous définissez **PromptBehavior::Auto**, la bibliothèque essaie d’utiliser le cache et d’actualiser le jeton si nécessaire
-   *ID d’utilisateur* : Nom d’utilisateur affiché dans la fenêtre d’invite

**C++**:

  ```cpp
    auto result = authContext.acquireToken(
                std::string("api.aadrm.com"),
                std::string("4a63455a-cfa1-4ac6-bd2e-0d046cf1c3f7"),
                std::string("https://client.test.app"),
                PromptBehavior::Auto,
                std::string("john.smith@msopentechtest01.onmicrosoft.com"));
  ```

**Étape 4** : Obtenir le jeton d’accès à partir du résultat Description : Appeler la méthode **result-> accessToken()**

**Remarque**  Toutes les méthodes de bibliothèque d’authentification peuvent lever **rmsauth::Exception**

 
**Acquisition du jeton d’authentification oAuth2 sans interface utilisateur** 
 **Source**: [rmsauth \_ Sample/MainWindow. cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rmsauth_sample)

**Étape 1** : Créer un point partagé de l’objet **rmsauth::FileCache** Description : Vous pouvez définir le chemin du cache ou utiliser la valeur par défaut

**C++**:

  ```cpp
    auto FileCachePtr = std::make_shared< rmsauth::FileCache>();
  ```


**Étape 2** : Créer l’objet **UserCredential** Description : Spécifier la *connexion utilisateur* et le *mot de passe*

**C++**:

  ```cpp
    auto userCred = std::make_shared<UserCredential>("john.smith@msopentechtest01.onmicrosoft.com",
                                                 "SomePass");
  ```

**Étape 3** : Créer l’objet **rmsauth::AuthenticationContext** Description : Spécifier l’*URI d’autorité* Azure et l’objet *FileCache*

**C++**:

  ```cpp
    AuthenticationContext authContext(
                        std::string("https://sts.aadrm.com/_sts/oauth/authorize"),
                        AuthorityValidationType::False,
                        FileCachePtr);
  ```


**Étape 4**: appelez la méthode **acquireToken** de **authContext** et spécifiez les paramètres :
-   *Ressource demandée* : Ressource protégée à laquelle vous souhaitez accéder
-   *ID du client unique* : Généralement un GUID
-   *Informations d’identification de l’utilisateur* : passer l’objet créé

**C++**:

  ```cpp
    auto result = authContext.acquireToken(
                std::string("api.aadrm.com"),
                std::string("4a63455a-cfa1-4ac6-bd2e-0d046cf1c3f7"),
                userCred);
  ```


**Étape 5** : Obtenir le jeton d’accès à partir du résultat Description : Appeler la méthode **result-> accessToken()**

**Remarque**  Toutes les méthodes de bibliothèque d’authentification peuvent lever **rmsauth::Exception**
