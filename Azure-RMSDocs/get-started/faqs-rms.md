---
title: "Forum aux questions sur le service de protection des données, Azure Rights Management, d’Azure Information Protection | Azure Information Protection"
description: "Certaines questions fréquentes sur le service de protection des données, Azure Rights Management (Azure RMS), d’Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/16/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 90df11c5-355c-4ae6-a762-351b05d0fbed
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 181357691df02c8532a6f28eef689dcacdfd937f


---

# <a name="frequently-asked-questions-about-data-protection-in-azure-information-protection"></a>Forum aux questions sur la protection des données dans Azure Information Protection

>*S’applique à : Azure Information Protection, Office 365*

Vous avez une question sur le service de protection des données, Azure Rights Management, d’Azure Information Protection ? Vous trouverez peut-être une réponse ici. 

## <a name="do-files-have-to-be-in-the-cloud-to-be-protected-by-azure-rights-management"></a>Pour bénéficier de la protection d’Azure Rights Management, les fichiers doivent-ils se trouver dans le cloud ?
Non, il s’agit d’une idée fausse répandue. Le service Azure Rights Management (et plus généralement Microsoft) ne voit pas et ne stocke pas vos données dans le cadre du processus de protection des informations. Les informations que vous protégez ne sont jamais stockées dans Azure, sauf si vous indiquez expressément votre volonté de les y stocker, ou si vous utilisez un autre service cloud qui les stocke dans Azure. 

Pour plus d’informations, consultez [How does Azure RMS work? Under the hood](../understand-explore/how-does-it-work.md) (Les coulisses du fonctionnement d’Azure RMS) pour comprendre comment une formule secrète du cola, créée et stockée localement, est protégée par le service Azure Rights Management tout en restant sur place.

## <a name="whats-the-difference-between-azure-rights-management-encryption-and-encryption-in-other-microsoft-cloud-services"></a>Quelle est la différence entre le chiffrement Azure Rights Management et le chiffrement dans d’autres services cloud Microsoft ?

Microsoft propose plusieurs technologies de chiffrement qui vous permettent de protéger vos données dans des scénarios différents et souvent complémentaires. Par exemple, si Office 365 offre le chiffrement au repos des données stockées dans Office 365, le service Azure Rights Management d’Azure Information Protection chiffre indépendamment vos données pour les protéger, quel que soit leur emplacement ou leur mode de transmission.

Pour utiliser ces technologies de chiffrement complémentaires, vous devez les activer et les configurer indépendamment. À ce stade, vous pouvez être invité à fournir votre propre clé de chiffrement. Il s’agit du scénario BYOK (« Bring Your Own Key »). Le fait d’activer BYOK avec l’une de ces technologies n’affecte pas les autres. Vous pouvez ainsi utiliser BYOK avec Azure Information Protection et ne pas l’utiliser avec d’autres technologies de chiffrement, ou vice versa. Les clés utilisées par ces différentes technologies peuvent être identiques ou non, selon la façon dont vous configurez les options de chiffrement pour chaque service.

## <a name="can-i-integrate-the-azure-rights-management-service-with-my-on-premises-servers"></a>Puis-je intégrer le service Azure Rights Management à mes serveurs locaux ?
Oui. Vous pouvez intégrer Azure Rights Management à vos serveurs locaux, tels que les serveurs de fichiers Windows, Exchange Server et SharePoint. Pour ce faire, utilisez le [connecteur Rights Management](../deploy-use/deploy-rms-connector.md). Ou bien, si vous êtes simplement intéressé par l’utilisation de l’Infrastructure de classification des fichiers avec Windows Server, vous pouvez utiliser les [applets de commande de protection RMS](https://technet.microsoft.com/library/mt601315%28v=ws.10%29.aspx). Vous pouvez également synchroniser et fédérer vos contrôleurs de domaine Active Directory avec Azure AD pour une expérience d'authentification plus agréable pour les utilisateurs, par exemple, en utilisant [Azure AD Connect](http://azure.microsoft.com/documentation/articles/active-directory-aadconnect/).

Azure Rights Management génère et gère automatiquement les certificats XrML de façon appropriée. Il n’utilise donc pas d’infrastructure à clé publique (PKI) locale. Pour plus d’informations sur la façon dont Azure Rights Management utilise les certificats, consultez la section [Procédure pas à pas décrivant le fonctionnement d’Azure RMS : première utilisation, protection du contenu, consommation du contenu](../understand-explore/how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption) dans l’article [Fonctionnement d’Azure RMS](../understand-explore/how-does-it-work.md).

## <a name="where-can-i-find-information-about-3rd-party-solutions-that-integrate-with-azure-rms"></a>Où puis-je trouver des informations sur les solutions tierces qui s’intègrent à Azure RMS ?

De nombreux fournisseurs de logiciels disposent de solutions ou implémentent des solutions qui s’intègrent à Azure Rights Management, et la liste augmente très rapidement. Il peut s’avérer utile de consulter [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services) (Blog de sécurité et de mobilité d’entreprise) et de récupérer les dernières mises à jour auprès de [Dan Plastina @TheRMSGuy](https://twitter.com/TheRMSGuy) sur Twitter. Toutefois, si vous avez une question, envoyez un e-mail à l’équipe Information Protection : askipteam@microsoft.com.

## <a name="is-there-a-management-pack-or-similar-monitoring-mechanism-for-the-rms-connector"></a>Existe-t-il un pack d’administration ou un mécanisme de surveillance similaire pour le connecteur RMS ?

Bien que le connecteur Rights Management consigne les messages d’information, d’avertissement et d’erreur dans le journal des événements, il n’existe pas de pack d’administration qui inclut la surveillance de ces événements. Toutefois, la liste des événements et leurs descriptions, ainsi que des informations supplémentaires pour vous aider à prendre une action corrective, sont documentées dans [Surveiller le connecteur Azure Rights Management](../deploy-use/monitor-rms-connector.md).

## <a name="do-you-need-to-be-a-global-admin-to-configure-azure-rms-or-can-i-delegate-to-other-administrators"></a>Dois-je être administrateur général pour configurer Azure RMS ou puis-je déléguer cette opération à d’autres administrateurs ?

Les administrateurs généraux pour un locataire Office 365 ou Azure AD peuvent évidemment exécuter toutes les tâches d’administration pour le service Azure Rights Management. Toutefois, si vous souhaitez affecter des autorisations administratives à d’autres utilisateurs, vous pouvez recourir à l’applet de commande PowerShell d’Azure RMS [Add-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/dn629417.aspx). Vous pouvez affecter ce rôle d’administration par compte d’utilisateur ou par groupe. Deux rôles sont disponibles : **Administrateur général** et **Administrateur du connecteur**. 

Comme ces noms de rôles le suggèrent, le premier rôle accorde des autorisations pour exécuter toutes les tâches d’administration pour Azure Rights Management (sans étendre le rôle d’administrateur général aux autres services cloud) et le second rôle accorde des autorisations pour exécuter uniquement le connecteur Rights Management (RMS).

Quelques éléments à prendre en compte :

- Seuls les administrateurs généraux pour Office 365 et les administrateurs généraux pour Azure AD peuvent utiliser les portails de gestion (Centre d’administration Office 365 ou portail Azure Classic) pour configurer Azure RMS. Les utilisateurs auxquels vous affectez le rôle d’administrateur général pour Azure RMS doivent utiliser des commandes PowerShell d’Azure RMS pour configurer Azure RMS. Pour déterminer les bonnes applets de commande suivant les tâches à effectuer, consultez [Administration d’Azure Rights Management à l’aide de Windows PowerShell](../deploy-use/administer-powershell.md).

- Si vous avez configuré des [contrôles d’intégration](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment), cela n’affecte pas la possibilité d’administrer Azure RMS, à l’exception du connecteur RMS. Par exemple, si vous avez configuré des contrôles d’intégration de manière à ce que seul le groupe « Département informatique » puisse protéger du contenu, le compte que vous utilisez pour installer et configurer le connecteur RMS doit être membre de ce groupe. 

- Aucun administrateur pour Azure RMS (l’administrateur général du client ou un administrateur général Azure RMS) ne peut supprimer automatiquement la protection des documents ou e-mails qui ont été protégés par Azure RMS. Seuls les utilisateurs ayant le statut de super utilisateurs pour Azure RMS peuvent effectuer cette opération, sous réserve que la fonctionnalité de super utilisateur soit activée. Toutefois, l’administrateur général du client et n’importe quel administrateur général Azure RMS peuvent affecter des utilisateurs comme super utilisateurs, y compris leur propre compte. Ils peuvent également activer la fonctionnalité de super utilisateur. Ces actions sont enregistrées dans le journal de l’administrateur Azure RMS. Pour plus d’informations, consultez la section des bonnes pratiques dans [Configuration de super utilisateurs pour Azure Rights Management et les services de découverte ou la récupération de données](../deploy-use/configure-super-users.md). 


## <a name="i-have-a-hybrid-deployment-of-exchange-with-some-users-on-exchange-online-and-others-on-exchange-serveris-this-supported-by-azure-rms"></a>J'ai un déploiement hybride d'Exchange avec certains utilisateurs sur Exchange Online et d'autres utilisateurs sur Exchange Server. Est-ce compatible avec Azure RMS ?
Absolument, et l'avantage est que les utilisateurs peuvent protéger et consommer sans problème des e-mails et pièces jointes entre les deux déploiements Exchange. Pour cette configuration, activez [Azure RMS](../deploy-use/activate-service.md) et [Gestion des droits relatifs à l’information (IRM) pour Exchange Online](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx), puis [déployez et configurez le connecteur RMS](../deploy-use/deploy-rms-connector.md) pour Exchange Server.

## <a name="if-i-use-this-protection-for-my-production-environment-is-my-company-then-locked-into-the-solution-or-risk-losing-access-to-content-that-we-protected-with-azure-rms"></a>Si j’utilise cette protection pour mon environnement de production, ma société est-elle enfermée dans la solution ou risque-t-elle de perdre l’accès au contenu protégé par Azure RMS ?
Non, vous gardez toujours le contrôle de vos données et pouvez continuer à y accéder, même si vous décidez de ne plus utiliser le service Azure Rights Management. Pour plus d’informations, consultez [Désaffectation et désactivation d’Azure Rights Management](../deploy-use/decommission-deactivate.md).

Toutefois, avant que vous désaffectiez votre déploiement Azure RMS, nous aimerions que vous nous aidiez à comprendre pourquoi vous avez pris cette décision. Si la protection Azure Rights Management ne répond pas à vos besoins, demandez-nous si de nouvelles fonctionnalités sont prévues dans un futur proche ou s’il existe des alternatives. Envoyez un e-mail à [AskIPTeam@Microsoft.com](mailto:askipteam@microsoft.com?subject=Planning%20to%20decommission%20Azure%20RMS). Nous serons heureux de discuter de vos exigences techniques et professionnelles.

## <a name="can-i-control-which-of-my-users-can-use-azure-rms-to-protect-content"></a>Puis-je contrôler les utilisateurs pouvant utiliser Azure RMS pour protéger du contenu ?
Oui, le service Azure Rights Management dispose de contrôles d’intégration d’utilisateur pour ce scénario. Pour plus d’informations, consultez la section [Configuration de contrôles d’intégration pour un déploiement échelonné](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) dans l’article [Activation d’Azure Rights Management](../deploy-use/activate-service.md).

## <a name="can-i-prevent-users-from-sharing-protected-documents-with-specific-organizations"></a>Puis-je empêcher des utilisateurs de partager des documents protégés avec des organisations spécifiques ?
L’un des avantages majeurs de l’utilisation du service Azure Rights Management pour la protection des données est qu’il prend en charge la collaboration interentreprises sans que vous soyez obligé de configurer des approbations explicites pour chaque organisation partenaire, car Azure AD se charge de l’authentification à votre place.

Il n'existe aucune option d'administration permettant d'empêcher des utilisateurs de partager en toute sécurité des documents avec des organisations spécifiques. Par exemple, imaginons que vous souhaitiez bloquer une organisation en laquelle vous n’avez pas confiance ou qui exerce une activité concurrente. Empêcher le service Azure Rights Management d’envoyer des documents protégés à des utilisateurs travaillant au sein de cette organisation n’aurait aucun sens, car ceux-ci partageraient leurs documents non protégés, ce qui est probablement la dernière chose que vous souhaitez dans le cadre de ce scénario. Par exemple, vous ne seriez pas en mesure d’identifier qui partage des documents confidentiels avec quels utilisateurs au sein de ces organisations, contrairement à ce que vous pouvez faire quand le document (ou l’e-mail) est protégé par le service Azure Rights Management.

## <a name="when-i-share-a-protected-document-with-somebody-outside-my-company-how-does-that-user-get-authenticated"></a>Lors du partage d'un document protégé avec une personne extérieure à mon organisation, comment cet utilisateur s'authentifie-t-il ?
Le service Azure Rights Management utilise toujours un compte Azure Active Directory et une adresse de messagerie associée pour l’authentification de l’utilisateur, ce qui rend la collaboration interentreprises transparente pour les administrateurs. Si l’autre organisation utilise des services Azure, les utilisateurs disposent déjà de comptes dans Azure Active Directory, même si ceux-ci sont créés et gérés localement, puis synchronisés avec Azure. Si l'organisation dispose d'Office 365, en arrière-plan, ce service utilise également Azure Active Directory pour les comptes d'utilisateur. Si l’organisation de l’utilisateur ne dispose pas de compte géré dans Azure, les utilisateurs peuvent s’inscrire à [RMS for individuals](../understand-explore/rms-for-individuals.md), ce qui a pour effet de créer un locataire Azure non géré et un annuaire pour l’organisation avec un compte pour l’utilisateur, afin que celui-ci, et les utilisateurs suivants, puissent s’authentifier auprès du service Azure Rights Management.

La méthode d'authentification pour ces comptes peut varier en fonction de la manière dont l'administrateur de l'autre organisation a configuré les comptes Azure Active Directory. Par exemple, ils peuvent utiliser des mots de passe créés pour ces comptes, Multi-Factor Authentication (MFA), une fédération ou des mots de passe créés dans les services de domaine Active Directory, puis synchronisés avec Azure Active Directory.

## <a name="can-i-add-external-users-people-from-outside-my-company-to-custom-templates"></a>Puis-je ajouter des utilisateurs externes (des personnes ne faisant pas partie de mon organisation) à des modèles personnalisés ?
Oui. La création de modèles personnalisés que les utilisateurs finaux (et administrateurs) peuvent sélectionner à partir d'applications accélère et facilite l'application de la protection des informations à l'aide de stratégies prédéfinies que vous spécifiez. L'un des paramètres du modèle définit qui peut accéder au contenu, et vous pouvez spécifier des utilisateurs et des groupes au sein de votre organisation, ainsi que des utilisateurs extérieurs à celle-ci.

Pour spécifier des utilisateurs extérieurs à votre organisation, ajoutez-les en tant que contacts à un groupe que vous sélectionnez dans le portail Azure Classic lors de la configuration de vos modèles. Ou, utilisez le [module Windows PowerShell pour Azure Rights Management](../deploy-use/install-powershell.md) :

-   **utiliser un objet de définition de droits pour créer ou mettre à jour un modèle**.    Spécifiez les adresses de messagerie externes et leurs droits dans un objet de définition de droits, que vous pouvez ensuite utiliser pour créer ou mettre à jour un modèle. Spécifiez l’objet de définition de droits à l’aide de l’applet de commande [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) pour créer une variable, puis spécifiez cette variable dans le paramètre -RightsDefinition avec l’applet de commande [Add-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx) (pour un nouveau modèle) ou l’applet de commande [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx) (si vous modifiez un modèle existant). Cependant, si vous ajoutez ces utilisateurs à un modèle existant, vous devez définir des objets de définition de droits pour les groupes existants des modèles et pas seulement les utilisateurs externes.

Pour plus d’informations sur les modèles personnalisés, consultez [Configuration de modèles personnalisés pour le service Azure Rights Management](../deploy-use/configure-custom-templates.md).

## <a name="does-azure-rms-work-with-dynamic-groups-in-azure-ad"></a>Azure RMS fonctionne-t-il avec des groupes dynamiques dans Azure AD ?
Une fonctionnalité Azure AD Premium vous permet de configurer l’appartenance dynamique à des groupes en spécifiant des [règles basées sur des attributs](https://azure.microsoft.com/documentation/articles/active-directory-accessmanagement-groups-with-advanced-rules/). Quand vous créez un groupe de sécurité dans Azure AD, ce type de groupe prend en charge l’appartenance dynamique. Toutefois, il ne prend pas en charge les adresses e-mail et ne peut donc pas être utilisé avec le service Azure Rights Management. Néanmoins, vous pouvez désormais créer dans Azure AD un type de groupe à extension messagerie, qui prend en charge l’appartenance dynamique. Quand vous ajoutez un nouveau groupe dans le portail Azure Classic, vous pouvez choisir le **TYPE DE GROUPE** d’**Office 365 « Preview »**. Dans la mesure où ce groupe est à extension messagerie, vous pouvez l’utiliser avec la protection Azure Rights Management.

Comme le montre clairement le nom de l’option, ce nouveau type de groupe est toujours en version préliminaire. Des fonctionnalités supplémentaires sont prévues, de même qu’une nouvelle documentation. En attendant, nous vous confirmons que vous pouvez utiliser ce nouveau type de groupe avec la protection Azure Rights Management.


## <a name="what-devices-and-which-file-types-are-supported-by-azure-rms"></a>Quels appareils et types de fichier Azure RMS prend-il en charge ?
Pour obtenir la liste des appareils qui prennent en charge le service Azure Rights Management, consultez [Appareils clients prenant en charge la protection des données Azure Rights Management](../get-started/requirements-client-devices.md). Les fonctionnalités Rights Management n’étant actuellement pas toutes disponibles sur tous les appareils pris en charge, pensez à consulter le tableau présenté dans [Applications prenant en charge la protection des données Azure Rights Management](../get-started/requirements-applications.md).

Le service Azure Rights Management peut prendre en charge tous les types de fichiers. Dans le cas de texte, d’images, de fichiers Microsoft Office (Word, Excel, PowerPoint), de fichiers .pdf et d’autres types de fichier d’application, Azure Rights Management offre une protection native qui comprend le chiffrement et la mise en application de droits (autorisations). Pour tous les autres types de fichier et d'application, la protection générique offre l'encapsulation et l'authentification des fichiers afin de vérifier si un utilisateur est autorisé à ouvrir le fichier.

Pour obtenir la liste des extensions prises en charge en mode natif par Azure Rights Management, consultez la section [Types et extensions de noms de fichiers pris en charge](../rms-client/sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions) dans le [Guide administrateur de l’application de partage Rights Management](../rms-client/sharing-app-admin-guide.md). Les extensions de nom de fichier qui ne figurent pas dans la liste sont prises en charge via l'utilisation de l'application de partage RMS qui applique automatiquement une protection générique à ces fichiers.

## <a name="when-i-open-an-rms-protected-office-document-does-the-associated-temporary-file-become-rms-protected-as-well"></a>Quand j’ouvre un document Office protégé par RMS, le fichier temporaire associé devient-il également protégé par RMS ?

Non. Dans ce scénario, le fichier temporaire associé ne contient pas les données du document d’origine, mais uniquement ce que l’utilisateur entre pendant que le fichier est ouvert. Contrairement au fichier d’origine, le fichier temporaire n’est évidemment pas conçu pour le partage. Il reste sur l’appareil, protégé par des contrôles de sécurité locaux tels que BitLocker et EFS.

## <a name="we-really-want-to-use-byok-with-azure-information-protection-but-learned-that-this-isnt-compatible-with-exchange-onlinewhats-your-advice"></a>Nous voulons utiliser BYOK avec Azure Information Protection mais avons appris que cette solution n’est pas compatible avec Exchange Online. Que conseillez-vous ?
Ne laissez pas cette limitation retarder l’utilisation du service Azure Rights Management d’Azure Information Protection. Si vous disposez d’Exchange Online et souhaitez utiliser la solution BYOK, nous vous recommandons de déployer maintenant Azure Information Protection en mode de gestion de clés par défaut dans lequel Microsoft génère et gère votre clé. De cette façon, vous bénéficiez de tous les avantages de la protection de vos fichiers et courriers électroniques importants, avec la possibilité de passer à BYOK ultérieurement (par exemple, si Exchange Online ne prend pas en charge BYOK). Si vous passez à BYOK, vous pouvez continuer d’utiliser vos documents et e-mails précédemment protégés en utilisant une clé archivée.

Toutefois, si vos stratégies d’entreprise vous obligent à utiliser un module de sécurité matériel (HSM) sans lequel votre déploiement d’Azure Information Protection serait bloqué, vous pouvez déployer Azure Information Protection avec l’option BYOK, et des fonctionnalités de protection Rights Management réduites pour Exchange. Pour plus d’informations, consultez [Tarifs et restrictions BYOK](../plan-design/byok-price-restrictions.md) dans [Planification et implémentation de la clé de locataire Azure Rights Management](../plan-design/plan-implement-tenant-key.md).

## <a name="a-feature-i-am-looking-for-doesnt-seem-to-work-with-sharepoint-protected-librariesis-support-for-my-feature-planned"></a>Il semble qu'une fonctionnalité que je recherche ne fonctionne pas avec les bibliothèques protégées SharePoint. Une prise en charge de ma fonctionnalité est-elle prévue ?
Actuellement, SharePoint prend en charge les documents protégés par Rights Management en utilisant des bibliothèques protégées par IRM, qui ne prennent pas en charge les modèles personnalisés, le suivi de document et d’autres fonctionnalités. Pour plus d’informations, consultez la section [SharePoint Online et SharePoint Server](../understand-explore/office-apps-services-support.md#sharepoint-online-and-sharepoint-server) dans l’article [Applications et services Office](../understand-explore/office-apps-services-support.md).

Si vous êtes intéressé par une fonctionnalité spécifique qui n’est pas encore prise en charge, surveillez les annonces publiées dans [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services) (Blog de sécurité et de mobilité d’entreprise).

## <a name="how-do-i-configure-one-drive-for-business-in-sharepoint-online-so-that-users-can-safely-share-their-files-with-people-inside-and-outside-the-company"></a>Comment configurer OneDrive Entreprise dans SharePoint Online, afin que les utilisateurs puissent partager en toute sécurité des fichiers avec des personnes à l'intérieur et à l'extérieur de l'organisation ?
Par défaut, en votre qualité d’administrateur Office 365, ce n’est pas vous qui configurez cela, mais les utilisateurs.

De la même manière qu’un administrateur de site SharePoint active et configure IRM pour une bibliothèque SharePoint dont il est propriétaire, OneDrive Entreprise a été conçu pour permettre aux utilisateurs d’activer et de configurer IRM pour leur propre bibliothèque OneDrive Entreprise.  Cependant, en utilisant PowerShell, vous pouvez le faire à leur place. Pour obtenir des instructions, consultez la section [SharePoint Online et OneDrive Entreprise : configuration de la gestion des droits relatifs à l’information](../deploy-use/configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration) dans l’article [Office 365 : configuration pour les clients et services en ligne](../deploy-use/configure-office365.md).

## <a name="do-you-have-any-tips-or-tricks-for-a-successful-deployment"></a>Avez-vous des conseils ou des astuces pour réussir le déploiement ?
Après avoir supervisé de nombreux déploiements et écouté nos clients, partenaires, consultants et ingénieurs du support technique, voici l'un des conseils les plus importants que nous pouvons vous donner : **Concevoir et déployer des stratégies de droits simples**.

Puisqu’Azure Information Protection permet de partager des fichiers en toute sécurité, vous pouvez faire preuve d’ambition concernant la portée de la protection de vos données. Mais faites bien attention aux stratégies relatives aux droits. Pour de nombreuses organisations, la meilleure chose à faire est de prévenir la fuite des données en appliquant le modèle de stratégie de droits par défaut, qui restreint l’accès aux seuls membres de votre organisation. Bien sûr, vous pouvez être bien plus précis si vous devez empêcher des personnes d’imprimer, d’éditer, etc. Évitez néanmoins d’être trop précis pour des documents nécessitant un niveau de sécurité élevé. Au lieu d’implémenter ces stratégies restrictives le premier jour, adoptez une approche plus progressive.

## <a name="how-do-we-regain-access-to-files-that-were-protected-by-an-employee-who-has-now-left-the-organization"></a>Comment récupérer l'accès à des fichiers protégés par un employé qui a quitté l'organisation ?
Utilisez la fonctionnalité de super utilisateur d'Azure RMS, qui permet à des utilisateurs autorisés d'exercer des droits de propriétaire sur toutes les licences d'utilisation accordées par le client RMS de votre organisation. Cette même fonctionnalité permet à des services autorisés d'indexer et d'inspecter des fichiers si nécessaire.

Pour plus d’informations, consultez [Configuration de super utilisateurs pour Azure Rights Management et les services de découverte ou la récupération de données](../deploy-use/configure-super-users.md).

## <a name="when-i-test-revocation-in-the-document-tracking-site-i-see-a-message-that-says-people-can-still-access-the-document-for-up-to-30-daysis-this-time-period-configurable"></a>Lorsque je teste la révocation dans le site de suivi des documents, je vois un message m’indiquant que les autres utilisateurs continueront d’avoir accès au document pendant 30 jours. Cette durée est-elle configurable ?

Oui. Ce message indique la licence d’utilisation de ce fichier en particulier. Une licence d'utilisation est un certificat par document qui est accordé à un utilisateur souhaitant ouvrir un e-mail ou un fichier protégé. Ce certificat contient les droits d’utilisateur du fichier ou de l’e-mail, la clé de chiffrement qui est utilisée pour chiffrer le contenu, ainsi que les restrictions d’accès supplémentaires définies dans la stratégie du document. Lorsque la période de validité de la licence d’utilisation expire et que l’utilisateur tente d’ouvrir le fichier ou l’e-mail, ses informations d’identification doivent être renvoyées au service Azure Rights Management. 

La révocation d’un fichier ne peut être appliquée que lorsque l’utilisateur doit s’authentifier auprès du service Azure Rights Management. Par conséquent, si la période de validité de la licence d’utilisation du fichier est de 30 jours, et si l’utilisateur a déjà ouvert le document, il pourra continuer d’y accéder pendant toute la durée de la licence d’utilisation. Quand la licence d’utilisation expire, l’utilisateur doit se réauthentifier. C’est à ce moment-là que l’utilisateur se voit refuser l’accès au document, car celui-ci a été révoqué.

Pour un locataire, la valeur par défaut de la période de validité de la licence est de 30 jours. Vous pouvez configurer cette valeur à l’aide de l’applet de commande PowerShell [Set-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932063.aspx). Ce paramètre peut être remplacé par un paramètre plus restrictif dans un modèle personnalisé. 

Les utilisateurs peuvent modifier le paramètre du locataire et le paramètre du modèle en utilisant l’application de partage RMS et en sélectionnant l’option **M’autoriser à révoquer de suite l’accès à ces documents**. Ce paramètre définit la période de validité de la licence d’utilisation sur 0. 

Pour plus d’informations et pour obtenir des exemples de la façon dont fonctionne la licence d’utilisation, consultez la description détaillée de [Set-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932063.aspx).

## <a name="can-rights-management-prevent-screen-captures"></a>Est-ce que Rights Management peut empêcher les captures d’écran ?
En n’accordant pas le [droit d’utilisation](../deploy-use/configure-usage-rights.md) **Copy**, Rights Management peut empêcher les captures d’écran de nombreux outils de capture écran couramment utilisés sur les plateformes Windows (Windows 7, Windows 8.1, Windows 10, Windows Phone) et Android. En revanche, les appareils iOS et Mac n’autorisent aucune application à empêcher les captures d’écran, et les navigateurs (par exemple, utilisés avec Outlook Web App et Office Online) ne peuvent pas non plus empêcher les captures d’écran.

La possibilité d’empêcher les captures d’écran peut également aider à éviter la divulgation accidentelle ou involontaire de renseignements confidentiels ou sensibles. Il existe par ailleurs de nombreuses façons de partager des données affichées sur un écran, et la capture d’écran n’est qu’une méthode parmi d’autres. Par exemple, un utilisateur désireux de partager des informations affichées peut parfaitement les photographier avec son téléphone, recopier les données ou simplement les communiquer verbalement à un tiers.

Comme le montrent ces exemples, même si la totalité des plateformes et logiciels prenaient en charge les API de Rights Management pour bloquer les captures d’écran, la technologie seule ne peut pas toujours empêcher des utilisateurs de partager des données qu’ils ne devraient pas. Même si Rights Management peut contribuer à protéger vos données importantes au moyen de stratégies d’autorisation et d’utilisation, cette solution de gestion des droits d’entreprise doit être assortie d’autres moyens de contrôle. Par exemple, vous pouvez mettre en place une sécurité physique, surveiller et soumettre à un contrôle strict les personnes autorisées à accéder aux données de votre organisation et investir dans la formation pour sensibiliser les utilisateurs à la question du partage de données.

## <a name="whats-the-difference-between-a-user-protecting-an-email-with-do-not-forward-and-a-template-that-doesnt-include-the-forward-right"></a>Quelle différence y a-t-il entre un utilisateur qui protège un e-mail avec l’option Ne pas transférer et un modèle qui n’inclut pas de droit de transfert ?

En dépit de son nom et de son apparence, l’option **Ne pas transférer** n’est ni le contraire du droit de transfert, ni un modèle. Il s’agit en fait d’un ensemble de droits qui incluent la restriction de copier, imprimer et enregistrer des pièces jointes, outre la restriction de transfert des e-mails. Les droits sont appliqués dynamiquement aux utilisateurs par le biais des destinataires choisis et non pas statiquement attribués par l’administrateur. Pour plus d’informations, consultez la section [Option Ne pas transférer pour les e-mails](../deploy-use/configure-usage-rights.md#do-not-forward-option-for-emails) dans [Configuration des droits d’utilisation pour Azure Rights Management](../deploy-use/configure-usage-rights.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]





<!--HONumber=Jan17_HO4-->


