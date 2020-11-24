---
title: Notes de publication
description: Consultez les notes de publication du kit de développement logiciel (SDK) Microsoft Rights Management Service SDK v 2.1 octobre 2019 et les mises à jour précédentes.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 10/18/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: CE379738-4E1D-42AD-83F4-F89B70456EBB
audience: developer
ms.reviewer: kartikk
ms.suite: ems
ms.custom: dev, has-adal-ref
ms.openlocfilehash: f8b0aa99b4a18f1e2b9d0c9b3ddedf2d745b3e19
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/19/2020
ms.locfileid: "95568283"
---
# <a name="release-notes"></a>Notes de publication

Cet article contient des informations importantes sur cette version du SDK RMS 2.1 et les précédentes.

## <a name="october-2019---update"></a>Mise à jour d’octobre 2019

- Dans certains cas, l’utilisation de l’authentification par clé symétrique échoue à authentifier l’utilisateur avec Azure RMS qui empêche la protection et la déprotection du contenu.
- Le client RMS peut se bloquer lors d’une tentative de vérification de la protection d’un certain nombre de documents PDF précédemment protégés et non protégés.
- L’utilisation de la redirection DNS pour les serveurs AD RMS qui ont été configurés sur des ports spéciaux ne fonctionnera pas correctement.

## <a name="september-2019---update"></a>Septembre 2019-mise à jour

- Correction d’un blocage qui peut se produire lors d’une tentative d’appel des méthodes d’initialisation en même temps qu’une autre méthode de client RMS.
- Correction d’un problème de détermination de la protection RMS des fichiers Office protégés par mot de passe.
-   Mettez à jour la validation des licences pour des licences à usage spécial.
- Mises à jour de la protection PDF.
- Correctifs de bogues mineurs.
- Mettez à jour pour lier statiquement aux bibliothèques Runtime C.

## <a name="april-2019---update"></a>2019 avril-mise à jour
- Résolution des bogues dans l’API de fichier.
- API de fichier mise à jour pour vérifier le droit d’exportation au lieu du droit d’extraction lors du déchiffrement du contenu.
- Correctif du programme d’installation pour vérifier que le nouveau protecteur PDF v2 est installé lors de la mise à niveau.
- Modifications de télémétrie. Cette modification nécessitait une mise à jour du package d’installation qui installe les bibliothèques Runtime C.
- Modification de l’authentification backend du service, **Mettez à jour vers cette version du kit de développement logiciel (SDK) vers minmize interruption si vous utilisez l’authentification par clé symétrique pour vos applications**
- Prise en charge de VC 15,9


## <a name="october-2017---update"></a>Mise à jour d’octobre 2017

- Ajout de deux nouvelles API pour l’initialisation et désinitialisation de l’environnement. Pour plus d’informations, consultez [IpcInitializeEnvironment](/previous-versions/windows/desktop/msipc/microsoft-information-protection-and-control-client-functions) et [IpcUninitializeEnvironment](/previous-versions/windows/desktop/msipc/microsoft-information-protection-and-control-client-functions).
- Les types de fichiers Visio sont désormais pris en charge. Pour plus d’informations, consultez Configuration de l' [API de fichier](file-api-configuration.md).

## <a name="february-2016---sdk-documentation-update"></a>Février 2016 - Mise à jour de la documentation du SDK

>[!Note]
> Les mises à jour de la documentation de fonctionnalités dans cette section s’appliquent au téléchargement du SDK daté du 11/12/2015.

- **Amélioration du flux d’authentification** : utilisation de l’authentification basée sur les jetons OAuth2 par le biais de la [bibliothèque ADAL (Azure Active Directory Authentication Library)](/azure/active-directory/azuread-dev/active-directory-authentication-libraries). Pour plus d’informations sur ce processus et sur les extensions d’API, consultez [authentification Adal pour votre application compatible RMS](how-to-use-adal-authentication.md).

- **Mise à jour vers la bibliothèque ADAL** : en mettant à jour votre application pour utiliser l’authentification ADAL au lieu de l’Assistant de connexion Microsoft Online, vous et vos clients pouvez :

  - utiliser l’authentification multifacteur ;
  - Installer le client RMS 2.1 sans nécessiter de privilèges d’administration sur l’ordinateur.
  - Certifier votre application pour Windows 10

- **La prise en charge de l’Assistant de connexion Microsoft Online avec le SDK RMS est supprimée.** Nous continuerons à prendre en charge l’utilisation de l’Assistant de connexion pendant six mois, après quoi la prise en charge cessera.


## <a name="december-2015-update"></a>Mise à jour de décembre 2015

- Des améliorations de performances ont été implémentées dans plusieurs domaines :
    - Publication depuis le serveur de licences principal lors de l’utilisation de serveurs de licence.
    - RMS SDK 2.1 échoue plus rapidement lorsqu’il n’existe aucune connexion réseau.

- Nombreuses mises à jour pour améliorer les messages d’erreur et le dépannage.
- Notez également que la liste des [plates-formes prises en charge](supported-platforms.md) est également mise à jour.
- Le besoin d’un environnement de préproduction et l’utilisation d’un manifeste d’application ont été supprimés du kit SDK RMS 2.1. Les sections de cet ensemble de documentation pour développeurs ont été supprimées et l’ensemble de la documentation simplifié et réorganisé.

## <a name="may-2015-update"></a>Mise à jour de mai 2015

-   **Applications de service et RMS**  -  basé sur le Cloud [IPC \_ La \_ \_ clé symétrique des informations d’identification](/previous-versions/windows/desktop/msipc/ipc-credential-symmetric-key) a besoin de trois éléments d’information : clé symétrique, **AppPrincipalId** et **TenantBposId**. L’article traitant de ce sujet a été mis à jour pour fournir des conseils sur le traitement de ces informations. Pour cette mise à jour, consultez la version mise à jour de [Permettre à votre application de service de fonctionner avec le service RMS cloud](how-to-use-file-api-with-aadrm-cloud.md).

## <a name="april-2015-update"></a>Mise à jour d’avril 2015

-   Le **suivi des documents** est maintenant possible grâce à un ensemble de nouvelles API. Pour plus d’informations, consultez [suivi du contenu](tracking-content.md).
-   **Type de chiffrement** : nous prenons désormais en charge le contrôle au niveau de l’API pour la sélection du package de chiffrement. Pour plus d’informations, consultez [utilisation du chiffrement](working-with-encryption.md).

    **Remarque**    Nous n’exposerons plus l’indicateur **d' \_ \_ \_ \_ algorithmes de chiffrement IPC Li déconseillé** dans notre API. Cela signifie que les futures applications ne seront plus compilées si elles font référence à cet indicateur. Toutefois les applications déjà créées continueront de fonctionner dans la mesure où nous respecterons de manière privée l’indicateur dans le code de l’API. Il est encore possible de tirer parti de l’ancien indicateur obsolète des algorithmes de chiffrement en modifiant simplement un indicateur. Pour plus d’informations, consultez [utilisation du chiffrement](working-with-encryption.md).

-   Les **applications en mode serveur**, celles utilisant des [valeurs du mode API](/previous-versions/windows/desktop/msipc/api-mode-values) de **IPC\_API\_MODE\_SERVER**, n’ont plus besoin d’installer de manifeste d’application. Vous pouvez tester votre application sur un serveur RMS de production et vous n’êtes pas obligé d’obtenir une licence de production quand vous passez à l’environnement de production. Pour plus d’informations sur les applications en mode serveur, consultez [types d’applications](application-types.md).
-   La **journalisation** est maintenant implémentée par le biais du fichier et de méthodes de suivi d’événements pour Windows.
-   Si l’exécution s’effectue sur un **ordinateur Windows 7 SP1 ou Windows Server 2008 R2**, lisez la remarque suivante sous « Remarques importantes à l’attention des développeurs ».

## <a name="january-2015-update"></a>Mise à jour de janvier 2015

-   **Prise en charge de l’augmentation de la taille du fichier protégé (pfile)**  : prise en charge de tailles de fichiers supérieures à un gigaoctet (1 Go). Pour plus d’informations sur les fichiers pfile, consultez [Formats de fichiers pris en charge](supported-file-formats.md).
-   **Amélioration de la journalisation pour un meilleur diagnostic** : les niveaux de journalisation indiquent **ERREUR** ou **AVERTISSEMENT** pour les messages qui doivent être examinés. Tous les autres messages, y compris les exceptions, qui sont toujours affichés, sont enregistrés en tant qu' **informations**.

    Nous avons choisi cette approche afin de ne perdre aucun détail. À présent, seuls les messages importants ayant le niveau AVERTISSEMENT sont affichés.

-   **Acquisition des modèles d’une société** :corrections importantes apportées au code d’acquisition de modèles en fonction des rapports et des commentaires clients.
-   Amélioration de la cohérence de la localisation

## <a name="october-2014-update"></a>Mise à jour d’octobre 2014

-   Les comportements par défaut du composant de l’API de fichier du Kit de développement logiciel a été mis à jour. Pour plus d’informations, consultez Configuration de l' [API de fichier](file-api-configuration.md).
-   La notification par e-mail, qui est une nouvelle fonctionnalité, est décrite dans l’article sur les remarques à l’attention des développeurs [Activation des notifications par e-mail](how-to-enable-email-notification.md).

## <a name="july-2014-update"></a>Mise à jour de juillet 2014

Le composant de l’API de fichier du SDK a été étendu et offre les fonctionnalités suivantes :

-   Identifie le protecteur à utiliser.
-   Fournit une protection RMS au niveau de granularité d’un fichier.

    Fonctions ajoutées dans cette version :

    **Remarque**   -La prise en charge des types de données et des structures, non répertoriés ici, a été ajoutée pour les extensions de l’API de fichier. Tous les articles mis à jour pour cette version sont marqués comme étant **préliminaires et susceptible d’être modifiés**.

    -   [IpcfOpenFileOnHandle](/previous-versions/windows/desktop/msipc/ipcfopenfileonhandle)
    -   [IpcfOpenFileOnILockBytes](/previous-versions/windows/desktop/msipc/ipcfopenfileonilockbytes)
    -   [IpcfGetFileProperty](/previous-versions/windows/desktop/msipc/ipcfgetfileproperty)
    -   [IpcfLogicalFileRangeToRawFileRange](/previous-versions/windows/desktop/msipc/ipcflogicalfilerangetorawfilerange)
    -   [IpcfReadFile](/previous-versions/windows/desktop/msipc/ipcfreadfile)
    -   [IpcfSetEndOfFile](/previous-versions/windows/desktop/msipc/ipcfsetendoffile)
    -   [IpcfWriteFile](/previous-versions/windows/desktop/msipc/ipcfwritefile)

## <a name="april-2014-update"></a>Mise à jour d’avril 2014

-   L’**utilisation de la mémoire d’API de fichier**, en particulier pour les PFiles volumineux, a été considérablement améliorée.
-   L' **ID de contenu** est désormais accessible en écriture via l' **\_ \_ \_ ID de contenu IPC Li** de la propriété. Pour plus d’informations, consultez [Types de propriété de licence](/previous-versions/windows/desktop/msipc/license-property-types).
-   **Besoin du manifeste de production** : le manifeste n’est plus nécessaire lorsque votre service ou application compatible avec RMS est exécutée en mode serveur. Pour plus d’informations, consultez [types d’applications](application-types.md).
-   **Mises à jour de la documentation**

    **Meilleure pratique en matière de test** : ajout de conseils pour l’utilisation d’un serveur local avant le test avec Azure RMS. Pour plus d’informations, consultez [Permettre à votre application de service d’opérer avec le service RMS cloud](how-to-use-file-api-with-aadrm-cloud.md).

## <a name="important-developer-notes"></a>Remarques importantes à l’attention des développeurs

-   **Prise en charge native pour tous les types de fichier**

    Une prise en charge native peut être ajoutée pour tout type de fichier (extension) avec cette version du SDK Rights Management Services 2.1. Par exemple, pour toute extension &lt;ext&gt; (non Office et pdf), \*.p&lt;ext&gt; est utilisé si la configuration d’administration pour cette extension est « NATIVE ».

    Pour plus d’informations sur les types de fichiers pris en charge, consultez Configuration de l' [API de fichier](file-api-configuration.md).

-   Les **ordinateurs Windows 7 SP1 et Windows Server 2008 R2 SP1** non dotés de la mise à jour [KB2533623](https://support.microsoft.com/kb/2533623) peuvent afficher l’erreur suivante lors de la protection des fichiers Office : « Le paramètre est incorrect. Code d’erreur 0x80070057 ». Si vous voyez cette erreur, réinstallez la mise à jour et réessayez. Si cette erreur persiste, contactez l’alias de commentaires de la version bêta du kit SDK RMS <rmcstbeta@microsoft.com>.

    **Remarque**    Depuis la version d’avril 2015, un contrôle a été ajouté au processus d’installation de cette base de connaissances.



-   **Intégration de l’API de fichier**

    L’ajout de l’API de fichier à Active Directory Rights Management Services offre les avantages et les fonctionnalités suivantes :

      - Vous pouvez protéger les données confidentielles de manière automatisée sans avoir à connaître les détails de l’implémentation de la Gestion des droits relatifs à l’information utilisée par les différents formats de fichiers.

      - Les fichiers Microsoft Office, Portable Document Format (PDF) et d’autres types de fichier sélectionnés peuvent être protégés à l’aide de la protection native. Pour obtenir la liste complète des types de fichiers qui peuvent être protégés avec la protection native, consultez Configuration de l' [API de fichier](file-api-configuration.md).

      - Tous les fichiers, à l’exception des fichiers système et des fichiers Office peuvent être protégés à l’aide du format de fichier de protégé par RMS (PFile).

    L’API de fichier est implémentée par le biais des quatre nouvelles fonctions suivantes : [IpcfDecryptFile](/previous-versions/windows/desktop/msipc/ipcfdecryptfile), [IpcfEncryptFile](/previous-versions/windows/desktop/msipc/ipcfencryptfile), [IpcfGetSerializedLicenseFromFile](/previous-versions/windows/desktop/msipc/ipcfgetserializedlicensefromfile) et [IpcfIsFileEncrypted](/previous-versions/windows/desktop/msipc/ipcfisfileencrypted).

    L’API de fichier exige l’installation du client RMS (Rights Management Services) 2.1 sur l’ordinateur client et la connectivité de l’ordinateur avec un serveur RMS. Pour plus d’informations sur le serveur RMS, sur le client RMS et sur leurs fonctionnalités, consultez le contenu TechNet de la [documentation RMS pour les professionnels de l’informatique](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771234(v=ws.10)).

-   **Problème** : lors de la création d’une nouvelle licence, les droits de propriété doivent être accordés de manière explicite.

    **Solution** : votre application doit ajouter explicitement les droits **Propriétaire** au propriétaire de la licence lors de la création d’une nouvelle licence à l’aide de [IpcCreateLicenseFromScratch](/previous-versions/windows/desktop/msipc/ipccreatelicensefromscratch). Pour plus d’informations, consultez [Ajouter des droits de propriétaire explicites](add-explicit-owner-rights.md).

-   **Problème**: si une application appelle [IpcProtectWindow](/previous-versions/windows/desktop/msipc/ipcprotectwindow) ou [IpcUnprotectWindow](/previous-versions/windows/desktop/msipc/ipcunprotectwindow) deux fois pour la même fenêtre à l’aide de son handle, kit de développement logiciel (SDK) RMS 2,1 renverra un échec dans le **HRESULT**.

    **Solution**: pour obtenir des instructions spécifiques, consultez la section Notes dans [IpcProtectWindow](/previous-versions/windows/desktop/msipc/ipcprotectwindow) et [IpcUnprotectWindow](/previous-versions/windows/desktop/msipc/ipcunprotectwindow).

-   **Problème** : lors de la création de plusieurs architectures, vous devez utiliser ce guide.

    **Solution**: Si vous souhaitez utiliser leisv.dll Ipcsecproc \* pour une architecture différente (par exemple, vous avez installé le kit de développement logiciel (SDK) 64 bits sur un ordinateur 64 bits, mais vous souhaitez à présent le déployer sur un ordinateur 32 bits qui requiert Ipcsecproc \*isv.dll), vous devez installer le kit de développement logiciel (SDK) 32 bits sur un autre ordinateur et y copier les \* fichiers Ipcsecprocisv.dll à partir du dossier "% ProgramFiles% \\ Microsoft information protection

## <a name="frequently-asked-questions"></a>Forum aux questions

**Q** : Comment se comporte la langue par défaut avec des fonctions qui prennent un paramètre LCID ?

**R** : Utilisez 0 pour les paramètres régionaux par défaut. Dans ce cas, le client AD RMS 2.1 recherche les noms et les descriptions dans l’ordre suivant et récupère le premier disponible :

1. LCID préféré de l’utilisateur.
2. LCID des paramètres régionaux système.
3. La première langue disponible spécifiée dans le modèle de serveur Rights Management (RMS).

Si aucun nom et aucune description ne peuvent être récupérés, une erreur est renvoyée. Un LCID spécifique ne peut avoir qu’un seul nom et qu’une seule description.