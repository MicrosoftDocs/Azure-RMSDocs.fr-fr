---
title: FAQ pour le client Azure Information Protection Classic
description: Quelques questions fréquemment posées sur Azure Information Protection et son service de protection, Azure Rights Management (Azure RMS). Les FAQ répertoriées ici sont pertinentes pour le client standard AIP uniquement.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 03/07/2021
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: 9f53544a201d3500f63c472b5cdd58e01c69dc1f
ms.sourcegitcommit: 8a45d209273d748ee0f2a96c97893288c0b7efa5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/08/2021
ms.locfileid: "102446896"
---
# <a name="frequently-asked-questions-for-the-azure-information-protection-classic-client"></a>Forum aux questions sur le client Azure Information Protection Classic

>***S’applique à** : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Concerne**: [client classique d’étiquetage unifié AIP uniquement](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Pour plus d’informations, consultez le [Forum aux questions pour Azure information protection](faqs.md). *

Cet article répertorie les questions fréquemment posées relatives au client Azure Information Protection Classic.

>[!NOTE] 
> Pour fournir une expérience client unifiée et homogène, le **client classique Azure Information Protection** et la **gestion des étiquettes** dans le portail Azure seront **dépréciés** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

## <a name="is-the-azure-information-protection-client-only-for-subscriptions-that-include-classification-and-labeling"></a>Le client Azure Information Protection est-il réservé aux abonnements qui comprennent la classification et l’étiquetage ?

Non. Le client AIP classique peut également être utilisé avec les abonnements qui incluent uniquement le service Azure Rights Management, pour la protection des données uniquement.

Lorsque le client Classic est installé sans Azure Information Protection stratégie, le client fonctionne automatiquement en [mode protection uniquement](./rms-client/client-protection-only-mode.md), ce qui permet aux utilisateurs d’appliquer des modèles de Rights Management et des autorisations personnalisées. 

Si vous décidez, plus tard, de souscrire un abonnement qui n’inclut ni la classification ni l’étiquetage, le client passe automatiquement en mode standard lors du téléchargement de la stratégie Azure Information Protection.


## <a name="whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner"></a>Quelle est la différence entre Windows Server FCI et le scanneur Azure Information Protection ?

L’Infrastructure de classification des fichiers (ICF) de Windows Server a toujours été une option permettant de classer les documents et de les protéger à l’aide du [connecteur Rights Management](deploy-rms-connector.md) (documents Office uniquement) ou d’un [script PowerShell](./rms-client/configure-fci.md) (tous types de fichiers). 

Nous vous recommandons maintenant d’utiliser le [scanneur Azure Information Protection](deploy-aip-scanner.md). Ce scanneur utilise le client Azure Information Protection ainsi que votre stratégie Azure Information Protection pour étiqueter les documents (tous les types de fichiers) afin que ces documents soient ensuite classés, et si vous le souhaitez, protégés.

Les principales différences entre ces deux solutions sont les suivantes :

|  |ICF de Windows Server  |Scanneur Azure Information Protection  |
|---------|---------|---------|
|**Magasins de données pris en charge**    | Dossiers locaux sur Windows Server        | - Dispositif de stockage NAS et partages de fichiers Windows<br /><br />- SharePoint Server 2016 et SharePoint Server 2013. SharePoint Server 2010 est également pris en charge pour les clients qui bénéficient d’un [support étendu pour cette version de SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).        |
|**Mode opérationnel**     |En temps réel         |Analyse systématiquement les magasins de données une fois ou plusieurs fois.         |
|**Types de fichiers pris en charge**     | - Tous les types de fichiers sont protégés par défaut <br /><br />- Des types de fichiers spécifiques peuvent être exclus de la protection par modification du registre|Prise en charge des types de fichiers : <br /><br />- Les types de fichiers Office et les documents PDF sont protégés par défaut <br /><br />- Des types de fichiers supplémentaires peuvent être inclus dans la protection par modification du Registre|

### <a name="setting-rights-management-owners"></a>Définition des propriétaires de Rights Management

Par défaut, pour Windows Server FCI et le scanneur Azure Information Protection, le [propriétaire](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner) de la Rights Management est défini sur le compte qui protège le fichier.

Remplacez les paramètres par défaut comme suit :

- **Windows Server FCI**: définissez le Rights Management propriétaire comme un compte unique pour tous les fichiers, ou définissez dynamiquement le propriétaire Rights Management pour chaque fichier. 

    Pour définir le propriétaire de Rights Management de façon dynamique, utilisez le paramètre et la valeur **- OwnerMail [Source File Owner Email]**. Cette configuration récupère l’adresse e-mail de l’utilisateur à partir d’Active Directory en utilisant le nom du compte d’utilisateur dans la propriété Propriétaire du fichier.

- **Scanner de Azure information protection**: pour les fichiers récemment protégés, définissez le propriétaire de la Rights Management sur un seul compte pour tous les fichiers d’une banque de données spécifiée, en spécifiant le paramètre de **propriétaire par défaut** dans le profil du scanneur. 

    Le fait de définir dynamiquement le propriétaire de Rights Management pour chaque fichier n’est pas pris en charge et le propriétaire de Rights Management n’est pas modifié pour les fichiers précédemment protégés. 

    > [!NOTE]
    > Quand le scanneur protège les fichiers sur les sites et bibliothèques SharePoint, le propriétaire de Rights Management est défini dynamiquement pour chaque fichier à l’aide de la valeur de l’éditeur de SharePoint.

## <a name="can-a-file-have-more-than-one-classification"></a>Un fichier peut-il avoir plusieurs classifications ?

Les utilisateurs ne peuvent sélectionner qu’une seule étiquette à la fois pour chaque document ou e-mail, ce qui aboutit la plupart du temps à une classification unique pour chaque élément. Toutefois, si les utilisateurs sélectionnent une sous-étiquette, cela revient à appliquer deux étiquettes à la fois : une étiquette principale et une étiquette secondaire. Les sous-étiquettes permettent d’attribuer à un fichier deux classifications avec une relation parent\enfant afin d’obtenir un niveau de contrôle supplémentaire.

Par exemple, l’étiquette **confidentiel** peut contenir des sous-étiquettes telles que **juridique** et **finance**. Vous pouvez appliquer différents marquages de classification visuels et différents modèles Rights Management à ces sous-étiquettes. Un utilisateur ne peut pas sélectionner l’étiquette **confidentiel** elle-même ; une seule de ses sous-étiquettes, par exemple **légal**. L’étiquette qui s’affiche est donc **Confidentiel \ Juridique**. Les métadonnées de ce fichier incluent une propriété de texte personnalisée pour **Confidentiel**, une propriété de texte personnalisée pour **Juridique** et une autre qui contient les deux valeurs (**Confidentiel Juridique**). 

Quand vous utilisez des sous-étiquettes, ne configurez pas de marquages visuels, de protection ou de conditions pour l’étiquette principale. Quand vous utilisez des sous-niveaux, configurez ces paramètres pour la sous-étiquette uniquement. Si vous configurez ces paramètres sur l’étiquette principale et sa sous-étiquette, ce sont les paramètres de la sous-étiquette qui sont prioritaires.
## <a name="how-do-i-prevent-somebody-from-removing-or-changing-a-label"></a>Comment empêcher une personne de supprimer ou de changer une étiquette ?

Bien qu’il existe un [paramètre de stratégie](configure-policy-settings.md) qui oblige les utilisateurs à indiquer la raison pour laquelle ils abaissent une étiquette de classification, supprime une étiquette ou suppriment la protection, ce paramètre n’empêche pas ces actions. Pour empêcher les utilisateurs de supprimer ou de modifier une étiquette, le contenu doit déjà être protégé et les autorisations de protection n’accordent pas à l’utilisateur le [droit d’utilisation](configure-usage-rights.md) exportation ou contrôle total

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>Comment faire pour intégrer les solutions DLP et autres applications avec Azure Information Protection ?

Azure Information Protection utilisant des métadonnées persistantes pour la classification, notamment une étiquette de texte en clair, ces informations peuvent être lues par les solutions DLP et d’autres applications. 

Pour plus d’informations sur ces métadonnées, consultez [Étiquettes d’information stockées dans des e-mails et des documents](configure-policy.md#label-information-stored-in-emails-and-documents).

Pour obtenir des exemples d’utilisation de ces métadonnées avec des règles de flux de messagerie Exchange Online, consultez [Configuration des règles de flux de messagerie Exchange Online pour les étiquettes Azure Information Protection](configure-exo-rules.md).

## <a name="can-i-create-a-document-template-that-automatically-includes-the-classification"></a>Peut-on créer un modèle de document qui inclut automatiquement la classification ?

Oui. Vous pouvez configurer une étiquette qui [applique un en-tête ou un pied de page comportant le nom d’étiquette](configure-policy-markings.md). Toutefois, si cela ne répond pas à vos besoins, pour le client Azure Information Protection Classic uniquement, vous pouvez créer un modèle de document avec la mise en forme de votre choix et ajouter la classification en tant que code de champ. 

Par exemple, vous pouvez avoir une table dans l’en-tête de votre document qui affiche la classification, ou utiliser une formulation spécifique pour une introduction faisant référence à la classification du document.

Pour ajouter ce code de champ dans votre document :

1. Étiquetez le document et enregistrez-le. Cette action crée de nouveaux champs de métadonnées que vous pouvez alors utiliser dans votre code de champ.

2. Dans le document, placez le curseur à l’endroit où vous souhaitez ajouter la classification de l’étiquette ; ensuite, dans l’onglet **Insérer**, sélectionnez **Texte** > **QuickPart** > **Champ**.

3. Dans la liste déroulante **Catégories** de la boîte de dialogue **Champ**, sélectionnez **Informations sur le document**. Ensuite, dans la liste déroulante **Noms de champs**, sélectionnez **DocProperty**.

4. Dans la liste déroulante **Propriété**, sélectionnez **Sensibilité**, puis **OK**.

La classification de l’étiquette actuelle s’affiche dans le document ; cette valeur est actualisée automatiquement à chaque fois que vous ouvrez le document ou que vous utilisez le modèle. Par conséquent, lorsque l’étiquette change, la classification qui s’affiche pour ce code de champ est automatiquement mise à jour dans le document.

## <a name="how-is-classification-for-emails-using-azure-information-protection-different-from-exchange-message-classification"></a>Comment la classification des e-mails utilise-t-elle Azure Information Protection différente de la classification des messages Exchange ?

La classification des messages Exchange est une fonctionnalité plus ancienne qui peut classer les e-mails et est implémentée indépendamment des étiquettes de Azure Information Protection ou des étiquettes de sensibilité qui appliquent la classification.

Toutefois, vous pouvez intégrer cette fonctionnalité plus ancienne à des étiquettes, de sorte que lorsque les utilisateurs classifient un e-mail à l’aide d’Outlook sur le Web et en utilisant des applications de messagerie mobile, la classification des étiquettes et les marques d’étiquette correspondantes sont automatiquement ajoutées.

Vous pouvez utiliser cette même technique pour utiliser vos étiquettes avec Outlook sur le web et les applications de messagerie mobile.

Notez qu’il n’est pas nécessaire de le faire si vous utilisez Outlook sur le Web avec Exchange Online, car cette combinaison prend en charge l’étiquetage intégré lorsque vous publiez des étiquettes de sensibilité à partir du centre de conformité d’Office 365 Security &, Microsoft 365 Security Center ou Microsoft Compliance Center.

Si vous ne pouvez pas utiliser l’étiquetage intégré avec Outlook sur le Web, consultez les étapes de configuration de cette solution de contournement : [intégration à la classification des messages Exchange héritée](rms-client/client-admin-guide-customizations.md#integration-with-the-legacy-exchange-message-classification)

## <a name="how-do-i-configure-a-mac-computer-to-protect-and-track-documents"></a>Comment configurer un ordinateur Mac pour protéger et suivre les documents ?

Tout d’abord, assurez-vous que vous avez installé Office pour Mac en utilisant le lien d’installation à partir de https://admin.microsoft.com. Pour obtenir des instructions complètes, consultez [Télécharger et installer ou réinstaller Microsoft 365 ou Office 2019 sur un PC ou un Mac](https://support.office.com/article/Download-and-install-or-reinstall-Office-365-or-Office-2016-on-a-PC-or-Mac-4414EAAF-0478-48BE-9C42-23ADC4716658).

Ouvrez Outlook et créez un profil à l’aide de votre compte professionnel ou scolaire Microsoft 365. Ensuite, créez un nouveau message, puis procédez comme suit pour configurer Office afin qu’il puisse protéger les documents et e-mails à l’aide du service Azure Rights Management :

1. Dans le nouveau message, dans l’onglet **Options**, cliquez sur **Autorisations**, puis cliquez sur **Vérifier les informations d’identification**.

2. Lorsque vous y êtes invité, spécifiez à nouveau les détails de votre compte Microsoft 365 professionnel ou scolaire, puis sélectionnez **se connecter**.

    Cela permet de télécharger les modèles Azure Rights Management, et **Vérifier les informations** est remplacé par des options qui incluent **Aucune restriction**, **Ne pas transférer**, ainsi que les modèles Azure Rights Management qui sont publiés pour votre client. Vous pouvez désormais annuler ce nouveau message.

Pour protéger un message électronique ou un document : dans l’onglet **Options**, cliquez sur **Autorisations** et choisissez une option ou un modèle qui protège votre adresse e-mail ou un document.

Pour effectuer le suivi d’un document une fois que vous l’avez protégé : à partir d’un ordinateur Windows sur lequel est installé le client Azure Information Protection Classic, enregistrez le document avec le site de suivi des documents à l’aide d’une application Office ou de l’Explorateur de fichiers. Pour obtenir des instructions, consultez [Suivre et révoquer vos documents](./rms-client/client-track-revoke.md). À partir de votre ordinateur Mac, vous pouvez maintenant utiliser votre navigateur web pour accéder au site de suivi des documents (https://track.azurerms.com) pour suivre et révoquer ce document.

## <a name="when-i-test-revocation-in-the-document-tracking-site-i-see-a-message-that-says-people-can-still-access-the-document-for-up-to-30-daysis-this-time-period-configurable"></a>Lorsque je teste la révocation dans le site de suivi des documents, je vois un message m’indiquant que les autres utilisateurs continueront d’avoir accès au document pendant 30 jours. Cette durée est-elle configurable ?

Oui. Ce message indique la [licence d’utilisation](configure-usage-rights.md#rights-management-use-license) de ce fichier en particulier.

La révocation d’un fichier ne peut être appliquée que lorsque l’utilisateur doit s’authentifier auprès du service Azure Rights Management. Par conséquent, si la période de validité de la licence d’utilisation du fichier est de 30 jours et que l’utilisateur a déjà ouvert le document, il peut continuer d’y accéder pendant toute la durée de la licence d’utilisation. Quand la licence d’utilisation expire, l’utilisateur doit se réauthentifier et l’accès lui est refusé, car le document a été révoqué.

L’utilisateur qui a protégé le document, [l’émetteur Rights Management](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner) n’est pas concerné par cette révocation et peut toujours accéder à ses documents.

Pour un locataire, la période de validité par défaut d’une licence d’utilisation est de 30 jours. Vous pouvez remplacer ce paramètre par un paramètre plus restrictif dans une étiquette ou un modèle. Pour plus d’informations sur la licence d’utilisation et sa configuration, consultez la documentation [Licence d’utilisation Rights Management](configure-usage-rights.md#rights-management-use-license).

## <a name="whats-the-difference-between-byok-and-hyok-and-when-should-i-use-them"></a>Quelle est la différence entre BYOK et HYOK et quand dois-je les utiliser ?

Dans Azure Information Protection, la solution **Bring your own key** vous permet de créer votre propre clé en local pour la protection offerte par Azure Rights Management. Ensuite, vous transférez cette clé à un module de sécurité matériel (HSM, Hardware Security Module) dans Azure Key Vault, mais elle reste en votre possession et vous continuez à la gérer. Si vous ne procédez pas ainsi, la fonctionnalité de protection d’Azure Rights Management utilise une clé automatiquement créée et gérée pour vous dans Azure. Cette configuration par défaut est considérée comme « gérée par Microsoft » plutôt que « gérée par le client » (option BYOK).

Pour en savoir plus sur la solution BYOK et déterminer si vous devez choisir cette topologie de clé pour votre organisation, voir [Planification et implémentation de votre clé de locataire Azure Information Protection](plan-implement-tenant-key.md).

Dans Azure Information Protection, la solution **Hold your own key** (HYOK) est destinée au petit nombre d’organisations disposant d’un ensemble de documents ou d’e-mails qui ne peuvent pas être protégés par une clé stockée dans le cloud. Pour ces organisations, cette restriction s’applique, même si elles ont créé la clé et la gèrent via la solution BYOK. Cette restriction a souvent pour origine des problèmes de conformité et de réglementation, la configuration HYOK devant uniquement être appliquée aux informations « Top Secret », qui ne seront jamais partagées en dehors de l’organisation et seront uniquement utilisées sur le réseau interne, et qui ne devront pas nécessairement être accessibles depuis des appareils mobiles.

Pour ces exceptions (soit un maximum de 10 % des contenus devant être protégés, en moyenne), les organisations peuvent utiliser une solution locale, à savoir Active Directory Rights Management Services, pour créer la clé, qui restera en local. Avec cette solution, les ordinateurs récupèrent leur stratégie Azure Information Protection à partir du cloud, mais ce contenu identifié peut être protégé à l’aide de la clé en local.

Pour en savoir plus sur la solution HYOK et vous assurer que vous comprenez ses limitations et restrictions, tout en bénéficiant de conseils sur son utilisation, voir [HYOK (conservez votre propre clé) : exigences et restrictions pour la protection AD RMS](configure-adrms-restrictions.md).

## <a name="what-do-i-do-if-my-question-isnt-here"></a>Que dois-je faire si ma question n’est pas disponible ?

Tout d’abord, passez en revue les questions fréquemment posées répertoriées ci-dessous, qui sont spécifiques à la classification et à l’étiquetage, ou spécifiques à la protection des données. Le [service Azure Rights Management (Azure RMS)](what-is-azure-rms.md) fournit la technologie de protection des données pour Azure information protection. Azure RMS peut être utilisé avec la classification et l’étiquetage, ou de façon autonome. 

- [Forum aux questions sur Azure Information Protection](faqs.md)

- [FAQ sur la classification et l’étiquetage](faqs-infoprotect.md)

- [FAQ sur la protection des données](faqs-rms.md)

Si votre question n’a pas de réponse, consultez les liens et les ressources figurant dans [informations et support pour Azure information protection](information-support.md).

De plus, il existe des questions fréquentes destinées aux utilisateurs finaux :

- [FAQ relatif à l’application Azure Information Protection pour iOS et Android](./rms-client/mobile-app-faq.md)

- [FAQ relatif à l’application de partage RMS pour les ordinateurs Mac](/previous-versions/msdn10/dn451248(v=msdn.10))