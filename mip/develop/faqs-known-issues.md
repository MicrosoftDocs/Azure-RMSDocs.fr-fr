---
title: Questions fréquentes (FAQ) et problèmes connus – Kit SDK Microsoft Information Protection
description: Questions fréquentes sur le kit SDK Microsoft Information Protection (MIP) et conseils de résolution des problèmes et erreurs.
author: msmbaldwin
ms.service: information-protection
ms.topic: troubleshooting
ms.date: 03/05/2019
ms.author: mbaldwin
ms.openlocfilehash: da1e3f26ca4c2a0326b6ae8dfee7a13a1855044a
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212601"
---
# <a name="microsoft-information-protection-mip-sdk-faqs-and-issues"></a>Questions fréquentes (FAQ) sur le kit SDK Microsoft Information Protection (MIP) et problèmes

Cet article fournit des réponses aux Questions fréquentes (FAQ) et des conseils de dépannage pour les problèmes connus et les erreurs courantes.

## <a name="frequently-asked-questions"></a>Forum Aux Questions (FAQ)

### <a name="metadata-storage-changes"></a>Modifications du stockage des métadonnées

Nous avons [récemment annoncé](https://aka.ms/mipsdkmetadata) que nous avons apporté une modification à l’emplacement de stockage des métadonnées d’étiquette pour les fichiers Office (Word, Excel, PowerPoint) pour prendre en charge de nouvelles fonctionnalités dans Office 365, SharePoint Online et d’autres services.

#### <a name="metadata-faq"></a>FAQ sur les métadonnées

**Question**: quand les Premières fonctionnalités seront-elles disponibles qui nécessitent ce nouvel emplacement de stockage ?

- Nous pensons que les Premières fonctionnalités seront disponibles au cours du deuxième trimestre de l’année civile 2021. Les clients peuvent s’abonner à des versions préliminaires privées ou publiques.  

**Question**: les autres formats sont-ils affectés, tels que PDF ?

- Non, uniquement les fichiers Office, notamment les fichiers Word, Excel et PowerPoint.

**Question**: existe-t-il une version spécifique du kit de développement logiciel MIP nécessaire ?

- MIP SDK 1,7 et versions ultérieures sont entièrement compatibles.

**Question**: existe-t-il une version spécifique du client Office qui sera obligatoire ou utiliser ce magasin ?

- À mesure que les fonctionnalités sont annoncées, le client Office est mis à jour pour tirer parti du nouvel emplacement de stockage. Les nouveaux emplacements de stockage ne seront pas utilisés tant que les fonctionnalités ne sont pas activées par les administrateurs clients.

**Question**: les métadonnées existantes seront-elles stockées en tant que propriété personnalisée dans *custom.xml* être tenues à jour ?

- Non. La première fois que le document est enregistré après l’activation du nouvel emplacement de stockage, les métadonnées d’étiquette sont déplacées vers le nouvel emplacement. Les métadonnées écrites via [`LabelingOptions.ExtendedProperties`](https://docs.microsoft.com/dotnet/api/microsoft.informationprotection.file.labelingoptions.extendedproperties?view=mipsdk-dotnet-1.7#Microsoft_InformationProtection_File_LabelingOptions_ExtendedProperties) sont conservées dans *custom.xml*.

**Question**: est-il possible de lire les métadonnées d’étiquette sans le SDK MIP ? 

- Oui, mais vous devez implémenter votre propre code pour analyser le fichier et extraire les informations.

**Question**: actuellement, il est facile de « lire » l’étiquette en extrayant les chaînes de paires clé/valeur du fichier. La lecture sera-t-elle toujours possible de cette manière ? 

- Oui, les métadonnées sont toujours disponibles dans le fichier Office XML à lire. Toutefois, il convient de noter que votre application devra savoir si le nouvel ensemble de fonctionnalités est activé pour savoir quelle section fait autorité (custom.xml ou labelinfo.xml). Passez [en revue les propriétés de document MS-OFFCRYPTO : LabelInfo et personnalisées | Microsoft Docs.](https://docs.microsoft.com/openspecs/office_file_formats/ms-offcrypto/13939de6-c833-44ab-b213-e0088bf02341) Pour plus d’informations sur l’implémentation.
  
**Question**: Comment puis-je découvrir si les nouvelles fonctionnalités sont activées ? 

- Nous partagerons ces informations au fur et à mesure que nous aborderons les dates de publication des fonctionnalités. 

**Question**: comment les étiquettes seront-elles migrées ?

- La logique suivante est utilisée pour déterminer la section qui est lue et utilisée pour lire ou écrire des données d’étiquette.

| Action                                                                                                | Fonctionnalité non activée                                                                    | Fonctionnalité activée                                              |
| ----------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| Lire                                                                                                  | Étiquette dans custom.xml (non protégée) ou doc SummaryInfo (protégé).                      | Si l’étiquette existe dans labelinfo.xml, il s’agit de l’étiquette effective.<br> S’il n’existe aucune étiquette dans labelinfo.xml, label dans custom.xml ou doc SummaryInfo est l’étiquette effective. |
| Write                                                                                                 | Toutes les nouvelles étiquettes sont écrites dans custom.xml (non protégé) ou doc SummaryInfo (protégé). | Toutes les nouvelles étiquettes sont écrites dans labelinfo.xml.                 |


<br>
<br>

### <a name="file-parsing"></a>Analyse des fichiers

**Question**: puis-je écrire dans le même fichier que celui que je lise actuellement avec le kit de développement logiciel (SDK) de fichier ?

Le kit de développement logiciel MIP ne prend pas en charge la lecture et l’écriture simultanées du même fichier. Les fichiers étiquetés génèrent une *copie* du fichier d’entrée avec les actions d’étiquette appliquées. Votre application doit remplacer le fichier d’origine par le fichier étiqueté.

### <a name="sdk-string-handling"></a>Gestion des chaînes SDK

**Question**: comment le kit de développement logiciel (SDK) gère-t-il les chaînes et quel type de chaîne dois-je utiliser dans mon code ?

Le kit SDK est destiné à un usage multiplateforme et utilise [UTF-8 (Unicode Transformation Format - 8 bits)](https://wikipedia.org/wiki/UTF-8) pour gérer les chaînes. Les instructions varient selon la plateforme que vous utilisez :

| Plate-forme        | Guidance                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Windows natif  | Pour les clients SDK C++, le type de bibliothèque standard C++ [`std::string`](https://wikipedia.org/wiki/C%2B%2B_string_handling) est utilisé pour passer des chaînes vers/à partir de fonctions API. La conversion depuis/vers UTF-8 est gérée en interne par le SDK MIP. Quand un `std::string` est retourné à partir d’une API, vous devez vous attendre à un encodage UTF-8 et devez gérer la chaîne en conséquence si vous la convertissez. Dans certains cas, une chaîne est retournée en tant que partie d’un vecteur `uint8_t` (par exemple, une licence de publication), mais doit être traitée comme un objet blob opaque.<br><br>Pour plus d’informations et d’exemples, consultez :<ul><li>[Fonction WideCharToMultiByte](/windows/desktop/api/stringapiset/nf-stringapiset-widechartomultibyte) pour obtenir une assistance sur la conversion des chaînes de caractères larges en caractères multioctets, comme UTF-8.<li>Les exemples de fichiers suivants inclus dans le [téléchargement du kit SDK](setup-configure-mip.md#configure-your-client-workstation) :<ul><li>Les exemples de fonctions d’utilitaire de chaînes dans `file\samples\common\string_utils.cpp`, pour la conversion vers/depuis des chaînes UTF-8 larges.<li>Une implémentation de `wmain(int argc, wchar_t *argv[])` dans `file\samples\file\main.cpp`, qui utilise les fonctions de conversion de chaînes précédentes.</li></ul></ul> |
| .NET            | Pour les clients du kit SDK .NET, toutes les chaînes utilisent l’encodage UTF-16 par défaut et aucune conversion spéciale n’est nécessaire. La conversion depuis/vers UTF-16 est gérée en interne par le SDK MIP.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Autres plateformes | Toutes les autres plateformes prises en charge par le SDK MIP ont une prise en charge native d’UTF-8.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |

## <a name="issues-and-errors-reference"></a>Références sur les problèmes et les erreurs

### <a name="error-file-format-not-supported"></a>Erreur : « Format de fichier non pris en charge »  

**Question**: Pourquoi est-ce que j’obtiens l’erreur suivante lors d’une tentative de protection ou d’étiquetage d’un fichier PDF ?

> Format de fichier non pris en charge.

Cette exception résulte d’une tentative de protection ou d’étiquetage d’un fichier PDF signé numériquement ou protégé par un mot de passe. Voir [New support for PDF encryption with Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/New-support-for-PDF-encryption-with-Microsoft-Information/ba-p/262757) pour plus d’informations sur la protection et l’étiquetage de fichiers PDF.

### <a name="error-failed-to-parse-the-acquired-compliance-policy"></a>Erreur : « Échec d’analyse de la stratégie de conformité acquise »  

**Question**: Pourquoi est-ce que j’obtiens l’erreur suivante après le téléchargement du kit de développement logiciel MIP et que vous tentez d’utiliser l’exemple de fichier pour répertorier toutes les étiquettes ?

> Un problème s’est produit : Échec d’analyse de la stratégie de conformité acquise. Échec avec : [class mip::CompliancePolicyParserException] Étiquette introuvable : policy, Type de nœud : 15, Nom : Nom introuvable, Valeur : , Ancêtres : <SyncFile><Content>, correlationId:[34668a40-blll-4ef8-b2af-00005aa674z9]

Cette erreur indique que vous n’avez pas migré vos étiquettes de Azure Information Protection à l’expérience d’étiquetage unifiée. Suivez le [Guide pratique pour migrer les étiquettes Azure Information Protection vers le Centre de sécurité et conformité Office 365](/azure/information-protection/configure-policy-migrate-labels) pour migrer les étiquettes, puis créer une stratégie d’étiquette dans le Centre de conformité et de sécurité Office 365. 

### <a name="error-nopolicyexception-label-policy-did-not-contain-data"></a>Erreur : « NoPolicyException : la stratégie d’étiquette ne contenait pas de données »

**Question**: Pourquoi reçois-je l’erreur suivante en tentant de lire une étiquette ou une liste d’étiquettes via le kit de développement logiciel (SDK) MIP ?

> NoPolicyException : la stratégie d’étiquette ne contenait pas de données, CorrelationId = GUID, CorrelationId. Description = PolicyProfile, NoPolicyError. Category = SyncFile, NoPolicyError. Category = SyncFile

Cette erreur indique qu’une stratégie d’étiquette n’a pas été publiée dans le centre de conformité et de sécurité Microsoft. Suivez les sections [créer et configurer les étiquettes de sensibilité et leurs stratégies](/microsoft-365/compliance/create-sensitivity-labels) pour configurer la stratégie d’étiquetage.

### <a name="error-systemcomponentmodelwin32exception-loadlibrary-failed"></a>Erreur : « System. ComponentModel. Win32Exception : échec de LoadLibrary »

**Question**: Pourquoi est-ce que j’obtiens l’erreur suivante lors de l’utilisation du wrapper .net MIP SDK ?

> System. ComponentModel. Win32Exception : échec de LoadLibrary pour : [sdk_wrapper_dotnet.dll] lors de l’appel de MIP.Initialize ().

Votre application n’a pas le runtime requis ou n’a pas été créée en tant que version. Pour plus d’informations, consultez [vérifier que votre application possède le runtime requis](setup-configure-mip.md#ensure-your-app-has-the-required-runtime) . 

### <a name="error-proxyautherror-exception"></a>Erreur : « ProxyAuthError exception »

**Question**: Pourquoi est-ce que j’obtiens l’erreur suivante lors de l’utilisation du kit de développement logiciel MIP ?

> « ProxyAuthenticatonError : l’authentification du proxy n’est pas prise en charge »

Le kit de développement logiciel MIP ne prend pas en charge l’utilisation de proxys authentifiés. Pour résoudre ce message, les administrateurs de proxy doivent définir les points de terminaison du service Microsoft Information Protection pour ignorer le proxy. Une liste de ces points de terminaison est disponible à la page [URL Office 365 et plages d’adresses IP](/office365/enterprise/urls-and-ip-address-ranges) . Le kit de développement logiciel (SDK) MIP requiert que `*.protection.outlook.com` (ligne 9) et les points de terminaison de service Azure information protection (ligne 73) contourner l’authentification du proxy.
