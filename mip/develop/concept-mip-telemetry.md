---
title: Concepts-principaux concepts du kit de développement logiciel MIP-contrôle de télémétrie
description: Cet article vous aidera à comprendre comment refuser la télémétrie et quels événements sont toujours envoyés en cas de refus.
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 10/01/2019
ms.author: tommos
ms.openlocfilehash: 3df1283cd678167b7daa4a5fc64b5bb3d6d3fa33
ms.sourcegitcommit: 6b159e050176a2cc1b308b1e4f19f52bb4ab1340
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/30/2020
ms.locfileid: "95567912"
---
# <a name="microsoft-information-protection-sdk---telemetry-configuration"></a>Microsoft Information Protection SDK-configuration de la télémétrie

## <a name="telemetry"></a>Télémétrie

Par défaut, le kit de développement logiciel (SDK) Microsoft Information Protection envoie des données de télémétrie à Microsoft. Ces données de télémétrie sont utiles pour le dépannage des bogues, de la qualité et des problèmes de performances dans la base d’installation du kit de développement logiciel (SDK) que nous ne pouvons pas capturer dans nos tests internes. Lors de l’implémentation de votre application avec le kit de développement logiciel (SDK), il est important de donner aux utilisateurs et aux administrateurs la possibilité de refuser la télémétrie si nécessaire.

## <a name="telemetry-configuration"></a>Configuration de la télémétrie

Les options de télémétrie dans le kit de développement logiciel MIP peuvent être contrôlées via [TelemetryConfiguration](/dotnet/api/microsoft.informationprotection.telemetryconfiguration). Créez une instance de cette classe, puis affectez à **IsTelemetryOptedOut** la valeur true. Fournissez l’objet de la classe **TelemetryConfiguration** à la fonction utilisée pour créer **MipContext**.

### <a name="minimum-telemetry-events"></a>Événements de télémétrie minimaux

Lorsque la télémétrie est définie sur la valeur *« refusé »*, un ensemble minimal de données est envoyé à Microsoft. Toutes les informations d’identification personnelle sont nettoyées à partir de ces informations. Ces données incluent des informations sur les pulsations pour comprendre que le kit de développement logiciel (SDK) est en cours d’utilisation et les métadonnées système. **Aucune information sur le contenu de l’utilisateur ou de l’utilisateur final n’est définie pour le service.**

Passez en revue les tableaux ci-dessous pour connaître exactement les événements et les données qui sont envoyés avec un ensemble de données de télémétrie minimal.

#### <a name="event-heartbeat"></a>Événement : pulsation

| Name                                 | Description                                                                            | Nettoyés |
| ------------------------------------ | -------------------------------------------------------------------------------------- | -------- |
| App. ApplicationId                    | Identificateur d’application fourni via MIP :: ApplicationInfo.                          | No       |
| App. ApplicationName                  | Nom de l’application fourni via MIP :: ApplicationInfo.                                | No       |
| Application. ApplicationVersion               | La version de l’application, par le biais de MIP :: ApplicationInfo.                             | No       |
| ApplicationId                        | La version de l’application, par le biais de MIP :: ApplicationInfo.                             | No       |
| ApplicationName                      | Nom de l’application fourni via MIP :: ApplicationInfo.                                | No       |
| CreationTime                         | L’événement de temps a été généré.                                                              | No       |
| DefaultLabel.Id                      | ID d’étiquette par défaut du locataire.                                                               | No       |
| Engine. TenantId                      | GUID du locataire de l’utilisateur authentifié.                                            | No       |
| Engine. UserObjectId                  | ID d’objet utilisateur dans Azure Active Directory.                                              | No       |
| Event. CorrelationId                  | ID unique généré associé à l’objet qui a déclenché l’événement.                   | No       |
| Event. CorrelationIdDescription       | Nom de classe C++ de l’objet qui a déclenché l’événement.                                     | No       |
| Event. ParentCorrelationId            | ID de corrélation de l’événement parent.                                                           | No       |
| Event. ParentCorrelationIdDescription | ID unique généré associé au parent de l’objet qui a déclenché l’événement. | No       |
| Event. UniqueId                       | ID unique généré affecté à l’événement.                                             | No       |
| MachineName                          | Nom du système qui a généré l’événement.                                           | **Oui**  |
| MIP. Version                          | Version du kit de développement logiciel (SDK) MIP.                                                                | No       |
| Opération                            | Heartbeat                                                                              | No       |
| OrganizationId                       | GUID du locataire de l’utilisateur authentifié.                                            | No       |
| Plateforme                             | Version du système d’exploitation.                                                              | No       |
| ProcessName                          | Nom du processus à l’aide du kit de développement logiciel (SDK).                                                     | No       |
| ProductVersion                       | Identique à « App. ApplicationVersion ».                                                      | No       |
| SDKVersion                           | Identique à MIP. Version.                                                                   | No       |
| UserId                               | Adresse e-mail de l’utilisateur.                                                             | **Oui**  |
| UserObjectId                         | Azure AD ID d’objet de l’utilisateur.                                                        | No       |
| Version                              | Schéma de la version d’audit (« 1,1 »).                                                          | No       |

#### <a name="event-discovery"></a>Événement : découverte

| Name                                 | Description                                                                            | Nettoyés |
| ------------------------------------ | -------------------------------------------------------------------------------------- | -------- |
| ActionId                             | ID d’action unique pour cet événement, utilisé pour la corrélation d’événements.                           | No       |
| App. ApplicationId                    | Identificateur d’application fourni via MIP :: ApplicationInfo.                          | No       |
| App. ApplicationName                  | Nom de l’application fourni via MIP :: ApplicationInfo.                                | No       |
| Application. ApplicationVersion               | La version de l’application, par le biais de MIP :: ApplicationInfo.                             | No       |
| ApplicationId                        | La version de l’application, par le biais de MIP :: ApplicationInfo.                             | No       |
| ApplicationName                      | Nom de l’application fourni via MIP :: ApplicationInfo.                                | No       |
| CreationTime                         | L’événement de temps a été généré.                                                              | No       |
| DataState                            | L’état des données à mesure que l’application agit sur « REST », « MOTION », « USE ».           | No       |
| DefaultLabel.Id                      | Identificateur d’étiquette par défaut du locataire.                                                       | No       |
| Engine. TenantId                      | GUID du locataire de l’utilisateur authentifié.                                            | No       |
| Engine. UserObjectId                  | Identificateur de l’objet utilisateur dans Azure Active Directory.                                      | No       |
| Event. CorrelationId                  | ID unique généré associé à l’objet qui a déclenché l’événement.                   | No       |
| Event. CorrelationIdDescription       | Nom de classe C++ de l’objet qui a déclenché l’événement.                                     | No       |
| Event. ParentCorrelationId            | ID de corrélation de l’événement parent.                                                           | No       |
| Event. ParentCorrelationIdDescription | ID unique généré associé au parent de l’objet qui a déclenché l’événement. | No       |
| Event. UniqueId                       | ID unique généré affecté à l’événement.                                             | No       |
| ID                              | Identificateur d’étiquette de contenu sur le fichier ou les données ouverts.                                   | No       |
| MachineName                          | Nom du système qui a généré l’événement.                                           | **Oui**  |
| MIP. Version                          | Version du kit de développement logiciel (SDK) MIP.                                                                | No       |
| ObjectId                             | Chemin d’accès/Description du fichier ou des données.                                             | **Oui**  |
| Opération                            | « Détection ».                                                                           | No       |
| OrganizationId                       | GUID du locataire de l’utilisateur authentifié.                                            | No       |
| Plateforme                             | Version du système d’exploitation.                                                              | No       |
| ProcessName                          | Nom du processus à l’aide du kit de développement logiciel (SDK).                                                     | No       |
| Protected                            | Valeur booléenne indiquant si le fichier est protégé ou non.                                       | No       |
| Protection                           | Identificateur du modèle de protection.                                                    | **Oui**  |
| ProtectionOwner                      | Adresse e-mail du propriétaire de la protection.                                                 | **Oui**  |
| SDKVersion                           | Identique à MIP. Version.                                                                   | No       |
| UserId                               | Adresse e-mail de l’utilisateur.                                                             | **Oui**  |
| UserObjectId                         | Azure AD ID d’objet de l’utilisateur.                                                        | No       |
| Version                              | Schéma de la version d’audit (« 1,1 »).                                                          | No       |

#### <a name="event-label-change"></a>Événement : modification de l’étiquette

| Name                                 | Description                                                                            | Nettoyés |
| ------------------------------------ | -------------------------------------------------------------------------------------- | -------- |
| ActionId                             | ID d’action unique pour cet événement, utilisé pour la corrélation d’événements.                           | No       |
| ActionIdBefore                       | ID de l’action précédente. Utilisé pour chaîner à un nouvel ID d’action.                                    | No       |
| ActionSource                         | Valeur de MIP :: ActionSource.                                                            | No       |
| App. ApplicationId                    | L’ID d’application fourni via MIP :: ApplicationInfo.                                  | No       |
| App. ApplicationName                  | Nom de l’application fourni via MIP :: ApplicationInfo.                                | No       |
| Application. ApplicationVersion               | La version de l’application, par le biais de MIP :: ApplicationInfo.                             | No       |
| ApplicationId                        | L’ID d’application fourni via MIP :: ApplicationInfo.                                  | No       |
| ApplicationName                      | Nom de l’application fourni via MIP :: ApplicationInfo.                                | No       |
| CreationTime                         | Heure à laquelle l’événement a été généré.                                                          | No       |
| DataState                            | L’état des données à mesure que l’application agit sur « REST », « MOTION », « USE ».           | No       |
| DefaultLabel.Id                      | Identificateur d’étiquette par défaut du locataire.                                                       | No       |
| Engine. TenantId                      | GUID du locataire de l’utilisateur authentifié.                                            | No       |
| Engine. UserObjectId                  | Identificateur de l’objet utilisateur dans Azure Active Directory.                                      | No       |
| Event. CorrelationId                  | ID unique généré associé à l’objet qui a déclenché l’événement.                   | No       |
| Event. CorrelationIdDescription       | Nom de classe C++ de l’objet qui a déclenché l’événement.                                     | No       |
| Event. ParentCorrelationId            | ID de corrélation de l’événement parent.                                                           | No       |
| Event. ParentCorrelationIdDescription | ID unique généré associé au parent de l’objet qui a déclenché l’événement. | No       |
| Event. UniqueId                       | ID unique généré affecté à l’événement.                                             | No       |
| IsLabelChanged                       | Valeur booléenne indiquant si l’étiquette a changé.                                                  | No       |
| IsProtectionChanged                  | Valeur booléenne indiquant si la protection a changé.                                                 | No       |
| ID                              | ID d’étiquette à appliquer au fichier ou aux données.                                    | No       |
| LabelIdBefore                        | ID de l’étiquette précédente qui était sur le fichier ou les données.                                        | No       |
| MachineName                          | Nom du système qui a généré l’événement.                                           | **Oui**  |
| MIP. Version                          | Version du kit de développement logiciel (SDK) MIP.                                                                | No       |
| ObjectId                             | Chemin d’accès/Description du fichier ou des données.                                             | **Oui**  |
| Opération                            | « Modifier ».                                                                              | No       |
| OrganizationId                       | GUID du locataire de l’utilisateur authentifié.                                            | No       |
| Plateforme                             | Version du système d’exploitation.                                                              | No       |
| ProcessName                          | Nom du processus à l’aide du kit de développement logiciel (SDK).                                                     | No       |
| Version du produit                      |                                                                                        | No       |
| Protected                            | Valeur booléenne indiquant si le fichier est protégé ou non.                                       | No       |
| Protégé avant                     | Valeur booléenne indiquant si le fichier a été précédemment protégé ou non.                           | No       |
| Protection                           | Identificateur du modèle de protection.                                                    | No       |
| Protection avant                    | Identificateur de modèle de protection précédent.                                           | No       |
| ProtectionContentId                  | Nouvel identificateur de contenu (GUID).                                                     | No       |
| ProtectionContentIdBefore            | Identificateur de contenu (GUID) précédent.                                                | No       |
| ProtectionOwner                      | Adresse e-mail du propriétaire de la protection.                                                 | **Oui**  |
| ProtectionOwnerBefore                | Adresse e-mail précédente du propriétaire de la protection.                                        | **Oui**  |
| SDKVersion                           | Identique à MIP. Version.                                                                   | No       |
| UserId                               | Adresse e-mail de l’utilisateur.                                                             | **Oui**  |
| UserObjectId                         | Azure AD ID d’objet de l’utilisateur.                                                        | No       |
| Version                              | Schéma de la version d’audit (« 1,1 »).                                                          | No       |

### <a name="opting-out-in-c"></a>Opt-out en C++

Pour définir la télémétrie sur minimum uniquement, créez un pointeur partagé de **MIP :: TelemetryConfiguration ()** et affectez à **isTelemetryOptedOut** la valeur true. Transmettez l’objet de configuration dans **MipContent :: Create ()**.

```cpp
auto telemetryConfig = std::make_shared<mip::TelemetryConfiguration>();                                     
telemetryConfig->isTelemetryOptedOut = true;
                       
// Create MipContext, passing in mip::TelemetryConfiguration object.
mMipContext = mip::MipContext::Create(
    mAppInfo,
    "mip_data",
    mip::LogLevel::Trace,
    false,
    nullptr /*loggerDelegateOverride*/,
    telemetryConfig /*telemetryOverride*/
);
```

### <a name="opting-out-in-net"></a>Si vous optez pour .NET

Pour définir la télémétrie sur minimum uniquement, créez un objet **TelemetryConfiguration ()** et affectez à **isTelemetryOptedOut** la valeur true. Transmettez l’objet de configuration dans au **MIP. CreateMipContext ()**.

```csharp
TelemetryConfiguration telemetryConfiguration = new TelemetryConfiguration();
telemetryConfiguration.IsTelemetryOptedOut = true;

// Create MipContext, passing in TelemetryConfiguration object.
mipContext = MIP.CreateMipContext(appInfo, 
    "mip_data", 
    LogLevel.Trace, 
    null, 
    telemetryConfiguration);
```

## <a name="telemetry-in-mip-sdk-16102-to-16152"></a>Télémétrie dans le kit de développement logiciel (SDK) MIP 1.6.102 à 1.6.152

Dans les versions du SDK MIP 1.6.102, 103, 113, 151 et 152, il a été documenté que lorsque a la valeur `IsTelemetryOptedOut` **true** , aucune télémétrie n’est envoyée. Un bogue a été identifié et les événements de télémétrie ont été émis lorsque cet indicateur est défini. Ces événements de télémétrie sont déclenchés lors de l’appel des API ci-dessous dans le kit de développement logiciel (SDK) de stratégie.

- MIP ::P olicyEngine :: ListSensitivityLabels ()
- MIP ::P olicyHandler :: ComputeActions ()
- MIP ::P olicyHandler :: NotifyCommitAsync ()
- MIP ::P olicyHandler :: GetSensitivityLabel ()

La fonctionnalité de MIP SDK 1.6. n rétablit le comportement précédent et envoie les événements détaillés dans les [événements de télémétrie minimum](#minimum-telemetry-events). Le kit de développement logiciel (SDK) MIP 1,7 met à jour le nom de `IsTelemetryOptedOut` vers `SendMinimumTelemetry` et suit le même comportement que décrit ci-dessus.