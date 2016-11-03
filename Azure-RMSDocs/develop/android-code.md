---
title: Exemples de code Android | Azure RMS
description: "Cette rubrique présente des éléments de code importants pour la version Android du Kit RMS SDK."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 58CC2E50-1E4D-4621-A947-25312C3FF519
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 503a99f01335f3085b5d13c9faaf0a6f05063490
ms.openlocfilehash: febc212cb6bc4b91058aa0e9f18d1e51f751b552


---

# Exemples de code Android

Cette rubrique présente des éléments de code importants pour la version Android du Kit RMS SDK.

**Remarque** : Dans l’exemple de code et les descriptions qui suivent, nous utilisons le terme MSIPC (Microsoft Information Protection and Control) pour faire référence au processus client.


## Utilisation de Microsoft Rights Management SDK 4.2 : principaux scénarios

Voici des exemples de code tirés d’un exemple d’application plus large représentant des scénarios de développement importants pour votre compréhension de ce SDK. Ces exemples illustrent l’utilisation du format de fichier protégé Microsoft (appelé « fichier protégé »), l’utilisation de formats de fichiers protégés personnalisés et l’utilisation de contrôles d’interface utilisateur personnalisés.



L’exemple d’application, *MSIPCSampleApp*, est disponible pour une utilisation avec ce SDK pour le système d’exploitation Android. Consultez [rms-sdk-ui-for-android](https://github.com/AzureAD/rms-sdk-ui-for-android) sur GitHub pour accéder à cette application.

### Scénario : Consommer un fichier protégé RMS

-   **Étape 1** : Créer un [ProtectedFileInputStream](https://msdn.microsoft.com/library/dn790851.aspx)

    **Source** : *MsipcAuthenticationCallback.java*

    **Description** : Instancier un objet [ProtectedFileInputStream](https://msdn.microsoft.com/library/dn790851.aspx) par le biais de sa méthode de création qui implémente l’authentification de service à l’aide de [AuthenticationRequestCallback](https://msdn.microsoft.com/library/dn758250.aspx) pour obtenir un jeton en passant une instance de **AuthenticationRequestCallback** comme paramètre *mRmsAuthCallback* à l’API MSIPC. Reportez-vous à l’appel à [ProtectedFileInputStream.create](https://msdn.microsoft.com/library/dn790851.aspx) vers la fin de la section de l’exemple de code suivant.

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

    **Description** : Dans cette étape, nous allons utiliser la bibliothèque ADAL pour implémenter un [AuthenticationRequestCallback](https://msdn.microsoft.com/library/dn758255.aspx) avec des exemples de paramètres d’authentification. Pour plus d’informations sur l’utilisation de la bibliothèque ADAL, consultez la [Bibliothèque d’authentification Azure AD (ADAL)](https://msdn.microsoft.com/library/jj573266.aspx).


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


-   **Étape 3** : Vérifier l’existence de l’autorisation **Edit** pour cet utilisateur avec ce contenu via la méthode [UserPolicy.accessCheck](https://msdn.microsoft.comlibrary/dn790885.aspx).

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

-   **Étape 1** : Afficher la liste de modèles via un objet [TemplateDescriptor](https://msdn.microsoft.com/library/dn790871.aspx).

    **Source** : *MsipcTaskFragment.java*



    CreationCallback<List<TemplateDescriptor>> getTemplatesCreationCallback = new CreationCallback<List<TemplateDescriptor>>() { @Override public Context getContext() { …
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
      }; try { …
          mIAsyncControl = TemplateDescriptor.getTemplates(emailId, mRmsAuthCallback, getTemplatesCreationCallback); } catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e) { …
      }


-    **Étape 2** : Créer un [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx) en utilisant le premier modèle de la liste.

    **Source** : *MsipcTaskFragment.java*



      CreationCallback<UserPolicy> userPolicyCreationCallback = new CreationCallback<UserPolicy>() { @Override public Context getContext() { …
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
      }; try { …
          mIAsyncControl = UserPolicy.create((TemplateDescriptor)selectedDescriptor, mEmailId, mRmsAuthCallback, UserPolicyCreationFlags.NONE, userPolicyCreationCallback); …
      } catch (InvalidParameterException e) { …
      }


-    **Étape 3** : Créer un [ProtectedFileOutputStream](https://msdn.microsoft.com/library/dn790855.aspx) et y écrire du contenu.

    **Source** : *MsipcTaskFragment.java*


    private void createPTxt(final byte[] contentToProtect) { …
            CreationCallback<ProtectedFileOutputStream> protectedFileOutputStreamCreationCallback = new CreationCallback<ProtectedFileOutputStream>() { @Override public Context getContext() { …
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

-   **Étape 1** : Créer un [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx) à partir d’un *serializedContentPolicy*.

    **Source** : *MsipcTaskFragment.java*


    CreationCallback<UserPolicy> userPolicyCreationCallbackFromSerializedContentPolicy = new CreationCallback<UserPolicy>() { @Override public void onSuccess(UserPolicy userPolicy) { …
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


    try {   ...

      // Read the serializedContentPolicyLength from the inputStream.
      long serializedContentPolicyLength = readUnsignedInt(inputStream);

      // Read the PL bytes from the input stream using the PL size.
      byte[] serializedContentPolicy = new byte[(int)serializedContentPolicyLength]; inputStream.read(serializedContentPolicy);

      ...

      UserPolicy.acquire(serializedContentPolicy, null, mRmsAuthCallback, PolicyAcquisitionFlags.NONE,           userPolicyCreationCallbackFromSerializedContentPolicy); } catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e) {   ... } catch (IOException e) {   ... }



-    **Étape 2** : Créer un [CustomProtectedInputStream](https://msdn.microsoft.com/library/dn758271.aspx) en utilisant le [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx) de l’**Étape 1**.

    **Source** : *MsipcTaskFragment.java*



      CreationCallback<CustomProtectedInputStream> customProtectedInputStreamCreationCallback = new CreationCallback<CustomProtectedInputStream>() { @Override public Context getContext() { …
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

    try {  ...

      // Retrieve the encrypted content size.
      long encryptedContentLength = readUnsignedInt(inputStream);

      updateTaskStatus(new TaskStatus(TaskState.Starting, "Consuming content", true));

      CustomProtectedInputStream.create(userPolicy, inputStream,                                 encryptedContentLength,                                 customProtectedInputStreamCreationCallback); } catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e) {  ... } catch (IOException e) {  ... }


-    **Étape 3** : Lire du contenu provenant de [CustomProtectedInputStream](https://msdn.microsoft.com/library/dn758271.aspx) dans *mDecryptedContent*, puis fermer.

    **Source** : *MsipcTaskFragment.java*


    @Override public void onSuccess(CustomProtectedInputStream customProtectedInputStream) {  mUserPolicy = customProtectedInputStream.getUserPolicy();  ByteArrayOutputStream buffer = new ByteArrayOutputStream();

      int nRead;                      
      byte[] dataChunk = new byte[16384];

      try  {    while ((nRead = customProtectedInputStream.read(dataChunk, 0,                                                        dataChunk.length)) != -1)    {       buffer.write(dataChunk, 0, nRead);    }

        buffer.flush();    mDecryptedContent = new String(buffer.toByteArray(), Charset.forName("UTF-8"));

        buffer.close();    customProtectedInputStream.close();  }  catch (IOException e)  {    ...  } }


### Scénario : Créer un fichier protégé personnalisé à l’aide d’une stratégie personnalisée (ad hoc)

-   **Étape 1** : Avec une adresse e-mail fournie par l’utilisateur, créer un descripteur de stratégie.

    **Source** : *MsipcTaskFragment.java*

    **Description** : Dans la pratique, les objets suivants sont créés en utilisant des entrées de l’utilisateur à partir de l’interface de l’appareil : [UserRights](https://msdn.microsoft.com/library/dn790911.aspx) et [PolicyDescriptor](https://msdn.microsoft.com/library/dn790843.aspx).



      // create userRights list   UserRights userRights = new UserRights(Arrays.asList("consumer@domain.com"),     Arrays.asList( CommonRights.View, EditableDocumentRights.Print));   ArrayList<UserRights> usersRigthsList = new ArrayList<UserRights>();   usersRigthsList.add(userRights);

      // Create PolicyDescriptor using userRights list   PolicyDescriptor policyDescriptor = PolicyDescriptor.createPolicyDescriptorFromUserRights(                                                          usersRigthsList);   policyDescriptor.setOfflineCacheLifetimeInDays(10);   policyDescriptor.setContentValidUntil(new Date());



-    **Étape 2** : Créer un [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx) personnalisé à partir du descripteur de stratégie *selectedDescriptor*.

    **Source** : *MsipcTaskFragment.java*


       mIAsyncControl = UserPolicy.create((PolicyDescriptor)selectedDescriptor,                                          mEmailId, mRmsAuthCallback,                                          UserPolicyCreationFlags.NONE,                                          userPolicyCreationCallback);



-   **Étape 3** : Créer et écrire du contenu dans [CustomProtectedOutputStream](https://msdn.microsoft.com/library/dn758274.aspx), puis fermer.

    **Source** : *MsipcTaskFragment.java*


    File file = new File(filePath); final OutputStream outputStream = new FileOutputStream(file); CreationCallback<CustomProtectedOutputStream> customProtectedOutputStreamCreationCallback = new CreationCallback<CustomProtectedOutputStream>() { @Override public Context getContext() { …
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


 

 



<!--HONumber=Oct16_HO3-->


