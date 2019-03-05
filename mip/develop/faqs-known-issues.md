---
title: Questions fréquentes (FAQ) et problèmes connus – Kit SDK Microsoft Information Protection
description: Questions fréquentes sur le kit SDK Microsoft Information Protection (MIP) et conseils de résolution des problèmes et erreurs.
author: msmbaldwin
ms.service: information-protection
ms.topic: troubleshooting
ms.collection: M365-security-compliance
ms.date: 10/19/2018
ms.author: mbaldwin
ms.openlocfilehash: e548b2b6e9b32899ceff693312cf510b9fff74aa
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57333546"
---
# <a name="microsoft-information-protection-mip-sdk-faqs-and-issues"></a>Questions fréquentes (FAQ) sur le kit SDK Microsoft Information Protection (MIP) et problèmes

Cet article fournit des réponses aux Questions fréquentes (FAQ) et des conseils de dépannage pour les problèmes connus et les erreurs courantes.

## <a name="frequently-asked-questions"></a>Forum Aux Questions 

### <a name="question-how-does-the-sdk-handle-strings-and-what-string-type-should-i-be-using-in-my-code"></a>Question : Comment le kit SDK gère les chaînes, et quel type de chaîne utiliser dans mon code ?

Le kit SDK est destiné à un usage multiplateforme et utilise [UTF-8 (Unicode Transformation Format - 8 bits)](https://wikipedia.org/wiki/UTF-8) pour gérer les chaînes. Les instructions varient selon la plateforme que vous utilisez :

| Plateforme | Instructions |
|-|-|
| Windows natif | Pour les clients du SDK C++, le type de bibliothèque C++ Standard [ `std::string` ](https://wikipedia.org/wiki/C%2B%2B_string_handling) est utilisé pour passer des chaînes depuis/vers des fonctions API. La conversion depuis/vers UTF-8 est gérée en interne par le SDK MIP. Quand un `std::string` est retourné à partir d’une API, vous devez vous attendre à un encodage UTF-8 et devez gérer la chaîne en conséquence si vous la convertissez. Dans certains cas, une chaîne est retournée en tant que partie d’un vecteur `uint8_t` (par exemple, une licence de publication), mais doit être traitée comme un objet blob opaque.<br><br>Pour plus d’informations et d’exemples, consultez :<ul><li>[Fonction WideCharToMultiByte](/windows/desktop/api/stringapiset/nf-stringapiset-widechartomultibyte) pour obtenir une assistance sur la conversion des chaînes de caractères larges en caractères multioctets, comme UTF-8.<li>Les exemples de fichiers suivants inclus dans le [téléchargement du kit SDK](setup-configure-mip.md#configure-your-client-workstation) :<ul><li>Les exemples de fonctions d’utilitaire de chaînes dans `file\samples\common\string_utils.cpp`, pour la conversion vers/depuis des chaînes UTF-8 larges.<li>Une implémentation de `wmain(int argc, wchar_t *argv[])` dans `file\samples\file\main.cpp`, qui utilise les fonctions de conversion de chaînes précédentes.</li></ul></ul>|
| .NET | Pour les clients du kit SDK .NET, toutes les chaînes utilisent l’encodage UTF-16 par défaut et aucune conversion spéciale n’est nécessaire. La conversion depuis/vers UTF-16 est gérée en interne par le SDK MIP. |
| Autres plateformes | Toutes les autres plateformes prises en charge par le SDK MIP ont une prise en charge native d’UTF-8. |

## <a name="issues-and-errors-reference"></a>Références sur les problèmes et les erreurs

### <a name="error-file-format-not-supported"></a>Erreur : « Format de fichier non pris en charge »  

| Erreur | Solution |
|-|-|
|*Format de fichier non pris en charge.*| Cette exception vient de la tentative de protéger ou d’étiqueter un fichier PDF qui a été signé numériquement ou qui est protégé par un mot de passe. Voir [New support for PDF encryption with Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/New-support-for-PDF-encryption-with-Microsoft-Information/ba-p/262757) pour plus d’informations sur la protection et l’étiquetage de fichiers PDF.|

### <a name="error-failed-to-parse-the-acquired-compliance-policy"></a>Erreur : « Impossible d’analyser la stratégie de conformité acquis »  

Vous avez téléchargé le SDK MIP et exécuté les exemples d’applications. Vous utilisez l’exemple de fichier pour tenter de lister toutes les étiquettes, mais vous obtenez l’erreur suivante :

| Erreur | Solution |
|-|-|
|*Un problème s’est produit : Impossible d’analyser la stratégie de conformité acquis. A échoué avec : [classe mip::CompliancePolicyParserException] étiquette introuvable : stratégie, NodeType : 15, nom : Aucun nom trouvé, valeur :, ancêtres : <SyncFile> <Content>, ID de corrélation : [34668a40-blll-4ef8-b2af-00005aa674z9]*| Cela indique que vous n’avez pas migré vos étiquettes d’Azure Information Protection vers l’expérience d’étiquetage unifiée. Suivez le [Guide pratique pour migrer les étiquettes Azure Information Protection vers le Centre de sécurité et conformité Office 365](/azure/information-protection/configure-policy-migrate-labels) pour migrer les étiquettes, puis créer une stratégie d’étiquette dans le Centre de conformité et de sécurité Office 365. Une fois que vous avez terminé, l’exemple s’exécute correctement.|
