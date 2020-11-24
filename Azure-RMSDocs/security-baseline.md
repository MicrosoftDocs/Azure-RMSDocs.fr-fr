---
title: Ligne de base de sécurité Azure pour Azure Information Protection
description: Le Azure Information Protection la ligne de base de sécurité fournit des instructions et des ressources pour la mise en œuvre des recommandations de sécurité spécifiées dans le test de sécurité Azure.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 11/18/2020
ms.author: mbaldwin
ms.custom: subject-security-benchmark
ms.openlocfilehash: cddb3ad6bd23a58922a87d27dcd6a0a1e82bd312
ms.sourcegitcommit: 173f46dd5f14c27911faec737be5986a33407477
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2020
ms.locfileid: "95568547"
---
# <a name="azure-security-baseline-for-azure-information-protection"></a>Ligne de base de sécurité Azure pour Azure Information Protection

Cette ligne de base de sécurité applique des instructions du [test de sécurité Azure version 2,0](https://docs.microsoft.com/azure/security/benchmarks/overview) à Azure information protection. Le benchmark de sécurité Azure fournit des recommandations sur la façon dont vous pouvez sécuriser vos solutions cloud sur Azure. Le contenu est regroupé en fonction des **contrôles de sécurité** définis par le test de sécurité Azure et des conseils associés à Azure information protection. Les **contrôles** non applicables aux Azure information protection ont été exclus.

Pour voir comment Azure Information Protection est entièrement mappé au test de sécurité Azure, consultez le fichier de mappage de la [ligne de base de sécurité Azure information protection complète](https://github.com/MicrosoftDocs/SecurityBenchmarks/tree/master/Azure%20Offer%20Security%20Baselines).

## <a name="network-security"></a>Sécurité réseau

*Pour plus d’informations, consultez [Benchmark de sécurité Azure : sécurité réseau](/azure/security/benchmarks/security-controls-v2-network-security).*

### <a name="ns-6-simplify-network-security-rules"></a>NS-6 : Simplifier les règles de sécurité réseau

**Aide**: utilisez les balises de service de réseau virtuel pour définir les contrôles d’accès réseau sur les groupes de sécurité réseau ou le pare-feu Azure, qui est configuré pour vos ressources Azure information protection. 

Lorsque vous créez des règles de sécurité, utilisez des balises de service à la place d’adresses IP spécifiques. Spécifiez le nom de balise de service, tel que {AzureInformationProtection}, dans le champ source ou de destination approprié d’une règle, pour autoriser ou refuser le trafic pour le service correspondant.

Microsoft gère les préfixes d’adresse englobés par la balise de service et met à jour automatiquement la balise de service quand les adresses changent.

- [Présentation et usage des balises de service](https://docs.microsoft.com/azure/virtual-network/service-tags-overview)

- [Balise de service Azure Information Protection](https://docs.microsoft.com/azure/information-protection/requirements#service-tags)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Customer

## <a name="identity-management"></a>Gestion des identités

*Pour plus d’informations, consultez [Benchmark de sécurité Azure : Gestion des identités](/azure/security/benchmarks/security-controls-v2-identity-management).*

### <a name="im-1-standardize-azure-active-directory-as-the-central-identity-and-authentication-system"></a>IM-1 : Normaliser Azure Active Directory comme système d’authentification et d’identité central

**Guide**: Azure information protection est intégré à Azure Active Directory (Azure AD), qui est le service de gestion des identités et des accès par défaut d’Azure. Sécurisez les Azure AD dans la pratique de sécurité Cloud de votre organisation. 

Passez en revue le score sécurisé de l’identité Azure AD pour vous aider à évaluer votre position de sécurité des identités par rapport aux recommandations de Microsoft en matière de meilleures pratiques. Utilisez le score pour évaluer avec précision votre configuration par rapport aux meilleures pratiques recommandées et apporter des améliorations à votre posture de sécurité.

Standardisez Azure AD pour régir la gestion des identités et des accès de votre organisation dans :

- Microsoft Cloud des ressources, telles que les Portail Azure, le stockage Azure, les machines virtuelles Azure (Linux et Windows), le Azure Key Vault, la plateforme en tant que service (PaaS) et les applications SaaS (Software as a service)

- Les ressources de votre organisation, telles que les applications sur Azure ou les ressources réseau de votre entreprise

Azure AD prend en charge les identités externes pour permettre aux utilisateurs sans compte Microsoft de se connecter à leurs applications et ressources avec leurs comptes non Microsoft.

- [Locataires dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/single-and-multi-tenant-apps)

- [Création et configuration d’une instance Azure AD](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-access-create-new-tenant)

- [Utilisez des fournisseurs d'identité externes pour l’application](https://docs.microsoft.com/azure/active-directory/b2b/identity-providers)

- [Quel est le score de sécurité d’identité dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/fundamentals/identity-secure-score)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Customer

### <a name="im-2-manage-application-identities-securely-and-automatically"></a>IM-2 : Gérer les identités d’application de façon sécurisée et automatique

**Guide**: Azure information protection est intégré à Azure Active Directory (Azure AD), qui est le service de gestion des identités et des accès d’Azure. Azure Rights Management Service utilise une identité d’application Azure AD tout en accédant aux clés des clients stockées avec Azure Key Vault pour les scénarios de Bring Your Own Key (BYOK). L’autorisation d’un service Azure Rights Management pour accéder à vos clés s’effectue par le biais de la configuration des stratégies d’accès Azure Key Vault, qui peuvent être effectuées à l’aide de l’Portail Azure ou à l’aide de PowerShell.

- [Autorisation du service Azure Rights Management pour BYOK](https://docs.microsoft.com/azure/information-protection/byok-price-restrictions#authorizing-the-azure-rights-management-service-to-use-your-key)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Customer

### <a name="im-3-use-azure-ad-single-sign-on-sso-for-application-access"></a>IM-3 : Utiliser l’authentification unique Azure AD pour l’accès aux applications

**Guide**: Azure information protection est intégré à Azure Active Directory (Azure AD), qui est le service de gestion des identités et des accès par défaut d’Azure. 

Azure Information Protection utilise Azure AD pour assurer la gestion des identités et des accès aux ressources Azure, aux applications Cloud et aux applications locales. Cela comprend les identités d’entreprise telles que les employés, ainsi que les identités externes telles que les partenaires, les fournisseurs et les fournisseurs. Cela permet à l’authentification unique de gérer et de sécuriser l’accès aux données et ressources de votre organisation en local et dans le Cloud. Connectez tous vos utilisateurs, applications et appareils au Azure AD pour un accès transparent et sécurisé, ainsi qu’une visibilité et un contrôle accrus.

- [Connectez-vous à Azure Information Protection avec Azure Active Directory](https://docs.microsoft.com/azure/information-protection/requirements)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Customer

### <a name="im-4-use-strong-authentication-controls-for-all-azure-active-directory-based-access"></a>IM-4 : Utiliser des contrôles d’authentification renforcés pour tous les accès basés sur Azure Active Directory

**Guide**: Azure information protection est intégré à Azure Active Directory (Azure AD), qui prend en charge une authentification forte via l’authentification multifacteur. Pour prendre en charge l’authentification et l’autorisation pour Azure Information Protection, vous devez disposer d’un Azure AD. Pour utiliser des comptes d'utilisateur à partir de votre directeur local (AD DS), vous devez également configurer une intégration d'annuaire.

- L’authentification unique est prise en charge pour Azure Information Protection, afin que les utilisateurs ne soient pas invités à saisir leurs informations d’identification à plusieurs reprises. Si vous utilisez une autre solution de fournisseur pour la fédération, vérifiez auprès de ce dernier comment la configurer pour Azure AD. WS-Trust est une exigence courante pour ces solutions afin de prendre en charge l’authentification unique.

- L’authentification multifacteur est prise en charge avec Azure Information Protection, lorsque vous disposez du logiciel client requis et que vous avez correctement configuré l’infrastructure de prise en charge de Multi-Factor Authentication.

Pour plus d’informations, consultez les références suivantes :

- [Authentification Azure Information Protection via Azure Active Directory](https://docs.microsoft.com/azure/information-protection/requirements)

**Supervision d’Azure Security Center** : Oui

**Responsabilité** : Customer

### <a name="im-5-monitor-and-alert-on-account-anomalies"></a>IM-5 : Surveiller et alerter en cas d’anomalies de compte

**Guide**: Azure information protection est intégré à Azure Active Directory (Azure AD), qui est le service de gestion des identités et des accès par défaut d’Azure. 

Aide supplémentaire concernant Azure AD :

- Connexion : le rapport de connexion fournit des informations sur l’utilisation des applications gérées et des activités de connexion des utilisateurs.
- Journaux d’audit : traçabilité proposée via des journaux d’activité pour toutes les modifications effectuées par diverses fonctionnalités au sein d’Azure AD. Des exemples de journaux d’audit incluent les modifications apportées aux ressources dans Azure AD, telles que l’ajout ou la suppression d’utilisateurs, d’applications, de groupes, de rôles et de stratégies.
- Connexion risquée : une connexion risquée est un indicateur pour une tentative de connexion qui a pu être effectuée par une personne qui n’est pas le propriétaire légitime d’un compte d’utilisateur.
- Utilisateurs avec indicateur de risque : un utilisateur à risque correspond à un indicateur de compte d’utilisateur susceptible d’être compromis.
Ces sources de données peuvent être intégrées à Azure Monitor, à Azure Sentinel ou à des systèmes SIEM tiers.

Azure Security Center pouvez également alerter certaines activités suspectes, telles qu’un nombre excessif de tentatives d’authentification ayant échoué ou des comptes dépréciés dans l’abonnement.

Azure-protection avancée contre les menaces (ATP) est une solution de sécurité qui peut utiliser Active Directory signaux permettant d’identifier, de détecter et d’examiner les menaces avancées, les identités compromises et les actions malveillantes de l’Insider.

- [Rapports d’activité d’audit dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/reports-monitoring/concept-audit-logs) 

- [Guide pratique pour afficher les connexions risquées Azure AD](https://docs.microsoft.com/azure/active-directory/reports-monitoring/concept-risky-sign-ins) 

- [Guide pratique pour identifier les utilisateurs Azure AD pour lesquels une activité à risque a été signalée](https://docs.microsoft.com/azure/active-directory/reports-monitoring/concept-user-at-risk) 

- [Guide pratique pour superviser l’activité liée aux identités et aux accès des utilisateurs dans Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-identity-access) 

- [Alertes dans le module de protection de renseignement sur les menaces d’Azure Security Center](https://docs.microsoft.com//azure/security-center/alerts-reference) 

- [Guide pratique pour intégrer des journaux d’activité Azure dans Azure Monitor](https://docs.microsoft.com/azure/active-directory/reports-monitoring/howto-integrate-activity-logs-with-log-analytics)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Customer

### <a name="im-6-restrict-azure-resource-access-based-on-conditions"></a>IM-6 : Restreindre l’accès aux ressources Azure en fonction des conditions

**Guide**: Azure information protection est intégré à Azure Active Directory (Azure AD), qui est le service de gestion des identités et des accès par défaut d’Azure. Dans Azure AD, configurez l’accès conditionnel pour Azure Information Protection. Les administrateurs peuvent bloquer ou accorder l’accès aux utilisateurs de leur locataire, pour les documents protégés par Azure Information Protection, en fonction des contrôles d’accès conditionnel standard.

L’authentification multifacteur est l’une des conditions les plus couramment demandées, alors que la conformité de l’appareil avec les stratégies Intune configurées en est une autre. Vous pouvez exiger des conditions pour que les appareils mobiles respectent les exigences de votre mot de passe d’organisation, disposent d’une version minimale du système d’exploitation et que les ordinateurs connectés soient joints à un domaine.

- [Stratégies d’accès conditionnel pour Azure Information Protection](https://cloudblogs.microsoft.com/enterprisemobility/2017/10/17/conditional-access-policies-for-azure-information-protection)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Customer

## <a name="privileged-access"></a>Accès privilégié

*Pour plus d’informations, consultez [Benchmark de sécurité Azure : Accès privilégié](/azure/security/benchmarks/security-controls-v2-privileged-access).*

### <a name="pa-1-protect-and-limit-highly-privileged-users"></a>PA-1 : Protéger et limiter les utilisateurs disposant de privilèges élevés

**Guide**: Azure information protection est intégré à Azure Active Directory (Azure AD), qui est le service de gestion des identités et des accès par défaut d’Azure. 

Azure Information Protection comprend un rôle de niveau administrateur dans Azure AD. Les utilisateurs affectés au rôle administrateur disposent d’autorisations complètes dans le service Azure Information Protection. Le rôle d’administrateur peut être utilisé pour configurer des étiquettes pour la stratégie de Azure Information Protection, la gestion des modèles de protection et l’activation de la protection. Toutefois, le rôle administrateur n’accorde aucune autorisation dans Identity Protection Center, Privileged Identity Management, Monitor Microsoft 365 Service Health ou Office 365 Security &amp; Compliance Center.

Limitez le nombre de comptes ou de rôles à privilèges élevés et protégez ces comptes à un niveau élevé, car les utilisateurs disposant de ce privilège peuvent lire et modifier directement ou indirectement chaque ressource dans votre environnement Azure. Activer l’accès privilégié juste-à-temps (JIT) aux ressources Azure et Azure AD à l’aide de Privileged Identity Management (PIM). L’accès juste-à-temps accorde des autorisations temporaires pour effectuer des tâches privilégiées uniquement lorsque les utilisateurs en ont besoin. PIM peut également générer des alertes de sécurité en cas d’activité suspecte ou non sécurisée dans votre organisation Azure AD.

- [Rôle d’administrateur Azure Information Protection](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#azure-information-protection-administrator)

- [Autorisations de rôle Administrateur dans Azure AD](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles)

- [Utiliser les alertes de sécurité Azure Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-how-to-configure-security-alerts) 

- [Sécurisation de l’accès privilégié pour les déploiements hybrides et cloud dans Azure AD](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-admin-roles-secure)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Customer

### <a name="pa-2-restrict-administrative-access-to-business-critical-systems"></a>PA-2 : Limiter l’accès administratif aux systèmes critiques de l’entreprise

**Guide**: Azure information protection est intégré à Azure Active Directory (Azure AD), qui est le service de gestion des identités et des accès par défaut d’Azure. 

Azure Information Protection comprend un rôle de niveau administrateur dans Azure AD. Les utilisateurs affectés au rôle administrateur disposent d’autorisations complètes dans le service Azure Information Protection. Le rôle d’administrateur permet de configurer des étiquettes pour la stratégie de Azure Information Protection, de gérer des modèles de protection et d’activer la protection. Le rôle d’administrateur n’accorde aucune autorisation dans Identity Protection Center, Privileged Identity Management, Monitor Microsoft 365 Service Health ou Office 365 Security &amp; Compliance Center.

- [Rôle d’administrateur Azure Information Protection](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#azure-information-protection-administrator)

- [Azure Information Protection actions que l’administrateur peut entreprendre](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#azure-information-protection-administrator-permissions)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Customer

### <a name="pa-3-review-and-reconcile-user-access-regularly"></a>PA-3 : Examiner et rapprocher régulièrement les accès utilisateur

**Guide**: Azure information protection est intégré à Azure Active Directory (Azure AD), qui est le service de gestion des identités et des accès par défaut d’Azure.

Utilisez Azure AD pour gérer les ressources, passer en revue les comptes d’utilisateur et accéder régulièrement aux affectations pour vous assurer que les comptes et leur accès sont valides. Effectuez des révisions d’accès Azure AD pour passer en revue les appartenances aux groupes, l’accès aux applications d’entreprise et les attributions de rôles. Détecte les comptes obsolètes avec les rapports de Azure AD. Les fonctionnalités de Privileged Identity Management de Azure AD peuvent être utilisées pour créer un flux de travail de rapport de révision d’accès afin de faciliter le processus de révision.

En outre, Azure Privileged Identity Management peut également être configuré pour alerter en cas de création d’un nombre excessif de comptes d’administrateur et pour identifier les comptes d’administrateur périmés ou mal configurés. Notez que certains services Azure prennent en charge les utilisateurs et les rôles locaux qui ne sont pas gérés par le biais de Azure AD. Les clients devront gérer ces utilisateurs séparément.

- [Rôle d’administrateur Azure Information Protection](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#azure-information-protection-administrator)

- [Azure Information Protection actions que l’administrateur peut entreprendre](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#azure-information-protection-administrator-permissions)

- [Créer une révision d’accès des rôles de ressources Azure dans Privileged Identity Management (PIM)](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-resource-roles-start-access-review) 

- [Utilisation des révisions d’accès et des identités Azure AD](https://docs.microsoft.com/azure/active-directory/governance/access-reviews-overvie)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Customer

### <a name="pa-4-set-up-emergency-access-in-azure-ad"></a>PA-4 : Configurer l’accès d’urgence dans Azure AD

**Guide**: Azure information protection est intégré à Azure Active Directory (Azure AD) pour gérer ses ressources. Pour empêcher le verrouillage accidentel de votre organisation Azure AD, configurez un compte d’accès d’urgence pour conserver un accès lorsque les comptes administratifs normaux ne peuvent pas être utilisés. Les comptes d’accès d’urgence sont généralement hautement privilégiés et ne doivent pas être attribués à des personnes spécifiques. Les comptes d’accès d’urgence sont limités à des cas d’urgence ou à des scénarios « de secours » où il est impossible d’utiliser des comptes d’administration normaux.

Vous devez vous assurer que les informations d’identification (telles que le mot de passe, le certificat ou la carte à puce) des comptes d’accès d’urgence restent sécurisées et connues des seules personnes autorisées à les utiliser en cas d’urgence.

- [Gérer des comptes d’accès d’urgence dans Azure AD](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-emergency-access)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Customer

### <a name="pa-5-automate-entitlement-management"></a>PA-5 : Automatiser la gestion des droits d'utilisation 

**Guide**: Azure information protection est intégré à Azure Active Directory (Azure AD), le service de gestion des identités et des accès par défaut d’Azure.

Azure AD offre des fonctionnalités de gestion des droits pour automatiser les flux de travail de demande d’accès, y compris les attributions d’accès, les révisions et l’expiration. L’approbation en deux ou plusieurs étapes est également prise en charge.

- [Présentation des révisions d’accès Azure AD](https://docs.microsoft.com/azure/active-directory/governance/access-reviews-overview) 

- [Présentation de la gestion des droits d’utilisation Azure AD](https://docs.microsoft.com/azure/active-directory/governance/entitlement-management-overview)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Customer

### <a name="pa-6-use-privileged-access-workstations"></a>PA-6 : Utiliser des stations de travail d’accès privilégié

**Guide**: Azure information protection peut être géré à partir d’une station de travail cliente via PowerShell. 

Les stations de travail sécurisées et isolées sont très importantes pour la sécurité des rôles sensibles, tels que les administrateurs, les développeurs et les opérateurs de service critiques. 

Utilisez des stations de travail utilisateur hautement sécurisées et/ou Azure Bastion pour les tâches d’administration. Utilisez Azure Active Directory, Microsoft Defender Advanced Threat Protection (MDATP) et/ou Microsoft Intune pour déployer une station de travail utilisateur sécurisée et gérée pour les tâches d’administration. Les stations de travail sécurisées peuvent être gérées de manière centralisée pour appliquer une configuration sécurisée, notamment une authentification forte, des lignes de base logicielles et matérielles et un accès réseau et logique restreint.

- [Aide sur l’utilisation de PowerShell pour Azure Information Protection](https://docs.microsoft.com/azure/information-protection/rms-client/client-admin-guide-powershell)

- [Comprendre les stations de travail d’accès privilégié](https://docs.microsoft.com/azure/active-directory/devices/concept-azure-managed-workstation) 

- [Déployer une station de travail d’accès privilégié](https://docs.microsoft.com/azure/active-directory/devices/howto-azure-managed-workstation)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Customer

### <a name="pa-7-follow-just-enough-administration-least-privilege-principle"></a>PA-7 : Suivre le principe Just Enough Administration (privilèges minimum) 

**Guide**: Azure information protection est intégré à Azure Active Directory (Azure AD), qui est le service de gestion des identités et des accès par défaut d’Azure. 

Azure Information Protection comprend un rôle de niveau administrateur dans Azure AD. Les utilisateurs affectés au rôle administrateur disposent d’autorisations complètes dans le service Azure Information Protection. Le rôle d’administrateur peut être utilisé pour configurer des étiquettes pour la stratégie de Azure Information Protection, la gestion des modèles de protection et l’activation de la protection. Toutefois, le rôle administrateur n’accorde aucune autorisation dans Identity Protection Center, Privileged Identity Management, Monitor Microsoft 365 Service Health ou Office 365 Security &amp; Compliance Center.

Limitez le nombre de comptes ou de rôles à privilèges élevés et protégez ces comptes à un niveau élevé, car les utilisateurs disposant de ce privilège peuvent lire et modifier directement ou indirectement chaque ressource dans votre environnement Azure. Activer l’accès privilégié juste-à-temps (JIT) aux ressources Azure et Azure AD à l’aide de Privileged Identity Management (PIM). L’accès juste-à-temps accorde des autorisations temporaires pour effectuer des tâches privilégiées uniquement lorsque les utilisateurs en ont besoin. PIM peut également générer des alertes de sécurité en cas d’activité suspecte ou non sécurisée dans votre organisation Azure AD.

- [Droits inclus dans les niveaux d’autorisation pour Azure Information Protection](https://docs.microsoft.com/azure/information-protection/configure-usage-rights#rights-included-in-permissions-levels)

- [Rights Management émetteur et Rights Management propriétaire](https://docs.microsoft.com/azure/information-protection/configure-usage-rights#rights-management-issuer-and-rights-management-owner)

- [Rôle d’administrateur Azure Information Protection](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#azure-information-protection-administrator)

- [Autorisations de rôle Administrateur dans Azure AD](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles)

- [Utiliser les alertes de sécurité Azure Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-how-to-configure-security-alerts) 

- [Sécurisation de l’accès privilégié pour les déploiements hybrides et cloud dans Azure AD](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-admin-roles-secure)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Customer

### <a name="pa-8-choose-approval-process-for-microsoft-support"></a>PA-8 : Choisir le processus d’approbation pour le support Microsoft  

**Guide**: Azure information protection prend en charge Azure Customer Lockbox pour offrir aux clients la possibilité d’examiner, d’approuver et de rejeter les demandes d’accès aux données, ainsi que de consulter les demandes en cours. 

- [Présentation de la boîte postale](https://docs.microsoft.com/azure/security/fundamentals/customer-lockbox-overview)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Customer

## <a name="data-protection"></a>Protection des données

*Pour plus d’informations, consultez [Benchmark de sécurité Azure : protection des données](/azure/security/benchmarks/security-controls-v2-data-protection).*

### <a name="dp-1-discovery-classify-and-label-sensitive-data"></a>DP-1 : Découvrir, classifier et étiqueter des données sensibles

**Guide**: Azure information protection permet de découvrir, de classer et d’étiqueter les informations sensibles. 

Azure Information Protection est une solution basée sur le Cloud qui permet aux organisations de classer et de protéger des documents et des e-mails en appliquant des étiquettes. Les étiquettes peuvent être appliquées automatiquement par les administrateurs à l’aide de règles et de conditions ou manuellement par les utilisateurs, qui peuvent éventuellement recevoir des suggestions définies par les administrateurs.

- [Vue d’ensemble de Azure Information Protection](https://docs.microsoft.com/azure/information-protection/)

- [Aide sur la configuration du client d’étiquetage unifié](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-user-guide)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Partagé

### <a name="dp-2-protect-sensitive-data"></a>DP-2 : Protection des données sensibles

**Guide**: Azure information protection fournit une protection des données en offrant la possibilité d’étiqueter les informations sensibles et de protéger ces données par le biais du chiffrement. La protection est assurée par le service Azure Rights Management.

- [Azure Rights Management](https://docs.microsoft.com/azure/information-protection/what-is-azure-rms)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Partagé

### <a name="dp-3-monitor-for-unauthorized-transfer-of-sensitive-data"></a>DP-3 : Détection des transferts non autorisés de données sensibles

**Guide**: Azure information protection permet de surveiller les transferts de données sensibles non autorisés via la fonctionnalité de suivi et de révocation. Le suivi et la révocation permettent au client de suivre la manière dont les utilisateurs utilisent les documents qu’ils ont envoyés et de révoquer l’accès si les utilisateurs ne doivent plus pouvoir les lire. 

- [Aide sur le suivi et la révocation](https://docs.microsoft.com/azure/information-protection/rms-client/client-track-revoke)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Partagé

## <a name="asset-management"></a>Gestion des ressources

*Pour plus d’informations, consultez [Benchmark de sécurité Azure : Gestion des ressources](/azure/security/benchmarks/security-controls-v2-asset-management).*

### <a name="am-1-ensure-security-team-has-visibility-into-risks-for-assets"></a>AM-1 : S’assurer que l’équipe de sécurité a une visibilité sur les risques pour les ressources

**Guide**: Assurez-vous que les équipes de sécurité reçoivent des autorisations de lecteur de sécurité dans votre locataire Azure et les abonnements afin qu’ils puissent surveiller les risques de sécurité à l’aide de Azure Security Center. 

Selon la façon dont les responsabilités de l’équipe de sécurité sont structurées, la surveillance des risques de sécurité peut tenir de la responsabilité d’une équipe de sécurité centrale ou d’une équipe locale. Cela dit, les insights et les risques liés à la sécurité doivent toujours être agrégés de manière centralisée au sein d’une organisation. 

Les autorisations de lecteur de sécurité peuvent être appliquées globalement à un locataire entier (groupe d’administration racine) ou étendues à des groupes d’administration ou à des abonnements spécifiques. 

Remarque : Des autorisations supplémentaires peuvent être nécessaires pour obtenir une visibilité sur les charges de travail et services. 

- [Vue d’ensemble du rôle lecteur de sécurité](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#security-reader)

- [Vue d'ensemble des groupes d'administration Azure](https://docs.microsoft.com/azure/governance/management-groups/overview)

**Supervision d’Azure Security Center** : actuellement non disponible

**Responsabilité** : Customer

### <a name="am-3-use-only-approved-azure-services"></a>AM-3 : Utiliser des services Azure approuvés uniquement

**Guide**: Azure information protection ne prend pas en charge les déploiements Azure Resource Manager ou permet aux clients de limiter les déploiements par le biais de définitions de Azure Policy intégrées, telles que « autoriser les ressources » ou « refuser des ressources ». Toutefois, les clients peuvent limiter l’utilisation des Azure Information Protection par le biais de stratégies d’étiquetage dans le centre de sécurité et conformité. 

- [Gérer la protection des informations par le biais du centre de sécurité et conformité](https://docs.microsoft.com/microsoft-365/compliance/protect-information?view=o365-worldwide&amp;preserve-view=true)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Customer

## <a name="logging-and-threat-detection"></a>Journalisation et détection des menaces

*Pour plus d’informations, consultez [Benchmark de sécurité Azure : Journalisation et détection des menaces](/azure/security/benchmarks/security-controls-v2-logging-threat-protection).*

### <a name="lt-2-enable-threat-detection-for-azure-identity-and-access-management"></a>LT-2 : Activer la détection des menaces pour la gestion des identités et des accès Azure

**Guide**: Azure information protection est intégré à Azure Active Directory (Azure AD), qui est le service de gestion des identités et des accès par défaut d’Azure. 

Affichez les journaux des utilisateurs fournis par Azure AD avec des rapports de Azure AD et d’autres solutions telles que Azure Monitor, Azure Sentinel ou d’autres outils SIEM/de surveillance pour des scénarios d’utilisation de surveillance et d’analyse plus sophistiqués. 

Il s'agit de : 

-   Rapport de connexion – le rapport de connexion fournit des informations sur l’utilisation des applications gérées et des activités de connexion des utilisateurs.

-   Journaux d’audit : traçabilité proposée via des journaux d’activité pour toutes les modifications effectuées par diverses fonctionnalités au sein d’Azure AD. Des exemples de journaux d’audit incluent les modifications apportées aux ressources dans Azure AD, telles que l’ajout ou la suppression d’utilisateurs, d’applications, de groupes, de rôles et de stratégies.

-   Connexions risquées : une connexion risquée est un indicateur pour une tentative de connexion qui a pu être effectuée par une personne qui n’est pas le propriétaire légitime d’un compte d’utilisateur.

-   Utilisateurs avec indicateur de risque : un utilisateur à risque correspond à un indicateur de compte d’utilisateur susceptible d’être compromis.

Azure Security Center pouvez également alerter certaines activités suspectes, telles qu’un nombre excessif de tentatives d’authentification ayant échoué et les comptes dépréciés dans l’abonnement. En plus de la surveillance de base de l’hygiène de sécurité, Security Center module de protection contre les menaces peut également collecter des alertes de sécurité plus approfondies à partir de ressources de calcul Azure individuelles (telles que des machines virtuelles, des conteneurs, app service), des ressources de données (telles que la base de données SQL et le stockage) et des couches de service Azure. Cette capacité vous permet de voir les anomalies de compte à l’intérieur des ressources individuelles.

- [Rapports d’activité d’audit dans Azure AD](https://docs.microsoft.com/azure/active-directory/reports-monitoring/concept-audit-logs)

- [Activer Azure AD Identity Protection](https://docs.microsoft.com/azure/active-directory/identity-protection/overview-identity-protection)

- [Protection contre les menaces dans Azure Security Center](https://docs.microsoft.com/azure/security-center/threat-protection)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Customer

### <a name="lt-4-enable-logging-for-azure-resources"></a>LT-4 : Activer la journalisation pour les ressources Azure

**Guide**: Azure information protection fournit une protection des données pour les documents et les e-mails d’une organisation, ainsi qu’un journal pour chaque demande.  Ces demandes incluent le moment où les utilisateurs protègent des documents et des e-mails, les actions effectuées par les administrateurs pour ce service, ainsi que les actions effectuées par les opérateurs Microsoft pour prendre en charge votre déploiement Azure Information Protection.

Les types de journaux générés par Azure Information Protection incluent :

- Journal d’administration-journalise les tâches d’administration pour le service de protection. Par exemple, si le service est désactivé, lorsque la fonctionnalité de super utilisateur est activée et lorsque des utilisateurs délèguent des autorisations d’administrateur au service.

- Suivi des documents : permet aux utilisateurs de suivre et de révoquer les documents qu’ils ont suivis avec le client Azure Information Protection. Les administrateurs généraux peuvent également effectuer le suivi de ces documents au nom des utilisateurs.

- Journaux des événements clients : activité d’utilisation pour le client Azure Information Protection, consigné dans le journal des événements des applications et services Windows local, Azure Information Protection.

- Fichiers journaux du client-journaux de dépannage pour le client Azure Information Protection

Les journaux d’utilisation de la protection peuvent être utilisés pour identifier « qui » accède à vos données protégées, à partir des appareils « quels » et à partir de « où ». Les journaux indiquent si les utilisateurs peuvent lire du contenu protégé, ainsi que pour identifier les personnes qui ont lu un document important qui a été protégé. 

- [Journalisation et analyse de l’utilisation de la protection à partir de Azure Information Protection](https://docs.microsoft.com/azure/information-protection/log-analyze-usage)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Customer

### <a name="lt-5-centralize-security-log-management-and-analysis"></a>LT-5 : Centraliser la gestion et l’analyse des journaux de sécurité

**Guide**: Assurez-vous que le personnel du support technique peut créer une vue complète de ce qui s’est passé au cours d’un événement, en interrogeant et en utilisant diverses sources de données, lors de l’examen d’incidents potentiels. 

Évitez les aveugles en recueillant divers journaux et en les envoyant à une solution SIEM centrale, telle qu’Azure Sentinel, pour suivre les activités d’un pirate potentiel sur la chaîne de destruction. Les journaux peuvent révéler si les utilisateurs parvient à lire du contenu protégé, ainsi qu’à identifier les personnes qui ont lu un document important qui a été protégé. Assurez-vous que les Insights et les apprentissages sont capturés pour d’autres analystes et pour une référence historique future.  

Azure Sentinel fournit des analyses de données approfondies sur pratiquement toutes les sources de journal et un portail de gestion des cas pour gérer le cycle de vie complet des incidents. Les renseignements obtenus au cours d’une enquête peuvent être associés à un incident à des fins de suivi et de rapport. 

- [Journalisation et analyse de l’utilisation de la protection à partir de Azure Information Protection](https://docs.microsoft.com/azure/information-protection/log-analyze-usage)

- [Examiner les incidents avec Azure Sentinel](https://docs.microsoft.com/azure/sentinel/tutorial-investigate-cases)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Customer

### <a name="lt-6-configure-log-storage-retention"></a>LT-6 : Configurer la rétention du stockage des journaux

**Guide**: Azure information protection fournit une protection des données pour les documents et les e-mails d’une organisation, avec un journal pour chaque demande.  Ces demandes incluent le moment où les utilisateurs protègent des documents et des e-mails, quand ils consomment ce contenu, les actions effectuées par vos administrateurs pour ce service et les actions effectuées par les opérateurs Microsoft pour prendre en charge votre déploiement Azure Information Protection.

La quantité de données collectées et stockées dans votre espace de travail Azure Information Protection et sa rétention varient considérablement pour chaque locataire, en fonction de facteurs tels que le nombre de clients Azure Information Protection et d’autres points de terminaison pris en charge, que vous collectiez des données de découverte de point de terminaison, que vous ayez déployé des scanneurs, le nombre de documents protégés auxquels vous accédez, etc.

Utilisez Azure Monitor fonctionnalité utilisation et estimation des coûts pour vous aider à estimer et à examiner la quantité de données stockées et à contrôler la période de rétention des données pour votre espace de travail Log Analytics. 

- [Journalisation et analyse de l’utilisation de la protection à partir de Azure Information Protection](https://docs.microsoft.com/azure/information-protection/log-analyze-usage)

- [Gérer l’utilisation et les coûts avec les journaux Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/platform/manage-cost-storage)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Customer

## <a name="incident-response"></a>Réponse aux incidents

*Pour plus d’informations, consultez [Benchmark de sécurité Azure : réponse aux incidents](/azure/security/benchmarks/security-controls-v2-incident-response).*

### <a name="ir-1-preparation--update-incident-response-process-for-azure"></a>IR-1 : Préparation – mettre à jour le processus de réponse aux incidents pour Azure

**Conseils** : Assurez-vous que votre organisation dispose de processus pour répondre aux incidents de sécurité, qu’elle a mis à jour ces processus pour Azure et qu’elle les exerce régulièrement pour garantir la préparation.

- [Implémenter la sécurité dans l’environnement de l’entreprise](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#4-process-update-incident-response-ir-processes-for-cloud)

- [Guide de référence sur les réponses aux incidents](https://docs.microsoft.com/microsoft-365/downloads/IR-Reference-Guide.pdf)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Customer

### <a name="ir-2-preparation--setup-incident-notification"></a>IR-2 : Préparation – configurer la notification d’incident

**Conseils** : Configurez les coordonnées des personnes à contacter en cas d’incident de sécurité dans Azure Security Center. Microsoft utilisera ces coordonnées afin de vous contacter si le Microsoft Security Response Center (MSRC) découvre que vos données ont été consultées de manière illégale ou par un tiers non autorisé. Vous avez également la possibilité de personnaliser les alertes et les notifications d’incidents dans différents services Azure en fonction de vos besoins en matière de réponse aux incidents. 

- [Comment définir le contact de sécurité d’Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-provide-security-contact-details)

**Supervision d’Azure Security Center** : Oui

**Responsabilité** : Customer

### <a name="ir-3-detection-and-analysis--create-incidents-based-on-high-quality-alerts"></a>IR-3 : Détection et analyse – créer des incidents en fonction d’alertes de haute qualité

**Guide**: Assurez-vous de disposer d’un processus pour créer des alertes de haute qualité et mesurer la qualité des alertes. Cela vous permet de tirer les leçons des incidents passés et de classer par ordre de priorité les alertes pour les analystes, afin qu’ils ne perdent pas de temps sur les faux positifs. 

Les alertes de haute qualité peuvent être générées en fonction de l’expérience des incidents passés, des sources de la communauté validées et des outils conçus pour générer et nettoyer les alertes en fusionnant et en mettant en corrélation diverses sources de signal. 

Azure Security Center fournit des alertes de haute qualité sur de nombreuses ressources Azure. Vous pouvez utiliser le connecteur de données ASC pour diffuser en continu les alertes vers Azure Sentinel. Azure Sentinel vous permet de créer des règles d’alerte avancées pour générer automatiquement des incidents à des fins d’enquête. 

Exportez vos alertes et recommandations Azure Security Center en utilisant la fonctionnalité d’exportation pour identifier les risques pesant sur les ressources Azure. Exportez les alertes et les recommandations manuellement ou automatiquement de manière continue.

- [Procédure de configuration de l’exportation](https://docs.microsoft.com/azure/security-center/continuous-export)

- [Comment envoyer des alertes à Azure Sentinel](https://docs.microsoft.com/azure/sentinel/connect-azure-security-center)

**Supervision d’Azure Security Center** : actuellement non disponible

**Responsabilité** : Customer

### <a name="ir-4-detection-and-analysis--investigate-an-incident"></a>IR-4 : Détection et analyse – enquêter sur un incident

**Guide**: Assurez-vous que les analystes peuvent créer une vue complète de ce qui s’est passé en interrogeant et en utilisant diverses sources de données lors de l’examen d’incidents potentiels. Évitez les spots aveugles en recueillant divers journaux pour suivre les activités d’un pirate potentiel sur la chaîne de destruction. En outre, assurez-vous que les Insights et les apprentissages sont capturés pour d’autres analystes et pour une référence historique future.  

Les sources de données à examiner comprennent les sources de journalisation centralisées qui sont déjà collectées auprès des services et des systèmes en fonctionnement concernés, mais elles peuvent également inclure les éléments suivants :

- Données réseau : utilisez les journaux de flux des groupes de sécurité réseau, Azure Network Watcher et Azure Monitor pour capturer des journaux de flux réseau et d’autres informations analytiques. 

- Captures instantanées des systèmes en fonctionnement : 

    - Utilisez la capacité de capture instantanée de la machine virtuelle Azure pour créer un instantané du disque du système en fonctionnement. 

    - Utilisez la capacité native de sauvegarde de la mémoire du système d’exploitation pour créer un instantané de la mémoire du système en fonctionnement.

    - Utilisez la capacité de capture instantanée des services Azure ou celle de votre logiciel pour créer des instantanés des systèmes en fonctionnement.

Azure Sentinel fournit des analyses de données approfondies sur pratiquement toutes les sources de journal et un portail de gestion des cas pour gérer le cycle de vie complet des incidents. Les renseignements obtenus au cours d’une enquête peuvent être associés à un incident à des fins de suivi et de rapport. 

- [Capture instantanée du disque d’un ordinateur Windows](https://docs.microsoft.com/azure/virtual-machines/windows/snapshot-copy-managed-disk)

- [Capture instantanée du disque d’un ordinateur Linux](https://docs.microsoft.com/azure/virtual-machines/linux/snapshot-copy-managed-disk)

- [Collecte de l’image mémoire et des informations de diagnostic par le support Microsoft Azure](https://azure.microsoft.com/support/legal/support-diagnostic-information-collection/) 

- [Examiner les incidents avec Azure Sentinel](https://docs.microsoft.com/azure/sentinel/tutorial-investigate-cases)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Customer

### <a name="ir-5-detection-and-analysis--prioritize-incidents"></a>IR-5 : Détection et analyse – classer par ordre de priorité les incidents

**Guide**: fournir un contexte aux analystes sur lesquels les incidents doivent se concentrer en premier sur la gravité des alertes et la sensibilité des ressources. 

Azure Security Center attribue un niveau de gravité à chaque alerte pour vous aider à hiérarchiser celles devant être examinées en premier. La gravité dépend du niveau de confiance que Security Center accorde à la recherche ou aux données analytiques utilisées pour émettre l’alerte, mais aussi de l’intention malveillante estimée de l’activité à l’origine de l’alerte.

En outre, marquez les ressources à l’aide d’étiquettes et créez un système de nommage pour identifier et classer les ressources Azure, en particulier celles qui traitent des données sensibles.  Il vous incombe de hiérarchiser le traitement des alertes en fonction de la criticité des ressources et de l’environnement Azure où l’incident s’est produit.

- [Alertes de sécurité dans le Centre de sécurité Azure](https://docs.microsoft.com/azure/security-center/security-center-alerts-overview)

- [Organisation des ressources Azure à l’aide de catégories](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)

**Supervision d’Azure Security Center** : actuellement non disponible

**Responsabilité** : Customer

### <a name="ir-6-containment-eradication-and-recovery--automate-the-incident-handling"></a>IR-6 : Confinement, éradication et récupération – automatiser la gestion des incidents

**Guide**: automatiser les tâches répétitives manuellement pour accélérer le temps de réponse et réduire la charge de travail des analystes. Les tâches manuelles sont plus longues à exécuter, ce qui ralentit chaque incident et réduit le nombre d’incidents qu’un analyste peut traiter. Les tâches manuelles augmentent également la fatigue des analystes, ce qui accroît le risque d’erreur humaine entraînant des retards et dégrade la capacité des analystes à se concentrer efficacement sur des tâches complexes. Utilisez les fonctionnalités d’automatisation des workflows dans Azure Security Center et Azure Sentinel pour déclencher automatiquement des actions ou exécuter un playbook pour répondre aux alertes de sécurité entrantes. Le playbook prend des mesures, telles que l’envoi de notifications, la désactivation de comptes et l’isolement des réseaux problématiques. 

- [Configurer l’automatisation du workflow dans Security Center](https://docs.microsoft.com/azure/security-center/workflow-automation)

- [Configurer des réponses automatisées aux menaces dans Azure Security Center](https://docs.microsoft.com/azure/security-center/tutorial-security-incident#triage-security-alerts)

- [Configurer des réponses automatisées aux menaces dans Azure Sentinel](https://docs.microsoft.com/azure/sentinel/tutorial-respond-threats-playbook)

**Supervision d’Azure Security Center** : actuellement non disponible

**Responsabilité** : Customer

## <a name="posture-and-vulnerability-management"></a>Gestion de la posture et des vulnérabilités

*Pour plus d’informations, consultez [Benchmark de sécurité Azure : Gestion de la posture et des vulnérabilités](/azure/security/benchmarks/security-controls-v2-vulnerability-management).*

### <a name="pv-1-establish-secure-configurations-for-azure-services"></a>PV-1 : Établir des configurations sécurisées pour les services Azure 

**Guide**: Azure information protection peut être configuré par le biais du centre de sécurité et conformité ou via PowerShell. 

Dans le centre de sécurité et de conformité, un administrateur peut créer des étiquettes de sensibilité, définir ce que chaque étiquette peut faire et publier les étiquettes. 

Créez les étiquettes : créez et nommez vos étiquettes de sensibilité en fonction de la taxonomie de classification de votre organisation pour différents niveaux de sensibilité du contenu. Utilisez des noms ou des termes communs qui ont un sens pour vos utilisateurs. Si vous n’avez pas encore de taxonomie établie, pensez à commencer par des noms d’étiquette tels que personnel, public, général, confidentiel et hautement confidentiel. Vous pouvez ensuite utiliser des sous-étiquettes pour regrouper des étiquettes similaires par catégorie. Lorsque vous créez une étiquette, utilisez le texte d’info-bulle pour aider les utilisateurs à sélectionner l’étiquette appropriée.

Définissez ce que chaque étiquette peut faire : configurez les paramètres de protection que vous souhaitez associer à chaque étiquette. Par exemple, vous souhaiterez peut-être appliquer un contenu de sensibilité plus faible (par exemple, une étiquette « général ») à un en-tête ou un pied de page, tandis que le contenu de sensibilité supérieure (par exemple, une étiquette « confidentielle ») doit avoir un filigrane et un chiffrement.

Publier les étiquettes : une fois vos étiquettes de sensibilité configurées, publiez-les à l’aide d’une stratégie d’étiquette. Choisissez les utilisateurs et les groupes qui doivent disposer des étiquettes et des paramètres de stratégie à utiliser. Une seule étiquette est réutilisable : vous la définissez une seule fois, puis vous pouvez l’inclure dans plusieurs stratégies d’étiquette affectées à différents utilisateurs. Par exemple, vous pouvez piloter vos étiquettes de sensibilité en affectant une stratégie d’étiquette à quelques utilisateurs seulement. Ensuite, lorsque vous êtes prêt à déployer les étiquettes au sein de votre organisation, vous pouvez créer une nouvelle stratégie d’étiquette pour vos étiquettes et cette fois, spécifier tous les utilisateurs.

Pour pouvoir utiliser PowerShell, installez le module PowerShell AIPService. Dans PowerShell, un administrateur peut effectuer ces tâches, ainsi que d’autres : 

- Migrer à partir de Rights Management sur site (AD RMS ou Windows RMS) vers Azure Information Protection
- Générer et gérer votre propre clé de locataire : le scénario BYOK (apportez votre propre clé)
- Activer ou désactiver le service Rights Management pour votre organisation
- Configurer des contrôles d’intégration pour un déploiement échelonné du service Azure Rights Management
- Créer et gérer des modèles de Rights Management pour votre organisation
- Gérer les utilisateurs et les groupes qui sont autorisés à administrer Rights Management Service pour votre organisation
- Consigner et analyser l’utilisation de Rights Management

Pour plus d’informations, consultez les références suivantes :

- [Prise en main des étiquettes de sensibilité dans le centre de conformité et de sécurité](https://docs.microsoft.com/microsoft-365/compliance/get-started-with-sensitivity-labels?view=o365-worldwide&amp;preserve-view=true)

- [Créer et publier des étiquettes de sensibilité](https://docs.microsoft.com/microsoft-365/compliance/create-sensitivity-labels?view=o365-worldwide&amp;preserve-view=true)

- [Appliquer le chiffrement aux étiquettes de sensibilité](https://docs.microsoft.com/microsoft-365/compliance/encryption-sensitivity-labels?view=o365-worldwide&amp;preserve-view=true)

- [PowerShell pour Azure Information Protection](https://docs.microsoft.com/azure/information-protection/administer-powershell)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Customer

### <a name="pv-8-conduct-regular-attack-simulation"></a>PV-8 : Effectuer une simulation d’attaque régulière

**Conseils**: si nécessaire, procédez à des tests d’intrusion ou à des activités de l’équipe Red Team sur vos ressources Azure, et assurez la mise à jour de toutes les découvertes de sécurité critiques.
Suivez les règles d’engagement de pénétration du cloud Microsoft pour vous assurer que vos tests d’intrusion sont conformes aux stratégies de Microsoft. Utilisez la stratégie et l’exécution de Red Teaming de Microsoft ainsi que les tests d’intrusion de site actif sur l’infrastructure cloud, les services et les applications gérés par Microsoft.

- [Test d’intrusion dans Azure](https://docs.microsoft.com/azure/security/fundamentals/pen-testing)

- [Règles d’engagement des tests d’intrusion](https://www.microsoft.com/msrc/pentest-rules-of-engagement?rtc=1) 

- [Microsoft Cloud Red Teaming](https://gallery.technet.microsoft.com/Cloud-Red-Teaming-b837392e)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Partagé

## <a name="backup-and-recovery"></a>Sauvegarde et récupération

*Pour plus d’informations, consultez le [test de sécurité Azure : sauvegarde et récupération](/azure/security/benchmarks/security-controls-v2-backup-recovery).*

### <a name="br-4-mitigate-risk-of-lost-keys"></a>BR-4 : Atténuer les risques liés aux clés perdues

**Guide**: Azure information protection permet aux clients de configurer leur locataire avec leur propre clé via Bring Your Own Key (BYOK). Les clés générées par le client doivent être stockées dans Azure Key Vault pour la protection. Azure Key Vault permet d’éviter la perte de clés par le biais de la suppression réversible, de la séparation des rôles et des domaines de sécurité séparés. 

- [Azure Information Protection Bring Your Own Key et intégration à Azure Key Vault](https://docs.microsoft.com/azure/information-protection/byok-price-restrictions)
- [Activer la suppression réversible dans Key Vault](https://docs.microsoft.com/azure/storage/blobs/storage-blob-soft-delete?tabs=azure-portal)

**Supervision d’Azure Security Center** : Oui

**Responsabilité** : Customer

## <a name="governance-and-strategy"></a>Gouvernance et stratégie

*Pour plus d’informations, consultez [Benchmark de sécurité Azure : Gouvernance et stratégie](/azure/security/benchmarks/security-controls-v2-governance-strategy).*

### <a name="gs-1-define-asset-management-and-data-protection-strategy"></a>GS-1 : Définir la stratégie de gestion des ressources et de protection des données 

**Conseils** : Veillez à documenter et à communiquer une stratégie claire pour la surveillance et la protection continues des systèmes et des données. Hiérarchisez la découverte, l’évaluation, la protection et la surveillance des données et systèmes critiques de l’entreprise. 

Cette stratégie doit inclure les recommandations, stratégies et normes documentées pour les éléments suivants : 

-   Norme de classification des données en fonction des risques pour l’entreprise

-   Visibilité de l’organisation de sécurité sur les risques et l’inventaire des actifs 

-   Approbation de l’organisation de sécurité pour les services Azure en vue de leur utilisation 

-   Sécurité des ressources tout au long de leur cycle de vie

-   Stratégie de contrôle d’accès requise conformément à la classification des données organisationnelles

-   Utilisation des fonctionnalités Azure natives et de protection des données tierces

-   Exigences de chiffrement des données pour les cas d’utilisation en transit et au repos

-   Normes de chiffrement appropriées

Pour plus d’informations, consultez les références suivantes :

- [Recommandation d’architecture de sécurité Azure - Stockage, données et chiffrement](https://docs.microsoft.com/azure/architecture/framework/security/storage-data-encryption?toc=/security/compass/toc.json&amp;bc=/security/compass/breadcrumb/toc.json)

- [Notions de base de la sécurité Azure - Sécurité, chiffrement et stockage des données Azure](https://docs.microsoft.com/azure/security/fundamentals/encryption-overview)

- [Cloud Adoption Framework - Meilleures pratiques en matière de chiffrement et de sécurité des données Azure](https://docs.microsoft.com/azure/security/fundamentals/data-encryption-best-practices?toc=/azure/cloud-adoption-framework/toc.json&amp;bc=/azure/cloud-adoption-framework/_bread/toc.json)

- [Benchmark de sécurité Azure - Gestion des ressources](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-asset-management)

- [Benchmark de sécurité Azure - Protection des données](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-data-protection)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Customer

### <a name="gs-2-define-enterprise-segmentation-strategy"></a>GS-2 : Définir la stratégie de segmentation d'entreprise 

**Conseils** : Établissez une stratégie à l'échelle de l'entreprise pour segmenter l'accès aux ressources à l'aide d'une combinaison de contrôles d'identité, de réseau, d'application, d'abonnement, de groupe de gestion et autres.

Trouvez le bon équilibre entre la nécessité de séparation sur le plan de la sécurité et la nécessité d'exécuter quotidiennement les systèmes qui doivent communiquer entre eux et accéder aux données.

Veillez à ce que la stratégie de segmentation soit implémentée de manière cohérente pour tous les types de contrôle, y compris pour les modèles d'identité, d'accès et de sécurité du réseau, les modèles d'autorisation/d'accès aux applications et les contrôles des processus humains.

- [Aide relative à la stratégie de segmentation dans Azure (vidéo)](https://docs.microsoft.com/security/compass/microsoft-security-compass-introduction#azure-components-and-reference-model-2151)

- [Aide relative à la stratégie de segmentation dans Azure (document)](https://docs.microsoft.com/security/compass/governance#enterprise-segmentation-strategy)

- [Aligner la segmentation du réseau avec la stratégie de segmentation d’entreprise](https://docs.microsoft.com/security/compass/network-security-containment#align-network-segmentation-with-enterprise-segmentation-strategy)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Customer

### <a name="gs-3-define-security-posture-management-strategy"></a>GS-3 : Définir la stratégie de gestion de la posture de la sécurité

**Guide**: Mesurez et atténuez en permanence les risques liés à vos ressources individuelles et à l’environnement dans lequel elles sont hébergées. Priorisez les ressources à valeur élevée et les surfaces d’attaque hautement exposées, comme les applications publiées, les points d’entrée et de sortie du réseau, les points de terminaison utilisateur et administrateur, etc.

- [Benchmark de sécurité Azure - Gestion de la posture et des vulnérabilités](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-posture-vulnerability-management)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Customer

### <a name="gs-4-align-organization-roles-responsibilities-and-accountabilities"></a>GS-4 : Aligner les rôles et les responsabilités de l’organisation

**Conseils** : Veillez à documenter et à communiquer une stratégie claire pour les rôles et les responsabilités de votre organisation de sécurité. Veillez à définir clairement les responsabilités pour les décisions relatives à la sécurité, à former tout le monde au modèle de responsabilité partagée et à former les équipes techniques à la technologie permettant de sécuriser le cloud.

- [Meilleures pratiques pour la sécurité Azure 1 – Personnes : Former les équipes pour le parcours vers la sécurité dans le cloud](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#1-people-educate-teams-about-the-cloud-security-journey)

- [Meilleures pratiques pour la sécurité Azure 2 – Personnes : Former les équipes pour les technologies de sécurité dans le cloud](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#2-people-educate-teams-on-cloud-security-technology)

- [Meilleures pratiques pour la sécurité Azure 3 – Processus : Affecter les responsabilités pour les décisions de sécurité dans le cloud](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#4-process-update-incident-response-ir-processes-for-cloud)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Customer

### <a name="gs-5-define-network-security-strategy"></a>GS-5 : Définir la stratégie de sécurité réseau

**Conseils** : Établissez une approche de sécurité réseau Azure dans le cadre de la stratégie de contrôle d’accès de sécurité globale de votre organisation.  

Cette stratégie doit inclure les recommandations, stratégies et normes documentées pour les éléments suivants : 

-   Responsabilité centralisée pour la gestion et la sécurité du réseau

-   Modèle de segmentation de réseau virtuel aligné avec la stratégie de segmentation de l’entreprise

-   Stratégie de correction dans différents scénarios de menaces et d’attaques

-   Stratégie de périphérie d’Internet et d’entrée et de sortie

-   Stratégie de cloud hybride et d’interconnexion locale

-   Artefacts de sécurité réseau à jour (par exemple diagrammes réseau, architecture de réseau de référence)

Pour plus d’informations, consultez les références suivantes :
- [Meilleures pratiques pour la sécurité Azure 11 – Architecture. Stratégie de sécurité unifiée unique](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#11-architecture-establish-a-single-unified-security-strategy)

- [Benchmark de sécurité Azure – Sécurité réseau](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-network-security)

- [Vue d’ensemble de la sécurité réseau d’Azure](https://docs.microsoft.com/azure/security/fundamentals/network-overview)

- [Stratégie d’architecture de réseau d’entreprise](https://docs.microsoft.com/azure/cloud-adoption-framework/ready/enterprise-scale/architecture)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Customer

### <a name="gs-6-define-identity-and-privileged-access-strategy"></a>GS-6 : Définir une stratégie d’accès privilégié et d’identité

**Guide**: établissez une approche d’identité et d’accès privilégié Azure dans le cadre de la stratégie de contrôle d’accès de sécurité globale de votre organisation.  

Cette stratégie doit inclure les recommandations, stratégies et normes documentées pour les éléments suivants : 

-   Un système centralisé d’identité et d’authentification et son interconnexion avec d’autres systèmes d’identité internes et externes

-   Méthodes d’authentification fortes dans différents cas d’usage et différentes conditions

-   Protection des utilisateurs disposant de privilèges élevés

-   Surveillance et gestion des activités anormales des utilisateurs  

-   Vérification de l’identité et de l’accès des utilisateurs et processus de rapprochement

Pour plus d’informations, consultez les références suivantes :

- [Benchmark de sécurité Azure - Gestion des identités](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-identity-management)

- [Benchmark de sécurité Azure - Accès privilégié](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-privileged-access)

- [Meilleures pratiques pour la sécurité Azure 11 – Architecture. Stratégie de sécurité unifiée unique](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#11-architecture-establish-a-single-unified-security-strategy)

- [Vue d’ensemble de la sécurité et de la gestion des identités Azure](https://docs.microsoft.com/azure/security/fundamentals/identity-management-overview)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Customer

### <a name="gs-7-define-logging-and-threat-response-strategy"></a>GS-7 : Définir la stratégie de journalisation et de réponse aux menaces

**Conseils** : Établissez une stratégie de journalisation et de réponse aux menaces pour détecter et corriger rapidement les menaces tout en répondant aux exigences de conformité. Hiérarchisez les analystes en fournissant des alertes de haute qualité et des expériences homogènes afin qu’ils puissent se concentrer sur les menaces plutôt que sur l’intégration et les étapes manuelles. 

Cette stratégie doit inclure les recommandations, stratégies et normes documentées pour les éléments suivants : 

-   Rôle et responsabilités de l’organisation d’opérations de sécurité (SecOP) 

-   Un processus de réponse aux incidents bien défini, aligné avec NIST ou autre cadre réglementaire du secteur 

-   Capture et rétention des journaux pour prendre en charge la détection des menaces, la réponse aux incidents et les besoins de conformité

-   Visibilité centralisée des informations de corrélation sur les menaces, avec SIEM, les fonctionnalités Azure natives et d’autres sources 

-   Plan de communication et de notification avec vos clients, fournisseurs et les parties publiques pertinentes

-   Utilisation de plateformes Azure natives et tierces pour la gestion des incidents, comme la journalisation et la détection des menaces, les investigations et la correction et l’éradication des attaques

-   Processus de gestion des incidents et des activités postérieures aux incidents, comme les leçons apprises et la rétention des preuves

Pour plus d’informations, consultez les références suivantes :

- [Benchmark de sécurité Azure - Journalisation et détection des menaces](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-logging-threat-detection)

- [Benchmark de sécurité Azure - Réponse aux incidents](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-incident-response)

- [Meilleures pratiques pour la sécurité Azure 4 - Processus. Mise à jour des processus de réponse aux incidents pour le cloud](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#4-process-update-incident-response-ir-processes-for-cloud)

- [Guide pour le cadre d’adoption d’Azure, la journalisation et la prise de décision pour les rapports](https://docs.microsoft.com/azure/cloud-adoption-framework/decision-guides/logging-and-reporting/)

- [Mise à l’échelle, gestion et surveillance d’entreprise Azure](https://docs.microsoft.com/azure/cloud-adoption-framework/ready/enterprise-scale/management-and-monitoring)

**Supervision d’Azure Security Center** : Non applicable

**Responsabilité** : Customer

## <a name="next-steps"></a>Étapes suivantes

- Consultez [Vue d’ensemble d’Azure Security Benchmark V2](/azure/security/benchmarks/overview)
- En savoir plus sur les [bases de référence de la sécurité Azure](/azure/security/benchmarks/security-baselines-overview)
