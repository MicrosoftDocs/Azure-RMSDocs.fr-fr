---
title: "FAQ relatives à Azure Information Protection"
description: "Certaines questions fréquentes sur Azure Information Protection et son service de protection des données, Azure Rights Management (Azure RMS)."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/07/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 71ce491f-41c1-4d15-9646-455a6eaa157d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: b27a4b536e135526bb7e1b4236e88b85b6ea84b1
ms.sourcegitcommit: 7b773ca5bf1abf30e527c34717ecb2dc96f88033
translationtype: HT
---
# <a name="frequently-asked-questions-for-azure-information-protection"></a>Forum aux questions sur Azure Information Protection

>*S’applique à : Azure Information Protection, Office 365*

Vous avez une question sur Azure Information Protection ou sur le service Azure Rights Management (Azure RMS) ? Vous trouverez peut-être une réponse ici.

Ces pages de FAQ seront régulièrement actualisées. Les nouveautés seront répertoriées dans les avis de mise à jour mensuels de la documentation, dans [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection,azure-rights-management-services) (Blog de sécurité et de mobilité d’entreprise).

## <a name="whats-the-difference-between-azure-information-protection-and-azure-rights-management"></a>Quelle est la différence entre Information Protection et Azure Rights Management ?

Azure Information Protection permet à une organisation de classifier, d’étiqueter et de protéger ses documents et e-mails. La technologie de protection utilise le service Azure Rights Management, désormais un composant d’Azure Information Protection.

## <a name="what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included"></a>De quel abonnement ai-je besoin pour Azure Information Protection et quelles sont les fonctionnalités incluses ?
Consultez les [informations sur les abonnements](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing) et la [liste des fonctionnalités](https://www.microsoft.com/cloud-platform/azure-information-protection-features) sur le site Azure Information Protection. 

Si vous avez un abonnement Office 365 incluant Rights Management, téléchargez la [feuille de données des licences Azure Information Protection](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf) à partir de la page **Fonctionnalités**.

## <a name="is-the-azure-information-protection-client-only-for-subscriptions-that-include-classification-and-labeling"></a>Le client Azure Information Protection est-il réservé aux abonnements qui comprennent la classification et l’étiquetage ?

Non. Bien que la plupart des présentations et démonstrations du client Azure Information Protection que vous avez vues montrent comment il prend en charge la classification et l’étiquetage, il peut également servir avec les abonnements incluant simplement le service Azure Rights Management pour la protection des données.

Lorsque le client Azure Information Protection pour Windows est installé et qu’il n’a pas de stratégie Azure Information Protection, le client fonctionne automatiquement en [mode protection seule](../rms-client/client-protection-only-mode.md). Dans ce mode, les utilisateurs peuvent facilement appliquer des modèles Rights Management et des autorisations personnalisées. Si vous décidez, plus tard, de souscrire un abonnement qui n’inclut ni la classification ni l’étiquetage, le client passe automatiquement en mode standard lors du téléchargement de la stratégie Azure Information Protection.

Si vous utilisez actuellement l’application de partage Rights Management pour Windows, nous vous conseillons de la remplacer par le client Azure Information Protection. La prise en charge de l’application de partage prendra fin le 31 janvier 2018. Pour vous aider à effectuer la transition, consultez la section [Tâches que vous aviez l’habitude d’effectuer avec l’application de partage RMS](../rms-client/upgrade-client-app.md).

## <a name="does-azure-information-protection-support-on-premises-and-hybrid-scenarios"></a>La solution Azure Information Protection prend-elle en charge les scénarios sur site et hybrides ?

Oui. Bien qu’Azure Information Protection soit une solution basée sur le cloud, elle peut classer, étiqueter et protéger des documents et des e-mails stockés sur site, ainsi que dans le cloud.

Si vous possédez des serveurs de fichiers Windows, Exchange Server et SharePoint Server, vous pouvez déployer le [connecteur Rights Management](../deploy-use/deploy-rms-connector.md) afin de permettre à ces serveurs locaux d’utiliser le service Azure Rights Management pour protéger vos messages e-mails et documents. Vous pouvez également synchroniser et fédérer vos contrôleurs de domaine Active Directory avec Azure AD pour une expérience d'authentification plus agréable pour les utilisateurs, par exemple, en utilisant [Azure AD Connect](http://azure.microsoft.com/documentation/articles/active-directory-aadconnect/).

Le service Azure Rights Management génère et gère automatiquement les certificats XrML de façon appropriée. Il n’utilise donc pas d’infrastructure à clé publique (PKI) locale. Pour plus d’informations sur la façon dont Azure Rights Management utilise les certificats, consultez la section [Procédure pas à pas décrivant le fonctionnement d’Azure RMS : première utilisation, protection du contenu, consommation du contenu](../understand-explore/how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption) dans l’article [Fonctionnement d’Azure RMS](../understand-explore/how-does-it-work.md).

## <a name="ive-heard-a-new-release-is-going-to-be-available-soon-for-azure-information-protectionwhen-will-it-be-released"></a>J’ai entendu dire qu’une nouvelle version sera disponible prochainement pour Azure Information Protection : quand sera-t-elle publiée ?

La documentation technique ne contient pas d’informations sur les versions à venir. Pour ce type d’informations et pour les annonces de version, consultez [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection,azure-rights-management-services) (Blog de sécurité et de mobilité d’entreprise) et récupérez les dernières mises à jour auprès de [Dan Plastina @TheRMSGuy](https://twitter.com/TheRMSGuy) sur Twitter. Si vous êtes intéressé par une version d’Office, consultez également le [blog Office](https://blogs.office.com/).

## <a name="where-can-i-find-supporting-information-for-azure-information-protectionsuch-as-legal-compliance-and-slas"></a>Où puis-je trouver des informations annexes sur Azure Information Protection (considérations juridiques, conformité, contrats de niveau de service, etc.) ?

Consultez [Conformité et informations annexes pour Azure Information Protection](../understand-explore/compliance.md).

## <a name="how-can-i-report-a-problem-or-send-feedback-for-azure-information-protection"></a>Comment puis-je signaler un problème ou envoyer des commentaires pour Azure Information Protection ?

Pour le support technique, utilisez vos canaux de support standard ou [contactez le support technique Microsoft](information-support.md#to-contact-microsoft-support).

Pour envoyer des commentaires, notamment des suggestions d’améliorations ou de nouvelles fonctionnalités : dans votre application Office, sous l’onglet **Accueil**, dans le groupe **Protection**, cliquez sur **Protéger**, puis sur **Aide et commentaires**. Dans la boîte de dialogue **Microsoft Azure Information Protection**, cliquez sur **Envoyez-nous des commentaires**. Un e-mail à envoyer à l’équipe Information Protection s’ouvre. Nous vous invitons également à contacter l’équipe d’ingénieurs sur son [site Yammer Azure Information Protection](https://www.yammer.com/askipteam/). 

## <a name="what-do-i-do-if-my-question-isnt-here"></a>Que puis-je faire si ma question ne figure pas dans cette rubrique ?

Tout d’abord, passez en revue les questions fréquentes qui sont spécifiques à la classification et à l’étiquetage ou spécifiques à la protection des données. Le service Azure Rights Management (Azure RMS) fournit la technologie de protection des données pour Azure Information Protection, et Azure RMS peut être utilisé avec ou sans la classification et l’étiquetage : 

- [Forum aux questions sur la classification et l’étiquetage](faqs-infoprotect.md)

- [Forum aux questions sur la protection des données](faqs-rms.md)

Si votre question ne fait pas l’objet d’une réponse, utilisez les liens et les ressources figurant dans [Informations et support technique pour Azure Rights Management](information-support.md).

En outre, il existe des FAQ conçus pour les utilisateurs finaux :

- [FAQ relatif à l’application Azure Information Protection pour iOS et Android](../rms-client/mobile-app-faq.md)

- [FAQ relatif à l’application de partage RMS pour les ordinateurs Mac et Windows Phone](https://technet.microsoft.com/dn451248)

- [FAQ concernant l’application de partage Rights Management pour Windows](https://technet.microsoft.com/dn467883)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]

