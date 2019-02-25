---
title: FAQ pour Azure RMS - AIP
description: Certaines questions fréquentes sur le service de protection des données, Azure Rights Management (Azure RMS), d’Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 02/19/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.custom: askipteam
ms.assetid: 90df11c5-355c-4ae6-a762-351b05d0fbed
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 3782d2cea93b2128530e66d82e366924e92abbbc
ms.sourcegitcommit: 95b7df32ecccdab4b80bc3a9f6433dc1c33dbbc5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/18/2019
ms.locfileid: "56407757"
---
# <a name="frequently-asked-questions-about-data-protection-in-azure-information-protection"></a>Forum aux questions sur la protection des données dans Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Vous avez une question sur le service de protection des données, Azure Rights Management, d’Azure Information Protection ? Vous trouverez peut-être une réponse ici.

## <a name="do-files-have-to-be-in-the-cloud-to-be-protected-by-azure-rights-management"></a>Pour bénéficier de la protection d’Azure Rights Management, les fichiers doivent-ils se trouver dans le cloud ?
Non, il s’agit d’une idée fausse répandue. Le service Azure Rights Management (et plus généralement Microsoft) ne voit pas et ne stocke pas vos données dans le cadre du processus de protection des informations. Les informations que vous protégez ne sont jamais stockées dans Azure, sauf si vous indiquez expressément votre volonté de les y stocker, ou si vous utilisez un autre service cloud qui les stocke dans Azure.

Pour plus d’informations, consultez [How does Azure RMS work? Under the hood](./how-does-it-work.md) (Les coulisses du fonctionnement d’Azure RMS) pour comprendre comment une formule secrète du cola, créée et stockée localement, est protégée par le service Azure Rights Management tout en restant sur place.

## <a name="whats-the-difference-between-azure-rights-management-encryption-and-encryption-in-other-microsoft-cloud-services"></a>Quelle est la différence entre le chiffrement Azure Rights Management et le chiffrement dans d’autres services cloud Microsoft ?

Microsoft propose plusieurs technologies de chiffrement qui vous permettent de protéger vos données dans des scénarios différents et souvent complémentaires. Par exemple, si Office 365 offre le chiffrement au repos des données stockées dans Office 365, le service Azure Rights Management d’Azure Information Protection chiffre indépendamment vos données pour les protéger, quel que soit leur emplacement ou leur mode de transmission.

Pour utiliser ces technologies de chiffrement complémentaires, vous devez les activer et les configurer indépendamment. À ce stade, vous pouvez être invité à fournir votre propre clé de chiffrement. Il s’agit du scénario BYOK (« Bring Your Own Key »). Le fait d’activer BYOK avec l’une de ces technologies n’affecte pas les autres. Vous pouvez ainsi utiliser BYOK avec Azure Information Protection et ne pas l’utiliser avec d’autres technologies de chiffrement, ou vice versa. Les clés utilisées par ces différentes technologies peuvent être identiques ou non, selon la façon dont vous configurez les options de chiffrement pour chaque service.

## <a name="whats-the-difference-between-byok-and-hyok-and-when-should-i-use-them"></a>Quelle est la différence entre les dispositifs BYOK et HYOK et quand dois-je les utiliser ?

Dans Azure Information Protection, la solution **Bring Your Own Key** (BYOK) vous permet de créer votre propre clé en local pour la protection offerte par Azure Rights Management. Ensuite, vous transférez cette clé à un module de sécurité matériel (HSM, Hardware Security Module) dans Azure Key Vault, mais elle reste en votre possession et vous continuez à la gérer. Si vous ne procédez pas ainsi, la fonctionnalité de protection d’Azure Rights Management utilise une clé automatiquement créée et gérée pour vous dans Azure. Cette configuration par défaut est considérée comme « gérée par Microsoft » plutôt que « gérée par le client » (option BYOK).

Pour en savoir plus sur la solution BYOK et déterminer si vous devez choisir cette topologie de clé pour votre organisation, voir [Planification et implémentation de votre clé de locataire Azure Information Protection](plan-implement-tenant-key.md).

Dans Azure Information Protection, la solution **Hold Your Own Key** (HYOK) est destinée au petit nombre d’organisations disposant d’un ensemble de documents ou d’e-mails qui ne peuvent pas être protégés par une clé stockée dans le cloud. Pour ces organisations, cette restriction s’applique, même si elles ont créé la clé et la gèrent via la solution BYOK. Cette restriction a souvent pour origine des problèmes de conformité et de réglementation, la configuration HYOK devant uniquement être appliquée aux informations « Top Secret », qui ne seront jamais partagées en dehors de l’organisation et seront uniquement utilisées sur le réseau interne, et qui ne devront pas nécessairement être accessibles depuis des appareils mobiles.

Pour ces exceptions (soit un maximum de 10 % des contenus devant être protégés, en moyenne), les organisations peuvent utiliser une solution locale, à savoir Active Directory Rights Management Services, pour créer la clé, qui restera en local. Avec cette solution, les ordinateurs récupèrent leur stratégie Azure Information Protection à partir du cloud, mais ce contenu identifié peut être protégé à l’aide de la clé en local.

Pour en savoir plus sur la solution HYOK et vous assurer que vous comprenez ses limitations et restrictions, tout en bénéficiant de conseils sur son utilisation, voir [HYOK (conservez votre propre clé) : exigences et restrictions pour la protection AD RMS](configure-adrms-restrictions.md).

## <a name="can-i-now-use-byok-with-exchange-online"></a>Puis-je désormais utiliser BYOK avec Exchange Online ?

Oui, vous pouvez maintenant utiliser BYOK avec Exchange Online quand vous suivez les instructions dans [Configurer de nouvelles fonctionnalités de chiffrement de messages Office 365 reposant sur Azure Information Protection](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e). Ces instructions activent les nouvelles fonctionnalités dans Exchange Online qui prennent en charge BYOK pour Azure Information Protection, ainsi que le nouveau chiffrement de messages Office 365.

Pour plus d’informations sur cette modification, consultez l’annonce du blog : [Chiffrement des messages Office 365 avec les nouvelles fonctionnalités](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801)

## <a name="where-can-i-find-information-about-third-party-solutions-that-integrate-with-azure-rms"></a>Où trouver des informations sur les solutions tierces qui s’intègrent à Azure RMS ?

De nombreux fournisseurs de logiciels disposent de solutions ou implémentent des solutions qui s’intègrent à Azure Rights Management, et la liste augmente rapidement. Il peut s’avérer utile de consulter la liste des [solutions compatibles avec RMS](requirements-applications.md#rms-enlightened-solutions) et d’obtenir les dernières mises à jour de [MicrosoftMobility@MSFTMobility](https://twitter.com/MSFTMobility) sur Twitter. Consultez également le [guide du développeur](./develop/developers-guide.md) et postez vos questions relatives à l’intégration sur le [site Yammer](https://www.yammer.com/AskIPTeam) Azure Information Protection.

## <a name="is-there-a-management-pack-or-similar-monitoring-mechanism-for-the-rms-connector"></a>Existe-t-il un pack d’administration ou un mécanisme de surveillance similaire pour le connecteur RMS ?

Bien que le connecteur Rights Management consigne les messages d’information, d’avertissement et d’erreur dans le journal des événements, il n’existe pas de pack d’administration qui inclut la surveillance de ces événements. Toutefois, la liste des événements et leurs descriptions, ainsi que des informations supplémentaires pour vous aider à prendre une action corrective, sont documentées dans [Surveiller le connecteur Azure Rights Management](monitor-rms-connector.md).

## <a name="do-you-need-to-be-a-global-admin-to-configure-azure-rms-or-can-i-delegate-to-other-administrators"></a>Dois-je être administrateur général pour configurer Azure RMS ou puis-je déléguer cette opération à d’autres administrateurs ?

Avec le rôle administrateur Information Protection récemment introduit, cette question (et la réponse) a été déplacée dans la page principale du Forum aux questions : [Faut-il être administrateur général pour configurer Azure Information Protection ou puis-je déléguer la configuration à d’autres administrateurs ?](faqs.md#do-you-need-to-be-a-global-admin-to-configure-azure-information-protection-or-can-i-delegate-to-other-administrators)

## <a name="how-do-i-create-a-new-custom-template-in-the-azure-portal"></a>Comment créer un nouveau modèle personnalisé dans le portail Azure ?

Les modèles personnalisés ont été déplacés dans le portail Azure, où vous pouvez continuer à les gérer en tant que modèles, ou les convertir en étiquettes. Pour créer un nouveau modèle, créez une nouvelle étiquette et configurez les paramètres de protection des données pour Azure RMS. En pratique, cela crée un nouveau modèle qui est ensuite accessible pour les services et applications qui s’intègrent avec les modèles Rights Management.

Pour plus d’informations sur les modèles dans le portail Azure, consultez [Configuration et gestion des modèles pour Azure Information Protection](configure-policy-templates.md).

## <a name="ive-protected-a-document-and-now-want-to-change-the-usage-rights-or-add-usersdo-i-need-to-reprotect-the-document"></a>J’ai protégé un document et je souhaite à présent changer les droits d’utilisation ou ajouter des utilisateurs. Dois-je reprotéger le document ?

Si le document est protégé à l’aide d’une étiquette ou d’un modèle, il est inutile de le reprotéger. Modifiez l’étiquette ou le modèle en changeant les droits d’utilisation ou en ajoutant de nouveaux groupes (ou utilisateurs), puis enregistrez ces changements :

- Si un utilisateur n’as pas accédé au document avant la publication des changements, ceux-ci prennent effet quand il ouvre le document.

- Si un utilisateur a déjà accédé au document, les changements prennent effet quand sa [licence d’utilisation](configure-usage-rights.md#rights-management-use-license) arrive à expiration. Ne reprotégez le document que si vous ne pouvez pas attendre l’expiration de la licence d’utilisation. La reprotection crée une nouvelle version du document, et donc une nouvelle licence d’utilisation pour l’utilisateur.

Si vous avez déjà configuré un groupe pour les autorisations nécessaires, vous pouvez également changer l’appartenance dans le groupe pour inclure ou exclure des utilisateurs. Dans ce cas, il est inutile de changer l’étiquette ou le modèle. Il peut y avoir un bref délai avant l’entrée en vigueur des changements, car l’appartenance dans le groupe est [mise en cache](prepare.md#group-membership-caching-by-azure-information-protection) par le service Azure Rights Management.

Si le document est protégé au moyen d’autorisations personnalisées, vous ne pouvez pas changer les autorisations du document existant. Vous devez reprotéger le document et spécifier tous les utilisateurs et droits d’utilisation exigés pour cette nouvelle version du document. Pour reprotéger un document protégé, vous devez avoir le droit d’utilisation Contrôle total.

Conseil : Pour vérifier si un document a été protégé avec un modèle ou une autorisation personnalisée, utilisez l’applet de commande PowerShell [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus). Vous verrez systématiquement une description de modèle **Accès limité** pour les autorisations personnalisées, avec un ID de modèle unique qui ne s’affiche pas quand vous exécutez [Get-RMSTemplate](/powershell/module/azureinformationprotection/get-rmstemplate).

## <a name="i-have-a-hybrid-deployment-of-exchange-with-some-users-on-exchange-online-and-others-on-exchange-serveris-this-supported-by-azure-rms"></a>J'ai un déploiement hybride d'Exchange avec certains utilisateurs sur Exchange Online et d'autres utilisateurs sur Exchange Server. Est-ce compatible avec Azure RMS ?
Absolument et l’avantage est que les utilisateurs peuvent protéger et utiliser sans problème des e-mails et pièces jointes entre les deux déploiements Exchange. Pour cette configuration, [activez Azure RMS](activate-service.md) et [activez la Gestion des droits relatifs à l’information (IRM) pour Exchange Online](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx), puis [déployez et configurez le connecteur RMS](deploy-rms-connector.md) pour Exchange Server.

## <a name="if-i-use-this-protection-for-my-production-environment-is-my-company-then-locked-into-the-solution-or-risk-losing-access-to-content-that-we-protected-with-azurerms"></a>Si j’utilise cette protection pour mon environnement de production, ma société est-elle enfermée dans la solution ou risque-t-elle de perdre l’accès au contenu protégé par Azure RMS ?
Non, vous gardez toujours le contrôle de vos données et pouvez continuer à y accéder, même si vous décidez de ne plus utiliser le service Azure Rights Management. Pour plus d’informations, consultez [Désaffectation et désactivation d’Azure Rights Management](decommission-deactivate.md).

## <a name="can-i-control-which-of-my-users-can-use-azure-rms-to-protect-content"></a>Puis-je contrôler les utilisateurs pouvant utiliser Azure RMS pour protéger du contenu ?
Oui, le service Azure Rights Management dispose de contrôles d’intégration d’utilisateur pour ce scénario. Pour plus d’informations, consultez la section [Configuration de contrôles d’intégration pour un déploiement échelonné](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) dans l’article [Activation d’Azure Rights Management](activate-service.md).

## <a name="can-i-prevent-users-from-sharing-protected-documents-with-specific-organizations"></a>Puis-je empêcher des utilisateurs de partager des documents protégés avec des organisations spécifiques ?
L’un des avantages majeurs de l’utilisation du service Azure Rights Management pour la protection des données est qu’il prend en charge la collaboration interentreprises sans que vous soyez obligé de configurer des approbations explicites pour chaque organisation partenaire, car Azure AD se charge de l’authentification à votre place.

Il n'existe aucune option d'administration permettant d'empêcher des utilisateurs de partager en toute sécurité des documents avec des organisations spécifiques. Par exemple, imaginons que vous souhaitiez bloquer une organisation en laquelle vous n’avez pas confiance ou qui exerce une activité concurrente. Empêcher le service Azure Rights Management d’envoyer des documents protégés à des utilisateurs travaillant au sein de cette organisation n’aurait aucun sens, car ceux-ci partageraient leurs documents non protégés, ce qui est probablement la dernière chose que vous souhaitez dans le cadre de ce scénario. Par exemple, vous ne seriez pas en mesure d’identifier qui partage des documents confidentiels avec quels utilisateurs au sein de ces organisations, contrairement à ce que vous pouvez faire quand le document (ou l’e-mail) est protégé par le service Azure Rights Management.

## <a name="when-i-share-a-protected-document-with-somebody-outside-my-company-how-does-that-user-get-authenticated"></a>Lors du partage d'un document protégé avec une personne extérieure à mon organisation, comment cet utilisateur s'authentifie-t-il ?

Par défaut, le service Azure Rights Management utilise un compte Azure Active Directory et une adresse e-mail associée pour l’authentification de l’utilisateur, ce qui rend la collaboration interentreprises homogène pour les administrateurs. Si l’autre organisation utilise des services Azure, les utilisateurs disposent déjà de comptes dans Azure Active Directory, même si ceux-ci sont créés et gérés localement, puis synchronisés avec Azure. Si l'organisation dispose d'Office 365, en arrière-plan, ce service utilise également Azure Active Directory pour les comptes d'utilisateur. Si l’organisation de l’utilisateur ne dispose pas de compte géré dans Azure, les utilisateurs peuvent s’inscrire à [RMS for individuals](./rms-for-individuals.md), ce qui a pour effet de créer un locataire Azure non géré et un annuaire pour l’organisation avec un compte pour l’utilisateur, afin que celui-ci, et les utilisateurs suivants, puissent s’authentifier auprès du service Azure Rights Management.

La méthode d'authentification pour ces comptes peut varier en fonction de la manière dont l'administrateur de l'autre organisation a configuré les comptes Azure Active Directory. Par exemple, ils peuvent utiliser des mots de passe créés pour ces comptes, une fédération ou des mots de passe créés dans les services de domaine Active Directory, puis synchronisés avec Azure Active Directory.

Autres méthodes d'authentification :

- Si vous protégez un e-mail avec un document Office en pièce jointe envoyé à un utilisateur qui n’a pas de compte dans Azure AD, la méthode d’authentification change. Le service Azure Rights Management est fédéré avec des fournisseurs d’identité sociale courants, comme Gmail. Si le fournisseur de messagerie de l’utilisateur est pris en charge, l’utilisateur peut se connecter à ce service, et son fournisseur de messagerie a la charge de son authentification. Si le fournisseur de messagerie de l’utilisateur n’est pas pris en charge ou s’il s’agit d’une préférence, l’utilisateur peut demander un code secret à usage unique qui l’authentifie et affiche l’e-mail avec le document protégé dans un navigateur web.

- Azure Information Protection peut utiliser des comptes Microsoft pour les applications prises en charge. Actuellement, toutes les applications ne peuvent pas ouvrir du contenu protégé lorsqu’un compte Microsoft est utilisé pour l’authentification. [Plus d’informations](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)

## <a name="can-i-add-external-users-people-from-outside-my-company-to-custom-templates"></a>Puis-je ajouter des utilisateurs externes (des personnes ne faisant pas partie de mon organisation) à des modèles personnalisés ?

Oui. Les [paramètres de protection](configure-policy-protection.md) que vous configurez dans le portail Azure vous permettent d’ajouter des autorisations à des utilisateurs et groupes extérieurs à votre organisation, et même à tous les utilisateurs d’une autre organisation. Vous trouverez peut-être utile de consulter l’exemple pas à pas, [Sécuriser la collaboration autour de documents à l’aide d’Azure Information Protection](secure-collaboration-documents.md). 

Notez que si vous avez des étiquettes Azure Information Protection, vous devez d’abord convertir votre modèle personnalisé en étiquette pour pouvoir configurer ces paramètres de protection dans le portail Azure. Pour plus d’informations, consultez [Configuration et gestion des modèles pour Azure Information Protection](configure-policy-templates.md).

Vous pouvez aussi ajouter des utilisateurs externes aux modèles personnalisés (et étiquettes) à l’aide de PowerShell. Cette configuration vous oblige à utiliser un objet de définition de droits pour mettre à jour votre modèle :

1. Spécifiez les adresses e-mail externes et leurs droits dans un objet de définition de droits en utilisant l’applet de commande [New-AadrmRightsDefinition](/powershell/module/aadrm/new-aadrmrightsdefinition) pour créer une variable.

2. Fournissez cette variable au paramètre RightsDefinition avec l’applet de commande [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty).

    Lorsque vous ajoutez des utilisateurs à un modèle existant, vous devez définir des objets de définition de droits pour les utilisateurs existants dans les modèles, ainsi que pour les nouveaux utilisateurs. Pour ce scénario, l’**Exemple 3 : Ajouter de nouveaux utilisateurs et de nouveaux droits à un modèle personnalisé** de la section [Exemples](/powershell/module/aadrm/set-aadrmtemplateproperty#examples) pour l’applet de commande peut vous être utile.

## <a name="what-type-of-groups-can-i-use-with-azure-rms"></a>Quels types de groupes puis-je utiliser avec Azure RMS ?
Pour la plupart des scénarios, vous pouvez utiliser n’importe quel type de groupe d’Azure AD qui a une adresse e-mail. Cette règle s’applique toujours quand vous affectez des droits d’utilisation, mais il existe certaines exceptions pour l’administration du service Azure Rights Management. Pour plus d’informations, consultez [Configuration requise d’Azure Information Protection pour les comptes de groupe](prepare.md#azure-information-protection-requirements-for-group-accounts).

## <a name="how-do-i-send-a-protected-email-to-a-gmail-or-hotmail-account"></a>Comment envoyer un e-mail protégé sur un compte Gmail ou Hotmail ?

Quand vous utilisez Exchange Online et le service Azure Rights Management, vous envoyez simplement l’e-mail à l’utilisateur sous forme de message protégé. Par exemple, vous pouvez sélectionner le nouveau bouton **Protéger** dans la barre de commandes Outlook sur le web, ou bien utiliser le bouton ou l’option de menu **Ne pas transférer** dans Outlook. Vous pouvez aussi sélectionner une étiquette Azure Information Protection qui applique l’option Ne pas transférer et classifie automatiquement l’e-mail.

Le destinataire voit une option qui lui permet de se connecter à son compte Gmail, Yahoo ou Microsoft, puis de lire l’e-mail protégé. Ils peuvent également choisir l’option de demander un code secret à usage unique pour lire l’e-mail dans un navigateur.

Pour prendre en charge ce scénario, Exchange Online doit être activé pour le service Azure Rights Management et pour les nouvelles fonctionnalités de chiffrement de messages Office 365. Pour plus d’informations sur cette configuration, consultez [Exchange Online : Configuration de la Gestion des droits relatifs à l’information (IRM)](configure-office365.md#exchangeonline-irm-configuration).

Pour plus d’informations sur les nouvelles fonctionnalités, parmi lesquelles la prise en charge de tous les comptes e-mail sur tous les appareils, consultez le billet de blog suivant : [Announcing new capabilities available in Office 365 Message Encryption](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801).

## <a name="what-devices-and-which-file-types-are-supported-by-azure-rms"></a>Quels appareils et types de fichier Azure RMS prend-il en charge ?
Pour obtenir la liste des appareils qui prennent en charge le service Azure Rights Management, consultez [Appareils clients prenant en charge la protection des données Azure Rights Management](./requirements-client-devices.md). Les fonctionnalités Rights Management n’étant pas toutes disponibles sur tous les appareils pris en charge, pensez à consulter le tableau des [applications compatibles avec RMS](./requirements-applications.md#rms-enlightened-applications).

Le service Azure Rights Management peut prendre en charge tous les types de fichiers. Dans le cas de texte, d’images, de fichiers Microsoft Office (Word, Excel, PowerPoint), de fichiers .pdf et d’autres types de fichier d’application, Azure Rights Management offre une protection native qui comprend le chiffrement et la mise en application de droits (autorisations). Pour tous les autres types de fichier et d'application, la protection générique offre l'encapsulation et l'authentification des fichiers afin de vérifier si un utilisateur est autorisé à ouvrir le fichier.

Pour obtenir la liste des extensions de noms de fichiers pris en charge en mode natif par Azure Rights Management, consultez [Types de fichiers pris en charge par Azure Information Protection](./rms-client/client-admin-guide-file-types.md). Les extensions de nom de fichier qui ne figurent pas dans la liste sont prises en charge grâce à l’utilisation du client Azure Information Protection qui applique automatiquement une protection générique à ces fichiers.

## <a name="how-do-i-configure-a-mac-computer-to-protect-and-track-documents"></a>Comment configurer un ordinateur Mac pour protéger et suivre les documents ?

Tout d’abord, assurez-vous que vous avez installé Office pour Mac en utilisant le lien d’installation à partir de https://portal.office.com. Pour obtenir des instructions complètes, consultez [Télécharger et installer ou réinstaller Office 365 ou Office 2019 sur un PC ou un Mac](https://support.office.com/en-us/article/Download-and-install-or-reinstall-Office-365-or-Office-2016-on-a-PC-or-Mac-4414EAAF-0478-48BE-9C42-23ADC4716658).

Ouvrez Outlook et créez un profil à l’aide de compte de travail ou scolaire Office 365. Ensuite, créez un nouveau message, puis procédez comme suit pour configurer Office afin qu’il puisse protéger les documents et e-mails à l’aide du service Azure Rights Management :

1. Dans le nouveau message, dans l’onglet **Options**, cliquez sur **Autorisations**, puis cliquez sur **Vérifier les informations d’identification**.

2. Lorsque vous y êtes invité, spécifiez à nouveau les détails votre compte de travail ou scolaire Office 365, puis sélectionnez **Connexion**.

    Cela permet de télécharger les modèles Azure Rights Management, et **Vérifier les informations d’identification** est remplacé par des options qui incluent **Aucune restriction**, **Ne pas transférer**, ainsi que les modèles Azure Rights Management qui sont publiés pour votre client. Vous pouvez désormais annuler ce nouveau message.

Pour protéger un message ou un document : Sous l’onglet **Options**, cliquez sur **Autorisations**, puis choisissez une option ou un modèle qui protège votre e-mail ou votre document.

Pour effectuer le suivi d’un document une fois que vous l’avez protégé : Sur un ordinateur Windows où le client Azure Information Protection est installé, enregistrez le document avec le site de suivi de documents en utilisant une application Office ou l’Explorateur de fichiers. Pour obtenir des instructions, consultez [Suivre et révoquer vos documents](./rms-client/client-track-revoke.md). À partir de votre ordinateur Mac, vous pouvez maintenant utiliser votre navigateur web pour accéder au site de suivi des documents (https://track.azurerms.com) pour suivre et révoquer ce document.

## <a name="when-i-open-an-rms-protected-office-document-does-the-associated-temporary-file-become-rms-protected-as-well"></a>Quand j’ouvre un document Office protégé par RMS, le fichier temporaire associé devient-il également protégé par RMS ?
Non. Dans ce scénario, le fichier temporaire associé ne contient pas les données du document d’origine, mais uniquement ce que l’utilisateur entre pendant que le fichier est ouvert. Contrairement au fichier d’origine, le fichier temporaire n’est évidemment pas conçu pour le partage. Il reste sur l’appareil, protégé par des contrôles de sécurité locaux tels que BitLocker et EFS.

## <a name="a-feature-i-am-looking-for-doesnt-seem-to-work-with-sharepoint-protected-librariesis-support-for-my-feature-planned"></a>Il semble qu'une fonctionnalité que je recherche ne fonctionne pas avec les bibliothèques protégées SharePoint. Une prise en charge de ma fonctionnalité est-elle prévue ?
Actuellement, SharePoint prend en charge les documents protégés par RMS en utilisant des bibliothèques protégées par IRM, qui ne prennent pas en charge les modèles Rights Management, le suivi de document et certaines autres fonctionnalités. Pour plus d’informations, consultez la section [SharePoint Online et SharePoint Server](./office-apps-services-support.md#sharepoint-online-and-sharepoint-server) dans l’article [Applications et services Office](./office-apps-services-support.md).

Si vous êtes intéressé par une fonctionnalité spécifique qui n’est pas encore prise en charge, surveillez les annonces publiées dans [Enterprise Mobility and Security Blog](https://cloudblogs.microsoft.com/enterprisemobility/?product=azure-rights-management-services) (Blog de sécurité et de mobilité d’entreprise).

## <a name="how-do-i-configure-one-drive-for-business-in-sharepoint-online-so-that-users-can-safely-share-their-files-with-people-inside-and-outside-the-company"></a>Comment configurer OneDrive Entreprise dans SharePoint Online, afin que les utilisateurs puissent partager en toute sécurité des fichiers avec des personnes à l'intérieur et à l'extérieur de l'organisation ?
Par défaut, en votre qualité d’administrateur Office 365, ce n’est pas vous qui configurez cela, mais les utilisateurs.

De la même manière qu’un administrateur de site SharePoint active et configure IRM pour une bibliothèque SharePoint dont il est propriétaire, OneDrive Entreprise a été conçu pour permettre aux utilisateurs d’activer et de configurer IRM pour leur propre bibliothèque OneDrive Entreprise. Cependant, en utilisant PowerShell, vous pouvez le faire à leur place. Pour des instructions, consultez la section [SharePoint Online et OneDrive Entreprise : Configuration d’IRM](configure-office365.md#sharepointonline-and-onedrive-for-business-irm-configuration) dans l’article [Office 365 : Configuration pour les clients et services en ligne](configure-office365.md).

## <a name="do-you-have-any-tips-or-tricks-for-a-successful-deployment"></a>Avez-vous des conseils ou des astuces pour réussir le déploiement ?

Après avoir supervisé de nombreux déploiements et écouté nos clients, partenaires, consultants et ingénieurs du support technique, voici l’un des conseils les plus importants que nous pouvons vous donner : **Concevoir et déployer des stratégies de droits simples**.

Puisqu’Azure Information Protection permet de partager des fichiers en toute sécurité, vous pouvez faire preuve d’ambition concernant la portée de la protection de vos données. Soyez prudent quand vous configurez les restrictions des droits d’utilisation. Pour de nombreuses organisations, la meilleure chose à faire est d’empêcher la fuite des données en limitant l’accès aux seuls membres de votre organisation. Bien sûr, vous pouvez être bien plus précis si vous devez empêcher des personnes d’imprimer, d’éditer, etc. Appliquez néanmoins les restrictions les plus fortes à titre exceptionnel pour les documents nécessitant réellement un niveau de sécurité élevé. Au lieu d’implémenter ces droits d’utilisation plus restrictifs dès le premier jour, adoptez une approche plus progressive.

## <a name="how-do-we-regain-access-to-files-that-were-protected-by-an-employee-who-has-now-left-the-organization"></a>Comment récupérer l'accès à des fichiers protégés par un employé qui a quitté l'organisation ?
Utilisez la [fonctionnalité de super utilisateur](configure-super-users.md), qui accorde les droits d’utilisation Contrôle total aux utilisateurs autorisés pour tous les documents et e-mails protégés par votre locataire. Les super utilisateurs peuvent toujours lire ce contenu protégé et, si nécessaire, supprimer la protection ou le reprotéger pour d’autres utilisateurs. Cette même fonctionnalité permet à des services autorisés d'indexer et d'inspecter des fichiers si nécessaire.

## <a name="when-i-test-revocation-in-the-document-tracking-site-i-see-a-message-that-says-people-can-still-access-the-document-for-up-to-30-daysis-this-time-period-configurable"></a>Lorsque je teste la révocation dans le site de suivi des documents, je vois un message m’indiquant que les autres utilisateurs continueront d’avoir accès au document pendant 30 jours. Cette durée est-elle configurable ?

Oui. Ce message indique la [licence d’utilisation](configure-usage-rights.md#rights-management-use-license) de ce fichier en particulier.

La révocation d’un fichier ne peut être appliquée que lorsque l’utilisateur doit s’authentifier auprès du service Azure Rights Management. Par conséquent, si la période de validité de la licence d’utilisation du fichier est de 30 jours et que l’utilisateur a déjà ouvert le document, il peut continuer d’y accéder pendant toute la durée de la licence d’utilisation. Quand la licence d’utilisation expire, l’utilisateur doit se réauthentifier et l’accès lui est refusé, car le document a été révoqué.

L’utilisateur qui a protégé le document, [l’émetteur Rights Management](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner) n’est pas concerné par cette révocation et peut toujours accéder à ses documents.

Pour un locataire, la période de validité par défaut d’une licence d’utilisation est de 30 jours. Vous pouvez remplacer ce paramètre par un paramètre plus restrictif dans une étiquette ou un modèle. Pour plus d’informations sur la licence d’utilisation et sa configuration, consultez la documentation [Licence d’utilisation Rights Management](configure-usage-rights.md#rights-management-use-license).

## <a name="can-rights-management-prevent-screen-captures"></a>Est-ce que Rights Management peut empêcher les captures d’écran ?
En n’accordant pas le [droit d’utilisation](configure-usage-rights.md) **Copy**, Rights Management peut empêcher des captures d’écran de nombreux outils de capture écran couramment utilisés sur les plateformes Windows (Windows 7, Windows 8.1, Windows 10, Windows 10 Mobile) et Android. Toutefois, appareils iOS et Mac n’autorisent aucune application à empêcher les captures d’écran. En outre, les navigateurs sur n’importe quel appareil ne peuvent pas empêcher les captures d’écran. Cela inclut Outlook sur le web et Office Online.

La possibilité d’empêcher les captures d’écran peut également aider à éviter la divulgation accidentelle ou involontaire de renseignements confidentiels ou sensibles. Il existe par ailleurs de nombreuses façons de partager des données affichées sur un écran, et la capture d’écran n’est qu’une méthode parmi d’autres. Par exemple, un utilisateur désireux de partager des informations affichées peut parfaitement les photographier avec son téléphone, recopier les données ou simplement les communiquer verbalement à un tiers.

Comme le montrent ces exemples, même si la totalité des plateformes et logiciels prenaient en charge les API de Rights Management pour bloquer les captures d’écran, la technologie seule ne peut pas toujours empêcher des utilisateurs de partager des données qu’ils ne devraient pas. Même si Rights Management peut contribuer à protéger vos données importantes au moyen de stratégies d’autorisation et d’utilisation, cette solution de gestion des droits d’entreprise doit être assortie d’autres moyens de contrôle. Par exemple, vous pouvez mettre en place une sécurité physique, surveiller et soumettre à un contrôle strict les personnes autorisées à accéder aux données de votre organisation et investir dans la formation pour sensibiliser les utilisateurs à la question du partage de données.

## <a name="whats-the-difference-between-a-user-protecting-an-email-with-do-not-forward-and-a-template-that-doesnt-include-the-forward-right"></a>Quelle différence y a-t-il entre un utilisateur qui protège un e-mail avec l’option Ne pas transférer et un modèle qui n’inclut pas de droit de transfert ?

En dépit de son nom et de son apparence, l’option **Ne pas transférer** n’est ni le contraire du droit de transfert, ni un modèle. Il s’agit en fait d’un ensemble de droits qui incluent la restriction de copier, imprimer et enregistrer des pièces jointes, outre la restriction de transfert des e-mails. Les droits sont appliqués dynamiquement aux utilisateurs par le biais des destinataires choisis et non pas statiquement attribués par l’administrateur. Pour plus d’informations, consultez la section [Option Ne pas transférer pour les e-mails](configure-usage-rights.md#do-not-forward-option-for-emails) dans [Configuration des droits d’utilisation pour Azure Rights Management](configure-usage-rights.md).

