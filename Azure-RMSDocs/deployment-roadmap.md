---
title: Feuille de route pour le déploiement d’Azure Information Protection
description: Utilisez ces étapes pour préparer, implémenter et gérer Azure Information Protection pour votre organisation.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/28/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 7f688b53f56254be52668d25b63e03734dde71de
ms.sourcegitcommit: f14ec329cef1967d2d66b0d550501449ee55abf9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/29/2019
ms.locfileid: "71673832"
---
# <a name="azure-information-protection-deployment-roadmap"></a>Feuille de route pour le déploiement d’Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Utilisez les étapes suivantes comme des recommandations visant à faciliter la préparation, l’implémentation et la gestion d’Azure Information Protection pour votre organisation.

Vous pouvez également 

- Vous recherchez des instructions basées sur des scénarios pour Azure Information Protection ? Consultez [les guides de procédures pour les scénarios courants qui utilisent Azure information protection](how-to-guides.md).

- Vous recherchez la feuille de route Azure Information Protection Release ? Consultez [les informations sur les nouvelles versions et les mises à jour](information-support.md#information-about-new-releases-and-updates).

### <a name="identify-your-deployment-roadmap"></a>Identifier la feuille de route de votre déploiement

Avant d’implémenter une des étapes ci-dessous pour déployer Azure Information Protection, prenez le temps de consulter [Conditions requises pour Azure Information Protection](./requirements.md).

Choisissez ensuite la feuille de route de déploiement qui s’applique à votre organisation et qui correspond aux [fonctionnalités de l’abonnement](https://azure.microsoft.com/pricing/details/information-protection/) dont vous avez besoin :

- [Utiliser la classification, l’étiquetage et la protection](#deployment-roadmap-for-classification-labeling-and-protection)
    
    Le chemin d’accès recommandé lorsque vous avez un abonnement de prise en charge, car les fonctionnalités supplémentaires prennent en charge la découverte d’informations sensibles et l’étiquetage des documents et des e-mails pour la classification. Les étiquettes peuvent également appliquer une protection, en faisant abstraction de cette complexité par rapport aux utilisateurs.
    
    Les étapes de déploiement sont adaptées à Azure Information Protection étiquettes et à des étiquettes de sensibilité qui utilisent la [plateforme d’étiquetage unifiée](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform).

- [Utiliser la protection des données uniquement](#deployment-roadmap-for-data-protection-only)
    
    Chemin d’accès à utiliser lorsque vous n’avez pas d’abonnement prenant en charge la classification et les étiquettes, mais qui prend en charge la protection sans étiquette.

## <a name="deployment-roadmap-for-classification-labeling-and-protection"></a>Feuille de route de déploiement pour la classification, l’étiquetage et la protection

> [!NOTE]
> Vous utilisez déjà la fonctionnalité de protection d’Azure Information Protection ? Vous pouvez ignorer la plupart de ces étapes et vous concentrer sur les étapes 3 et 5.1.

### <a name="step-1-confirm-your-subscription-and-assign-user-licenses"></a>Étape 1 : Vérifier votre abonnement et attribuer des licences utilisateur
Examinez les informations sur les abonnements et la liste des fonctionnalités de la page [Tarification Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) pour vérifier que votre organisation dispose d’un abonnement incluant les fonctionnalités attendues. Ensuite, attribuez des licences à partir de cet abonnement à chaque utilisateur de votre organisation susceptible de classifier, d’étiqueter et de protéger des documents et des e-mails.

Remarque : N’attribuez pas manuellement des licences utilisateur à partir de l’abonnement gratuit RMS for individuals et n’utilisez pas cette licence pour administrer le service Azure Rights Management dans votre organisation. Ces licences apparaissent sous la forme **Rights Management Adhoc** dans le Centre d’administration Microsoft 365 et **RIGHTSMANAGEMENT_ADHOC** quand vous exécutez l’applet de commande PowerShell Azure AD [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx). Pour plus d’informations sur la façon dont l’abonnement RMS for individuals est automatiquement accordé et attribué aux utilisateurs, consultez [RMS for individuals et Protection des informations Azure](./rms-for-individuals.md).

### <a name="step-2-prepare-your-tenant-to-use-azure-information-protection"></a>Étape 2 : Préparer votre locataire à l’utilisation d’Azure Information Protection

Avant de commencer à utiliser Azure Information Protection, vérifiez que vous avez dans Office 365 ou Azure Active Directory des comptes et des groupes d’utilisateurs. Azure Information Protection les utilisera pour authentifier et autoriser les utilisateurs de votre organisation. Si nécessaire, créez ces comptes et groupes, ou synchroniser-les à partir de votre répertoire local. 

Pour plus d’informations, consultez [Préparation des utilisateurs et groupes pour Azure Information Protection](prepare.md).

### <a name="step-3-configure-and-deploy-classification-and-labeling"></a>Étape 3 : Configurer et déployer la classification et l’étiquetage

Avant de configurer des étiquettes et des paramètres de stratégie, choisissez le client Azure Information Protection que vous allez utiliser : Le client classique ou le client d’étiquetage unifié. Ou vous pouvez avoir besoin des deux clients. Cette décision du client est désormais nécessaire pour vous permettre de connaître le portail de gestion à utiliser pour configurer les étiquettes et les paramètres de stratégie. Pour plus d’informations et pour vous aider dans cette décision, consultez [choisir le client Azure information protection à utiliser](./rms-client/use-client.md#choose-which-azure-information-protection-client-to-use).

> [!TIP]
> **Facultatif mais recommandé** : Envisagez d’utiliser le [démarrage rapide du scanneur](quickstart-findsensitiveinfo.md) pour découvrir les informations sensibles que vous avez sur vos banques de données locales. Les informations trouvées par le scanneur peuvent vous aider dans votre taxonomie de classification ainsi que fournir de précieuses informations sur les étiquettes dont vous avez besoin et les fichiers à protéger.
> 
> Étant donné que le mode de détection de l’analyseur n’exige pas que vous configuriez des étiquettes ou que votre taxonomie de classification soit définie, l’exécution du scanneur de cette manière est adaptée à cette phase très précoce de votre déploiement. Vous pouvez également utiliser cette configuration du scanneur en parallèle avec les étapes de déploiement suivantes, jusqu’à ce que vous configuriez l’étiquetage automatique ou recommandé.

Si vous n’avez pas encore de stratégie de classification, passez en revue la [stratégie de Azure information protection par défaut](./configure-policy-default.md) et utilisez-la comme base pour déterminer les étiquettes de classification à affecter aux données de votre organisation. Vous pouvez les personnaliser en fonction des besoins de votre entreprise.

Reconfigurez vos étiquettes pour apporter les modifications nécessaires pour prendre en charge vos décisions de classification. Configurez la stratégie d’étiquetage manuel par les utilisateurs et écrivez un guide de l’utilisateur qui explique quelle étiquette appliquer et à quel moment. Si votre stratégie par défaut a été créée avec des étiquettes qui appliquent automatiquement la protection, supprimez temporairement les paramètres de protection ou désactivez l’étiquette. Pour plus d’informations sur la configuration des étiquettes et des paramètres de stratégie, consultez la documentation suivante :

- Étiquettes de Azure Information Protection pour le client classique : [Configuration de la stratégie Azure Information Protection](./configure-policy.md)

- Étiquettes de sensibilité pour le client d’étiquetage unifié : [Vue d’ensemble des étiquettes de sensibilité](https://docs.microsoft.com/en-us/microsoft-365/compliance/sensitivity-labels)

Déployez ensuite le client Azure Information Protection (Classic) ou le client d’étiquetage unifié Azure Information Protection pour les utilisateurs. Fournissez une formation utilisateur et des instructions spécifiques pour sélectionner les étiquettes. Pour plus d’informations sur l’installation et la prise en charge des clients, consultez les guides d’administration :

- [Client Azure Information Protection - Guide de l’administrateur](./rms-client/client-admin-guide.md)

- [Guide de l’administrateur du client d’étiquetage unifié Azure Information Protection](./rms-client/clientv2-admin-guide.md)

Après un certain temps, quand les utilisateurs sont à l’aise avec l’étiquetage de leurs documents et e-mails, introduisez des configurations plus avancées. Celles-ci peuvent être les suivantes :

- Appliquer une étiquette par défaut

- Inviter les utilisateurs à fournir une justification s’ils choisissent une étiquette avec un faible niveau de classification ou supprimer une étiquette

- Imposer que tous les documents et e-mails aient une étiquette

- Personnaliser les en-têtes, pieds de page ou filigranes

- Étiquetage automatique et recommandé

À ce stade, ne sélectionnez pas l’option qui permet de protéger les documents et les e-mails. Toutefois, une fois que vous avez configuré des étiquettes pour un étiquetage automatique, exécutez le [scanneur Azure Information Protection](deploy-aip-scanner.md) dans vos banques de données locales en mode découverte et pour correspondre à votre stratégie. L’exécution du scanneur avec cette configuration vous indique les étiquettes qui doivent être appliquées aux fichiers. Ces informations vous aident à optimiser votre configuration d’étiquettes et vous préparent pour la classification et la protection des fichiers en bloc. 

### <a name="step-4-prepare-for-data-protection"></a>Étape 4 : Préparer la protection des données

Quand les utilisateurs sont à l’aise avec l’étiquetage des documents et des e-mails, vous pouvez introduire la protection des données pour vos données les plus sensibles. Cette étape nécessite la préparation suivante :

1. Déterminez si vous voulez que Microsoft gère votre clé de locataire (option par défaut) ou si vous voulez la générer et la gérer vous-même (option BYOK, Bring Your Own Key). Pour plus d’informations, consultez [Planning and implementing your Azure Information Protection tenant key](plan-implement-tenant-key.md) (Planification et implémentation de la clé de locataire Azure Information Protection).

2. Installez le module PowerShell pour AIPService sur au moins un ordinateur qui a accès à Internet. Vous pouvez effectuer cette étape maintenant ou ultérieurement. Pour plus d’informations, consultez [installation du module PowerShell AIPService](./install-powershell.md).

3. Si vous utilisez actuellement AD RMS : Effectuez une migration pour déplacer les clés, les modèles et les URL vers le Cloud. Pour plus d’informations, consultez [Migration d’AD RMS vers Information Protection](migrate-from-ad-rms-to-azure-rms.md).

4. Vérifiez que le service de protection est activé pour pouvoir commencer à protéger des documents et des e-mails. Si un déploiement échelonné est nécessaire, configurez les contrôles d’intégration pour limiter la capacité des utilisateurs à appliquer la protection. Pour plus d’informations, consultez [Activation du service de protection à partir d’Azure Information Protection](./activate-service.md).

Configurez éventuellement les éléments suivants :

- La journalisation de l’utilisation pour pouvoir surveiller l’usage que fait votre organisation du service de protection. Vous pouvez effectuer cette étape maintenant ou ultérieurement. Pour plus d’informations, consultez [journalisation et analyse de l’utilisation de la protection à partir de Azure information protection](./log-analyze-usage.md).

### <a name="step-5-configure-labels-and-settings-applications-and-services-for-data-protection"></a>Étape 5 : Configurer des étiquettes et des paramètres, des applications et des services pour la protection des données

1. Mettre à jour vos étiquettes pour appliquer la protection
    
    Pour le client Azure Information Protection (classique), consultez [Comment configurer une étiquette pour la protection de Rights Management](./configure-policy-protection.md).
    
    Pour le client d’étiquetage unifié Azure Information Protection, consultez [restreindre l’accès au contenu à l’aide du chiffrement dans les étiquettes de sensibilité](https://docs.microsoft.com/Office365/SecurityCompliance/encryption-sensitivity-labels).
    
    Notez que les utilisateurs peuvent appliquer des étiquettes dans Outlook qui appliquent la protection Rights Management, même si Exchange n’est pas configuré pour la gestion des droits relatifs à l'information (IRM). Cependant, tant qu’Exchange n’est pas configuré pour IRM ou pour le [chiffrement de messages Office 365 avec de nouvelles fonctionnalités](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e), votre organisation ne peut pas bénéficier des fonctionnalités complètes de la protection Azure Rights Management avec Exchange. Cette configuration supplémentaire est incluse dans la liste suivante (l’étape 2 pour Exchange Online et l’étape 5 pour Exchange sur site). 

2. Configurer des applications et des services Office
    
    Configurez des applications et services Office pour les fonctionnalités de gestion des droits relatifs à l’information (IRM) dans SharePoint Online ou Exchange Online. Pour plus d’informations, consultez [Configuration d’applications pour Azure Rights Management](configure-applications.md).

3. Configurez la fonctionnalité de super utilisateur pour la récupération de données.
    
    Si vous avez des services informatiques, tels que des solutions de protection contre la perte de données (DLP), des passerelles de chiffrement de contenu (CEG) et d’autres logiciels anti-programme malveillant, qui sont chargés d’inspecter les fichiers qu’Azure Information Protection doit protéger, configurez les comptes de service en tant que super utilisateurs pour Azure Rights Management. Pour plus d’informations, consultez [configuration de super utilisateurs pour les Azure information protection et les services de découverte ou la récupération de données](./configure-super-users.md).

4. Classifier et protéger les fichiers existants en bloc
    
    Pour vos banques de données locales, exécutez maintenant le [scanneur Azure Information Protection](deploy-aip-scanner.md) en mode de mise en conformité afin que les fichiers soient automatiquement étiquetés. Pour les banques de données basées sur le cloud, utilisez [Azure Cloud App Security](https://docs.microsoft.com/cloud-app-security).
    
    Pour les fichiers sur les PC, vous pouvez utiliser les applets de commande PowerShell pour classifier et protéger des fichiers. Pour plus d’informations, consultez les guides d’administration suivants :
    
    - Client Azure Information Protection (classique) : [Utilisation de PowerShell avec le client Azure Information Protection](./rms-client/client-admin-guide-powershell.md)
    
    - Client d’étiquetage unifié Azure Information Protection : [Utilisation de PowerShell avec le client d’étiquetage unifié Azure Information Protection](./rms-client/clientv2-admin-guide-powershell.md)

6. Déployez le connecteur pour les bibliothèques protégées par IRM sur SharePoint Server et les e-mails protégés par IRM pour Exchange sur site
    
    Si vous avez SharePoint et Exchange sur site, et souhaitez utiliser leurs fonctionnalités de gestion des droits relatifs à l’information (IRM), installez et configurez le connecteur Rights Management. Pour plus d’informations, consultez [Déploiement du connecteur Azure Rights Management](./deploy-rms-connector.md).

### <a name="step-6-use-and-monitor-your-data-protection-solutions"></a>Étape 6 : Utiliser et superviser vos solutions de protection des données
Vous êtes maintenant prêt à superviser la façon dont votre organisation utilise les étiquettes que vous avez configurées et à confirmer que vous protégez des informations sensibles. Pour plus d’informations sur la prise en charge de cette phase de déploiement, consultez les éléments suivants :

- [Rapports centraux pour Azure information protection](reports-aip.md) actuellement en version préliminaire

- [Journalisation de l’utilisation locale avec l’analyseur d’événements Windows](./rms-client/client-admin-guide-files-and-logging.md#usage-logging-for-the-azure-information-protection-client) pour le client Azure information protection (Classic)

- [Journalisation et analyse de l’utilisation de la protection à partir de Azure Information Protection](./log-analyze-usage.md)

### <a name="step-7-administer-the-protection-service-for-your-tenant-account-as-needed"></a>Étape 7 : Administrer le service de protection pour votre compte de locataire selon les besoins

Quand vous commencez à utiliser le service de protection, PowerShell peut s’avérer utile pour automatiser les changements administratifs ou générer des scripts sur ces changements. PowerShell peut également être nécessaire pour certaines configurations avancées. 

Pour plus d’informations, consultez [administration de la protection à partir de Azure information protection à l’aide de PowerShell](./administer-powershell.md).


## <a name="deployment-roadmap-for-data-protection-only"></a>Feuille de route de déploiement pour la protection des données uniquement

### <a name="step-1-confirm-that-you-have-a-subscription-that-includes-the-protection-service-from-azure-information-protection"></a>Étape 1 : Confirmer que vous avez un abonnement qui inclut le service de protection d’Azure Information Protection

Examinez les informations sur les abonnements et la liste des fonctionnalités de la page [Tarification Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) pour vérifier que votre organisation dispose d’un abonnement incluant les fonctionnalités attendues. Ensuite, attribuez une licence à partir de cet abonnement à chaque utilisateur de votre organisation susceptible de protéger des documents et des e-mails.

Remarque : N’attribuez pas manuellement des licences utilisateur à partir de l’abonnement gratuit RMS for individuals et n’utilisez pas cette licence pour administrer le service Azure Rights Management dans votre organisation. Ces licences apparaissent sous la forme **Rights Management Adhoc** dans le Centre d’administration Microsoft 365 et **RIGHTSMANAGEMENT_ADHOC** quand vous exécutez l’applet de commande PowerShell Azure AD [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx). Pour plus d’informations sur la façon dont l’abonnement RMS for individuals est automatiquement accordé et attribué aux utilisateurs, consultez [RMS for individuals et Protection des informations Azure](./rms-for-individuals.md).


### <a name="step-2-prepare-your-tenant-to-use-azure-information-protection"></a>Étape 2 : Préparer votre locataire à l’utilisation d’Azure Information Protection

Avant de commencer à utiliser le service de protection d’Azure Information Protection, effectuez la préparation suivante :

1. Vérifiez que votre locataire Office 365 contient les comptes et groupes d’utilisateurs qu’Azure Information Protection utilisera pour authentifier et autoriser les utilisateurs de votre organisation. Si nécessaire, créez ces comptes et groupes, ou synchroniser-les à partir de votre répertoire local. Pour plus d’informations, consultez [Préparation des utilisateurs et groupes pour Azure Information Protection](prepare.md).

2. Déterminez si vous voulez que Microsoft gère votre clé de locataire (option par défaut) ou si vous voulez la générer et la gérer vous-même (option BYOK, Bring Your Own Key). Pour plus d’informations, consultez [Planning and implementing your Azure Information Protection tenant key](plan-implement-tenant-key.md) (Planification et implémentation de la clé de locataire Azure Information Protection).

3. Installez le module PowerShell pour AIPService sur au moins un ordinateur qui a accès à Internet. Vous pouvez effectuer cette étape maintenant ou ultérieurement. Pour plus d’informations, consultez [installation du module PowerShell AIPService](./install-powershell.md).

4. Si vous utilisez actuellement AD RMS : Effectuez une migration pour déplacer les clés, les modèles et les URL vers le Cloud. Pour plus d’informations, consultez [Migration d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

5. Vérifiez que le service de protection est activé pour pouvoir commencer à protéger des documents et des e-mails. Si un déploiement échelonné est nécessaire, configurez les contrôles d’intégration pour limiter la capacité des utilisateurs à appliquer la protection. Pour plus d’informations, consultez [Activation du service de protection à partir d’Azure Information Protection](./activate-service.md).

Configurez éventuellement les éléments suivants :

- Des modèles personnalisés pour des paramètres de protection si les modèles par défaut ne suffisent pas à votre organisation. Vous pouvez effectuer cette étape maintenant ou ultérieurement. Pour plus d’informations, consultez [Configuration et gestion des modèles pour Azure Information Protection](./configure-policy-templates.md).

- La journalisation de l’utilisation pour pouvoir surveiller l’usage que fait votre organisation du service de protection. Vous pouvez effectuer cette étape maintenant ou ultérieurement. Pour plus d’informations, consultez [journalisation et analyse de l’utilisation de la protection à partir de Azure information protection](./log-analyze-usage.md).

### <a name="step-3-install-the-azure-information-protection-client-classic-and-configure-applications-and-services-for-rights-management"></a>Étape 3 : Installez le client Azure Information Protection (Classic) et configurez les applications et les services pour Rights Management

1. Déployer le client Azure Information Protection (Classic)
    
    Installez le client Classic pour que les utilisateurs prennent en charge Office 2010, afin de protéger les fichiers autres que les documents Office et les e-mails, et d’effectuer le suivi des documents protégés. Formez les utilisateurs à ce client. Pour plus d’informations, consultez [Client Azure Information Protection pour Windows](./rms-client/aip-client.md).

2. Configurer des applications et des services Office
    
    Configurez des applications et services Office pour les fonctionnalités de gestion des droits relatifs à l’information (IRM) dans SharePoint Online ou Exchange Online. Pour plus d’informations, consultez [Configuration d’applications pour Azure Rights Management](./configure-applications.md).

3. Configurez la fonctionnalité de super utilisateur pour la récupération de données.
    
    Si vous avez des services informatiques, tels que des solutions de protection contre la perte de données (DLP), des passerelles de chiffrement de contenu (CEG) et d’autres logiciels anti-programme malveillant, qui sont chargés d’inspecter les fichiers qu’Azure Information Protection doit protéger, configurez les comptes de service en tant que super utilisateurs pour Azure Rights Management. Pour plus d’informations, consultez [configuration de super utilisateurs pour les Azure information protection et les services de découverte ou la récupération de données](./configure-super-users.md).

4. Protéger les fichiers existants en bloc 
    
    Vous pouvez utiliser les applets de commande PowerShell pour protéger en bloc plusieurs types de fichiers ou annuler cette protection en bloc. Pour plus d’informations, consultez [Utilisation de PowerShell avec le client Azure Information Protection](./rms-client/client-admin-guide-powershell.md) dans le Guide de l’administrateur.
    
    Pour les fichiers sur les serveurs de fichiers Windows, vous pouvez utiliser ces applets de commande avec un script et l’infrastructure de classification des fichiers de Windows Server. Pour plus d’informations, consultez [Protection RMS avec l’infrastructure de classification des fichiers (ICF) de Windows Server](./rms-client/configure-fci.md).

5. Déployez le connecteur pour les serveurs locaux.
    
    Si vous voulez utiliser des services locaux avec le service de protection, installez et configurez le connecteur Microsoft Rights Management. Pour plus d’informations, consultez [Déploiement du connecteur Azure Rights Management](./deploy-rms-connector.md).

### <a name="step-4-use-and-monitor-your-data-protection-solutions"></a>Étape 4 : Utiliser et superviser vos solutions de protection des données

Vous êtes maintenant prêt à protéger vos données, ainsi qu’à journaliser la manière dont votre entreprise utilise le service de protection. Pour plus d’informations sur la prise en charge de cette phase de déploiement, consultez [aider les utilisateurs à protéger des fichiers à l’aide du service Azure Rights Management](./help-users.md) et [journalisation et analyse de l’utilisation de la protection à partir de Azure information protection](./log-analyze-usage.md).

### <a name="step-5-administer-the-protection-service-for-your-tenant-account-as-needed"></a>Étape 5 : Administrer le service de protection pour votre compte de locataire selon les besoins

Quand vous commencez à utiliser le service de protection, PowerShell peut s’avérer utile pour automatiser les changements administratifs ou générer des scripts sur ces changements. PowerShell peut également être nécessaire pour certaines configurations avancées. 

Pour plus d’informations, consultez [administration de la protection à partir de Azure information protection à l’aide de PowerShell](./administer-powershell.md).

## <a name="next-steps"></a>Étapes suivantes

Lorsque vous déployez Azure Information Protection, il peut s’avérer utile de consulter les [questions fréquemment posées](faqs.md), ainsi que la page [informations et support](information-support.md) pour obtenir des ressources supplémentaires.