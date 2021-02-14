---
title: Concepts-principaux concepts du kit de développement logiciel (SDK) MIP-contrôle de diagnostic
description: Cet article vous aidera à comprendre comment refuser les données de diagnostic et quels événements sont toujours envoyés quand ils sont désactivés.
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 10/01/2019
ms.author: tommos
ms.openlocfilehash: a0c8cd7d551f68242f67c8a3619fd0ff6fea64e9
ms.sourcegitcommit: 0f694bf6c7ea9c7709954bfb5dbd1c5f009b85a7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100360717"
---
# <a name="microsoft-information-protection-sdk---diagnostic-configuration"></a>SDK Microsoft Information Protection-configuration de diagnostic

## <a name="diagnostic-data"></a>Données de diagnostic

Par défaut, le kit de développement logiciel (SDK) Microsoft Information Protection envoie des données de diagnostic à Microsoft. Ces données sont utiles pour le dépannage des bogues, de la qualité et des problèmes de performances dans la base d’installation du kit de développement logiciel (SDK) que nous ne pouvons pas capturer dans nos tests internes. Lors de l’implémentation de votre application avec le kit de développement logiciel (SDK), il est important de donner aux utilisateurs et aux administrateurs la possibilité de refuser l’envoi de données de diagnostic si nécessaire.

## <a name="diagnostic-configuration"></a>Configuration du diagnostic

Les options de diagnostic dans le kit de développement logiciel MIP peuvent être contrôlées via `DiagnosticConfiguration` . Créez une instance de cette classe, puis affectez à **isMinimalTelemetryEnabled** la valeur true. Fournissez l’objet de la classe **DiagnosticConfiguration** à la fonction utilisée pour créer **MipContext**.

### <a name="minimum-diagnostic-events"></a>Événements de diagnostic minimum

Lorsque la configuration de diagnostic est définie sur minimale, un ensemble minimal de données est envoyé à Microsoft. Toutes les informations d’identification personnelle sont nettoyées à partir de ces informations. Ces données incluent des informations sur les pulsations pour comprendre que le kit de développement logiciel (SDK) est en cours d’utilisation et les métadonnées système. **Aucune information sur le contenu de l’utilisateur ou de l’utilisateur final n’est définie pour le service.**

Passez en revue les tableaux ci-dessous pour voir exactement quels événements et données sont envoyés avec les diagnostics minimum activés.

#### <a name="event-heartbeat"></a>Événement : pulsation

| Nom                                 | Description                                                                            | Nettoyés |
| ------------------------------------ | -------------------------------------------------------------------------------------- | -------- |
| App. ApplicationId                    | Identificateur d’application fourni via MIP :: ApplicationInfo.                          | Non       |
| App. ApplicationName                  | Nom de l’application fourni via MIP :: ApplicationInfo.                                | Non       |
| Application. ApplicationVersion               | Version de l’application fournie via MIP :: ApplicationInfo.                             | Non       |
| ApplicationId                        | Version de l’application fournie via MIP :: ApplicationInfo.                             | Non       |
| ApplicationName                      | Nom de l’application fourni via MIP :: ApplicationInfo.                                | Non       |
| CreationTime                         | L’événement de temps a été généré.                                                              | Non       |
| DefaultLabel.Id                      | ID d’étiquette par défaut du locataire.                                                               | Non       |
| Engine. TenantId                      | GUID du locataire de l’utilisateur authentifié.                                            | Non       |
| Engine. UserObjectId                  | ID d’objet utilisateur dans Azure Active Directory.                                              | Non       |
| Event. CorrelationId                  | ID unique généré associé à l’objet qui a déclenché l’événement.                   | Non       |
| Event. CorrelationIdDescription       | Nom de classe C++ de l’objet qui a déclenché l’événement.                                     | Non       |
| Event. ParentCorrelationId            | ID de corrélation de l’événement parent.                                                           | Non       |
| Event. ParentCorrelationIdDescription | ID unique généré associé au parent de l’objet qui a déclenché l’événement. | Non       |
| Event. UniqueId                       | ID unique généré affecté à l’événement.                                             | Non       |
| MachineName                          | Nom du système qui a généré l’événement.                                           | **Oui**  |
| MIP. Version                          | Version du kit de développement logiciel (SDK) MIP.                                                                | Non       |
| Opération                            | Heartbeat                                                                              | Non       |
| OrganizationId                       | GUID du locataire de l’utilisateur authentifié.                                            | Non       |
| Plate-forme                             | Version du système d’exploitation.                                                              | Non       |
| ProcessName                          | Nom du processus à l’aide du kit de développement logiciel (SDK).                                                     | Non       |
| ProductVersion                       | Identique à « App. ApplicationVersion ».                                                      | Non       |
| SDKVersion                           | Identique à MIP. Version.                                                                   | Non       |
| UserId                               | Adresse e-mail de l’utilisateur.                                                             | **Oui**  |
| UserObjectId                         | Azure AD ID d’objet de l’utilisateur.                                                        | Non       |
| Version                              | Schéma de la version d’audit (« 1,1 »).                                                          | Non       |

#### <a name="event-discovery"></a>Événement : découverte

| Nom                                 | Description                                                                            | Nettoyés |
| ------------------------------------ | -------------------------------------------------------------------------------------- | -------- |
| ActionId                             | ID d’action unique pour cet événement, utilisé pour la corrélation d’événements.                           | Non       |
| App. ApplicationId                    | Identificateur d’application fourni via MIP :: ApplicationInfo.                          | Non       |
| App. ApplicationName                  | Nom de l’application fourni via MIP :: ApplicationInfo.                                | Non       |
| Application. ApplicationVersion               | Version de l’application fournie via MIP :: ApplicationInfo.                             | Non       |
| ApplicationId                        | Version de l’application fournie via MIP :: ApplicationInfo.                             | Non       |
| ApplicationName                      | Nom de l’application fourni via MIP :: ApplicationInfo.                                | Non       |
| CreationTime                         | L’événement de temps a été généré.                                                              | Non       |
| DataState                            | L’état des données à mesure que l’application agit sur « REST », « MOTION », « USE ».           | Non       |
| DefaultLabel.Id                      | Identificateur d’étiquette par défaut du locataire.                                                       | Non       |
| Engine. TenantId                      | GUID du locataire de l’utilisateur authentifié.                                            | Non       |
| Engine. UserObjectId                  | Identificateur de l’objet utilisateur dans Azure Active Directory.                                      | Non       |
| Event. CorrelationId                  | ID unique généré associé à l’objet qui a déclenché l’événement.                   | Non       |
| Event. CorrelationIdDescription       | Nom de classe C++ de l’objet qui a déclenché l’événement.                                     | Non       |
| Event. ParentCorrelationId            | ID de corrélation de l’événement parent.                                                           | Non       |
| Event. ParentCorrelationIdDescription | ID unique généré associé au parent de l’objet qui a déclenché l’événement. | Non       |
| Event. UniqueId                       | ID unique généré affecté à l’événement.                                             | Non       |
| ID                              | Identificateur d’étiquette de contenu sur le fichier ou les données ouverts.                                   | Non       |
| MachineName                          | Nom du système qui a généré l’événement.                                           | **Oui**  |
| MIP. Version                          | Version du kit de développement logiciel (SDK) MIP.                                                                | Non       |
| ObjectId                             | Chemin d’accès/Description du fichier ou des données.                                             | **Oui**  |
| Opération                            | « Détection ».                                                                           | Non       |
| OrganizationId                       | GUID du locataire de l’utilisateur authentifié.                                            | Non       |
| Plate-forme                             | Version du système d’exploitation.                                                              | Non       |
| ProcessName                          | Nom du processus à l’aide du kit de développement logiciel (SDK).                                                     | Non       |
| Protected                            | Valeur booléenne indiquant si le fichier est protégé ou non.                                       | Non       |
| Protection                           | Identificateur du modèle de protection.                                                    | **Oui**  |
| ProtectionOwner                      | Adresse e-mail du propriétaire de la protection.                                                 | **Oui**  |
| SDKVersion                           | Identique à MIP. Version.                                                                   | Non       |
| UserId                               | Adresse e-mail de l’utilisateur.                                                             | **Oui**  |
| UserObjectId                         | Azure AD ID d’objet de l’utilisateur.                                                        | Non       |
| Version                              | Schéma de la version d’audit (« 1,1 »).                                                          | Non       |

#### <a name="event-label-change"></a>Événement : modification de l’étiquette

| Nom                                 | Description                                                                            | Nettoyés |
| ------------------------------------ | -------------------------------------------------------------------------------------- | -------- |
| ActionId                             | ID d’action unique pour cet événement, utilisé pour la corrélation d’événements.                           | Non       |
| ActionIdBefore                       | ID de l’action précédente. Utilisé pour chaîner à un nouvel ID d’action.                                    | Non       |
| ActionSource                         | Valeur de MIP :: ActionSource.                                                            | Non       |
| App. ApplicationId                    | L’ID d’application fourni via MIP :: ApplicationInfo.                                  | Non       |
| App. ApplicationName                  | Nom de l’application fourni via MIP :: ApplicationInfo.                                | Non       |
| Application. ApplicationVersion               | Version de l’application fournie via MIP :: ApplicationInfo.                             | Non       |
| ApplicationId                        | L’ID d’application fourni via MIP :: ApplicationInfo.                                  | Non       |
| ApplicationName                      | Nom de l’application fourni via MIP :: ApplicationInfo.                                | Non       |
| CreationTime                         | Heure à laquelle l’événement a été généré.                                                          | Non       |
| DataState                            | L’état des données à mesure que l’application agit sur « REST », « MOTION », « USE ».           | Non       |
| DefaultLabel.Id                      | Identificateur d’étiquette par défaut du locataire.                                                       | Non       |
| Engine. TenantId                      | GUID du locataire de l’utilisateur authentifié.                                            | Non       |
| Engine. UserObjectId                  | Identificateur de l’objet utilisateur dans Azure Active Directory.                                      | Non       |
| Event. CorrelationId                  | ID unique généré associé à l’objet qui a déclenché l’événement.                   | Non       |
| Event. CorrelationIdDescription       | Nom de classe C++ de l’objet qui a déclenché l’événement.                                     | Non       |
| Event. ParentCorrelationId            | ID de corrélation de l’événement parent.                                                           | Non       |
| Event. ParentCorrelationIdDescription | ID unique généré associé au parent de l’objet qui a déclenché l’événement. | Non       |
| Event. UniqueId                       | ID unique généré affecté à l’événement.                                             | Non       |
| IsLabelChanged                       | Valeur booléenne indiquant si l’étiquette a changé.                                                  | Non       |
| IsProtectionChanged                  | Valeur booléenne indiquant si la protection a changé.                                                 | Non       |
| ID                              | ID d’étiquette à appliquer au fichier ou aux données.                                    | Non       |
| LabelIdBefore                        | ID de l’étiquette précédente qui était sur le fichier ou les données.                                        | Non       |
| MachineName                          | Nom du système qui a généré l’événement.                                           | **Oui**  |
| MIP. Version                          | Version du kit de développement logiciel (SDK) MIP.                                                                | Non       |
| ObjectId                             | Chemin d’accès/Description du fichier ou des données.                                             | **Oui**  |
| Opération                            | « Modifier ».                                                                              | Non       |
| OrganizationId                       | GUID du locataire de l’utilisateur authentifié.                                            | Non       |
| Plate-forme                             | Version du système d’exploitation.                                                              | Non       |
| ProcessName                          | Nom du processus à l’aide du kit de développement logiciel (SDK).                                                     | Non       |
| Version du produit                      |                                                                                        | Non       |
| Protected                            | Valeur booléenne indiquant si le fichier est protégé ou non.                                       | Non       |
| Protégé avant                     | Valeur booléenne indiquant si le fichier a été précédemment protégé ou non.                           | Non       |
| Protection                           | Identificateur du modèle de protection.                                                    | Non       |
| Protection avant                    | Identificateur de modèle de protection précédent.                                           | Non       |
| ProtectionContentId                  | Nouvel identificateur de contenu (GUID).                                                     | Non       |
| ProtectionContentIdBefore            | Identificateur de contenu (GUID) précédent.                                                | Non       |
| ProtectionOwner                      | Adresse e-mail du propriétaire de la protection.                                                 | **Oui**  |
| ProtectionOwnerBefore                | Adresse e-mail précédente du propriétaire de la protection.                                        | **Oui**  |
| SDKVersion                           | Identique à MIP. Version.                                                                   | Non       |
| UserId                               | Adresse e-mail de l’utilisateur.                                                             | **Oui**  |
| UserObjectId                         | Azure AD ID d’objet de l’utilisateur.                                                        | Non       |
| Version                              | Schéma de la version d’audit (« 1,1 »).                                                          | Non       |

### <a name="opting-out-in-c"></a>Opt-out en C++

Pour définir le niveau de diagnostic sur minimal uniquement, créez un pointeur partagé de **MIP ::D iagnosticconfiguration ()** et affectez à **isMinimalTelemetryEnabled** la valeur true. Transmettez l’objet de configuration dans **MipContent :: Create ()**.

```cpp
auto diagnosticConfig = std::make_shared<mip::DiagnosticConfiguration>();
diagnosticConfig->isMinimalTelemetryEnabled = true;
                       
// Create MipContext, passing in mip::TelemetryConfiguration object.
mMipContext = mip::MipContext::Create(
    mAppInfo,
    "mip_data",
    mip::LogLevel::Trace,
    false,
    nullptr /*loggerDelegateOverride*/,
    diagnosticConfig /*diagnosticOverride*/
);
```

### <a name="opting-out-in-net"></a>Si vous optez pour .NET

Pour définir les données de diagnostic sur minimal uniquement, créez un objet **DiagnosticConfiguration ()** et affectez à **isMinimalTelemetryEnabled** la valeur true. Transmettez l’objet de configuration dans au **MIP. CreateMipContext ()**.

```csharp
DiagnosticConfiguration diagnosticConfiguration = new DiagnosticConfiguration();
diagnosticConfiguration.IsTelemetryOptedOut = true;

// Create MipContext, passing in TelemetryConfiguration object.
mipContext = MIP.CreateMipContext(appInfo, 
    "mip_data", 
    LogLevel.Trace, 
    null, 
    diagnosticConfiguration);
```
