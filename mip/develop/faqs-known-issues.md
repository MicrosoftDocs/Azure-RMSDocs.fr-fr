---
title: Questions fréquentes (FAQ) et problèmes connus – Kit SDK Microsoft Information Protection
description: Questions fréquentes sur le kit SDK Microsoft Information Protection (MIP) et conseils de résolution des problèmes et erreurs.
author: msmbaldwin
ms.service: information-protection
ms.topic: troubleshooting
ms.date: 03/05/2019
ms.author: mbaldwin
ms.openlocfilehash: c599fdf5f44458aa390bade3736060919cb552e6
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/31/2019
ms.locfileid: "75555328"
---
# <a name="microsoft-information-protection-mip-sdk-faqs-and-issues"></a>Questions fréquentes (FAQ) sur le kit SDK Microsoft Information Protection (MIP) et problèmes

Cet article fournit des réponses aux Questions fréquentes (FAQ) et des conseils de dépannage pour les problèmes connus et les erreurs courantes.

## <a name="frequently-asked-questions"></a>Forum Aux Questions 

### <a name="sdk-string-handling"></a>Gestion des chaînes SDK

**Question**: comment le kit de développement logiciel (SDK) gère-t-il les chaînes et quel type de chaîne dois-je utiliser dans mon code ?

Le kit SDK est destiné à un usage multiplateforme et utilise [UTF-8 (Unicode Transformation Format - 8 bits)](https://wikipedia.org/wiki/UTF-8) pour gérer les chaînes. Les instructions varient selon la plateforme que vous utilisez :

| Plate-forme | Instructions |
|-|-|
| Windows natif | Pour les clients du SDK C++, le type de bibliothèque C++ Standard [`std::string`](https://wikipedia.org/wiki/C%2B%2B_string_handling) est utilisé pour passer des chaînes depuis/vers des fonctions API. La conversion depuis/vers UTF-8 est gérée en interne par le SDK MIP. Quand un `std::string` est retourné à partir d’une API, vous devez vous attendre à un encodage UTF-8 et devez gérer la chaîne en conséquence si vous la convertissez. Dans certains cas, une chaîne est retournée en tant que partie d’un vecteur `uint8_t` (par exemple, une licence de publication), mais doit être traitée comme un objet blob opaque.<br><br>Pour plus d’informations et d’exemples, consultez :<ul><li>[Fonction WideCharToMultiByte](/windows/desktop/api/stringapiset/nf-stringapiset-widechartomultibyte) pour obtenir une assistance sur la conversion des chaînes de caractères larges en caractères multioctets, comme UTF-8.<li>Les exemples de fichiers suivants inclus dans le [téléchargement du kit SDK](setup-configure-mip.md#configure-your-client-workstation) :<ul><li>Les exemples de fonctions d’utilitaire de chaînes dans `file\samples\common\string_utils.cpp`, pour la conversion vers/depuis des chaînes UTF-8 larges.<li>Une implémentation de `wmain(int argc, wchar_t *argv[])` dans `file\samples\file\main.cpp`, qui utilise les fonctions de conversion de chaînes précédentes.</li></ul></ul>|
| .NET | Pour les clients du kit SDK .NET, toutes les chaînes utilisent l’encodage UTF-16 par défaut et aucune conversion spéciale n’est nécessaire. La conversion depuis/vers UTF-16 est gérée en interne par le SDK MIP. |
| Autres plateformes | Toutes les autres plateformes prises en charge par le SDK MIP ont une prise en charge native d’UTF-8. |

## <a name="issues-and-errors-reference"></a>Références sur les problèmes et les erreurs

### <a name="error-file-format-not-supported"></a>Erreur : « Format de fichier non pris en charge »  

**Question**: Pourquoi est-ce que j’obtiens l’erreur suivante lors d’une tentative de protection ou d’étiquetage d’un fichier PDF ?

> Format de fichier non pris en charge

Cette exception résulte d’une tentative de protection ou d’étiquetage d’un fichier PDF signé numériquement ou protégé par un mot de passe. Voir [New support for PDF encryption with Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/New-support-for-PDF-encryption-with-Microsoft-Information/ba-p/262757) pour plus d’informations sur la protection et l’étiquetage de fichiers PDF.

### <a name="error-failed-to-parse-the-acquired-compliance-policy"></a>Erreur : « Échec d’analyse de la stratégie de conformité acquise »  

**Question**: Pourquoi est-ce que j’obtiens l’erreur suivante après le téléchargement du kit de développement logiciel MIP et que vous tentez d’utiliser l’exemple de fichier pour répertorier toutes les étiquettes ?

> Une erreur incorrecte s’est produite : échec de l’analyse de la stratégie de conformité acquise. Échec avec : la balise [classe MIP :: CompliancePolicyParserException] est introuvable : stratégie, NodeType : 15, nom : aucun nom trouvé, valeur :, ancêtres : <SyncFile><Content>, correlationId : [34668a40-blll-4ef8-B2AF-00005aa674z9]

Cela indique que vous n’avez pas migré vos étiquettes de Azure Information Protection à l’expérience d’étiquetage unifiée. Suivez le [Guide pratique pour migrer les étiquettes Azure Information Protection vers le Centre de sécurité et conformité Office 365](/azure/information-protection/configure-policy-migrate-labels) pour migrer les étiquettes, puis créer une stratégie d’étiquette dans le Centre de conformité et de sécurité Office 365. 

### <a name="error-systemcomponentmodelwin32exception-loadlibrary-failed"></a>Erreur : « System. ComponentModel. Win32Exception : échec de LoadLibrary »

**Question**: Pourquoi est-ce que j’obtiens l’erreur suivante lors de l’utilisation du wrapper .net MIP SDK ?

> System. ComponentModel. Win32Exception : échec de LoadLibrary pour : [sdk_wrapper_dotnet. dll] lors de l’appel de MIP. Initialize ().

Votre application n’a pas le runtime requis ou n’a pas été créée en tant que version. Pour plus d’informations, consultez [vérifier que votre application possède le runtime requis](setup-configure-mip.md#ensure-your-app-has-the-required-runtime) . 

### <a name="error-proxyautherror-exception"></a>Erreur : « ProxyAuthError exception »

**Question**: Pourquoi est-ce que j’obtiens l’erreur suivante lors de l’utilisation du kit de développement logiciel MIP ?

> « ProxyAuthenticatonError : l’authentification du proxy n’est pas prise en charge »

Le kit de développement logiciel MIP ne prend pas en charge l’utilisation de proxys authentifiés. Pour résoudre ce message, les administrateurs de proxy doivent définir les points de terminaison du service Microsoft Information Protection pour ignorer le proxy. Une liste de ces points de terminaison est disponible à la page [URL Office 365 et plages d’adresses IP](https://docs.microsoft.com/office365/enterprise/urls-and-ip-address-ranges) . Le kit de développement logiciel MIP requiert que `*.protection.outlook.com` (ligne 9) et les points de terminaison de service Azure Information Protection (ligne 73) contournent l’authentification du proxy.
