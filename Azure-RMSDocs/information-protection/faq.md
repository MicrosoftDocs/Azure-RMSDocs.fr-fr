---
title: "Forum aux questions pour Azure Information Protection (préversion) | Azure Information Protection"
description: "Vous avez une question à propos de la préversion d’Azure Information Protection ? Vous trouverez peut-être une réponse ici."
author: cabailey
manager: mbaldwin
ms.date: 09/14/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 459cbe65741ea415defced844034f62cfd4654ed
ms.openlocfilehash: 39334a5cc18f1b45eabd7cf5b4f9b891fb10a5e6


---

# Forum aux questions pour Azure Information Protection (préversion)

>*S’applique à : Azure Information Protection (préversion)*

**[ Cette information est préliminaire et susceptible d'être modifiée. ]**

Vous avez une question à propos de la préversion d’Azure Information Protection ?  Vous trouverez peut-être une réponse ici. 

Cette liste est mise à jour fréquemment à mesure que des informations sont déplacées vers la documentation principale et que de nouvelles questions sont soumises par nos clients. 

## Que puis-je faire avec la préversion d’Azure Information Protection et quelles sont les limitations actuelles ?

Cette préversion ajoute une barre Information Protection aux applications Microsoft Office, qui permet d’afficher et de modifier des étiquettes de classification affectées à des données. La classification peut s’effectuer manuellement, vous être recommandée, ou être appliquée automatiquement. Pour les classifications que vous spécifiez, les données peuvent être protégées à l’aide d’un modèle Azure Rights Management.  

La configuration des étiquettes et du comportement de classification s’effectue dans le portail Azure. Vous pouvez utiliser les stratégies intégrées par défaut pour évaluer rapidement Azure Information Protection, ou personnaliser vos propres stratégies. Vous pouvez modifier les couleurs, les noms et l’ordre des étiquettes de classification visibles par les utilisateurs. Vous pouvez également configurer des info-bulles et des marquages de classification visuels comme des en-têtes, des pieds de page ou des filigranes.

Essayez notre didacticiel de démarrage rapide pour obtenir une démonstration en quelques minutes : [Didacticiel de démarrage rapide pour Azure Information Protection](infoprotect-quick-start-tutorial.md).

Notez que la préversion vous permet d’essayer le nouveau **plan de service Premium P2** et que certaines fonctionnalités avancées, telles que l’étiquetage automatique et recommandé, peuvent ne pas être disponibles avec votre plan actuel au moment de la disponibilité générale. Pour plus d’informations sur les différents plans de service (Azure Information Protection Premium P1 et Azure Information Protection Premium P2), consultez le blog suivant : [Introducing Enterprise Mobility + Security](https://blogs.technet.microsoft.com/enterprisemobility/2016/07/07/introducing-enterprise-mobility-security/) (Présentation d’Enterprise Mobility + Security).

Cette préversion a les limitations suivantes. Pour être tenu au courant de la disponibilité de fonctionnalités supplémentaires, consultez les annonces publiées sur le [Blog Enterprise Mobility and Security](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection) et sur notre [site Yammer](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all):

- Il n’existe aucun enregistrement centralisé pour la classification et l’étiquetage.

- Les noms des étiquettes et des info-bulles sont pris en charge dans une seule langue uniquement.

- Les conditions de classification automatique doivent être des expressions ou des modèles.

- Les fichiers ne peuvent pas être classés à partir de l’Explorateur Windows.

- Les applications Office pour les appareils mobiles (iOS et Android) et les ordinateurs Mac, ainsi que les applications web Office (Office Online) ne sont pas encore prises en charge.

- Aucune intégration à Exchange Online ou SharePoint Online.

- Le SDK pour les développeurs et les partenaires n’est pas disponible.

## De quel abonnement ai-je besoin pour essayer Azure Information Protection ?

Pour la préversion, vous pouvez utiliser n’importe quel abonnement Office 365 incluant la protection des documents Office et les messages électronique à l’aide d’Azure Rights Management. Azure Information Protection est disponible dans toutes les régions. Pour plus d’informations sur les abonnements disponibles et pour obtenir des liens vers des essais gratuits, consultez la section [Abonnement Office 365](../get-started/requirements-subscriptions.md#office-365-subscription) dans la documentation sur les conditions requises pour Azure RMS.

Pour configurer les stratégies Azure Information Protection dans le portail Azure, vous devez avoir un abonnement Azure. Si vous n’avez pas encore d’abonnement Azure pour votre organisation, vous pouvez en obtenir un en vous inscrivant pour une évaluation gratuite : accédez à la page [Prise en main d’Azure](https://account.windowsazure.com/organization) et suivez les instructions.

Toute modification apportée aux conditions requises des abonnements sera annoncée sur le [Blog Enterprise Mobility and Security](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection).

## Dois-je être administrateur général pour essayer Azure Information Protection (préversion) ?

Pour la préversion uniquement, tout utilisateur authentifié par Azure peut voir et configurer la stratégie Azure Information Protection de son locataire sur le portail Azure à des fins de classification et d’étiquetage dans le portail Azure. Toutefois, si vous voulez configurer une étiquette pour appliquer un modèle Azure Rights Management, vous devez être connecté tant qu’administrateur général pour Azure Active Directory.

Si vous sélectionnez l’option d’installation de la stratégie de démonstration quand vous installez le [client Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018), vous n’êtes même pas obligé de vous connecter au portail pour essayer la préversion. La stratégie de démonstration installe localement la stratégie par défaut pour Azure Information Protection. Vous pourrez donc essayer l’étiquetage des documents et des e-mails, mais vous ne pourrez pas modifier ni ajouter de nouvelles étiquettes sans vous connecter au portail. 

Si vous souhaitez protéger les documents et les e-mails que vous classifiez et étiquetez, mais que vous n’avez pas encore activé Azure Rights Management, le processus d’activation nécessite des autorisations d’administrateur spéciales. Pour plus d’informations, consultez [Dois-je être administrateur général pour configurer Azure RMS ou puis-je déléguer cette opération à d’autres administrateurs ?](../get-started/faqs.md#do-you-need-to-be-a-global-admin-to-configure-azure-rms-or-can-i-delegate-to-other-administrators)


## Azure Information Protection prend-il en charge les scénarios locaux et hybrides ?

Azure Information Protection est une solution basée sur le cloud. Si le déploiement d’Azure Information Protection dans le cadre d’un scénario hybride vous intéresse, contactez l’équipe Information Protection en envoyant un e-mail à askipteam@microsoft.com.

## Quelles sont les applications et les plateformes clientes prises en charge par Azure Information Protection ?

Ces informations sont maintenant documentées et seront mises à jour dans [Configuration requise pour Azure Information Protection](requirements-azure-infoprotect.md).


## Comment les ordinateurs obtiennent-ils les informations sur les stratégies à partir d’Azure Information Protection et quelle est la fréquence d’actualisation ?

Chaque fois qu’un utilisateur ouvre une application Office, le client Azure Information Protection vérifie s’il existe une version ultérieure de la stratégie Azure Information Protection. De plus, une vérification des applications Office est automatiquement effectuée toutes les 24 heures. S’il existe une version ultérieure, le client la télécharge à l’aide d’un lien HTTPS pour sécuriser les données. 

Si plusieurs instances de l’application Office sont chargées lors de la publication d’une nouvelle stratégie Azure Information Protection, vous devez fermer toutes les instances pour obtenir la dernière version de la stratégie. Par exemple, vous avez deux documents Word ouverts et souhaitez tester la stratégie Azure Information Protection mise à jour dans un seul document : fermez les deux documents Word et rouvrez le document que vous souhaitez utiliser avec la dernière stratégie.

## Où les fichiers peuvent-ils être stockés pour utiliser Azure Information Protection ? 

Les étiquettes et la protection appliquées aux fichiers et aux e-mails par Azure Information Protection étant persistantes, peu importe où sont stockés les fichiers.

## Puis-je classifier uniquement les nouvelles données, ou puis-je également classifier les données existantes ?

Les actions de stratégie Azure Information Protection prennent effet lors de l’enregistrement des documents et lors de l’envoi des e-mails, à la fois pour le nouveau contenu et pour les modifications apportées au contenu existant. 

Si vous avez enregistré des fichiers que vous souhaitez classifier, il vous suffit de les ouvrir et de les enregistrer dans votre application Office. 

Actuellement, vous ne pouvez pas analyser et appliquer la classification en bloc. Vous devez ouvrir et enregistrer tous les documents dans l’application Office. 

## Puis-je utiliser Azure Information Protection pour la classification uniquement, sans appliquer de chiffrement ni limiter les droits d’utilisation ?

Oui. Vous pouvez configurer une stratégie Azure Information Protection qui applique uniquement une étiquette. En fait, nous pensons que ce sera le cas d’usage le plus courant pour les réseaux de déploiement où vous devez protéger uniquement un sous-ensemble de documents ou d’e-mails qui nécessitent une gestion de données spéciale.

## Comment fonctionne la classification automatique ?

Dans le portail Azure, vous pouvez utiliser des modèles prédéfinis, tels que « Numéros de carte de crédit » ou « Numéro de sécurité sociale USA ». Vous pouvez aussi définir une chaîne ou un modèle personnalisé comme condition de classification automatique.

Le [Didacticiel de démarrage rapide pour Azure Information Protection](infoprotect-quick-start-tutorial.md) en donne un exemple. 

La précision de classification dépend de la façon dont vous configurez la règle de classification, qui est basée sur des conditions. Actuellement, les conditions prennent en charge les modèles de texte et les expressions régulières. Pour obtenir une explication sur chacune des options disponibles lors de l’aperçu, avec des exemples suggérés pour vous permettre de les tester, consultez [Comment configurer des conditions pour la classification automatique et recommandée pour Azure Information Protection](configure-policy-classification.md). La détection s’exécute quand le document est enregistré ou quand un e-mail est envoyé.

Pour bénéficier de la meilleure expérience utilisateur et pour garantir assurer la continuité d’activité, nous vous recommandons de commencer avec des actions de recommandation utilisateur, plutôt que des actions entièrement automatiques. Cela permet aux utilisateurs d’accepter l’action d’étiquetage ou de protection, ou d’ignorer ces suggestions.   

## Azure Information Protection peut-il inviter les utilisateur à classifier les fichiers eux-mêmes plutôt qu’utiliser la classification automatique ? 

Oui. Utilisez le portail Azure pour configurer s’il faut utiliser la classification automatique ou présenter une recommandation aux utilisateurs, en affectant la valeur **recommandé** à l’option **Select how this label is applied: automatically or recommended to user** (Sélectionner comment cette étiquette est appliquée : automatiquement ou recommandée à l’utilisateur).

Le [Didacticiel de démarrage rapide pour Azure Information Protection](infoprotect-quick-start-tutorial.md) en donne un exemple.  

## Puis-je forcer la classification de tous les documents ?

Oui. Si vous souhaitez que les utilisateurs classifient tous les fichiers qu’ils enregistrent, dans le portail Azure, affectez la valeur **On** à l’option **All documents and emails must have a label** (Tous les documents et e-mails doivent avoir une étiquette). 

## Puis-je supprimer la classification d’un fichier ?

Oui. Pour supprimer la classification d’un fichier, ouvrez-le dans l’application Office, cliquez sur l’icône **Edit label** (Modifier l’étiquette) dans la barre Information Protection, cliquez sur l’icône **Remove label** (Supprimer l’étiquette), puis cliquez sur **OK** pour confirmer votre action. 


## Puis-je demander aux utilisateurs de justifier pourquoi ils modifient le niveau de classification ?

Oui. Pour forcer les utilisateurs à justifier le changement de classification, dans le portail Azure, affectez la valeur **On** à l’option **Users must provide justification to set a lower classification label, remove a label, or remove protection** (Les utilisateurs doivent fournir une justification pour définir une étiquette de classification d’un niveau inférieur, supprimer une étiquette ou enlever la protection). Dans ce cas, la raison de l’action et la justification sont enregistrées dans le journal des événements Windows local de l’utilisateur : **Application** > **Microsoft Azure Information Protection**.

## Comment faire pour protéger automatiquement le contenu une fois qu’il a été classifié ?

Dans le portail Azure, vous pouvez sélectionner un modèle Azure Rights Management pour protéger automatiquement le contenu, en fonction du niveau de classification que vous spécifiez.

Le [Didacticiel de démarrage rapide pour Azure Information Protection](infoprotect-quick-start-tutorial.md) en donne un exemple. Pour en savoir plus, consultez la rubrique [Comment configurer une étiquette pour appliquer Rights Management protection](configure-policy-protection.md).

## Un fichier peut-il être classifié avec deux classifications différentes ?

Si nécessaire, vous pouvez créer des sous-étiquettes pour mieux décrire les sous-catégories d’une étiquette de confidentialité spécifique. Par exemple, l’étiquette principale **Secret** peut contenir des sous-étiquettes telles que **Secret : juridique** et **Secret : Finance**. Vous pouvez ensuite appliquer différents marquages de classification visuels et différents modèles Rights Management à différentes sous-étiquettes.

Bien que vous puissiez définir actuellement des marquages visuels, une protection et des conditions aux deux niveaux, quand vous utilisez des sous-niveaux, vous devez configurer ces paramètres uniquement au sous-niveau. Si vous configurez les mêmes paramètres sur l’étiquette parente et à son sous-niveau, les paramètres au sous-niveau sont prioritaires.

## Quand un e-mail est étiqueté, les pièces jointes reçoivent-elles automatiquement le même étiquetage ?

Non. Quand vous étiquetez un e-mail comportant des pièces jointes, ces dernières n’héritent pas de la même étiquette. Les pièces jointes peuvent rester sans étiquette ou conserver une étiquette appliquée séparément. Toutefois, si l’étiquette de l’e-mail applique une protection, cette protection est appliquée aux pièces jointes.

## Comment faire pour intégrer les solutions DLP et autres applications avec Azure Information Protection ?

Azure Information Protection utilisant des métadonnées persistantes pour la classification, notamment une étiquette de texte en clair, ces informations peuvent être lues par les solutions DLP et d’autres applications. Dans les fichiers, ces métadonnées sont stockées dans des propriétés personnalisées. Dans les e-mails, ces informations figurent dans les en-têtes.

## Comment fonctionnent le suivi des documents et la révocation pour Azure Information Protection ?

Le suivi des documents pour les fichiers que vous classifiez et protégez à l’aide d’Azure Information Protection fonctionne comme aujourd’hui pour Azure Rights Management et l’application de partage RMS. Vous pouvez également accéder au site de suivi des documents à l’aide du client Azure Information Protection (version 1.0.233 ou ultérieure) : 

- Dans une application Office, sous l’onglet **Accueil**, dans le groupe **Protection**, cliquez sur **Protéger** > **Suivre l’utilisation**. 

Pour plus d’informations, consultez [Suivre et révoquer vos documents lorsque vous utilisez l’application de partage RMS](../rms-client/sharing-app-track-revoke.md).

## Comment Azure Information Protection applique-t-il les stratégies que je configure ?

Quand un document est protégé à l’aide d’un modèle Azure Rights Management, l’utilisateur est d’abord authentifié pour s’assurer qu’il dispose de droits d’accès au document, puis la stratégie des droits d’utilisation est appliquée par l’application. 

## Comment Azure Information Protection utilise-t-il Azure Active Directory ?

Azure Information Protection utilise Azure Active Directory pour l’authentification utilisateur.

## Puis-je contrôler quels utilisateurs peuvent utiliser Azure Information Protection pour classifier et protéger le contenu ?

Vous pouvez limiter les utilisateurs qui classifient et protègent les données en contrôlant la distribution du client Azure Information Protection. 

Les fichiers et les e-mails classés par Azure Information Protection peuvent être consommés ou modifiés par n’importe quel utilisateur, qu’il ait installé ou non le client Azure Information Protection. 

## Comment puis-je signaler un problème ou envoyer des commentaires pour cette préversion ?

Si vous identifiez un problème lors de l’utilisation de cette préversion, dans votre application Office, sous l’onglet **Accueil**, dans le groupe **Protection**, cliquez sur **Protéger**, puis sur **Aide et commentaires**. Dans la boîte de dialogue **Microsoft Azure Information Protection**, cliquez sur **Envoyer des commentaires**. Un e-mail est envoyé à l’équipe Information Protection et les fichiers journaux de votre ordinateur sont joints automatiquement pour aider à diagnostiquer le problème. 

Si vous avez des questions ou des commentaires, rendez-vous sur le [site Yammer Azure Information Protection](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all). 

## Que puis-je faire si ma question ne figure pas dans cette rubrique ?

Tout d’abord, vérifiez que votre question ne figure pas dans l’[annonce Azure Information Protection (préversion)](https://blogs.technet.microsoft.com/enterprisemobility/2016/07/12/azure-information-protection-public-preview-available-now/), sur le blog Enterprise Mobility and Security.

Ensuite, accédez à notre [site Yammer](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all) pour voir si quelqu’un d’autre a posé la même question. Dans la négative, publiez votre question à cet endroit.







<!--HONumber=Sep16_HO2-->


