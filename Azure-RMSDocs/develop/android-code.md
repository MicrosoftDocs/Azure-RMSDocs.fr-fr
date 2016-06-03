---
# required metadata

title: Exemples de code Android | Azure RMS
description: Cette rubrique présente des éléments de code importants pour la version Android du Kit RMS SDK.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 58CC2E50-1E4D-4621-A947-25312C3FF519
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Exemples de code Android

Cette rubrique présente des éléments de code importants pour la version Android du Kit RMS SDK.

**Remarque** : Dans l’exemple de code et les descriptions qui suivent, nous utilisons le terme MSIPC (Microsoft Information Protection and Control) pour faire référence au processus client.


## Utilisation de Microsoft Rights Management SDK 4.2 : principaux scénarios

Voici des exemples de code tirés d’un exemple d’application plus large représentant des scénarios de développement importants pour votre compréhension de ce SDK. Ces exemples illustrent l’utilisation du format de fichier protégé Microsoft (appelé « fichier protégé »), l’utilisation de formats de fichiers protégés personnalisés et l’utilisation de contrôles d’interface utilisateur personnalisés.



L’exemple d’application, *MSIPCSampleApp*, est disponible pour une utilisation avec ce SDK pour le système d’exploitation Android. Consultez [rms-sdk-ui-for-android](https://github.com/AzureAD/rms-sdk-ui-for-android) sur GitHub pour accéder à cette application.

### Scénario : Consommer un fichier protégé RMS

-   **Étape 1** : Créer un [**ProtectedFileInputStream**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_protectedfileinputstream_class_java)

    **Source** : *MsipcAuthenticationCallback.java*

    **Description** : instancier un objet [**ProtectedFileInputStream**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_protectedfileinputstream_class_java) par le biais de sa méthode de création qui implémente l’authentification de service à l’aide de [**AuthenticationRequestCallback**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_authenticationrequestcallback_interface_java) pour obtenir un jeton en passant une instance de **AuthenticationRequestCallback** comme paramètre *mRmsAuthCallback* à l’API MSIPC. Reportez-vous à l’appel à [**ProtectedFileInputStream.create**](/rights-management/sdk/4.2/api/android/protectedfileinputstream#msipcthin2_protectedfileinputstream_create_method) vers la fin de la section de l’exemple de code suivant.

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


-   **Étape 2** : Configurer l’authentification à l’aide de la bibliothèque d’authentification Active Directory (ADAL).

    **Source** : *MsipcAuthenticationCallback.java*.

    **Description** : dans cette étape, nous allons utiliser la bibliothèque ADAL pour implémenter un [**AuthenticationRequestCallback**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_authenticationrequestcallback_interface_java) avec des exemples de paramètres d’authentification. Pour plus d’informations sur l’utilisation de la bibliothèque ADAL, consultez [Bibliothèque d’authentification Azure AD (ADAL)](https://msdn.microsoft.com/en-us/library/jj573266.aspx).


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


-   **Étape 3** : vérifier l’existence de l’autorisation **Edit** pour cet utilisateur avec ce contenu via la méthode [**accessCheck**](/rights-management/sdk/4.2/api/android/userpolicy#msipcthin2_userpolicy_accesscheck_method_java) de [**UserPolicy**](/rights-management/sdk/4.2/api/android/userpolicy).

    **Source** : *TextEditorFragment.java*


         //check if user has edit rights and apply enforcements
                if (!mUserPolicy.accessCheck(EditableDocumentRights.Edit))
                {
                    mTextEditor.setFocusableInTouchMode(false);
                    mTextEditor.setFocusable(false);
                    mTextEditor.setEnabled(false);
                    …
                }


### Scénario : Créer un fichier protégé à l’aide d’un modèle

Ce scénario commence par obtenir une liste de modèles, sélectionne le premier pour créer une stratégie, puis nous crée et écrit dans le nouveau fichier protégé.

-   **Étape 1** : afficher la liste de modèles via un objet [**TemplateDescriptor**](/rights-management/sdk/4.2/api/android/templatedescriptor#msipcthin2_templatedescriptor_class_java).

    **Source** : *MsipcTaskFragment.java*



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


-    **Étape 2** : créer une [**UserPolicy**](/rights-management/sdk/4.2/api/android/userpolicy) en utilisant le premier modèle de la liste.

    **Source**: *MsipcTaskFragment.java*



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


-    **Étape 3** : créer un [**ProtectedFileOutputStream**](/rights-management/sdk/4.2/api/android/protectedfileoutputstream#msipcthin2_protectedfileoutputstream_class_java) et y écrire du contenu.

    **Source**: *MsipcTaskFragment.java*


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



### Scénario : Ouvrir un fichier protégé personnalisé

-   **Étape 1** : créer une [**UserPolicy**](/rights-management/sdk/4.2/api/android/userpolicy) à partir d’une *serializedContentPolicy*.

    **Source** : *MsipcTaskFragment.java*


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



-    **Étape 2** : créer un [**CustomProtectedInputStream**](/rights-management/sdk/4.2/api/android/customprotectedinputstream#msipcthin2_customprotectedinputstream_class_java) en utilisant la [**UserPolicy**](/rights-management/sdk/4.2/api/android/userpolicy) de l’**étape 1**.

    **Source**: *MsipcTaskFragment.java*



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


-    **Étape 3** : lire du contenu provenant du [**CustomProtectedInputStream**](/rights-management/sdk/4.2/api/android/customprotectedinputstream#msipcthin2_customprotectedinputstream_class_java) dans *mDecryptedContent*, puis fermer.

    **Source**: *MsipcTaskFragment.java*


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


### Scénario : Créer un fichier protégé personnalisé à l’aide d’une stratégie personnalisée (ad hoc)

-   **Étape 1** : Avec une adresse e-mail fournie par l’utilisateur, créer un descripteur de stratégie.

    **Source** : *MsipcTaskFragment.java*

    **Description** : dans la pratique, les objets suivants seront créés en utilisant des entrées de l’utilisateur à partir de l’interface de l’appareil : [**UserRights**](/rights-management/sdk/4.2/api/android/userrights#msipcthin2_userrights_class_java) et [**PolicyDescriptor**](/rights-management/sdk/4.2/api/android/policydescriptor#msipcthin2_policydescriptor_interface_java).



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



-    **Étape 2** : créer une [**UserPolicy**](/rights-management/sdk/4.2/api/android/userpolicy) personnalisée à partir du descripteur de stratégie *selectedDescriptor*.

    **Source**: *MsipcTaskFragment.java*


       mIAsyncControl = UserPolicy.create((PolicyDescriptor)selectedDescriptor,
                                              mEmailId, mRmsAuthCallback,
                                              UserPolicyCreationFlags.NONE,
                                              userPolicyCreationCallback);



-   **Étape 3** : créer et écrire du contenu dans [**CustomProtectedOutputStream**](/rights-management/sdk/4.2/api/android/customprotectedoutputstream#msipcthin2_customprotectedoutputstream_class_java), puis fermer.

    **Source** : *MsipcTaskFragment.java*


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


 

 


<!--HONumber=Apr16_HO4-->


