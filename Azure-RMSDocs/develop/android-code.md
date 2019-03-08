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
ms.openlocfilehash: 7ae70446b932d9f78c2dccc99b2f5727c2e9418e
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57331446"
---
# <a name="android-code-examples"></a>Exemples de code Android

Cet article explique comment coder des éléments pour la version Android du Kit RMS SDK.

**Remarque** Dans cet article, le terme _MSIPC_ (Microsoft Information Protection and Control) fait référence au processus client.


## <a name="using-the-microsoft-rights-management-sdk-42---key-scenarios"></a>Utilisation de Microsoft Rights Management SDK 4.2 : principaux scénarios

Ces exemples de code sont tirés d’un exemple d’application plus large représentant des scénarios de développement importants pour votre compréhension de ce Kit SDK. Ils montrent comment utiliser :

- Le format de fichier protégé de Microsoft, également appelé _fichier protégé_.
- Formats de fichiers protégés personnalisés
- Contrôles d’interface utilisateur (IU) personnalisés

L’exemple d’application *MSIPCSampleApp* est disponible pour une utilisation avec ce Kit SDK pour le système d’exploitation Android. Pour plus d’informations, consultez [rms-sdk-ui-for-android](https://github.com/AzureAD/rms-sdk-ui-for-android).

### <a name="scenario-consume-an-rms-protected-file"></a>Scénario : Consommer un fichier protégé par RMS

- **Étape 1** : Créer un [ProtectedFileInputStream](https://msdn.microsoft.com/library/dn790851.aspx).

    **Source** : *MsipcAuthenticationCallback.java*

    **Description** : Instancier un objet [ProtectedFileInputStream](https://msdn.microsoft.com/library/dn790851.aspx) et implémenter l’authentification du service.  Utilisez [AuthenticationRequestCallback](https://msdn.microsoft.com/library/dn758250.aspx) pour obtenir un jeton en passant une instance de **AuthenticationRequestCallback**, comme le paramètre *mRmsAuthCallback*, à l’API MSIPC. Reportez-vous à l’appel à [ProtectedFileInputStream.create](https://msdn.microsoft.com/library/dn790851.aspx) vers la fin de la section de l’exemple de code suivant.

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

- **Étape 2** : Configurer l’authentification avec la bibliothèque d’authentification Active Directory (ADAL).

    **Source** : *MsipcAuthenticationCallback.java*.

    **Description** : Cette étape utilise la bibliothèque ADAL pour implémenter un [AuthenticationRequestCallback](https://msdn.microsoft.com/library/dn758255.aspx) avec des exemples de paramètres d’authentification. Pour en savoir plus, consultez la [bibliothèque d'authentification Azure AD (ADAL)](https://msdn.microsoft.com/library/jj573266.aspx).


~~~
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
~~~

- **Étape 3** : Vérifier l’existence de l’autorisation **Edit** pour cet utilisateur avec ce contenu via la méthode [UserPolicy.accessCheck](https://msdn.microsoft.com/library/dn790885.aspx).

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


### <a name="scenario-create-a-new-protected-file-using-a-template"></a>Scénario : Créer un fichier protégé en utilisant un modèle

Ce scénario commence par obtenir une liste de modèles, sélectionne le premier pour créer une stratégie, puis nous crée et écrit dans le nouveau fichier protégé.

- **Étape 1** : Obtenir la liste de modèles via un objet [TemplateDescriptor](https://msdn.microsoft.com/library/dn790871.aspx).

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

- **Étape 2** : Créer une [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx) en utilisant le premier modèle de la liste.

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

-  **Étape 3** : Créer un [ProtectedFileOutputStream](https://msdn.microsoft.com/library/dn790855.aspx) et y écrire du contenu.

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


### <a name="scenario-open-a-custom-protected-file"></a>Scénario : Ouvrir un fichier protégé personnalisé

- **Étape 1** : Créer une [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx) à partir d’une *serializedContentPolicy*.

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


~~~
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
~~~


- **Step 2**: Create a [CustomProtectedInputStream](https://msdn.microsoft.com/library/dn758271.aspx) using the [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx) from **Step 1**.

    **Source**: *MsipcTaskFragment.java*

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

- **Step 3**: Read content from the [CustomProtectedInputStream](https://msdn.microsoft.com/library/dn758271.aspx) into *mDecryptedContent* then close.

    **Source**: *MsipcTaskFragment.java*

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

### Scenario: Create a custom protected file using a custom policy

- **Step 1**: With an email address provided by the user, create a policy descriptor.

    **Source**: *MsipcTaskFragment.java*

    **Description**: In practice, the following objects would be created by using user inputs from the device interface; [UserRights](https://msdn.microsoft.com/library/dn790911.aspx) and [PolicyDescriptor](https://msdn.microsoft.com/library/dn790843.aspx).

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


- **Step 2**: Create a custom [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx) from the policy descriptor, *selectedDescriptor*.

    **Source**: *MsipcTaskFragment.java*

    ``` java
       mIAsyncControl = UserPolicy.create((PolicyDescriptor)selectedDescriptor,
         mEmailId, mRmsAuthCallback, UserPolicyCreationFlags.NONE, userPolicyCreationCallback);
    ```


- **Step 3**: Create and write content to the [CustomProtectedOutputStream](https://msdn.microsoft.com/library/dn758274.aspx) and then close.

    **Source**: *MsipcTaskFragment.java*

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
