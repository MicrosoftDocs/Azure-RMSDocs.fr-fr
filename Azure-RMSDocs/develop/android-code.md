---
title: Exemples de code Android | Azure RMS
description: Cette rubrique présente des éléments de code importants pour la version Android du Kit RMS SDK.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 12/10/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 58CC2E50-1E4D-4621-A947-25312C3FF519
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev, has-adal-ref
ms.openlocfilehash: 075eae9729ac9175e570a8f0386dadcbfc22bb05
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/19/2020
ms.locfileid: "95568332"
---
# <a name="android-code-examples"></a>Exemples de code Android

[!INCLUDE [deprecation notice](../includes/deprecation-warning.md)]

Cet article explique comment coder des éléments pour la version Android du Kit RMS SDK.

**Remarque** Dans cet article, le terme _MSIPC_ (Microsoft Information Protection and Control) fait référence au processus client.


## <a name="using-the-microsoft-rights-management-sdk-42---key-scenarios"></a>Utilisation de Microsoft Rights Management SDK 4.2 - Principaux scénarios

Ces exemples de code sont tirés d’un exemple d’application plus large représentant des scénarios de développement importants pour votre compréhension de ce Kit SDK. Ils montrent comment utiliser :

- Le format de fichier protégé de Microsoft, également appelé _fichier protégé_.
- Formats de fichiers protégés personnalisés
- Contrôles d’interface utilisateur (IU) personnalisés

L’exemple d’application *MSIPCSampleApp* est disponible pour une utilisation avec ce Kit SDK pour le système d’exploitation Android. Pour plus d’informations, consultez [rms-sdk-ui-for-android](https://github.com/AzureAD/rms-sdk-ui-for-android).

### <a name="scenario-consume-an-rms-protected-file"></a>Scénario : Consommer un fichier protégé RMS

- **Étape 1** : Créer un [ProtectedFileInputStream](/previous-versions/windows/desktop/msipcthin2/protectedfileinputstream-class-java).

    **Source** : *MsipcAuthenticationCallback.java*

    **Description** : instancier un objet [ProtectedFileInputStream](/previous-versions/windows/desktop/msipcthin2/protectedfileinputstream-class-java) et implémenter l’authentification du service.  Utilisez [AuthenticationRequestCallback](/previous-versions/windows/desktop/msipcthin2/authenticationcompletioncallback-interface-java) pour obtenir un jeton en passant une instance de **AuthenticationRequestCallback**, comme le paramètre *mRmsAuthCallback*, à l’API MSIPC. Reportez-vous à l’appel à [ProtectedFileInputStream.create](/previous-versions/windows/desktop/msipcthin2/protectedfileinputstream-class-java) vers la fin de la section de l’exemple de code suivant.

    ``` java
        public void startContentConsumptionFromPtxtFileFormat(InputStream inputStream)
        {
            CreationCallback<ProtectedFileInputStream> protectedFileInputStreamCreationCallback =
              new CreationCallback<ProtectedFileInputStream>()
            {
                @Override
                public Context getContext()
                {
                   …
               }

                @Override
                public void onCancel()
                {
                   …
                }

                @Override
                public void onFailure(ProtectionException e)
                {
                   …
                }

                @Override
                public void onSuccess(ProtectedFileInputStream protectedFileInputStream)
                {
                   …
                   …
                    byte[] dataChunk = new byte[16384];
                    try
                    {
                        while ((nRead = protectedFileInputStream.read(dataChunk, 0,
                                dataChunk.length)) != -1)
                        {
                            …
                        }
                         …
                        protectedFileInputStream.close();
                    }
                    catch (IOException e)
                    {
                      …
                    }
              }
            };
            try
            {
               …
                ProtectedFileInputStream.create(inputStream, null, mRmsAuthCallback,
                                                PolicyAcquisitionFlags.NONE,
                                                protectedFileInputStreamCreationCallback);
            }
            catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e)
            {
                …
            }
        }
    ```

- **Étape 2** : Configurer l’authentification à l’aide de la bibliothèque d’authentification Active Directory (ADAL).

    **Source**: *MsipcAuthenticationCallback. Java*.

    **Description** : cette étape utilise la bibliothèque ADAL pour implémenter un [AuthenticationRequestCallback](/previous-versions/windows/desktop/msipcthin2/authenticationrequestcallback-interface-java) avec des exemples de paramètres d’authentification. Pour en savoir plus, consultez la [bibliothèque d'authentification Azure AD (ADAL)](/previous-versions/azure/jj573266(v=azure.100)).


   ``` java
       class MsipcAuthenticationCallback implements AuthenticationRequestCallback
       {

       …

       @Override
       public void getToken(Map<String, String> authenticationParametersMap,
                            final AuthenticationCompletionCallback authenticationCompletionCallbackToMsipc)
       {
           String authority = authenticationParametersMap.get("oauth2.authority");
           String resource = authenticationParametersMap.get("oauth2.resource");
           String userId = authenticationParametersMap.get("userId");
           final String userHint = (userId == null)? "" : userId;
           AuthenticationContext authenticationContext = App.getInstance().getAuthenticationContext();
           if (authenticationContext == null || !authenticationContext.getAuthority().equalsIgnoreCase(authority))
           {
               try
               {
                   authenticationContext = new AuthenticationContext(App.getInstance().getApplicationContext(), authority, …);
                   App.getInstance().setAuthenticationContext(authenticationContext);
               }
               catch (NoSuchAlgorithmException e)
               {
                   …
                   authenticationCompletionCallbackToMsipc.onFailure();
               }
               catch (NoSuchPaddingException e)
               {
                   …
                   authenticationCompletionCallbackToMsipc.onFailure();
               }
          }
           App.getInstance().getAuthenticationContext().acquireToken(mParentActivity, resource, mClientId, mRedirectURI, userId, mPromptBehavior,
                          "&USERNAME=" + userHint, new AuthenticationCallback<AuthenticationResult>()
                           {
                               @Override
                               public void onError(Exception exc)
                               {
                                   …
                                   if (exc instanceof AuthenticationCancelError)
                                   {
                                        …
                                       authenticationCompletionCallbackToMsipc.onCancel();
                                   }
                                   else
                                   {
                                        …
                                       authenticationCompletionCallbackToMsipc.onFailure();
                                   }
                               }

                               @Override
                               public void onSuccess(AuthenticationResult result)
                               {
                                   …
                                   if (result == null || result.getAccessToken() == null
                                           || result.getAccessToken().isEmpty())
                                   {
                                        …
                                   }
                                   else
                                   {
                                       // request is successful
                                       …
                                       authenticationCompletionCallbackToMsipc.onSuccess(result.getAccessToken());
                                   }
                               }
                           }

                           );
                     }
   ```

- **Étape 3** : Vérifier l’existence de l’autorisation **Edit** pour cet utilisateur avec ce contenu via la méthode [UserPolicy.accessCheck](/previous-versions/windows/desktop/msipcthin2/userpolicy-accesscheck-method-java).

    **Source** : *TextEditorFragment.java*

    ``` java
         //check if user has edit rights and apply enforcements
                if (!mUserPolicy.accessCheck(EditableDocumentRights.Edit))
                {
                    mTextEditor.setFocusableInTouchMode(false);
                    mTextEditor.setFocusable(false);
                    mTextEditor.setEnabled(false);
                    …
                }
    ```


### <a name="scenario-create-a-new-protected-file-using-a-template"></a>Scénario : Créer un fichier protégé à l’aide d’un modèle

Ce scénario commence par obtenir une liste de modèles, sélectionne le premier pour créer une stratégie, puis nous crée et écrit dans le nouveau fichier protégé.

- **Étape 1** : afficher la liste de modèles via un objet [TemplateDescriptor](/previous-versions/windows/desktop/msipcthin2/templatedescriptor-class-java).

    **Source** : *MsipcTaskFragment.java*

    ``` java
    CreationCallback<List<TemplateDescriptor>> getTemplatesCreationCallback = new CreationCallback<List<TemplateDescriptor>>()
      {
          @Override
          public Context getContext()
          {
              …
          }

          @Override
          public void onCancel()
          {
              …
          }

          @Override
          public void onFailure(ProtectionException e)
          {
              …
          }

          @Override
          public void onSuccess(List<TemplateDescriptor> templateDescriptors)
          {
             …
          }
      };
      try
      {
              …
          mIAsyncControl = TemplateDescriptor.getTemplates(emailId, mRmsAuthCallback, getTemplatesCreationCallback);
      }
      catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e)
      {
              …
      }
    ```


- **Étape 2** : créer une [UserPolicy](/previous-versions/windows/desktop/msipcthin2/userpolicy-class-java) en utilisant le premier modèle de la liste.

    **Source** : *MsipcTaskFragment.java*

    ``` java
      CreationCallback<UserPolicy> userPolicyCreationCallback = new CreationCallback<UserPolicy>()
      {
          @Override
          public Context getContext()
          {
              …
          }

          @Override
          public void onCancel()
          {
              …
          }

          @Override
          public void onFailure(ProtectionException e)
          {
              …
          }

          @Override
          public void onSuccess(final UserPolicy item)
          {
              …
          }
      };
      try
      {
           …
          mIAsyncControl = UserPolicy.create((TemplateDescriptor)selectedDescriptor, mEmailId, mRmsAuthCallback,
                            UserPolicyCreationFlags.NONE, userPolicyCreationCallback);
           …
      }
      catch (InvalidParameterException e)
      {
              …
      }
    ```


-  **Étape 3** : créer un [ProtectedFileOutputStream](/previous-versions/windows/desktop/msipcthin2/protectedfileoutputstream-class-java) et y écrire du contenu.

    **Source** : *MsipcTaskFragment.java*

    ``` java
    private void createPTxt(final byte[] contentToProtect)
        {
             …
            CreationCallback<ProtectedFileOutputStream> protectedFileOutputStreamCreationCallback = new CreationCallback<ProtectedFileOutputStream>()
            {
                @Override
                public Context getContext()
                {
                 …
                }

                @Override
                public void onCancel()
                {
                 …
                }

                @Override
                public void onFailure(ProtectionException e)
                {
                 …
                }

                @Override
                public void onSuccess(ProtectedFileOutputStream protectedFileOutputStream)
                {
                    try
                    {
                        // write to this stream
                        protectedFileOutputStream.write(contentToProtect);
                        protectedFileOutputStream.flush();
                        protectedFileOutputStream.close();
                        …
                    }
                    catch (IOException e)
                    {
                        …
                    }
                }
            };
            try
            {
                File file = new File(filePath);
                outputStream = new FileOutputStream(file);
                mIAsyncControl = ProtectedFileOutputStream.create(outputStream, mUserPolicy, originalFileExtension,
                        protectedFileOutputStreamCreationCallback);
            }
            catch (FileNotFoundException e)
            {
                 …
            }
            catch (InvalidParameterException e)
            {
                 …
            }
        }
    ```


### <a name="scenario-open-a-custom-protected-file"></a>Scénario : Ouvrir un fichier protégé personnalisé

- **Étape 1** : créer une [UserPolicy](/previous-versions/windows/desktop/msipcthin2/userpolicy-class-java) à partir d’une *serializedContentPolicy*.

    **Source** : *MsipcTaskFragment.java*

    ``` java
    CreationCallback<UserPolicy> userPolicyCreationCallbackFromSerializedContentPolicy = new CreationCallback<UserPolicy>()
            {
                @Override
                public void onSuccess(UserPolicy userPolicy)
                {
                  …
                }

                @Override
                public void onFailure(ProtectionException e)
                {
                  …
                }

                @Override
                public void onCancel()
                {
                  …
                }

                @Override
                public Context getContext()
                {
                  …
                }
            };
            try
            {
                ...

                // Read the serializedContentPolicyLength from the inputStream.
                long serializedContentPolicyLength = readUnsignedInt(inputStream);

                // Read the PL bytes from the input stream using the PL size.
                byte[] serializedContentPolicy = new byte[(int)serializedContentPolicyLength];
                inputStream.read(serializedContentPolicy);

                ...

                UserPolicy.acquire(serializedContentPolicy, null, mRmsAuthCallback, PolicyAcquisitionFlags.NONE,
                userPolicyCreationCallbackFromSerializedContentPolicy);
            }
            catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e)
            {
            ...
            }
            catch (IOException e)
            {
            ...
            }
   ```


- **Étape 2** : créer un [CustomProtectedInputStream](/previous-versions/windows/desktop/msipcthin2/customprotectedinputstream-class-java) en utilisant la [UserPolicy](/previous-versions/windows/desktop/msipcthin2/userpolicy-class-java) de l’**étape 1**.

    **Source** : *MsipcTaskFragment.java*

    ``` java
      CreationCallback<CustomProtectedInputStream> customProtectedInputStreamCreationCallback = new CreationCallback<CustomProtectedInputStream>()
      {
         @Override
         public Context getContext()
         {
             …
         }

         @Override
         public void onCancel()
         {
             …
         }

         @Override
         public void onFailure(ProtectionException e)
         {
             …
         }

         @Override
         public void onSuccess(CustomProtectedInputStream customProtectedInputStream)
         {
            …

             byte[] dataChunk = new byte[16384];
             try
             {
                 while ((nRead = customProtectedInputStream.read(dataChunk, 0, dataChunk.length)) != -1)
                 {
                      …
                 }
                  …
                 customProtectedInputStream.close();
             }
             catch (IOException e)
             {
                …
             }
             …
         }
     };

    try
    {
      ...

      // Retrieve the encrypted content size.
      long encryptedContentLength = readUnsignedInt(inputStream);

      updateTaskStatus(new TaskStatus(TaskState.Starting, "Consuming content", true));

      CustomProtectedInputStream.create(userPolicy, inputStream,
                                     encryptedContentLength,
                                     customProtectedInputStreamCreationCallback);
    }
    catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e)
    {
      ...
    }
    catch (IOException e)
    {
      ...
    }
    ```


- **Étape 3** : lire du contenu provenant du [CustomProtectedInputStream](/previous-versions/windows/desktop/msipcthin2/customprotectedinputstream-class-java) dans *mDecryptedContent*, puis fermer.

    **Source** : *MsipcTaskFragment.java*

    ``` java
    @Override
    public void onSuccess(CustomProtectedInputStream customProtectedInputStream)
    {
      mUserPolicy = customProtectedInputStream.getUserPolicy();
      ByteArrayOutputStream buffer = new ByteArrayOutputStream();

      int nRead;
      byte[] dataChunk = new byte[16384];

      try
      {
        while ((nRead = customProtectedInputStream.read(dataChunk, 0,
                                                            dataChunk.length)) != -1)
        {
           buffer.write(dataChunk, 0, nRead);
        }

        buffer.flush();
        mDecryptedContent = new String(buffer.toByteArray(), Charset.forName("UTF-8"));

        buffer.close();
        customProtectedInputStream.close();
      }
      catch (IOException e)
      {
        ...
      }
    }
    ```


### <a name="scenario-create-a-custom-protected-file-using-a-custom-policy"></a>Scénario : Créer un fichier protégé personnalisé à l’aide d’une stratégie personnalisée

- **Étape 1** : Avec une adresse e-mail fournie par l’utilisateur, créer un descripteur de stratégie.

    **Source** : *MsipcTaskFragment.java*

    **Description** : Dans la pratique, les objets suivants sont créés en utilisant des entrées de l’utilisateur à partir de l’interface de l’appareil : [UserRights](/previous-versions/windows/desktop/msipcthin2/userrights-class-java) et [PolicyDescriptor](/previous-versions/windows/desktop/msipcthin2/policydescriptor-interface-java).

    ``` java
      // create userRights list
      UserRights userRights = new UserRights(Arrays.asList("consumer@domain.com"),
        Arrays.asList( CommonRights.View, EditableDocumentRights.Print));
      ArrayList<UserRights> usersRigthsList = new ArrayList<UserRights>();
      usersRigthsList.add(userRights);

      // Create PolicyDescriptor using userRights list
      PolicyDescriptor policyDescriptor = PolicyDescriptor.createPolicyDescriptorFromUserRights(
                                                             usersRigthsList);
      policyDescriptor.setOfflineCacheLifetimeInDays(10);
      policyDescriptor.setContentValidUntil(new Date());
    ```


- **Étape 2** : créer une [UserPolicy](/previous-versions/windows/desktop/msipcthin2/userpolicy-class-java) personnalisée à partir du descripteur de stratégie *selectedDescriptor*.

    **Source** : *MsipcTaskFragment.java*

    ``` java
       mIAsyncControl = UserPolicy.create((PolicyDescriptor)selectedDescriptor,
         mEmailId, mRmsAuthCallback, UserPolicyCreationFlags.NONE, userPolicyCreationCallback);
    ```


- **Étape 3** : créer et écrire du contenu dans [CustomProtectedOutputStream](/previous-versions/windows/desktop/msipcthin2/customprotectedoutputstream-class-java), puis fermer.

    **Source** : *MsipcTaskFragment.java*

    ``` java
    File file = new File(filePath);
        final OutputStream outputStream = new FileOutputStream(file);
        CreationCallback<CustomProtectedOutputStream> customProtectedOutputStreamCreationCallback = new CreationCallback<CustomProtectedOutputStream>()
        {
            @Override
            public Context getContext()
            {
              …
            }

            @Override
            public void onCancel()
            {
              …
            }

            @Override
            public void onFailure(ProtectionException e)
            {
              …
            }

            @Override
            public void onSuccess(CustomProtectedOutputStream protectedOutputStream)
            {
                try
                {
                    // write serializedContentPolicy
                    byte[] serializedContentPolicy = mUserPolicy.getSerializedContentPolicy();
                    writeLongAsUnsignedIntToStream(outputStream, serializedContentPolicy.length);
                    outputStream.write(serializedContentPolicy);
                    // write encrypted content
                    if (contentToProtect != null)
                    {
                        writeLongAsUnsignedIntToStream(outputStream,
                                CustomProtectedOutputStream.getEncryptedContentLength(contentToProtect.length,
                                        protectedOutputStream.getUserPolicy()));
                        protectedOutputStream.write(contentToProtect);
                        protectedOutputStream.flush();
                        protectedOutputStream.close();
                    }
                    else
                    {
                        outputStream.flush();
                        outputStream.close();
                    }
                    …
                }
                catch (IOException e)
                {
                  …
                }
            }
        };
        try
        {
            mIAsyncControl = CustomProtectedOutputStream.create(outputStream, mUserPolicy,
                    customProtectedOutputStreamCreationCallback);
        }
        catch (InvalidParameterException e)
        {
          …
        }
    ```