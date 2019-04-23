---
title: Questions fréquentes (FAQ) et problèmes connus – Kit SDK Microsoft Information Protection
description: Questions fréquentes sur le kit SDK Microsoft Information Protection (MIP) et conseils de résolution des problèmes et erreurs.
author: msmbaldwin
ms.service: information-protection
ms.topic: troubleshooting
ms.collection: M365-security-compliance
ms.date: 03/05/2019
ms.author: mbaldwin
ms.openlocfilehash: 78dc655d8244378fcc37b22030d3060fd291ef16
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "60175461"
---
# <a name="microsoft-information-protection-mip-sdk-faqs-and-issues"></a>Questions fréquentes (FAQ) sur le kit SDK Microsoft Information Protection (MIP) et problèmes

Cet article fournit des réponses aux Questions fréquentes (FAQ) et des conseils de dépannage pour les problèmes connus et les erreurs courantes.

## <a name="frequently-asked-questions"></a>Forum Aux Questions 

### <a name="sdk-string-handling"></a>Gestion des chaînes de kit de développement logiciel

**Question**: Comment le SDK gère-t-elle les chaînes, et quel type de chaîne dois-je utiliser dans mon code ?

Le kit SDK est destiné à un usage multiplateforme et utilise [UTF-8 (Unicode Transformation Format - 8 bits)](https://wikipedia.org/wiki/UTF-8) pour gérer les chaînes. Les instructions varient selon la plateforme que vous utilisez :

| Plateforme | Instructions |
|-|-|
| Windows natif | Pour les clients du SDK C++, le type de bibliothèque C++ Standard [ `std::string` ](https://wikipedia.org/wiki/C%2B%2B_string_handling) est utilisé pour passer des chaînes depuis/vers des fonctions API. La conversion depuis/vers UTF-8 est gérée en interne par le SDK MIP. Quand un `std::string` est retourné à partir d’une API, vous devez vous attendre à un encodage UTF-8 et devez gérer la chaîne en conséquence si vous la convertissez. Dans certains cas, une chaîne est retournée en tant que partie d’un vecteur `uint8_t` (par exemple, une licence de publication), mais doit être traitée comme un objet blob opaque.<br><br>Pour plus d’informations et d’exemples, consultez :<ul><li>[Fonction WideCharToMultiByte](/windows/desktop/api/stringapiset/nf-stringapiset-widechartomultibyte) pour obtenir une assistance sur la conversion des chaînes de caractères larges en caractères multioctets, comme UTF-8.<li>Les exemples de fichiers suivants inclus dans le [téléchargement du kit SDK](setup-configure-mip.md#configure-your-client-workstation) :<ul><li>Les exemples de fonctions d’utilitaire de chaînes dans `file\samples\common\string_utils.cpp`, pour la conversion vers/depuis des chaînes UTF-8 larges.<li>Une implémentation de `wmain(int argc, wchar_t *argv[])` dans `file\samples\file\main.cpp`, qui utilise les fonctions de conversion de chaînes précédentes.</li></ul></ul>|
| .NET | Pour les clients du kit SDK .NET, toutes les chaînes utilisent l’encodage UTF-16 par défaut et aucune conversion spéciale n’est nécessaire. La conversion depuis/vers UTF-16 est gérée en interne par le SDK MIP. |
| Autres plateformes | Toutes les autres plateformes prises en charge par le SDK MIP ont une prise en charge native d’UTF-8. |

## <a name="issues-and-errors-reference"></a>Références sur les problèmes et les erreurs

### <a name="error-file-format-not-supported"></a>Erreur : « Format de fichier non pris en charge »  

**Question**: Je reçois l’erreur suivante lorsque vous tentez de protéger ou d’un fichier PDF de l’étiquette ?

> Format de fichier non pris en charge.

Cette exception provoque de la tentative de protéger ou d’un fichier PDF qui a été signé numériquement de l’étiquette ou de mot de passe protégé. Voir [New support for PDF encryption with Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/New-support-for-PDF-encryption-with-Microsoft-Information/ba-p/262757) pour plus d’informations sur la protection et l’étiquetage de fichiers PDF.

### <a name="error-failed-to-parse-the-acquired-compliance-policy"></a>Erreur : « Impossible d’analyser la stratégie de conformité acquis »  

**Question**: Je reçois l’erreur suivante après le téléchargement du SDK MIP et tente d’utiliser l’exemple de fichier pour répertorier toutes les étiquettes ?

> Un problème s’est produit : Impossible d’analyser la stratégie de conformité acquis. A échoué avec : [classe mip::CompliancePolicyParserException] étiquette introuvable : stratégie, NodeType : 15, nom : Aucun nom trouvé, valeur :, ancêtres : <SyncFile> <Content>, ID de corrélation : [34668a40-blll-4ef8-b2af-00005aa674z9]

Cela indique que vous n’avez pas migré vos étiquettes d’Azure Information Protection à l’expérience d’étiquetage unifiée. Suivez le [Guide pratique pour migrer les étiquettes Azure Information Protection vers le Centre de sécurité et conformité Office 365](/azure/information-protection/configure-policy-migrate-labels) pour migrer les étiquettes, puis créer une stratégie d’étiquette dans le Centre de conformité et de sécurité Office 365. 

### <a name="error-systemcomponentmodelwin32exception-loadlibrary-failed"></a>Erreur : « System.ComponentModel.Win32Exception : Échec de LoadLibrary »

**Question**: Je reçois l’erreur suivante lors de l’utilisation du Wrapper de .NET SDK MIP ?

> System.ComponentModel.Win32Exception : LoadLibrary a échoué pour : [sdk_wrapper_dotnet.dll] lors de l’appel MIP. Initialize().

Votre application n’a pas le runtime requis, ou n’a pas été créée en tant que mise en production. Consultez [vous assurer que votre application dispose le runtime requis](setup-configure-mip.md#ensure-your-app-has-the-required-runtime) pour plus d’informations. 

### <a name="error-proxyautherror-exception"></a>Erreur : « exception ProxyAuthError »

**Question**: Je reçois l’erreur suivante lors de l’utilisation du SDK MIP ?

> « ProxyAuthenticatonError : L’authentification du proxy est non pris en charge »

Le SDK MIP ne prend pas en charge l’utilisation de serveurs proxy authentifiés. Pour résoudre ce message, les administrateurs de serveur proxy doivent définir les points de terminaison de service Microsoft Information Protection pour ignorer le proxy. Une liste de ces points de terminaison sont disponibles sur le [plages d’adresses IP et Office 365 URL](https://docs.microsoft.com/office365/enterprise/urls-and-ip-address-ranges) page. Du SDK MIP requiert que `*.protection.outlook.com` (lignes 9) et les points de terminaison de service Azure Information Protection (ligne 73) contournent l’authentification de proxy.
