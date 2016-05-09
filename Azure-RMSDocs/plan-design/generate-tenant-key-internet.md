---
# required metadata

title: Générer et transférer votre clé de locataire via Internet | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1bff9b06-8c5a-4b1d-9962-6668219210e6

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Générer et transférer votre clé de locataire par Internet
Utilisez les procédures suivantes si vous avez décidé de [gérer votre propre clé de locataire](plan-implement-tenant-key.md#choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok-) et que vous voulez la transférer via Internet au lieu de vous déplacer jusqu’à un établissement Microsoft pour la transférer en personne.


## préparation du poste de travail connecté à Internet
Pour préparer le poste de travail connecté à Internet, suivez ces 3 étapes :

-   [Étape 1 : installation de Windows PowerShell pour Azure Rights Management](#step-1-install-windows-powershell-for-azure-rights-management)

-   [Étape 2 : obtention de l'ID de locataire Azure Active Directory](#step-2-get-your-azure-active-directory-tenant-id)

-   [Étape 3 : téléchargement de l'ensemble d'outils BYOK](#step-3-download-the-byok-toolset)

### Étape 1 : installation de Windows PowerShell pour Azure Rights Management
Depuis le poste de travail connecté à Internet, téléchargez et installez le module Windows PowerShell pour Azure Rights Management.

> [!NOTE]
> Si vous avez déjà téléchargé ce module Windows PowerShell, exécutez la commande suivante pour vérifier que le numéro de votre version est au minimum 2.1.0.0 : `(Get-Module aadrm -ListAvailable).Version`

Pour des instructions d’installation, consultez [Installation de Windows PowerShell pour Azure Rights Management](../deploy-use/install-powershell.md).

### Étape 2 : obtention de l'ID de locataire Azure Active Directory
Lancez Windows PowerShell avec l'option **Exécuter en tant qu'administrateur** , puis exécutez les commandes suivantes :

-   Utilisez l'applet de commande [Connect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629415.aspx) pour vous connecter au service Azure RMS :

    ```
    Connect-AadrmService
    ```
    Quand vous y êtes invité, entrez vos informations d’identification d’administrateur de locataire [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (en général, vous allez utiliser un compte d’administrateur global pour Azure Active Directory ou Office 365).

-   Utilisez l'applet de commande [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) pour afficher la configuration de votre locataire :

    ```
    Get-AadrmConfiguration
    ```
    Dans le résultat de l'applet de commande, identifiez et enregistrez l'identificateur global unique à partir de la première ligne (BPOSId). Il s'agit de votre ID de locataire Azure Active Directory, dont vous aurez besoin ultérieurement lorsque vous préparerez votre clé de locataire pour le téléchargement.

-   Utilisez l'applet de commande [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) pour vous déconnecter du service Azure RMS jusqu'à ce que vous soyez prêt à télécharger votre clé :

    ```
    Disconnect-AadrmService
    ```

Ne fermez pas la fenêtre Windows PowerShell.

### Étape 3 : téléchargement de l'ensemble d'outils BYOK
Accédez au centre de téléchargement Microsoft et [téléchargez l'ensemble d'outils BYOK](http://go.microsoft.com/fwlink/?LinkId=335781) pour votre région.

|Région|Nom du package|
|----------|----------------|
|Amérique du Nord|AzureRMS-BYOK-tools-UnitedStates.zip|
|Europe|AzureRMS-BYOK-tools-Europe.zip|
|Asie|AzureRMS-BYOK-tools-AsiaPacific.zip|
L'ensemble d'outils inclut les éléments suivants :

-   Un package Key Exchange Key (KEK) dont le nom commence par **BYOK-KEK-pkg-**.

-   Un package Security World dont le nom commence par **BYOK-SecurityWorld-pkg-**.

-   Un script Python nommé **verifykeypackage.py**.

-   Un fichier exécutable en ligne de commande nommé **KeyTransferRemote.exe**, un fichier de métadonnées nommé **KeyTransferRemote.exe.config** et les fichiers DLL associés.

-   Un package Visual C++ Redistribuable, nommé **vcredist_x64.exe**.

Copiez le package sur une clé USB ou un autre support de stockage portable.

## préparation du poste de travail déconnecté
Pour préparer le poste de travail non connecté à un réseau (ni à Internet, ni à votre réseau interne), suivez ces 2 étapes :

-   [Étape 1 : préparation du poste de travail déconnecté avec le module de sécurité matériel Thales](#step-1-prepare-the-disconnected-workstation-with-thales-hsm)

-   [Étape 2 : installation de l'ensemble d'outils BYOK sur le poste de travail déconnecté](#step-2-install-the-byok-toolset-on-the-disconnected-workstation)

### Étape 1 : préparation du poste de travail déconnecté avec le module de sécurité matériel Thales
Sur le poste de travail déconnecté, installez le logiciel de support nCipher (Thales) sur un ordinateur Windows, puis joignez un module de sécurité matériel Thales à cet ordinateur.

Vérifiez que les outils Thales se trouvent dans votre chemin **(%nfast_home%\bin** et **%nfast_home%\python\bin)**. Par exemple, tapez ce qui suit :

```
set PATH=%PATH%;”%nfast_home%\bin”;”%nfast_home%\python\bin”
```
Pour plus d'informations, reportez-vous au guide d'utilisation inclus avec le module de sécurité matériel Thales, ou visitez le site Web de Thales pour Azure RMS à l'adresse [http://www.thales-esecurity.com/msrms/cloud](http://www.thales-esecurity.com/msrms/cloud).

### Étape 2 : installation de l'ensemble d'outils BYOK sur le poste de travail déconnecté
Copiez le package de l'ensemble d'outils BYOK à partir de la clé USB ou du support de stockage portable utilisé, puis procédez comme suit :

1.  Extrayez les fichiers du package téléchargé dans un dossier.

2.  À partir de ce dossier, exécutez le fichier vcredist_x64.exe.

3.  Suivez les instructions pour installer les composants d’exécution Visual C++ pour Visual Studio 2012.

## Génération de la clé de locataire
Sur le poste de travail déconnecté, suivez ces 3 étapes pour générer votre propre clé de locataire :

-   [Étape 1 : création d'un monde de sécurité](#step-1-create-a-security-world)

-   [Étape 2 : validation du package téléchargé](#step-2-validate-the-downloaded-package)

-   [Étape 3 : création d'une nouvelle clé](#step-3-create-a-new-key)

### Étape 1 : création d'un monde de sécurité
Ouvrez une invite de commande et exécutez le programme de nouveau monde Thales.

```
new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3
```
Ce programme crée un fichier **Security World** à l’emplacement %NFAST_KMDATA%\local\world, qui correspond au dossier C:\ProgramData\nCipher\Key Management Data\local. Vous pouvez utiliser différentes valeurs pour le quorum mais, dans notre exemple, vous êtes invité à entrer trois cartes et codes confidentiels nuls pour chacun. Deux des trois cartes seront ensuite nécessaires pour avoir un accès administratif au monde de sécurité (votre quorum spécifié).  Ces cartes constituent l' **ensemble de cartes administrateur** du nouveau monde de sécurité. À ce stade, vous pouvez spécifier le mot de passe ou code confidentiel pour chaque carte ACS, ou l'ajouter ultérieurement avec une commande.

> [!TIP]
> Vous pouvez vérifier l'état actuel de la configuration de votre module de sécurité matériel à l'aide de la commande `nkminfo` .

Ensuite, procédez comme suit :

1.  Installez le fournisseur Thales CNG tel que décrit dans la documentation Thales et configurez-le pour utiliser le nouveau monde de sécurité.

2.  Sauvegardez le fichier world dans **%nfast_kmdata%\local**. Sécurisez et protégez ensuite le fichier de monde, les cartes administrateur et leurs codes confidentiels. Veillez à ce que personne n'ait accès à plus d'une carte.

### Étape 2 : validation du package téléchargé
Cette étape est facultative mais recommandée, pour vous permettre de vérifier les points suivants :

-   la clé d'échange de clés incluse dans l'ensemble d'outils a été générée à partir d'un module de sécurité matériel Thales authentique ;

-   le hachage d'Azure RMS Security World inclus dans l'ensemble d'outils a été généré au sein d'un module de sécurité matériel Thales authentique ;

-   la clé d'échange de clés n'est pas exportable.

> [!NOTE]
> Pour valider le package téléchargé, le module de sécurité matériel doit être connecté, sous tension et doté d'un monde de sécurité (tel que celui que vous avez créé).

#### Pour valider le package téléchargé

1.  Exécutez le script verifykeypackage.py en tapant l'une des commandes ci-après, selon votre région :

    -   Pour l'Amérique du Nord :

        ```
        python verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
        ```

    -   Pour l'Europe :

        ```
        python verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
        ```

    -   Pour l'Asie :

        ```
        python verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
        ```

    > [!TIP]
    > Le logiciel Thales inclut un interpréteur Python sous %NFAST_HOME%\python\bin.

2.  Vérifiez que les éléments suivants s'affichent. Ils indiquent une validation réussie : **Résultat :  SUCCESS**

Ce script valide la chaîne de signataire jusqu'à la clé racine Thales. Le hachage de cette clé racine est incorporé dans le script. Sa valeur doit être **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**. Vous pouvez également confirmer cette valeur séparément via le [site web de Thales](http://www.thalesesec.com/).

Vous pouvez à présent créer une clé qui sera votre clé de locataire RMS.

### Étape 3 : création d'une nouvelle clé
Générez une clé CNG à l'aide des programmes Thales **generatekey** et **cngimport** .

Exécutez la commande suivante pour générer la clé :

```
generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=
```
Tenez compte des instructions suivantes pour l'exécution de cette commande :

-   Le paramètre **protect** doit être définie sur la valeur **module**, comme indiqué. Ceci crée une clé protégée par module. L’ensemble d’outils BYOK ne prend pas en charge les clés protégées par OCS.

-   Nous recommandons la taille de clé 2048, mais les clés RSA 1024 bits sont également prises en charge pour les clients AD RMS existants possédant de telles clés et migrant vers Azure RMS.

-   Remplacez la valeur de *contosokey* pour les paramètres **ident** et **plainname** par une valeur de chaîne. Afin de minimiser la charge administrative et de réduire le risque d'erreurs, nous vous recommandons d'utiliser la même valeur pour les deux et d'utiliser des caractères en minuscules.

-   La zone pubexp est vide (par défaut) dans cet exemple, mais vous pouvez indiquer des valeurs spécifiques. Pour plus d'informations, consultez la documentation Thales.

Exécutez ensuite la commande suivante pour importer la clé dans CNG :

```
cngimport --import -M --key=contosokey --appname=simple contosokey
```
Tenez compte des instructions suivantes pour l'exécution de cette commande :

-   Remplacez *contosokey* par la même valeur que celle spécifiée à l’[Étape 1 : création d’un monde de sécurité](#step-1-create-a-security-world) de la section *Génération de votre clé de locataire*.

-   Utilisez l’option **-M** afin que la clé convienne pour ce scénario. Dans le cas contraire, la clé résultante sera une clé spécifique à l'utilisateur actuel.

-   L’option **appname** est le nom de l’application indiqué dans le fichier de clé. Si vous avez utilisé ces instructions pour créer une clé, nous avons utilisé la valeur « simple » comme indiqué dans la commande. Cependant, si vous migrez une clé protégée par module de sécurité matériel existante pour une migration d’AD RMS vers Azure RMS, spécifiez votre nom existant dans cette commande et dans celle qui suivent quand elles utilisent également l’option appname.

Cette commande crée un fichier de clé tokenisée dans votre dossier %NFAST_KMDATA%\local avec un nom commençant par **key_caping`_`** suivi d’un SID. Par exemple : **key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb**. Ce fichier contient une clé chiffrée.

> [!TIP]
> Vous pouvez voir l'état actuel de la configuration de vos clés à l'aide de la commande `nkminfo –k` .

Sauvegardez ce fichier de clé tokénisée à un emplacement sûr.

> [!IMPORTANT]
> Lorsque vous transférerez ultérieurement votre clé à Azure RMS, Microsoft ne pourra pas réexporter cette clé. Il est donc extrêmement important que vous sauvegardiez soigneusement votre clé et votre monde de sécurité. Contactez Thales pour connaître les conseils et meilleures pratiques pour sauvegarder votre clé.

Vous pouvez à présent transférer votre clé de locataire à Azure RMS.

## préparation de la clé de client pour le transfert
Sur le poste de travail déconnecté, suivez ces 4 étapes pour préparer votre clé de locataire :

-   [Étape 1 : création d'une copie de la clé avec autorisations réduites](#step-1-create-a-copy-of-your-key-with-reduced-permissions)

-   [Étape 2 : inspection de la copie de la clé](#step-2-inspect-the-new-copy-of-the-key)

-   [Étape 3 : Chiffrer votre clé à l'aide de la clé d'échange de clés Microsoft](#step-3-encrypt-your-key-by-using-microsoft-s-key-exchange-key)

-   [Étape 4 : copie du package de transfert de clé sur le poste de travail connecté à Internet](#step-4-copy-your-key-transfer-package-to-the-internet-connected-workstation)

### Étape 1 : création d'une copie de la clé avec autorisations réduites
Procédez comme suit pour réduire les autorisations pour la clé de locataire :

-   Dans une invite de commande, exécutez l'une des commandes suivantes, selon votre région :

    -   Pour l'Amérique du Nord :

        ```
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
        ```

    -   Pour l'Europe :

        ```
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
        ```

    -   Pour l'Asie :

        ```
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
        ```

Lors de l’exécution de cette commande, remplacez *contosokey* par la même valeur que celle spécifiée à l’[Étape 1 : création d’un monde de sécurité](##step-1-create-a-security-world) de la section *Génération de votre clé de locataire*.

Vous serez invité à connecter vos cartes ACS de monde de sécurité et, le cas échéant, leur mot de passe ou code confidentiel.

Quand la commande se termine, vous voyez **Résultat : RÉUSSITE**, et la copie de votre clé de locataire avec des autorisations réduites est enregistrée dans le fichier nommé key_xferacId_*&lt;contosokey&gt;*.

### Étape 2 : inspection de la copie de la clé
Vous pouvez exécuter les utilitaires Thales pour confirmer les autorisations minimales sur la nouvelle clé de locataire :

-   aclprint.py :

    ```
    "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
    ```

-   kmfile-dump.exe :

    ```
    "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
    ```

Lors de l’exécution de cette commande, remplacez *contosokey* par la même valeur que celle spécifiée à l’[Étape 1 : création d’un monde de sécurité](##step-1-create-a-security-world) de la section *Génération de votre clé de locataire*.

### Étape 3 : Chiffrer votre clé à l'aide de la clé d'échange de clés Microsoft
Exécutez l'une des commandes suivantes, selon votre région :

-   Pour l'Amérique du Nord :

    ```
    KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -TenantBposId GUID -KeyFriendlyName ContosoFirstkey
    ```

-   Pour l'Europe :

    ```
    KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -TenantBposId GUID -KeyFriendlyName ContosoFirstkey
    ```

-   Pour l'Asie :

    ```
    KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -TenantBposId GUID -KeyFriendlyName ContosoFirstkey
    ```

Tenez compte des instructions suivantes pour l'exécution de cette commande :

-   Remplacez *contosokey* par l’identificateur que vous avez utilisé pour générer la clé à l’[Étape 1 : création d’un monde de sécurité](##step-1-create-a-security-world) de la section *Génération de votre clé de locataire*.

-   Remplacez *GUID* par l’ID de locataire Azure Active Directory que vous avez récupéré à l’[Étape 2 : obtention de votre ID de locataire Azure Active Directory](#step-2-get-your-azure-active-directory-tenant-id) de la section *Préparation du poste de travail connecté à Internet*.

-   Remplacez *ContosoFirstKey* par une étiquette qui sera utilisée pour votre nom de fichier de sortie.

Une fois cette opération terminée avec succès, **Résultat : RÉUSSITE** s’affiche et un nouveau fichier apparaît dans le dossier actuel avec le nom suivant : TransferPackage-*ContosoFirstkey*.byok

### Étape 4 : copie du package de transfert de clé sur le poste de travail connecté à Internet
Utilisez une clé USB ou un autre support de stockage portable pour copier le fichier de sortie obtenu à l’étape précédente (KeyTransferPackage-*ContosoFirstkey*.byok) sur le poste de travail connecté à Internet.

> [!NOTE]
> Utilisez des pratiques de sécurité pour protéger le fichier, car il inclut votre clé privée.

## transfert de votre clé de client vers Azure RMS
Sur le poste de travail connecté à Internet, suivez ces 3 étapes pour transférer votre nouvelle clé de locataire à Azure RMS :

-   [Étape 1 : connexion à Azure RMS](#step-1-connect-to-azure-rms)

-   [Étape 2 : envoi du package de clé](#step-2-upload-the-key-package)

-   [Étape 3 : Énumérer vos clés de locataire selon les besoins](#step-3-enumerate-your-tenant-keys-as-needed)

### Étape 1 : connexion à Azure RMS
Revenez dans la fenêtre Windows PowerShell et procédez comme suit :

1.  Reconnectez-vous au service [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] :

    ```
    Connect-AadrmService
    ```

2.  Utilisez l'applet de commande [Get-AadrmKeys](http://msdn.microsoft.com/library/windowsazure/dn629420.aspx) pour afficher la configuration actuelle de votre clé de locataire :

    ```
    Get-AadrmKeys
    ```

### Étape 2 : envoi du package de clé
Utilisez l'applet de commande [Add-AadrmKey](http://msdn.microsoft.com/library/windowsazure/dn629418.aspx) pour télécharger le package de transfert de clé copié à partir du poste de travail déconnecté :

```
Add-AadrmKey –KeyFile <PathToPackageFile> -Verbose
```
> [!WARNING]
> Vous êtes invité à confirmer cette action. Il est important de noter que cette action ne peut pas être annulée. Quand vous téléchargez une clé de locataire, elle devient automatiquement la clé de locataire principale de votre organisation et les utilisateurs commencent à l'utiliser dès qu'ils protègent des documents et des fichiers.

Si l'envoi abouti, le message suivant s'affiche : **« The Rights management service successfully added the key. ».**

Notez que le changement prend un certain temps pour se propager à tous les centres de données [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

### Étape 3 : Énumérer vos clés de locataire selon les besoins
Utilisez à nouveau l'applet de commande Get-AadrmKeys pour afficher la modification de la clé de locataire, ou dès que vous souhaitez consulter la liste de vos clés de locataire. Cette liste comprend la clé de locataire initiale générée par Microsoft ainsi que l'ensemble des clés de locataire que vous avez ajoutées.

```
Get-AadrmKeys
```
La clé de locataire marquée comme **Active** est celle actuellement utilisée par l'organisation pour protéger les documents et les fichiers.

Vous avez à présent effectué toutes les étapes requises pour la solution BYOK (Bring your own key) sur Internet, et vous pouvez passer aux étapes suivantes pour la planification et l’implémentation de votre clé de locataire.


> [!div class="button"]
[Étapes suivantes >>](plan-implement-tenant-key.md#next-steps)




<!--HONumber=Apr16_HO3-->


