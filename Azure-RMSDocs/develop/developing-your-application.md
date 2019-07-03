---
title: Développement de votre application - AIP
description: Instructions pour une application console de base qui implémente la protection des documents avec Azure Information Protection (AIP)
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 07/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 396A2C19-3A00-4E9A-9088-198A48B15289
audience: developer
ms.reviewer: kartikk
ms.suite: ems
ms.openlocfilehash: feb0636c025d13dd3a290eb34ecb49eec4ebe284
ms.sourcegitcommit: a5f595f8a453f220756fdc11fd5d466c71d51963
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520758"
---
# <a name="developing-your-application"></a>Développement de votre application

Dans cet exemple, vous allez développer une application console simple qui interagit avec le service Azure Information Protection (AIP).  Celle-ci prend comme entrée le chemin d’un document à protéger, puis le protège à l’aide d’une stratégie ad hoc ou d’un modèle Azure. L’application applique ensuite les stratégies appropriées en fonction des entrées, ce qui permet de créer un document dont les informations sont protégées. L’exemple de code que vous allez utiliser est l’[application de test Azure IP](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/AzureIP_Test) qui se trouve sur Github.

## <a name="sample-app-prerequisites"></a>Prérequis de l’exemple d’application
- **Système d’exploitation** : Windows 10, Windows 8, Windows 7, Windows Server 2008, Windows Server 2008 R2 ou Windows Server 2012
- **Langage de programmation** : C# (.NET Framework 3.0 et ultérieur)
- **Environnement de développement** : Visual Studio 2015 (et ultérieur)

## <a name="setting-up-your-azure-configuration"></a>Définition de votre configuration Azure

La configuration Azure pour cette application vous oblige à créer un ID de locataire, une clé symétrique et un ID de principal d’application.

### <a name="azure-ad-tenant-configuration"></a>Configuration du locataire Azure AD

Pour configurer l’environnement Azure AD pour Azure Information Protection, suivez les instructions de [activation du service de protection d’Azure Information Protection](https://docs.microsoft.com/information-protection/deploy-use/activate-service).

Une fois que le service est activé, vous avez besoin des composants PowerShell pour les étapes suivantes. Suivez [administration protection d’Azure Information Protection à l’aide de PowerShell](https://docs.microsoft.com/information-protection/deploy-use/administer-powershell) pour effectuer cette opération.

### <a name="getting-your-tenant-id"></a>Obtention de votre ID de locataire

- En tant qu’administrateur, exécutez PowerShell.
- Importez le module RMS : `Import-Module AIPService`
- Connectez-vous au service avec les informations d’identification de l’utilisateur affecté : `Connect-AipService –Verbose`
- Vérifiez que RMS est activé : `enable-aipservice`
- Obtenez votre ID de locataire en exécutant : `Get-AipServiceConfiguration`

>Enregistrez la valeur BPOSId (ID de locataire). Vous en aurez besoin dans les étapes suivantes.

*Exemple de sortie*
![sortie de l’applet de commande](../media/develop/output-of-Get-AadrmConfiguration.png)

- Déconnectez-vous du service : `Disconnect-AipServiceService`

### <a name="create-a-service-principal"></a>Créer un principal du service
Suivez ces étapes pour créer un principal du service :
> Un principal du service correspond à des informations d’identification configurées globalement pour le contrôle d’accès qui permet à un service de s’authentifier auprès de Microsoft Azure AD et de protéger des informations à l’aide de Microsoft Azure AD Rights Management.

- En tant qu’administrateur, exécutez PowerShell.
- Importez le module Microsoft Azure AD en utilisant : `Import-Module MSOnline`
- Connectez-vous à votre service en ligne avec les informations d’identification de l’utilisateur affecté : `Connect-MsolService`
- Créez un principal du service en exécutant : `New-MsolServicePrincipal`
- Fournissez un nom à votre principal du service.
  > Enregistrez la clé symétrique et l’ID de principal d’application pour une utilisation ultérieure.

*Exemple de sortie*
![sortie de l’applet de commande](../media/develop/output-of-NewMsolServicePrincipal.png)

- Ajoutez votre ID de principal d’application, votre clé symétrique et votre ID de locataire au fichier App.config de l’application.

*Example de fichier App.config*
![sortie de l’applet de commande](../media/develop/example-App.config-file.png)

- Les valeurs *ClientID* et *RedirectUri* sont mises à votre disposition quand vous inscrivez votre application dans Azure. Pour plus d’informations sur la façon d’inscrire votre application dans Azure et d’obtenir les valeurs *ClientID* et *RedirectUri*, consultez [Configurer Azure RMS pour l’authentification ADAL](adal-auth.md).


## <a name="design-summary"></a>Résumé de conception
Le diagramme suivant illustre une architecture et un flux de processus pour l’application que vous créez. Les étapes sont décrites ci-après.
![résumé de conception](../media/develop/design-summary.png)

1. L’utilisateur entre :
   - Le chemin du fichier à protéger
   - Sélectionne un modèle ou crée une stratégie ad hoc.
2. L’application demande une authentification auprès d’AIP.
3. AIP confirme l’authentification.
4. L’application demande des modèles à AIP.
5. AIP retourne des modèles prédéfinis.
6. L’application recherche le fichier spécifié avec l’emplacement donné.
7. L’application applique la stratégie de protection AIP au fichier.

## <a name="how-the-code-works"></a>Fonctionnement du code

Dans l’exemple, Test Azure IP, la solution commence avec le fichier Iprotect.cs. Il s’agit d’une application console C# et, comme avec toute autre application AIP, vous commencez par charger *MSIPC.dll* comme indiqué dans la méthode `main()`.

    //Loads MSIPC.dll
    SafeNativeMethods.IpcInitialize();
    SafeNativeMethods.IpcSetAPIMode(APIMode.Server);

Charger les paramètres nécessaires pour se connecter à Azure

    //Loads credentials for the service principal from App.Config
    SymmetricKeyCredential symmetricKeyCred = new SymmetricKeyCredential();
    symmetricKeyCred.AppPrincipalId = ConfigurationManager.AppSettings["AppPrincipalId"];
    symmetricKeyCred.Base64Key = ConfigurationManager.AppSettings["Base64Key"];
    symmetricKeyCred.BposTenantId = ConfigurationManager.AppSettings["BposTenantId"];

Quand vous fournissez le chemin du fichier dans l’application console, l’application vérifie si le document est déjà chiffré. La méthode relève de la classe **SafeFileApiNativeMethods**.

    var checkEncryptionStatus = SafeFileApiNativeMethods.IpcfIsFileEncrypted(filePath);

Si le document n’est pas chiffré, elle procède au chiffrement du document avec la sélection fournie à l’invite.

    if (!checkEncryptionStatus.ToString().ToLower().Contains(alreadyEncrypted))
    {
      if (method == EncryptionMethod1)
      {
        //Encrypt a file via AIP template
        ProtectWithTemplate(symmetricKeyCred, filePath);

      }
      else if (method == EncryptionMethod2)
      {
        //Encrypt a file using ad-hoc policy
        ProtectWithAdHocPolicy(symmetricKeyCred, filePath);
      }

L’option de protection avec un modèle permet d’obtenir la liste des modèles à partir du serveur et offre à l’utilisateur la possibilité de faire une sélection.
>Si vous n’avez pas modifié les modèles, alors vous obtenez les modèles par défaut d’AIP.

     public static void ProtectWithTemplate(SymmetricKeyCredential symmetricKeyCredential, string filePath)
     {
       // Gets the available templates for this tenant             
       Collection<TemplateInfo> templates = SafeNativeMethods.IpcGetTemplateList(null, false, true,
           false, true, null, null, symmetricKeyCredential);

       //Requests tenant template to use for encryption
       Console.WriteLine("Please select the template you would like to use to encrypt the file.");

       //Outputs templates available for selection
       int counter = 0;
       for (int i = 0; i < templates.Count; i++)
       {
         counter++;
         Console.WriteLine(counter + ". " + templates.ElementAt(i).Name + "\n" +
             templates.ElementAt(i).Description);
       }

       //Parses template selection
       string input = Console.ReadLine();
       int templateSelection;
       bool parseResult = Int32.TryParse(input, out templateSelection);

       //Returns error if no template selection is entered
       if (parseResult)
       {
         //Ensures template value entered is valid
         if (0 < templateSelection && templateSelection <= counter)
         {
           templateSelection -= templateSelection;

           // Encrypts the file using the selected template             
           TemplateInfo selectedTemplateInfo = templates.ElementAt(templateSelection);

           string encryptedFilePath = SafeFileApiNativeMethods.IpcfEncryptFile(filePath,
               selectedTemplateInfo.TemplateId,
               SafeFileApiNativeMethods.EncryptFlags.IPCF_EF_FLAG_KEY_NO_PERSIST, true, false, true, null,
               symmetricKeyCredential);
          }
        }
      }

Si vous sélectionnez la stratégie ad hoc, l’utilisateur de l’application doit fournir les adresses e-mail des personnes dotées de droits. Dans cette section, la licence est créée à l’aide de la méthode **IpcCreateLicenseFromScratch()** et en appliquant la nouvelle stratégie dans le modèle.

    if (issuerDisplayName.Trim() != "")
    {
      // Gets the available issuers of rights policy templates.              
      // The available issuers is a list of RMS servers that this user has already contacted.
      try
      {
        Collection<TemplateIssuer> templateIssuers = SafeNativeMethods.IpcGetTemplateIssuerList(
                                                        null,
                                                        true,
                                                        false,
                                                        false, true, null, symmetricKeyCredential);

        // Creates the policy and associates the chosen user rights with it             
        SafeInformationProtectionLicenseHandle handle = SafeNativeMethods.IpcCreateLicenseFromScratch(
                                                            templateIssuers.ElementAt(0));
        SafeNativeMethods.IpcSetLicenseOwner(handle, owner);
        SafeNativeMethods.IpcSetLicenseUserRightsList(handle, userRights);
        SafeNativeMethods.IpcSetLicenseDescriptor(handle, new TemplateInfo(null, CultureInfo.CurrentCulture,
                                                                policyName,
                                                                policyDescription,
                                                                issuerDisplayName,
                                                                false));

        //Encrypts the file using the ad hoc policy             
        string encryptedFilePath = SafeFileApiNativeMethods.IpcfEncryptFile(
                                       filePath,
                                       handle,
                                       SafeFileApiNativeMethods.EncryptFlags.IPCF_EF_FLAG_KEY_NO_PERSIST,
                                       true,
                                       false,
                                       true,
                                       null,
                                       symmetricKeyCredential);
       }
    }

## <a name="user-interaction-example"></a>Exemple d’interaction de l’utilisateur

Une fois que tout est généré et en cours d’exécution, les sorties de l’application doivent ressembler à ce qui suit :

1.Vous êtes invité à sélectionner une méthode de chiffrement.
![sortie de l’application - étape 1](../media/develop/app-output-1.png)

2. Vous devez fournir le chemin du fichier à protéger.
   ![sortie de l’application - étape 2](../media/develop/app-output-2.png)

3. Vous êtes invité à entrer l’adresse e-mail d’un détenteur de licence (ce détenteur doit posséder des privilèges d’administrateur général sur le locataire Azure AD).
   ![sortie de l’application - étape 3](../media/develop/app-output-3.png)

4. Vous entrez les adresses e-mail des utilisateurs qui vont disposer de droits d’accès au fichier (en les séparant par des espaces).
   ![sortie de l’application - étape 4](../media/develop/app-output-4.png)

5. Vous sélectionnez les droits à octroyer aux utilisateurs autorisés dans la liste.
   ![sortie de l’application - étape 5](../media/develop/app-output-5.png)

6. Enfin, vous entrez certaines métadonnées de stratégie : nom de la stratégie, description et nom complet de l’émetteur (locataire Azure AD) ![sortie de l’application - étape 6](../media/develop/app-output-6.png)

