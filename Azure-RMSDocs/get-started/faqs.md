---
# required metadata

title: Forum Aux Questions sur Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/13/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 71ce491f-41c1-4d15-9646-455a6eaa157d

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Forum Aux Questions sur Azure Rights Management

*S’applique à : Azure Rights Management, Office 365*

Forum Aux Questions sur Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)], également appelé Azure RMS :

## Quelles sont les conditions requises pour déployer Azure RMS et comment procéder ?
Tout d’abord, pour plus d’informations sur les options d’abonnement au cloud, l’utilisation des serveurs locaux avec Azure RMS, les scénarios de déploiement non pris en charge, les appareils et applications prenant en charge Azure RMS, et l’obtention d’un lien vers une liste d’adresses IP et de noms de domaine pour les pare-feu ou les serveurs proxy, consultez [Conditions requises pour Azure Rights Management](requirements-azure-rms.md). Vous pouvez également consulter les autres articles de cette section **Prise en main** et de la section **Comprendre et explorer** pour comprendre comment [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] peut vous aider à protéger les données de votre organisation, comment cette fonctionnalité interagit avec les applications, comment elle se différencie de la version locale d’Active Directory Rights Management, ainsi que pour connaître les termes et abréviations propres à [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

## Pour bénéficier de la protection d’Azure RMS, les fichiers doivent-ils se trouver dans le cloud ?
Non, il s’agit d’une idée fausse répandue. Le service Azure Rights Management (et plus généralement Microsoft) ne voit pas et ne stocke pas vos données dans le cadre du processus de protection des informations. Les informations que vous protégez ne sont jamais stockées dans Azure, sauf si vous indiquez expressément votre volonté de les y stocker, ou si vous utilisez un autre service cloud qui les stocke dans Azure. 

Pour plus d’informations, consultez [How does Azure RMS work? Under the hood](../understand-explore/how-does-it-work.md) (Les coulisses du fonctionnement d’Azure RMS) pour comprendre comment une formule secrète du cola, créée et stockée localement, est protégée par Azure RMS tout en restant sur place.

## Puis-je intégrer Azure RMS à mes serveurs locaux ?
Oui. Vous pouvez intégrer Azure RMS à vos serveurs locaux, tels que les serveurs de fichiers Windows, Exchange Server et SharePoint. Pour ce faire, utilisez le [connecteur Rights Management](../deploy-use/deploy-rms-connector.md). Ou bien, si vous êtes simplement intéressé par l’utilisation de l’Infrastructure de classification des fichiers avec Windows Server, vous pouvez utiliser les [applets de commande de protection RMS](https://technet.microsoft.com/library/mt601315%28v=ws.10%29.aspx). Vous pouvez également synchroniser et fédérer vos contrôleurs de domaine Active Directory avec Azure AD pour une expérience d'authentification plus agréable pour les utilisateurs, par exemple, en utilisant [Azure AD Connect](http://azure.microsoft.com/documentation/articles/active-directory-aadconnect/).

Azure RMS génère et gère automatiquement les certificats XrML de façon appropriée. Il n’utilise donc pas d’infrastructure à clé publique (PKI) locale. Pour plus d’informations sur la façon dont Azure RMS utilise les certificats, consultez la section [Procédure pas à pas décrivant le fonctionnement d’Azure RMS : première utilisation, protection du contenu, consommation du contenu](../understand-explore/how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption) dans l’article [Fonctionnement d’Azure RMS](../understand-explore/how-does-it-work.md).

## J'ai un déploiement hybride d'Exchange avec certains utilisateurs sur Exchange Online et d'autres utilisateurs sur Exchange Server. Est-ce compatible avec Azure RMS ?
Absolument, et l'avantage est que les utilisateurs peuvent protéger et consommer sans problème des e-mails et pièces jointes entre les deux déploiements Exchange. Pour cette configuration, activez [Azure RMS](../deploy-use/activate-service.md) et [Gestion des droits relatifs à l’information (IRM) pour Exchange Online](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx), puis [déployez et configurez le connecteur RMS](../deploy-use/deploy-rms-connector.md) pour Exchange Server.

## Y a-t-il des instructions étape par étape pour configurer Exchange Online pour utiliser Azure RMS ?

Oui. Consultez [Exchange Online : configuration de la gestion des droits relatifs à l’information](../deploy-use/configure-office365.md#exchange-online-irm-configuration.md ) pour voir un ensemble typique de commandes permettant à Exchange Online d’utiliser Azure RMS, comprendre pourquoi Outlook Web App n’affiche pas immédiatement les options du menu **Définir les autorisations**, et découvrir la commande à exécuter si vous changez ou mettez à jour les modèles Azure RMS. 

## Si je déploie Azure RMS en production, ma société est-elle enfermée dans la solution ou risque-t-elle de perdre l’accès au contenu protégé par Azure RMS ?
Non, vous gardez toujours le contrôle de vos données et pouvez continuer à y accéder, même si vous décidez de ne plus utiliser Azure RMS. Pour plus d’informations, consultez [Désaffectation et désactivation d’Azure Rights Management](../deploy-use/decommission-deactivate.md).

Toutefois, avant que vous désaffectiez votre déploiement Azure RMS, nous aimerions que vous nous aidiez à comprendre pourquoi vous avez pris cette décision. Si Azure RMS ne répond pas à vos besoins, demandez-nous si de nouvelles fonctionnalités sont prévues dans un futur proche ou s’il existe des alternatives. Envoyez un e-mail à [AskIPTeam@Microsoft.com](mailto:askipteam@microsoft.com?subject=Planning%20to%20decommission%20Azure%20RMS) . Nous serons heureux de discuter de vos exigences techniques et professionnelles.

## Puis-je contrôler les utilisateurs pouvant utiliser Azure RMS pour protéger du contenu ?
Oui, Azure RMS dispose de contrôles d'intégration d'utilisateur pour ce scénario. Pour plus d’informations, consultez la section [Configuration de contrôles d’intégration pour un déploiement échelonné](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) dans l’article [Activation d’Azure Rights Management](../deploy-use/activate-service.md).

## Puis-je empêcher des utilisateurs de partager des documents protégés avec des organisations spécifiques ?
L’un des avantages majeurs d’Azure RMS est qu’il prend en charge la collaboration interentreprises sans que vous soyez obligé de configurer des approbations explicites pour chaque organisation partenaire, car Azure AD se charge de l’authentification à votre place.

Il n'existe aucune option d'administration permettant d'empêcher des utilisateurs de partager en toute sécurité des documents avec des organisations spécifiques. Par exemple, imaginons que vous souhaitiez bloquer une organisation en laquelle vous n’avez pas confiance ou qui exerce une activité concurrente. Empêcher Azure RMS d’envoyer des documents protégés à des utilisateurs travaillant au sein de cette organisation n’aurait aucun sens, car ceux-ci partageraient leurs documents non protégés, ce qui est probablement la dernière chose que vous souhaitez dans le cadre de ce scénario. Par exemple, vous ne seriez pas en mesure d'identifier qui partage des documents confidentiels avec quels utilisateurs au sein de ces organisations, contrairement à ce que vous pouvez faire quand le document (ou le message électronique) est protégé par Azure RMS.

## Lors du partage d'un document protégé avec une personne extérieure à mon organisation, comment cet utilisateur s'authentifie-t-il ?
Azure RMS utilise toujours un compte Azure Active Directory et une adresse de messagerie associée pour l’authentification de l’utilisateur, ce qui rend la collaboration interentreprises transparente pour les administrateurs. Si l’autre organisation utilise des services Azure, les utilisateurs disposent déjà de comptes dans Azure Active Directory, même si ceux-ci sont créés et gérés localement, puis synchronisés avec Azure.  Si l'organisation dispose d'Office 365, en arrière-plan, ce service utilise également Azure Active Directory pour les comptes d'utilisateur.  Si l’organisation de l’utilisateur ne dispose pas de compte géré dans Azure, les utilisateurs peuvent s’inscrire à [RMS for individuals](../understand-explore/rms-for-individuals.md), ce qui a pour effet de créer un client Azure non géré et un annuaire pour l’organisation avec un compte pour l’utilisateur, afin que celui-ci puisse s’authentifier après d’Azure RMS.

La méthode d'authentification pour ces comptes peut varier en fonction de la manière dont l'administrateur de l'autre organisation a configuré les comptes Azure Active Directory. Par exemple, ils peuvent utiliser des mots de passe créés pour ces comptes, Multi-Factor Authentication (MFA), une fédération ou des mots de passe créés dans les services de domaine Active Directory, puis synchronisés avec Azure Active Directory.

## Puis-je ajouter des utilisateurs ne faisant pas partie de mon organisation à des modèles personnalisés ?
Oui.  La création de modèles personnalisés que les utilisateurs finaux (et administrateurs) peuvent sélectionner à partir d'applications accélère et facilite l'application de la protection des informations à l'aide de stratégies prédéfinies que vous spécifiez. L'un des paramètres du modèle définit qui peut accéder au contenu, et vous pouvez spécifier des utilisateurs et des groupes au sein de votre organisation, ainsi que des utilisateurs extérieurs à celle-ci.

Pour spécifier des utilisateurs extérieurs à votre organisation, utilisez le [module Windows PowerShell pour Azure Rights Management](../deploy-use/install-powershell.md) :

-   **utiliser un objet de définition de droits pour créer ou mettre à jour un modèle**.    Spécifiez les adresses de messagerie externes et leurs droits dans un objet de définition de droits, que vous pouvez ensuite utiliser pour créer ou mettre à jour un modèle. Spécifiez l’objet de définition de droits à l’aide de l’applet de commande [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) pour créer une variable, puis spécifiez cette variable dans le paramètre -RightsDefinition avec l’applet de commande [Add-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx) (pour un nouveau modèle) ou l’applet de commande [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx) (si vous modifiez un modèle existant). Cependant, si vous ajoutez ces utilisateurs à un modèle existant, vous devez définir des objets de définition de droits pour les groupes existants des modèles et pas seulement les utilisateurs externes.

Pour plus d’informations sur les modèles personnalisés, consultez [Configuration de modèles personnalisés pour Azure Rights Management](../deploy-use/configure-custom-templates.md).

## Azure RMS fonctionne-t-il avec des groupes dynamiques dans Azure AD ?
Une fonctionnalité Azure AD Premium vous permet de configurer l’appartenance dynamique à des groupes en spécifiant des [règles basées sur des attributs](https://azure.microsoft.com/documentation/articles/active-directory-accessmanagement-groups-with-advanced-rules/). Quand vous créez un groupe de sécurité dans Azure AD, ce type de groupe prend en charge l’appartenance dynamique. Toutefois, il ne prend pas en charge les adresses e-mail et ne peut donc pas être utilisé avec Azure RMS. Néanmoins, vous pouvez désormais créer dans Azure AD un type de groupe à extension messagerie, qui prend en charge l’appartenance dynamique. Quand vous ajoutez un nouveau groupe dans le portail Azure Classic, vous pouvez choisir le **TYPE DE GROUPE** d’**Office 365 « Preview »**. Dans la mesure où ce groupe est à extension messagerie, vous pouvez l’utiliser avec Azure RMS.

Comme le montre clairement le nom de l’option, ce nouveau type de groupe est toujours en version préliminaire. Des fonctionnalités supplémentaires sont prévues, de même qu’une nouvelle documentation. En attendant, nous vous confirmons que vous pouvez utiliser ce nouveau type de groupe avec Azure RMS.


## Quels appareils et types de fichier Azure RMS prend-il en charge ?
Pour obtenir la liste des appareils pris en charge, consultez [Appareils client prenant en charge Azure RMS](../get-started/requirements-client-devices.md). Les fonctionnalités RMS n’étant pas disponibles actuellement sur tous les appareils pris en charge, pensez à consulter le tableau [Fonctionnalités d’un appareil client](../get-started/requirements-client-devices.md#client-device-capabilities) dans le même article.

Azure RMS peut prendre en charge tous les types de fichier. Dans le cas de texte, d'images, de fichiers Microsoft Office (Word, Excel, PowerPoint), de fichiers .pdf et d'autres types de fichier d'application, Azure RMS offre une protection native qui comprend le chiffrement et la mise en application de droits (autorisations). Pour tous les autres types de fichier et d'application, la protection générique offre l'encapsulation et l'authentification des fichiers afin de vérifier si un utilisateur est autorisé à ouvrir le fichier.

Pour obtenir la liste des extensions prises en charge en mode natif par Azure RMS, consultez la section [Types et extensions de noms de fichiers pris en charge](../rms-client/sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions) dans le [Guide administrateur de l’application de partage Rights Management](../rms-client/sharing-app-admin-guide.md). Les extensions de nom de fichier qui ne figurent pas dans la liste sont prises en charge via l'utilisation de l'application de partage RMS qui applique automatiquement une protection générique à ces fichiers.

## Quand j’ouvre un document Office protégé par RMS, le fichier temporaire associé devient-il également protégé par RMS ?

Non. Dans ce scénario, le fichier temporaire associé ne contient pas les données du document d’origine, mais uniquement ce que l’utilisateur entre pendant que le fichier est ouvert. Contrairement au fichier d’origine, le fichier temporaire n’est évidemment pas conçu pour le partage. Il reste sur l’appareil, protégé par des contrôles de sécurité locaux tels que BitLocker et EFS.

## Quand la migration à partir d'AD RMS sera-t-elle prise en charge ?
Initialement, Azure RMS ne prenait pas en charge la migration à partir d'un déploiement local de Rights Management, tel que AD RMS. Cette migration est désormais prise en charge.

Pour plus d’informations, consultez [Migration d’AD RMS vers Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md).

## Nous voulons utiliser BYOK avec Azure RMS mais avons appris que cette solution n'est pas compatible avec Exchange Online. que conseillez-vous ?
Ne laissez pas cette limitation retarder votre déploiement d'Azure RMS. Si vous disposez d'Exchange Online et souhaitez utiliser la solution BYOK, nous vous recommandons de déployer maintenant Azure RMS en mode de gestion de clés par défaut dans lequel Microsoft génère et gère votre clé. De cette façon, vous bénéficiez de tous les avantages de la protection de vos fichiers et courriers électroniques importants, avec la possibilité de passer à BYOK ultérieurement (par exemple, si Exchange Online ne prend pas en charge BYOK).

Toutefois, si vos stratégies d'entreprise vous obligent à utiliser un module de sécurité matériel (HSM) sans lequel votre déploiement d'Azure RMS serait bloqué, vous pouvez déployer Azure RMS avec l'option BYOK, et des fonctionnalités RMS réduites pour Exchange. Pour plus d’informations, consultez [Tarifs et restrictions BYOK](../plan-design/byok-price-restrictions.md) dans [Planification et implémentation de la clé de locataire Azure Rights Management](../plan-design/plan-implement-tenant-key.md).

## Il semble qu'une fonctionnalité que je recherche ne fonctionne pas avec les bibliothèques protégées SharePoint. Une prise en charge de ma fonctionnalité est-elle prévue ?
Actuellement, SharePoint prend en charge les documents protégés par les des bibliothèques protégées des services RMS, qui ne prennent pas en charge les modèles personnalisés, le suivi de document et d'autres fonctionnalités. Pour plus d’informations, consultez la section [SharePoint Online et SharePoint Server](../understand-explore/office-apps-services-support.md#sharepoint-online-and-sharepoint-server) dans l’article [Applications et services Office](../understand-explore/office-apps-services-support.md).

Si vous êtes intéressé par une fonctionnalité spécifique qui n'est pas encore prise en charge, surveillez les annonces publiées sur le [blog de l'équipe RMS](http://blogs.technet.com/b/rms/).

## Comment configurer OneDrive Entreprise dans SharePoint Online, afin que les utilisateurs puissent partager en toute sécurité des fichiers avec des personnes à l'intérieur et à l'extérieur de l'organisation ?
Par défaut, en votre qualité d’administrateur Office 365, ce n’est pas vous qui configurez cela, mais les utilisateurs.

De la même manière qu’un administrateur de site SharePoint active et configure IRM pour une bibliothèque SharePoint dont il est propriétaire, OneDrive Entreprise a été conçu pour permettre aux utilisateurs d’activer et de configurer IRM pour leur propre bibliothèque OneDrive Entreprise.  Cependant, en utilisant PowerShell, vous pouvez le faire à leur place. Pour obtenir des instructions, consultez la section [SharePoint Online et OneDrive Entreprise : configuration de la gestion des droits relatifs à l’information](../deploy-use/configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration) dans l’article [Office 365 : configuration pour les clients et services en ligne](../deploy-use/configure-office365.md).

## Avez-vous des conseils ou des astuces pour réussir le déploiement de RMS ?
Après avoir supervisé de nombreux déploiements et écouté nos clients, partenaires, consultants et ingénieurs du support technique, voici l'un des conseils les plus importants que nous pouvons vous donner : **Concevoir et déployer des stratégies de droits simples**.

Puisqu'Azure RMS permet de partager des fichiers en toute sécurité, vous pouvez faire preuve d'ambition concernant la portée de la protection de vos informations. Mais faites bien attention aux stratégies relatives aux droits. Pour de nombreuses organisations, la meilleure chose à faire est de prévenir la fuite des données en appliquant le modèle de stratégie de droits par défaut, qui restreint l’accès aux seuls membres de votre organisation. Bien sûr, vous pouvez être bien plus précis si vous devez empêcher des personnes d’imprimer, d’éditer, etc. Évitez néanmoins d’être trop précis pour des documents nécessitant un niveau de sécurité élevé. Au lieu d’implémenter ces stratégies restrictives le premier jour, adoptez une approche plus progressive.

## Quelles fonctionnalités peuvent ou ne peuvent pas être utilisées avec les différents abonnements Azure RMS ?
Pour les abonnements payants qui prennent en charge Azure RMS (Office 365, Azure RMS Premium et Enterprise Mobility Suite), il existe quelques différences pour ce qui est des fonctionnalités RMS prises en charge. Pour obtenir la liste de ces fonctionnalités, consultez [Comparaison des offres Rights Management Services (RMS)](http://technet.microsoft.com/dn858608).

L'abonnement gratuit qui prend en charge Azure RMS (RMS for individuals) prend en charge la consommation de contenu protégé par Azure RMS. Pour plus d’informations, consultez [RMS for individuals et Azure Rights Management](../understand-explore/rms-for-individuals.md).

## Où trouver des informations techniques sur l'abonnement gratuit Azure RMS (RMS for Individuals), par exemple, son fonctionnement, la façon de prendre le contrôle des comptes et les domaines non utilisables ?
Vous trouverez des réponses à ces questions dans [RMS for individuals et Azure Rights Management](../understand-explore/rms-for-individuals.md) et les articles connexes.

## Comment récupérer l'accès à des fichiers protégés par un employé qui a quitté l'organisation ?
Utilisez la fonctionnalité de super utilisateur d'Azure RMS, qui permet à des utilisateurs autorisés d'exercer des droits de propriétaire sur toutes les licences d'utilisation accordées par le client RMS de votre organisation. Cette même fonctionnalité permet à des services autorisés d'indexer et d'inspecter des fichiers si nécessaire.

Pour plus d’informations, consultez [Configuration de super utilisateurs pour Azure Rights Management et les services de découverte ou la récupération de données](../deploy-use/configure-super-users.md).

## Est-ce que Rights Management peut empêcher les captures d’écran ?
En n’accordant pas le [droit d’utilisation](../deploy-use/configure-usage-rights.md) **Copy**, Rights Management peut empêcher les captures d’écran de nombreux outils de capture écran couramment utilisés sur les plateformes Windows (Windows 7, Windows 8.1, Windows 10, Windows Phone) et Android. En revanche, les appareils iOS et Mac n’autorisent aucune application à empêcher les captures d’écran, et les navigateurs (par exemple, utilisés avec Outlook Web App et Office Online) ne peuvent pas non plus empêcher les captures d’écran.

La possibilité d’empêcher les captures d’écran peut également aider à éviter la divulgation accidentelle ou involontaire de renseignements confidentiels ou sensibles. Il existe par ailleurs de nombreuses façons de partager des données affichées sur un écran, et la capture d’écran n’est qu’une méthode parmi d’autres. Par exemple, un utilisateur désireux de partager des informations affichées peut parfaitement les photographier avec son téléphone, recopier les données ou simplement les communiquer verbalement à un tiers.

Comme le montrent ces exemples, même si la totalité des plateformes et logiciels prenaient en charge les API de Rights Management pour bloquer les captures d’écran, la technologie seule ne peut pas toujours empêcher des utilisateurs de partager des données qu’ils ne devraient pas. Même si Rights Management peut contribuer à protéger vos données importantes au moyen de stratégies d’autorisation et d’utilisation, cette solution de gestion des droits d’entreprise doit être assortie d’autres moyens de contrôle. Par exemple, vous pouvez mettre en place une sécurité physique, surveiller et soumettre à un contrôle strict les personnes autorisées à accéder aux données de votre organisation et investir dans la formation pour sensibiliser les utilisateurs à la question du partage de données.

## Où puis-je trouver des informations annexes sur Azure RMS (considérations juridiques, conformité, contrats de niveau de service, etc.) ?
Azure RMS prend en charge d'autres services et s'appuie également sur d'autres services. Si vous recherchez des informations relatives au service Azure RMS qui n'ont pas trait à son utilisation, consultez les ressources suivantes :

**Juridique et confidentialité :**

-   Pour plus d'informations sur le contrat Microsoft Azure : [Contrat Microsoft Azure](http://azure.microsoft.com/support/legal/subscription-agreement/)

-   Pour plus d'informations sur la confidentialité dans Microsoft Azure : [Déclaration de confidentialité de Microsoft Azure](http://azure.microsoft.com/support/legal/privacy-statement/)

**Sécurité, conformité et audit :**

Consultez la section [Respect des obligations réglementaires, de conformité et de sécurité](../understand-explore/azure-rms-problems-it-solves.md#security-compliance-and-regulatory-requirements) dans l’article [Quels problèmes Azure RMS résout-il ?](../understand-explore/azure-rms-problems-it-solves.md). De plus :

-   Pour connaître les certifications externes pour Azure RMS : [Centre de gestion de la confidentialité Microsoft Azure](http://azure.microsoft.com/support/trust-center/)

-   Pour plus d'informations sur FIPS 140 : [Validation FIPS 140](https://technet.microsoft.com/library/security/cc750357.aspx)

**Contrats de niveau de service :**

-   Contrat de niveau de service Azure RMS, par région sélectionnée : [télécharger à partir de la page de recherche des licences de produits](http://microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&amp;DocumentTypeId=37)

    - Par exemple, cliquez sur **OnlineSvcsConsolidatedSLA(WW)(English)(March2016)** pour télécharger le contrat de niveau de service de mars 2016 pour l’Amérique du Nord.

-   Contrat de niveau de service pour Azure Active Directory : [Contrats de niveau de service](http://azure.microsoft.com/support/legal/sla/)

**Documentation :**

-   Site de documentation sur Azure Active Directory : [Azure Active Directory](http://azure.microsoft.com/documentation/services/active-directory/)

-   Bibliothèque Azure Active Directory : [Azure Active Directory](http://msdn.microsoft.com/library/azure/jj673460.aspx)

-   Bibliothèque Office 365 : [Office 365](http://technet.microsoft.com/library/dn127064%28v=office.14%29.aspx)

## Que puis-je faire si ma question ne figure pas dans cette rubrique ?
Utilisez les liens et ressources figurant dans [Informations et support technique pour Azure Rights Management](information-support.md).

En outre, il existe des FAQ conçus pour les utilisateurs finaux :

-   [FAQ concernant l’application de partage Rights Management pour Windows](https://technet.microsoft.com/dn467883)

-   [FAQ relatif à l'application de partage Rights Management pour plateformes mobiles et Mac](https://technet.microsoft.com/dn451248)

-   [FAQ pour le suivi de document](http://go.microsoft.com/fwlink/?LinkId=523977)

Cette page de FAQ sera régulièrement actualisée. Les nouveautés seront répertoriées dans les avis de mise à jour mensuels de la documentation, sur le blog de l’ [équipe Rights Management (RMS) de Microsoft](http://blogs.technet.com/b/rms/) .

> [!TIP] Vous pouvez utiliser la [balise docs](http://blogs.technet.com/b/rms/archive/tags/docs/) sur le blog pour repérer plus facilement ces avis de documentation.




<!--HONumber=May16_HO2-->


