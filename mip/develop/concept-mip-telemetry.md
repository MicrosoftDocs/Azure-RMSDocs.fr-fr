---
title: Concepts-principaux concepts du kit de développement logiciel MIP-contrôle de télémétrie
description: Cet article vous aidera à comprendre comment refuser la télémétrie et quels événements sont toujours envoyés en cas de refus.
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 10/01/2019
ms.author: tommos
ms.openlocfilehash: 3d97bdbf5307d7f0faefe6b6434b1df1ebc67798
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "74484851"
---
# <a name="microsoft-information-protection-sdk---telemetry-configuration"></a>Microsoft Information Protection SDK-configuration de la télémétrie

## <a name="telemetry"></a>Télémétrie

Par défaut, le kit de développement logiciel (SDK) Microsoft Information Protection envoie des données de télémétrie à Microsoft. Ces données de télémétrie sont utiles pour le dépannage des bogues, de la qualité et des problèmes de performances dans la base d’installation du kit de développement logiciel (SDK) que nous ne pouvons pas capturer dans nos tests internes. Lors de l’implémentation de votre application avec le kit de développement logiciel (SDK), il est important de donner aux utilisateurs et aux administrateurs la possibilité de refuser la télémétrie si nécessaire.

## <a name="telemetry-configuration"></a>Configuration de la télémétrie

Les options de télémétrie dans le kit de développement logiciel MIP peuvent être contrôlées via [TelemetryConfiguration](https://docs.microsoft.com/dotnet/api/microsoft.informationprotection.telemetryconfiguration?view=mipsdk-dotnet). Créez une instance de cette classe, puis affectez à **IsTelemetryOptedOut** la valeur true. Fournissez l’objet de la classe **TelemetryConfiguration** à la fonction utilisée pour créer **MipContext**. Cela n’élimine pas complètement les données de télémétrie, mais réduit à un nombre minimal d’informations identifiables par l’utilisateur final.

### <a name="minimum-telemetry-events"></a>Événements de télémétrie minimaux

Lorsque la télémétrie est définie sur la valeur *« refusé »* , un ensemble minimal de données est envoyé à Microsoft. Toutes les informations d’identification personnelle sont nettoyées à partir de ces informations. Ces données incluent des informations sur les pulsations pour comprendre que le kit de développement logiciel (SDK) est en cours d’utilisation et les métadonnées système. **Aucune information sur le contenu de l’utilisateur ou de l’utilisateur final n’est définie pour le service.**

Passez en revue les tableaux ci-dessous pour connaître exactement les événements et les données qui sont envoyés avec un ensemble de données de télémétrie minimal.

#### <a name="event-heartbeat"></a>Événement : pulsation

| Nom                                 | Description                                                                            | Nettoyés |
| ------------------------------------ | -------------------------------------------------------------------------------------- | -------- |
| App. ApplicationId                    | Identificateur d’application fourni via MIP :: ApplicationInfo.                          | Non       |
| App. ApplicationName                  | Nom de l’application fourni via MIP :: ApplicationInfo.                                | Non       |
| Application. ApplicationVersion               | La version de l’application, par le biais de MIP :: ApplicationInfo.                             | Non       |
| ApplicationId                        | La version de l’application, par le biais de MIP :: ApplicationInfo.                             | Non       |
| ApplicationName                      | Nom de l’application fourni via MIP :: ApplicationInfo.                                | Non       |
| CreationTime                         | L’événement de temps a été généré.                                                              | Non       |
| DefaultLabel.Id                      | ID d’étiquette par défaut du locataire.                                                               | Non       |
| Engine. TenantId                      | GUID du locataire de l’utilisateur authentifié.                                            | Non       |
| Engine. UserObjectId                  | ID d’objet utilisateur dans Azure Active Directory.                                              | Non       |
| Event. CorrelationId                  | ID unique généré associé à l’objet qui a déclenché l’événement.                   | Non       |
| Event. CorrelationIdDescription       | C++nom de classe de l’objet qui a déclenché l’événement.                                     | Non       |
| Event. ParentCorrelationId            | ID de corrélation de l’événement parent.                                                           | Non       |
| Event. ParentCorrelationIdDescription | ID unique généré associé au parent de l’objet qui a déclenché l’événement. | Non       |
| Event. UniqueId                       | ID unique généré affecté à l’événement.                                             | Non       |
| MachineName                          | Nom du système qui a généré l’événement.                                           | **Oui**  |
| MIP. Version                          | Version du kit de développement logiciel (SDK) MIP.                                                                | Non       |
| Opération                            | Pulsation                                                                              | Non       |
| OrganizationId                       | GUID du locataire de l’utilisateur authentifié.                                            | Non       |
| Plate-forme                             | Version du système d'exploitation.                                                              | Non       |
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
| Application. ApplicationVersion               | La version de l’application, par le biais de MIP :: ApplicationInfo.                             | Non       |
| ApplicationId                        | La version de l’application, par le biais de MIP :: ApplicationInfo.                             | Non       |
| ApplicationName                      | Nom de l’application fourni via MIP :: ApplicationInfo.                                | Non       |
| CreationTime                         | L’événement de temps a été généré.                                                              | Non       |
| dataState                            | L’état des données à mesure que l’application agit sur « REST », « MOTION », « USE ».           | Non       |
| DefaultLabel.Id                      | Identificateur d’étiquette par défaut du locataire.                                                       | Non       |
| Engine. TenantId                      | GUID du locataire de l’utilisateur authentifié.                                            | Non       |
| Engine. UserObjectId                  | Identificateur de l’objet utilisateur dans Azure Active Directory.                                      | Non       |
| Event. CorrelationId                  | ID unique généré associé à l’objet qui a déclenché l’événement.                   | Non       |
| Event. CorrelationIdDescription       | C++nom de classe de l’objet qui a déclenché l’événement.                                     | Non       |
| Event. ParentCorrelationId            | ID de corrélation de l’événement parent.                                                           | Non       |
| Event. ParentCorrelationIdDescription | ID unique généré associé au parent de l’objet qui a déclenché l’événement. | Non       |
| Event. UniqueId                       | ID unique généré affecté à l’événement.                                             | Non       |
| LabelId                              | Identificateur d’étiquette de contenu sur le fichier ou les données ouverts.                                   | Non       |
| MachineName                          | Nom du système qui a généré l’événement.                                           | **Oui**  |
| MIP. Version                          | Version du kit de développement logiciel (SDK) MIP.                                                                | Non       |
| ObjectId                             | Chemin d’accès/Description du fichier ou des données.                                             | **Oui**  |
| Opération                            | « Détection ».                                                                           | Non       |
| OrganizationId                       | GUID du locataire de l’utilisateur authentifié.                                            | Non       |
| Plate-forme                             | Version du système d'exploitation.                                                              | Non       |
| ProcessName                          | Nom du processus à l’aide du kit de développement logiciel (SDK).                                                     | Non       |
| Protégé                            | Valeur booléenne indiquant si le fichier est protégé ou non.                                       | Non       |
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
| Application. ApplicationVersion               | La version de l’application, par le biais de MIP :: ApplicationInfo.                             | Non       |
| ApplicationId                        | L’ID d’application fourni via MIP :: ApplicationInfo.                                  | Non       |
| ApplicationName                      | Nom de l’application fourni via MIP :: ApplicationInfo.                                | Non       |
| CreationTime                         | Heure à laquelle l’événement a été généré.                                                          | Non       |
| dataState                            | L’état des données à mesure que l’application agit sur « REST », « MOTION », « USE ».           | Non       |
| DefaultLabel.Id                      | Identificateur d’étiquette par défaut du locataire.                                                       | Non       |
| Engine. TenantId                      | GUID du locataire de l’utilisateur authentifié.                                            | Non       |
| Engine. UserObjectId                  | Identificateur de l’objet utilisateur dans Azure Active Directory.                                      | Non       |
| Event. CorrelationId                  | ID unique généré associé à l’objet qui a déclenché l’événement.                   | Non       |
| Event. CorrelationIdDescription       | C++nom de classe de l’objet qui a déclenché l’événement.                                     | Non       |
| Event. ParentCorrelationId            | ID de corrélation de l’événement parent.                                                           | Non       |
| Event. ParentCorrelationIdDescription | ID unique généré associé au parent de l’objet qui a déclenché l’événement. | Non       |
| Event. UniqueId                       | ID unique généré affecté à l’événement.                                             | Non       |
| IsLabelChanged                       | Valeur booléenne indiquant si l’étiquette a changé.                                                  | Non       |
| IsProtectionChanged                  | Valeur booléenne indiquant si la protection a changé.                                                 | Non       |
| LabelId                              | ID d’étiquette à appliquer au fichier ou aux données.                                    | Non       |
| LabelIdBefore                        | ID de l’étiquette précédente qui était sur le fichier ou les données.                                        | Non       |
| MachineName                          | Nom du système qui a généré l’événement.                                           | **Oui**  |
| MIP. Version                          | Version du kit de développement logiciel (SDK) MIP.                                                                | Non       |
| ObjectId                             | Chemin d’accès/Description du fichier ou des données.                                             | **Oui**  |
| Opération                            | « Modifier ».                                                                              | Non       |
| OrganizationId                       | GUID du locataire de l’utilisateur authentifié.                                            | Non       |
| Plate-forme                             | Version du système d'exploitation.                                                              | Non       |
| ProcessName                          | Nom du processus à l’aide du kit de développement logiciel (SDK).                                                     | Non       |
| Version du produit                      |                                                                                        | Non       |
| Protégé                            | Valeur booléenne indiquant si le fichier est protégé ou non.                                       | Non       |
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


### <a name="opting-out-in-c"></a>Vous en désabonnerC++

Pour définir la télémétrie sur minimum uniquement, créez un pointeur partagé de **MIP :: TelemetryConfiguration ()** et affectez à **isTelemetryOptedOut** la valeur true. Transmettez l’objet de configuration dans **MipContent :: Create ()** .

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

Pour définir la télémétrie sur minimum uniquement, créez un objet **TelemetryConfiguration ()** et affectez à **isTelemetryOptedOut** la valeur true. Transmettez l’objet de configuration dans au **MIP. CreateMipContext ()** .

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

