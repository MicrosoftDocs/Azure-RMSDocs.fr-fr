---
title: FAQ relatives à Azure Information Protection
description: Certaines questions fréquentes sur Azure Information Protection et son service de protection des données, Azure Rights Management (Azure RMS).
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/05/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 71ce491f-41c1-4d15-9646-455a6eaa157d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 04cafed6317bd17f08e6b09a7f0b42b2cb2e20c7
ms.sourcegitcommit: 80de8762953bdea2553c48b02259cd107d0c71dd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51026670"
---
# <a name="frequently-asked-questions-for-azure-information-protection"></a>Forum aux questions sur Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Vous avez une question sur Azure Information Protection ou sur la protection Rights Management (Azure RMS) ? Vous trouverez peut-être une réponse ici.

Ces pages de questions fréquentes sont régulièrement actualisées. Les nouveautés sont répertoriées dans les avis de mise à jour mensuels de la documentation sur le [blog technique d’Azure Information Protection](https://aka.ms/AIPblog).

## <a name="whats-the-difference-between-azure-information-protection-and-microsoft-information-protection"></a>Quelle est la différence entre Azure Information Protection et Microsoft Information Protection ?

Contrairement à Azure Information Protection, Microsoft Information Protection n’est pas un abonnement ou un produit que vous pouvez acheter. Au lieu de cela, il s’agit d’un framework pour les produits et les fonctionnalités intégrées qui vous aident à protéger les informations sensibles de votre organisation :

- Les produits individuels de ce framework incluent Azure Information Protection, Office 365 Information Protection (par exemple, Office 365 DLP), Windows Information Protection et Microsoft Cloud App Security. 

- Les fonctions intégrées dans ce framework incluent la gestion d’étiquette unifiée, les expériences d’étiquetage de l’utilisateur final intégrées aux applications Office, la possibilité pour Windows de comprendre les étiquettes unifiées et appliquer une protection aux données, le SDK Microsoft Information Protection et de nouvelles fonctionnalités dans Adobe Acrobat Reader pour afficher les fichiers PDF étiquetés et protégés.

Pour plus d’informations, consultez [Announcing availability of information protection capabilities to help protect your sensitive data](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Announcing-availability-of-information-protection-capabilities/ba-p/261967) (Annonce de la disponibilité des fonctionnalités de protection des informations pour protéger vos données sensibles).

## <a name="whats-the-difference-between-azure-information-protection-and-azure-rights-management"></a>Quelle est la différence entre Information Protection et Azure Rights Management ?

Azure Information Protection permet à une organisation de classifier, d’étiqueter et de protéger ses documents et e-mails. La technologie de protection utilise le service Azure Rights Management, désormais un composant d’Azure Information Protection.

## <a name="what-is-the-role-of-identity-management-for-azure-information-protection"></a>Quel est le rôle de gestion des identités pour Azure Information Protection ?

Un utilisateur doit avoir un nom d’utilisateur et un mot de passe valides pour accéder au contenu protégé par Azure Information Protection. Pour en savoir plus sur la façon dont Azure Information Protection permet de sécuriser vos données, consultez [Rôle d’Azure Information Protection dans la sécurisation des données](/enterprise-mobility-security/solutions/azure-information-protection-securing-data). 

## <a name="what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included"></a>De quel abonnement ai-je besoin pour Azure Information Protection et quelles sont les fonctionnalités incluses ?
Consultez les informations sur les abonnements et la liste des fonctionnalités de la page [Tarification Azure Information Protection](https://azure.microsoft.com/en-us/pricing/details/information-protection). 

Si vous avez un abonnement Office 365 incluant la protection des données Azure Rights Management, téléchargez la [feuille de données des licences Azure Information Protection](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf) qui contient également des questions fréquentes sur les licences.

## <a name="ive-just-got-my-azure-information-protection-subscriptionhow-do-i-get-going"></a>J’ai juste mon abonnement Azure Information Protection ; comment puis-je procéder ?

Si Azure Information Protection est nouveau pour vous et que vous souhaitez vous lancer rapidement, commencez par nos [démarrages rapides](quickstart-viewpolicy.md), puis passez en revue les [guides pratiques des scénarios courants](how-to-guides.md).

## <a name="is-the-azure-information-protection-client-only-for-subscriptions-that-include-classification-and-labeling"></a>Le client Azure Information Protection est-il réservé aux abonnements qui comprennent la classification et l’étiquetage ?

Non. Bien que la plupart des présentations et démonstrations du client Azure Information Protection que vous avez vues montrent comment il prend en charge la classification et l’étiquetage, il peut également servir avec les abonnements incluant simplement le service Azure Rights Management pour la protection des données.

Lorsque le client Azure Information Protection pour Windows est installé et qu’il n’a pas de stratégie Azure Information Protection, le client fonctionne automatiquement en [mode protection seule](./rms-client/client-protection-only-mode.md). Dans ce mode, les utilisateurs peuvent facilement appliquer des modèles Rights Management et des autorisations personnalisées. Si vous décidez, plus tard, de souscrire un abonnement qui n’inclut ni la classification ni l’étiquetage, le client passe automatiquement en mode standard lors du téléchargement de la stratégie Azure Information Protection.

Si vous utilisez actuellement l’application de partage Rights Management pour Windows, nous vous conseillons de la remplacer par le client Azure Information Protection. La prise en charge de l’application de partage prendra fin le 31 janvier 2019. Pour vous aider à effectuer la transition, consultez la section [Tâches que vous aviez l’habitude d’effectuer avec l’application de partage RMS](./rms-client/upgrade-client-app.md).

## <a name="do-you-need-to-be-a-global-admin-to-configure-azure-information-protection-or-can-i-delegate-to-other-administrators"></a>Faut-il être administrateur général pour configurer Azure Information Protection ou puis-je déléguer la configuration à d’autres administrateurs ?

Les administrateurs généraux d’un locataire Office 365 ou Azure AD peuvent évidemment exécuter toutes les tâches d’administration d’Azure Information Protection. Toutefois, si vous voulez affecter des autorisations d’administration à d’autres utilisateurs, vous avez les options suivantes :

- **Administrateur Information Protection** : ce rôle d’administrateur Azure Active Directory permet à un administrateur de configurer tous les aspects d’Azure Information Protection, mais pas d’autres services. Un administrateur qui a ce rôle peut activer et désactiver le service de protection Azure Rights Management, configurer les paramètres de protection et les étiquettes, et configurer la stratégie Azure Information Protection. Par ailleurs, un administrateur avec ce rôle peut exécuter toutes les applets de commande PowerShell du [client Azure Information Protection](./rms-client/client-admin-guide-powershell.md) et du [module AADRM](administer-powershell.md). 
    
    Pour affecter un utilisateur à ce rôle d’administration, consultez [Affecter un utilisateur à des rôles d’administration dans Azure Active Directory](/azure/active-directory/active-directory-users-assign-role-azure-portal).

- **Administrateur de sécurité** : Ce rôle d’administrateur Azure Active Directory permet à un administrateur de configurer tous les aspects d’Azure Information Protection dans le portail Azure, en plus de configurer certains aspects d’autres services Azure. Un administrateur avec ce rôle ne peut exécuter aucune des [applets de commande PowerShell du module AADRM](administer-powershell.md).
    
    Pour affecter un utilisateur à ce rôle d’administration, consultez [Affecter un utilisateur à des rôles d’administration dans Azure Active Directory](/azure/active-directory/active-directory-users-assign-role-azure-portal). Pour connaître les autres autorisations qu’un rôle donne à un utilisateur, consultez la section [Rôles disponibles](/azure/active-directory/active-directory-assign-admin-roles-azure-portal#available-roles) dans la documentation d’Azure Active Directory.

- **Administrateur général** et **Administrateur du connecteur** Azure Rights Management : Le premier de ces rôles d’administrateur Azure Rights Management accorde aux utilisateurs l’autorisation d’exécuter toutes les [applets de commande PowerShell du module AADRM](administer-powershell.md) sans pour autant être l’administrateur général des autres services cloud. Le deuxième rôle accorde l’autorisation d’exécuter uniquement le connecteur Rights Management (RMS). Aucun des rôles d’administration n’accorde d’autorisations à des consoles de gestion, ni n’utilise le mode Administrateur sur le site de suivi du document.

    Pour affecter un de ces rôles d’administration, utilisez l’applet de commande PowerShell AADRM [Add-AadrmRoleBasedAdministrator](/powershell/module/aadrm/add-aadrmrolebasedadministrator).

Quelques éléments à prendre en compte :

- Si vous avez configuré des [contrôles d’intégration](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment), cette configuration n’affecte pas la possibilité d’administrer Azure Information Protection, à l’exception du connecteur RMS. Par exemple, si vous avez configuré des contrôles d’intégration de manière à ce que seul le groupe « Département informatique » puisse protéger du contenu, le compte que vous utilisez pour installer et configurer le connecteur RMS doit être membre de ce groupe. 

- Les utilisateurs avec un rôle d’administration ne peuvent pas supprimer automatiquement la protection des documents ou des e-mails qui ont été protégés par Azure Information Protection. Seuls les super utilisateurs peuvent le faire, sous réserve que la fonctionnalité de super utilisateur soit activée. Toutefois, tout utilisateur avec des autorisations d’administrateur sur Azure Information Protection peut affecter un rôle de super utilisateur, y compris à lui-même. Ils peuvent également activer la fonctionnalité de super utilisateur. Ces actions sont enregistrées dans un journal d’administrateur. Pour plus d’informations, consultez la section des bonnes pratiques dans [Configuration de super utilisateurs pour Azure Rights Management et les services de découverte ou la récupération de données](configure-super-users.md). 

- Si vous migrez vos étiquettes Azure Information Protection vers Office 365, veillez à lire la section suivante de la documentation sur la migration d’étiquette : [Informations importantes sur les rôles administratifs](configure-policy-migrate-labels.md#important-information-about-administrative-roles).

## <a name="does-azure-information-protection-support-on-premises-and-hybrid-scenarios"></a>La solution Azure Information Protection prend-elle en charge les scénarios sur site et hybrides ?

Oui. Bien qu’Azure Information Protection soit une solution basée sur le cloud, elle peut classer, étiqueter et protéger des documents et des e-mails stockés sur site, ainsi que dans le cloud.

Si vous possédez Exchange Server, SharePoint Server et des serveurs de fichiers Windows, vous pouvez déployer le [connecteur Rights Management](deploy-rms-connector.md) afin de permettre à ces serveurs locaux d’utiliser le service Azure Rights Management pour protéger vos e-mails et documents. Vous pouvez également synchroniser et fédérer vos contrôleurs de domaine Active Directory avec Azure AD afin d’offrir une expérience d'authentification simple aux utilisateurs, par exemple, en utilisant [Azure AD Connect](http://azure.microsoft.com/documentation/articles/active-directory-aadconnect/).

Le service Azure Rights Management génère et gère automatiquement les certificats XrML en fonction des besoins. Il n’utilise donc pas d’infrastructure à clé publique (PKI) locale. Pour plus d’informations sur la façon dont Azure Rights Management utilise les certificats, voir la section [Présentation du fonctionnement d’Azure RMS : première utilisation, protection du contenu, consommation du contenu](./how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption) de l’article [Fonctionnement d’Azure RMS](./how-does-it-work.md).

## <a name="what-types-of-data-can-azure-information-protection-classify-and-protect"></a>Quels sont les types de données qu’Azure Information Protection peut classifier et protéger ?

Azure Information Protection peut classifier et protéger des e-mails et des documents, localement ou dans le cloud. Ces documents sont notamment des documents Word, des feuilles de calcul Excel, des présentations PowerPoint, des documents PDF, des fichiers texte et des fichiers image. Pour connaître les types de document pris en charge, consultez la liste des [types de fichier pris en charge](./rms-client/client-admin-guide-file-types.md) dans le guide d’administration.

Azure Information Protection ne peut pas classifier et protéger les données structurées comme les fichiers de base de données, les éléments de calendrier, les rapports Power BI, les billets Yammer, le contenu Sway et les blocs-notes OneNote.

## <a name="i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work"></a>Je vois qu’Azure Information Protection est répertoriée en tant qu’application cloud disponible pour l’accès conditionnel : comment cela fonctionne-t-il ?

Oui, dans le cadre d’une offre de préversion publique, vous pouvez à présent configurer l’accès conditionnel Azure AD pour Azure Information Protection.

Lorsqu’un utilisateur ouvre un document protégé par Azure Information Protection, les administrateurs peuvent à présent lui bloquer ou lui accorder l’accès, selon les contrôles d’accès conditionnel standard. L’authentification multifacteur (MFA) est l’une des conditions les plus couramment demandées. Une autre condition veut que les appareils soient [conformes à vos stratégies Intune](/intune/conditional-access-intune-common-ways-use) afin que, par exemple, les appareils mobiles puissent répondre à vos critères de mot de passe et de version minimale du système d’exploitation, et que les ordinateurs soient joints à un domaine.

Pour plus d’informations et des exemples de procédure pas à pas, consultez le blog suivant : [Conditional Access policies for Azure Information Protection](https://cloudblogs.microsoft.com/enterprisemobility/2017/10/17/conditional-access-policies-for-azure-information-protection/) (Stratégies d’accès conditionnel pour Azure Information Protection).

Informations complémentaires :

- Pour les ordinateurs Windows : pour la préversion actuelle, les stratégies d’accès conditionnel pour Azure Information Protection sont évaluées quand l’[environnement de l’utilisateur est initialisé](./how-does-it-work.md#initializing-the-user-environment) (ce processus est également appelé amorçage), puis tous les 30 jours.

- Vous devrez peut-être ajuster la fréquence à laquelle vos stratégies d’accès conditionnel sont évaluées. Pour cela, configurez la durée de vie des jetons. Pour plus d’informations, consultez [Durées de vie de jeton configurables dans Azure Active Directory](/azure/active-directory/active-directory-configurable-token-lifetimes).

- Nous vous recommandons de ne pas ajouter de comptes d’administrateur à vos stratégies d’accès conditionnel sans quoi ces comptes ne seront plus en mesure d’accéder au panneau Azure Information Protection dans le portail Azure.

- Si vous utilisez MFA dans vos stratégies d’accès conditionnel pour collaborer avec d’autres organisations (B2B), vous devez utiliser [Azure AD B2B Collaboration](/active-directory/b2b/what-is-b2b) et créer des comptes Invité pour les utilisateurs de l’autre organisation avec lesquels vous souhaitez partager.

- Si vous utilisez un grand nombre d’applications cloud pour l’accès conditionnel, **Microsoft Azure Information Protection** risque de ne pas s’afficher dans la liste de sélection. Dans ce cas, utilisez la zone de recherche située en haut de la liste. Commencez à taper « Microsoft Azure Information Protection » pour filtrer les applications disponibles. À condition d’avoir un abonnement pris en charge, vous pourrez alors sélectionner **Microsoft Azure Information Protection**. 

## <a name="whats-the-difference-between-labels-in-azure-information-protection-and-labels-in-office-365"></a>Quelle est la différence entre les étiquettes dans Azure Information Protection et celles dans Office 365 ?

Jusqu’à récemment, Office 365 disposait uniquement [d’étiquettes de rétention](https://support.office.com/article/af398293-c69d-465e-a249-d74561552d30) pour vous permettre de classifier les documents et les e-mails à des fins d’audit et de rétention quand ce contenu se trouvait dans les services Office 365. Par comparaison, les étiquettes Azure Information Protection vous permettent d’appliquer une stratégie de classification et de protection cohérente aux documents et aux e-mails, qu’ils soient locaux ou dans le cloud.

Annoncée à la conférence Microsoft Ignite 2018, vous allez maintenant commencer à voir une option pour créer et configurer des [étiquettes de sensibilité](https://docs.microsoft.com/Office365/SecurityCompliance/sensitivity-labels) en plus des étiquettes de rétention dans le Centre de sécurité et conformité Office 365. En outre, vous pouvez migrer vos étiquettes Azure Information Protection existantes vers le nouveau magasin d’étiquetage unifié (fonctionnalité en préversion). 

Pour plus d’informations sur la gestion de l’étiquetage unifié et la prise en charge de ces étiquettes, lisez le billet de blog [Announcing availability of information protection capabilities to help protect your sensitive data](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Announcing-availability-of-information-protection-capabilities/ba-p/261967).

Pour plus d’informations sur la migration de vos étiquettes existantes, consultez [Guide pratique pour migrer les étiquettes Azure Information Protection vers le Centre de sécurité et conformité Office 365](configure-policy-migrate-labels.md).

## <a name="whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner"></a>Quelle différence y a-t-il entre l’ICF de Windows Server et le scanneur d’Azure Information Protection ?

L’Infrastructure de classification des fichiers (ICF) de Windows Server a toujours été une option permettant de classer les documents et de les protéger à l’aide du [connecteur Rights Management](deploy-rms-connector.md) (documents Office uniquement) ou d’un [script PowerShell](./rms-client/configure-fci.md) (tous types de fichiers). 

Nous vous recommandons maintenant d’utiliser le [scanneur Azure Information Protection](deploy-aip-scanner.md). Ce scanneur utilise le client Azure Information Protection ainsi que votre stratégie Azure Information Protection pour étiqueter les documents (tous les types de fichiers) afin que ces documents soient ensuite classés, et si vous le souhaitez, protégés.

Les principales différences entre ces deux solutions sont les suivantes :

|ICF de Windows Server|Scanneur Azure Information Protection|
|--------------------------------|-------------------------------------|
|Magasins de données pris en charge : <br /><br />- Dossiers locaux sur Windows Server|Magasins de données pris en charge : <br /><br />- Dossiers locaux sur Windows Server<br /><br />- Dispositif de stockage NAS et partages de fichiers Windows<br /><br />- SharePoint Server 2016 et SharePoint Server 2013. SharePoint Server 2010 est également pris en charge pour les clients qui bénéficient d’un [support étendu pour cette version de SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).|
|Mode de fonctionnement : <br /><br />- Temps réel|Mode de fonctionnement : <br /><br />- Analyse systématiquement les magasins de données et ce cycle peut s’exécuter une ou plusieurs fois|
|Prise en charge des types de fichiers : <br /><br />- Tous les types de fichiers sont protégés par défaut <br /><br />- Des types de fichiers spécifiques peuvent être exclus de la protection par modification du registre|Prise en charge des types de fichiers : <br /><br />- Les fichiers de type Office sont protégés par défaut <br /><br />- Des types de fichiers spécifiques peuvent être inclus dans la protection par modification du registre|

Actuellement, il existe une différence dans la définition du [propriétaire de Rights Management](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner) pour les fichiers qui sont protégés sur un partage réseau ou dans un dossier local. Par défaut, dans les deux solutions, le propriétaire de Rights Management est défini sur le compte qui protège le fichier, mais vous pouvez remplacer ce paramètre :

- Pour l’ICF de Windows Server, vous pouvez définir le propriétaire de Rights Management sur un seul compte pour tous les fichiers, ou définir de façon dynamique ce propriétaire pour chaque fichier. Pour définir le propriétaire de Rights Management de façon dynamique, utilisez le paramètre et la valeur **- OwnerMail [Source File Owner Email]**. Cette configuration récupère l’adresse e-mail de l’utilisateur à partir d’Active Directory en utilisant le nom du compte d’utilisateur dans la propriété Propriétaire du fichier.

- Pour le scanneur Azure Information Protection, vous pouvez définir le propriétaire de Rights Management sur un seul compte pour tous les fichiers pour un magasin de données spécifique, mais vous ne pouvez pas définir de façon dynamique ce propriétaire pour chaque fichier. Pour définir le compte, spécifiez le paramètre **-DefaultOwner** pour le [profil du référentiel de données](/powershell/module/azureinformationprotection/Set-AIPScannerRepository?view=azureipps#optional-parameters).

Lorsque le scanneur protège les fichiers sur les sites et bibliothèques SharePoint, le propriétaire de Rights Management est défini dynamiquement pour chaque fichier à l’aide de la valeur d’auteur de SharePoint.

## <a name="ive-heard-a-new-release-is-going-to-be-available-soon-for-azure-information-protectionwhen-will-it-be-released"></a>J’ai entendu dire qu’une nouvelle version sera disponible prochainement pour Azure Information Protection : quand sera-t-elle publiée ?

La documentation technique ne contient pas d’informations sur les versions à venir. Pour ce type d’informations et pour les annonces des versions publiées, consultez le [blog Enterprise Mobility and Security](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/bg-p/enterprisemobilityandsecurity?product=azure-information-protection,azure-rights-management-services) et recevez les dernières mises à jour de [MicrosoftMobility@MSFTMobility](https://twitter.com/MSFTMobility) sur Twitter. Si vous êtes intéressé par une version d’Office, n’oubliez pas de consulter également le [blog Office 365](https://techcommunity.microsoft.com/t5/Office-365-Blog/bg-p/Office365Blog) et le [blog Office Apps](https://techcommunity.microsoft.com/t5/Office-Apps-Blog/bg-p/OfficeAppsBlog).

## <a name="is-azure-information-protection-suitable-for-my-country"></a>Azure Information Protection peut-il être utilisé dans mon pays ?

Les pays ont chacun leurs réglementations et leurs exigences. Pour vous aider à répondre à cette question pour votre organisation, consultez [Adaptation aux différents pays](./compliance.md#suitability-for-different-countries).

## <a name="how-can-azure-information-protection-help-with-gdpr"></a>Comment Azure Information Protection peut-il aider pour le RGPD ?

Pour savoir comment Azure Information Protection peut vous aider à respecter le Règlement général sur la protection des données (RGPD), consultez l’annonce du billet de blog suivant qui contient une vidéo : [Microsoft 365 provides an information protection strategy to help with the GDPR](https://blogs.office.com/2018/02/22/microsoft-365-provides-an-information-protection-strategy-to-help-with-the-gdpr).

## <a name="where-can-i-find-supporting-information-for-azureinformation-protectionsuch-as-legal-compliance-and-slas"></a>Où puis-je trouver des informations annexes sur Azure Information Protection (considérations juridiques, conformité, contrats de niveau de service, etc.) ?
Consultez [Conformité et informations annexes pour Azure Information Protection](./compliance.md).

## <a name="how-can-i-report-a-problem-or-send-feedback-for-azure-information-protection"></a>Comment puis-je signaler un problème ou envoyer des commentaires pour Azure Information Protection ?

Pour le support technique, utilisez vos canaux de support standard ou [contactez le support technique Microsoft](information-support.md#to-contact-microsoft-support).

Pour envoyer des commentaires, notamment des suggestions d’améliorations ou de nouvelles fonctionnalités : dans votre application Office, sous l’onglet **Accueil**, dans le groupe **Protection**, cliquez sur **Protéger**, puis sur **Aide et commentaires**. Dans la boîte de dialogue **Microsoft Azure Information Protection**, cliquez sur **Envoyez-nous des commentaires**. Cette option permet d’ouvrir un e-mail à envoyer à l’équipe Information Protection.

Nous vous invitons également à contacter l’équipe d’ingénieurs sur son [site Yammer Azure Information Protection](https://www.yammer.com/askipteam/). 

## <a name="what-do-i-do-if-my-question-isnt-here"></a>Que puis-je faire si ma question ne figure pas dans cette rubrique ?

Tout d’abord, passez en revue les questions fréquentes suivantes propres à la classification et à l’étiquetage ou spécifiques de la protection des données. Le service Azure Rights Management (Azure RMS) fournit la technologie de protection des données à Azure Information Protection. Azure RMS peut être utilisé avec la classification et l’étiquetage, ou de façon autonome. 

- [Forum aux questions sur la classification et l’étiquetage](faqs-infoprotect.md)

- [Forum aux questions sur la protection des données](faqs-rms.md)

Si votre question ne fait pas l’objet d’une réponse, utilisez les liens et les ressources figurant dans [Informations et support technique pour Azure Rights Management](information-support.md).

De plus, il existe des questions fréquentes destinées aux utilisateurs finaux :

- [FAQ relatif à l’application Azure Information Protection pour iOS et Android](./rms-client/mobile-app-faq.md)

- [FAQ relatif à l’application de partage RMS pour les ordinateurs Mac et Windows Phone](https://technet.microsoft.com/dn451248)

- [FAQ concernant l’application de partage Rights Management pour Windows](https://technet.microsoft.com/dn467883)



