---
title: Exemples de code iOS/OS X | Azure RMS
description: Cette rubrique présente des éléments de code importants pour la version iOS/OS X du Kit RMS SDK.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 7E12EBF2-5A19-4A8D-AA99-531B09DA256A
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev, has-adal-ref
ms.openlocfilehash: 3c50c4579d32add393b680616106b37e92d2364c
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/19/2020
ms.locfileid: "95568296"
---
# <a name="iosos-x-code-examples"></a>Exemples de code iOS/OS X

[!INCLUDE [deprecation notice](../includes/deprecation-warning.md)]

Cette rubrique présente des éléments de code importants pour la version iOS/OS X du Kit RMS SDK.

**Remarque**  Dans l’exemple de code et les descriptions qui suivent, nous utilisons le terme MSIPC (Microsoft Information Protection and Control) pour faire référence au processus client.



## <a name="using-the-microsoft-rights-management-sdk-42---key-scenarios"></a>Utilisation de Microsoft Rights Management SDK 4.2 - Principaux scénarios


Vous trouverez ci-dessous des exemples de code **Objective C** tirés d’un exemple d’application représentant des scénarios de développement importants pour l’orientation de ce SDK. Ces exemples illustrent l’utilisation du format de fichier protégé Microsoft (appelé « fichier protégé »), l’utilisation de formats de fichiers protégés personnalisés et l’utilisation de contrôles d’interface utilisateur personnalisés.

### <a name="scenario-consume-an-rms-protected-file"></a>Scénario : Consommer un fichier protégé RMS


- **Étape 1** : Créer un objet [MSProtectedData](/previous-versions/windows/desktop/msipcthin2/msprotecteddata-interface-objc)

  **Description** : Instancier un objet [MSProtectedData](/previous-versions/windows/desktop/msipcthin2/msprotecteddata-interface-objc) par le biais de sa méthode de création qui implémente l’authentification de service à l’aide de [MSAuthenticationCallback](/previous-versions/windows/desktop/msipcthin2/msauthenticationcallback-protocol-objc) pour obtenir un jeton en passant une instance de **MSAuthenticationCallback**, comme paramètre *authenticationCallback*, à l’API MSIPC. Consultez l’appel à [MSProtectedData protectedDataWithProtectedFile](/previous-versions/windows/desktop/msipcthin2/msprotecteddata-protecteddatawithprotectedfile-completionblock-method-objc) dans la section d’exemple de code suivante.

    ```objectivec
        + (void)consumePtxtFile:(NSString *)path authenticationCallback:(id<MSAuthenticationCallback>)authenticationCallback
        {
            // userId can be provided as a hint for authentication
            [MSProtectedData protectedDataWithProtectedFile:path
                                                 userId:nil
                                 authenticationCallback:authenticationCallback
                                                options:Default
                                        completionBlock:^(MSProtectedData *data, NSError *error)
            {
                //Read the content from the ProtectedData, this will decrypt the data
                NSData *content = [data retrieveData];
            }];
        }
    ```

- **Étape 2** : Configurer l’authentification à l’aide de la bibliothèque d’authentification Active Directory (ADAL).

  **Description** : Lors de cette étape, nous allons utiliser la bibliothèque ADAL pour implémenter un [MSAuthenticationCallback](/previous-versions/windows/desktop/msipcthin2/msauthenticationcallback-protocol-objc) avec des exemples de paramètres d’authentification. Pour plus d’informations sur l’utilisation de la bibliothèque ADAL, consultez la Bibliothèque d’authentification Azure AD (ADAL).

    ```objectivec
      // AuthenticationCallback holds the necessary information to retrieve an access token.
      @interface MsipcAuthenticationCallback : NSObject<MSAuthenticationCallback>

      @end

      @implementation MsipcAuthenticationCallback

      - (void)accessTokenWithAuthenticationParameters:
             (MSAuthenticationParameters *)authenticationParameters
                                    completionBlock:
             (void(^)(NSString *accessToken, NSError *error))completionBlock
      {
          ADAuthenticationError *error;
          ADAuthenticationContext* context = [
              ADAuthenticationContext authenticationContextWithAuthority:authenticationParameters.authority
                                                                error:&error
          ];
          NSString *appClientId = @"com.microsoft.sampleapp";
          NSURL *redirectURI = [NSURL URLWithString:@"local://authorize"];
          // Retrieve token using ADAL
          [context acquireTokenWithResource:authenticationParameters.resource
                                 clientId:appClientId
                              redirectUri:redirectURI
                                   userId:authenticationParameters.userId
                          completionBlock:^(ADAuthenticationResult *result) {
                              if (result.status != AD_SUCCEEDED)
                              {
                                  NSLog(@"Auth Failed");
                                  completionBlock(nil, result.error);
                              }
                              else
                              {
                                  completionBlock(result.accessToken, result.error);
                              }
                          }];
       }
    ```

- **Étape 3** : Vérifier l’existence de l’autorisation de modification pour cet utilisateur avec ce contenu par le biais de la méthode [MSUserPolicy accessCheck](/previous-versions/windows/desktop/msipcthin2/msuserpolicy-accesscheck-method-objc) d’un objet [MSUserPolicy](/previous-versions/windows/desktop/msipcthin2/msuserpolicy-interface-objc).

    ```objectivec
      - (void)accessCheckWithProtectedData:(MSProtectedData *)protectedData
      {
          //check if user has edit rights and apply enforcements
          if (!protectedData.userPolicy.accessCheck(EditableDocumentRights.Edit))
          {
              // enforce on the UI
              textEditor.focusableInTouchMode = NO;
              textEditor.focusable = NO;
              textEditor.enabled = NO;
          }
      }
    ```

### <a name="scenario-create-a-new-protected-file-using-a-template"></a>Scénario : Créer un fichier protégé à l’aide d’un modèle

Dans ce scénario, nous commençons par obtenir une liste de modèles, [MSTemplateDescriptor](/previous-versions/windows/desktop/msipcthin2/mstemplatedescriptor-interface-objc), nous sélectionnons le premier pour créer une stratégie, puis nous créons et écrivons dans le nouveau fichier protégé.

-   **Étape 1** : Obtenir la liste des modèles

    ```objectivec
        + (void)templateListUsageWithAuthenticationCallback:(id<MSAuthenticationCallback>)authenticationCallback
        {
            [MSTemplateDescriptor templateListWithUserId:@"user@domain.com"
                            authenticationCallback:authenticationCallback
                                   completionBlock:^(NSArray/*MSTemplateDescriptor*/ *templates, NSError *error)
                                   {
                                     // use templates array of MSTemplateDescriptor (Note: will be nil on error)
                                   }];
        }
    ```

-   **Étape 2** : Créer un [MSUserPolicy](/previous-versions/windows/desktop/msipcthin2/msuserpolicy-interface-objc) à l’aide du premier modèle de la liste.

    ```objectivec
        + (void)userPolicyCreationFromTemplateWithAuthenticationCallback:(id<MSAuthenticationCallback>)authenticationCallback
        {
            [MSUserPolicy userPolicyWithTemplateDescriptor:[templates objectAtIndex:0]
                                            userId:@"user@domain.com"
                                     signedAppData:nil
                            authenticationCallback:authenticationCallback
                                           options:None
                                   completionBlock:^(MSUserPolicy *userPolicy, NSError *error)
            {
            // use userPolicy (Note: will be nil on error)
            }];
        }
    ```

-   **Étape 3** : Créer un [MSMutableProtectedData](/previous-versions/windows/desktop/msipcthin2/msmutableprotecteddata-interface-objc) et y écrire du contenu.

    ```objectivec
        + (void)createPtxtWithUserPolicy:(MSUserPolicy *)userPolicy contentToProtect:(NSData *)contentToProtect
        {
            // create an MSMutableProtectedData to write content
            [contentToProtect protectedDataInFile:filePath
                        originalFileExtension:kDefaultTextFileExtension
                               withUserPolicy:userPolicy
                              completionBlock:^(MSMutableProtectedData *data, NSError *error)
            {
             // use data (Note: will be nil on error)
            }];
        }
    ```

### <a name="scenario-open-a-custom-protected-file"></a>Scénario : Ouvrir un fichier protégé personnalisé


-   **Étape 1** : Créer un [MSUserPolicy](/previous-versions/windows/desktop/msipcthin2/msuserpolicy-interface-objc) à partir d’un *serializedContentPolicy*.

    ```objectivec
        + (void)userPolicyWith:(NSData *)protectedData
        authenticationCallback:(id<MSAuthenticationCallback>)authenticationCallback
        {
            // Read header information from protectedData and extract the  PL
            /*-------------------------------------------
            | PL length | PL | ContetSizeLength |
            -------------------------------------------*/
            NSUInteger serializedPolicySize;
            NSMutableData *serializedPolicy;
            [protectedData getBytes:&serializedPolicySize length:sizeof(serializedPolicySize)];
            [protectedData getBytes:[serializedPolicy mutableBytes] length:serializedPolicySize];

            // Get the user policy , this is an async method as it hits the REST service
            // for content key and usage restrictions
            // userId provided as a hint for authentication
            [MSUserPolicy userPolicyWithSerializedPolicy:serializedPolicy
                                              userId:@"user@domain.com"
                              authenticationCallback:authenticationCallback
                                             options:Default
                                     completionBlock:^(MSUserPolicy *userPolicy,
                                                       NSError *error)
            {

            }];
         }
    ```

-   **Étape 2** : Créer un [MSCustomProtectedData](/previous-versions/windows/desktop/msipcthin2/msmutablecustomprotecteddata-interface-objc) à l’aide du [MSUserPolicy](/previous-versions/windows/desktop/msipcthin2/msuserpolicy-interface-objc) de l’**Étape 1** et le lire.

    ```objectivec
        + (void)customProtectedDataWith:(NSData *)protectedData
        {
            // Read header information from protectedData and extract the  protectedContentSize
            /*-------------------------------------------
            | PL length | PL | ContetSizeLength |
            -------------------------------------------*/
            NSUInteger protectedContentSize;
            [protectedData getBytes:&protectedContentSize
                         length:sizeof(protectedContentSize)];

            // Create the MSCustomProtector used for decrypting the content
            // The content start position is the header length
            [MSCustomProtectedData customProtectedDataWithPolicy:userPolicy
                                               protectedData:protectedData
                                        contentStartPosition:sizeof(NSUInteger) + serializedPolicySize
                                                 contentSize:protectedContentSize
                                             completionBlock:^(MSCustomProtectedData *customProtector,
                                                               NSError *error)
            {
             //Read the content from the custom protector, this will decrypt the data
             NSData *content = [customProtector retrieveData];
             NSLog(@"%@", content);
            }];
         }
    ```

### <a name="scenario-create-a-custom-protected-file-using-a-custom-ad-hoc-policy"></a>Scénario : Créer un fichier protégé personnalisé à l’aide d’une stratégie personnalisée (ad hoc)


-   **Étape 1** : Avec une adresse e-mail fournie par l’utilisateur, créer un descripteur de stratégie.

    **Description** : Dans la pratique, les objets suivants doivent être créés à l’aide d’entrées d’utilisateur à partir de l’interface de l’appareil : [MSUserRights](/previous-versions/windows/desktop/msipcthin2/msuserrights-interface-objc) et [MSPolicyDescriptor](/previous-versions/windows/desktop/msipcthin2/mspolicydescriptor-interface-objc).

    ```objectivec
        + (void)policyDescriptor
        {
            MSUserRights *userRights = [[MSUserRights alloc] initWithUsers:[NSArray arrayWithObjects: @"user1@domain.com", @"user2@domain.com", nil] rights:[MSEmailRights all]];

            MSPolicyDescriptor *policyDescriptor = [[MSPolicyDescriptor alloc] initWithUserRights:[NSArray arrayWithObjects:userRights, nil]];
            policyDescriptor.contentValidUntil = [[NSDate alloc] initWithTimeIntervalSinceNow:NSTimeIntervalSince1970 + 3600.0];
            policyDescriptor.offlineCacheLifetimeInDays = 10;
        }
    ```

-   **Étape 2** : Créer un [MSUserPolicy](/previous-versions/windows/desktop/msipcthin2/msuserpolicy-interface-objc) personnalisé à partir du descripteur de stratégie, *selectedDescriptor*.

    ```objectivec
        + (void)userPolicyWithPolicyDescriptor:(MSPolicyDescriptor *)policyDescriptor
        {
            [MSUserPolicy userPolicyWithPolicyDescriptor:policyDescriptor
                                          userId:@"user@domain.com"
                          authenticationCallback:authenticationCallback
                                         options:None
                                 completionBlock:^(MSUserPolicy *userPolicy, NSError *error)
            {
              // use userPolicy (Note: will be nil on error)
            }];
        }
    ```

-   **Étape 3** :Créer et écrire du contenu dans [MSMutableCustomProtectedData](/previous-versions/windows/desktop/msipcthin2/msmutablecustomprotecteddata-interface-objc), puis le fermer.

    ```objectivec
        + (void)mutableCustomProtectedData:(NSMutableData *)backingData policy:(MSUserPolicy *)policy contentToProtect:(NSString *)contentToProtect
        {
            //Get the serializedPolicy from a given policy
            NSData *serializedPolicy = [policy serializedPolicy];

            // Write header information to backing data including the PL
            // ------------------------------------
            // | PL length | PL | ContetSizeLength |
            // -------------------------------------
            NSUInteger serializedPolicyLength = [serializedPolicy length];
            [backingData appendData:[NSData dataWithBytes:&serializedPolicyLength length:sizeof(serializedPolicyLength)]];
            [backingData appendData:serializedPolicy];
            NSUInteger protectedContentLength = [MSCustomProtectedData getEncryptedContentLengthWithPolicy:policy contentLength:unprotectedData.length];
            [backingData appendData:[NSData dataWithBytes:&protectedContentLength length:sizeof(protectedContentLength)]];

            NSUInteger headerLength = sizeof(serializedPolicyLength) + serializedPolicyLength + sizeof(protectedContentLength);

            // Create the MSMutableCustomProtector used for encrypting content
            // The content start position is the current length of the backing data
            // The encryptedContentSize content size is 0 since there is no content yet
            [MSMutableCustomProtectedData customProtectorWithUserPolicy:policy
                                                        backingData:backingData
                                             protectedContentOffset:headerLength
                                                    completionBlock:^(MSMutableCustomProtectedData *customProtector,
                                                                      NSError *error)
            {
                //Append data to the custom protector, this will encrypt the data and write it to the backing data
                [customProtector appendData:[contentToProtect dataUsingEncoding:NSUTF8StringEncoding] error:&error];

                //close the custom protector so it will flush and finalise encryption
                [customProtector close:&error];

            }];
          }
    ```