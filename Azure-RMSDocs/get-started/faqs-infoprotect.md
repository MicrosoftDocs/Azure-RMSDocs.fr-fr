---
title: "Forum aux questions sur la classification et l’étiquetage | Azure Information Protection"
description: "Vous avez une question à propos de la préversion d’Azure Information Protection ? Vous trouverez peut-être une réponse ici."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/09/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 946daa8dedba71d5887dd96f6853e8d90400bfb1
ms.openlocfilehash: 125752671ec0ca556cc6967a2a3011fb0bf7d9ab


---

# <a name="frequently-asked-questions-about-classification-and-labeling-in-azure-information-protection"></a>Forum aux questions sur la classification et l’étiquetage dans Azure Information Protection

>*S’applique à : Azure Information Protection, Office 365*

Vous avez une question concernant Azure Information Protection qui porte spécifiquement sur la classification et l’étiquetage ?  Vous trouverez peut-être une réponse ici. 

## <a name="what-can-i-do-with-the-classification-capabilities-in-azure-information-protection"></a>Que puis-je faire avec les fonctionnalités de classification disponibles dans Azure Information Protection ?

Le client Azure Information Protection ajoute une barre Information Protection aux applications Microsoft Office, qui permet d’afficher et de modifier des étiquettes de classification affectées à des données. La classification peut s’effectuer manuellement, vous être recommandée, ou être appliquée automatiquement. Pour les classifications que vous spécifiez, les données peuvent être protégées à l’aide d’un service Rights Management.  

La configuration des étiquettes et du comportement de classification s’effectue dans le portail Azure. Vous pouvez utiliser la stratégie intégrée par défaut pour évaluer rapidement Azure Information Protection, ou personnaliser vos propres stratégies. Vous pouvez modifier les couleurs, les noms et l’ordre des étiquettes de classification visibles par les utilisateurs. Vous pouvez également configurer des info-bulles et des marquages de classification visuels comme des en-têtes, des pieds de page ou des filigranes.

Essayez notre didacticiel de démarrage rapide pour obtenir une démonstration en quelques minutes : [Didacticiel de démarrage rapide pour Azure Information Protection](infoprotect-quick-start-tutorial.md).

La version actuelle présente les limitations ci-après. Pour être tenu au courant de la disponibilité de fonctionnalités supplémentaires, consultez les annonces publiées sur le [Blog Enterprise Mobility and Security](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection) et sur notre [site Yammer](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all):

- Les noms des étiquettes et des info-bulles sont pris en charge dans une seule langue uniquement.

- Il n’existe aucun enregistrement centralisé pour la classification et l’étiquetage.

- Les conditions de classification automatique doivent être des expressions ou des modèles.

- Les applications Office pour les appareils mobiles (iOS et Android) et les ordinateurs Mac, ainsi que les applications web Office (Office Online) ne sont pas encore prises en charge.

- Aucune intégration à Exchange Online ou SharePoint Online.

- Le SDK pour les développeurs et les partenaires n’est pas disponible.

Certaines des limitations mentionnées précédemment sont désormais disponibles dans la préversion. Pour plus d’informations, consultez le billet de blog sur la disponibilité de la [préversion de décembre d’Azure Information protection](https://blogs.technet.microsoft.com/enterprisemobility/2016/12/07/azure-information-protection-december-preview-now-available/).


## <a name="do-i-need-to-be-a-global-admin-to-try-azure-information-protection"></a>Dois-je être administrateur général pour essayer Azure Information Protection ?

Pour configurer la stratégie Azure Information Protection, vous devez vous connecter au portail Azure en tant qu’administrateur général pour Azure Active Directory.

Toutefois, si vous sélectionnez l’option d’installation de la stratégie de démonstration quand vous installez le [client Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018), vous n’êtes pas obligé de vous connecter au portail pour voir et essayer la fonctionnalité d’étiquetage. La stratégie de démonstration installe localement la stratégie par défaut pour Azure Information Protection. Vous pourrez donc essayer l’étiquetage des documents et des e-mails, mais vous ne pourrez pas modifier ni ajouter de nouvelles étiquettes sans vous connecter au portail. 

## <a name="which-options-in-the-azure-portal-are-p1-or-p2"></a>Que sont les options P1 et P2 dans le portail Azure ?

Pour vérifier les fonctionnalités qui sont incluses dans l’abonnement **Azure Information Protection Premium 1** (P1) et l’abonnement **Azure Information Protection Premium 2** (P2), consultez la [liste des fonctionnalités](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features) sur le site Azure Information Protection. Toutefois, en règle générale, les fonctionnalités avancées telles que la classification automatique et HYOK (Hold Your Own Key) sont propres à l’abonnement Azure Information Protection Premium 2.

## <a name="does-azure-information-protection-support-on-premises-and-hybrid-scenarios"></a>Azure Information Protection prend-il en charge les scénarios locaux et hybrides ?

Azure Information Protection est une solution basée sur le cloud. Si le déploiement d’Azure Information Protection dans le cadre d’un scénario hybride vous intéresse, contactez l’équipe Information Protection en envoyant un e-mail à askipteam@microsoft.com.

## <a name="how-do-computers-get-the-policy-information-from-azure-information-protection-and-how-often-is-it-refreshed"></a>Comment les ordinateurs obtiennent-ils les informations sur les stratégies à partir d’Azure Information Protection et quelle est la fréquence d’actualisation ?

Chaque fois qu’un utilisateur ouvre une application Office, le client Azure Information Protection vérifie s’il existe une version ultérieure de la stratégie Azure Information Protection. De plus, une vérification des applications Office est effectuée toutes les 24 heures. S’il existe une version ultérieure, le client la télécharge à l’aide d’un lien HTTPS pour sécuriser les données. 

Si plusieurs instances de l’application Office sont chargées lors de la publication d’une nouvelle stratégie Azure Information Protection, vous devez fermer toutes les instances pour obtenir la dernière version de la stratégie. Par exemple, vous avez deux documents Word ouverts et souhaitez tester la stratégie Azure Information Protection mise à jour dans un seul document : fermez les deux documents Word et rouvrez le document que vous souhaitez utiliser avec la dernière stratégie.

## <a name="where-can-files-be-stored-to-use-azure-information-protection"></a>Où les fichiers peuvent-ils être stockés pour utiliser Azure Information Protection ? 

Les étiquettes et la protection appliquées aux fichiers et aux e-mails par Azure Information Protection étant persistantes, peu importe où sont stockés les fichiers.

## <a name="can-i-classify-only-new-data-or-can-i-also-classify-existing-data"></a>Puis-je classifier uniquement les nouvelles données, ou puis-je également classifier les données existantes ?

Les actions de stratégie Azure Information Protection prennent effet lors de l’enregistrement des documents et lors de l’envoi des e-mails, à la fois pour le nouveau contenu et pour les modifications apportées au contenu existant.

Si vous disposez de la préversion du client, vous pouvez aussi classer (et éventuellement protéger) rapidement les fichiers existants à partir de l’Explorateur de fichiers. 

## <a name="can-i-use-azure-information-protection-for-classification-only-without-enforcing-encryption-and-restricting-usage-rights"></a>Puis-je utiliser Azure Information Protection pour la classification uniquement, sans appliquer de chiffrement ni limiter les droits d’utilisation ?

Oui. Vous pouvez configurer une stratégie Azure Information Protection qui applique uniquement la classification sans la protection, si le type de fichier prend en charge cette action. En fait, nous pensons que ce sera le cas d’usage le plus courant pour les réseaux de déploiement où vous devez protéger uniquement un sous-ensemble de documents ou d’e-mails qui nécessitent une gestion de données spéciale.

## <a name="how-does-automatic-classification-work"></a>Comment fonctionne la classification automatique ?

Dans le portail Azure, vous pouvez utiliser des modèles prédéfinis, tels que « Numéros de carte de crédit » ou « Numéro de sécurité sociale USA ». Vous pouvez aussi définir une chaîne ou un modèle personnalisé comme condition de classification automatique.

Le [Didacticiel de démarrage rapide pour Azure Information Protection](infoprotect-quick-start-tutorial.md) en donne un exemple. 

La précision de classification dépend de la façon dont vous configurez la règle de classification, qui est basée sur des conditions. Actuellement, les conditions prennent en charge les modèles de texte et les expressions régulières. Pour obtenir une explication sur chacune des options disponibles lors de l’aperçu, avec des exemples suggérés pour vous permettre de les tester, consultez [Comment configurer des conditions pour la classification automatique et recommandée pour Azure Information Protection](../deploy-use/configure-policy-classification.md). La détection s’exécute quand le document est enregistré ou quand un e-mail est envoyé.

Pour bénéficier de la meilleure expérience utilisateur et pour garantir assurer la continuité d’activité, nous vous recommandons de commencer avec des actions de recommandation utilisateur, plutôt que des actions entièrement automatiques. Cela permet aux utilisateurs d’accepter l’action d’étiquetage ou de protection, ou d’ignorer ces suggestions.   

## <a name="can-azure-information-protection-prompt-users-to-classify-files-themselves-rather-than-use-automatic-classification"></a>Azure Information Protection peut-il inviter les utilisateur à classifier les fichiers eux-mêmes plutôt qu’utiliser la classification automatique ? 

Oui. Utilisez le portail Azure pour configurer s’il faut utiliser la classification automatique ou présenter une recommandation aux utilisateurs, en affectant la valeur **recommandé** à l’option **Sélectionner comment cette étiquette est appliquée : automatiquement ou recommandée à l'utilisateur**.

Le [Didacticiel de démarrage rapide pour Azure Information Protection](infoprotect-quick-start-tutorial.md) en donne un exemple.  

## <a name="can-i-force-all-documents-to-be-classified"></a>Puis-je forcer la classification de tous les documents ?

Oui. Si vous souhaitez que les utilisateurs classifient tous les fichiers qu’ils enregistrent, dans le portail Azure, affectez la valeur **On** à l’option **Tous les documents et e-mails doivent avoir une étiquette**. 

## <a name="can-i-remove-classification-from-a-file"></a>Puis-je supprimer la classification d’un fichier ?

Oui. Pour supprimer la classification d’un fichier, ouvrez-le dans l’application Office, cliquez sur l’icône **Modifier l’étiquette** dans la barre Information Protection, cliquez sur l’icône **Supprimer l’étiquette**, puis cliquez sur **OK** pour confirmer votre action. 


## <a name="can-i-prompt-users-to-justify-why-they-are-changing-the-classification-level"></a>Puis-je demander aux utilisateurs de justifier pourquoi ils modifient le niveau de classification ?

Oui. Pour forcer les utilisateurs à justifier le changement de classification, dans le portail Azure, affectez la valeur **Activé** à l’option **Les utilisateurs doivent fournir une justification pour définir une étiquette de classification moins élevée, supprimer une étiquette ou supprimer la protection**. Dans ce cas, la raison de l’action et la justification sont enregistrées dans le journal des événements Windows local de l’utilisateur : **Journaux des applications et des services** > **Microsoft Azure Information Protection**.

## <a name="how-can-i-automatically-protect-the-content-after-its-been-classified"></a>Comment faire pour protéger automatiquement le contenu une fois qu’il a été classifié ?

Dans le portail Azure, vous pouvez sélectionner un modèle Rights Management pour protéger automatiquement le contenu, en fonction du niveau de classification que vous spécifiez.

Le [Didacticiel de démarrage rapide pour Azure Information Protection](infoprotect-quick-start-tutorial.md) en donne un exemple. Pour en savoir plus, consultez la rubrique [Comment configurer une étiquette pour appliquer Rights Management protection](../deploy-use/configure-policy-protection.md).

## <a name="can-a-file-have-more-than-one-classification"></a>Un fichier peut-il avoir plusieurs classifications ?

Les utilisateurs ne peuvent sélectionner qu’une seule étiquette à la fois pour chaque document ou e-mail, ce qui aboutit la plupart du temps à une classification unique pour chaque élément. Vous avez toutefois la possibilité d’appliquer une étiquette principale et une étiquette secondaire (ou sous-étiquette) à chaque document ou e-mail. Les étiquettes secondaires permettent d’attribuer à un fichier deux classifications ayant une relation parent\enfant afin d’obtenir un niveau de contrôle supplémentaire.

Par exemple, l’étiquette **Secret** peut contenir des sous-étiquettes telles que **Juridique** et **Finance**. Vous pouvez appliquer différents marquages de classification visuels et différents modèles Rights Management à ces sous-étiquettes. L’utilisateur ne peut pas sélectionner uniquement l’étiquette **Secret**. Il peut seulement sélectionner les sous-étiquettes, telles que **Juridique**. L’étiquette qui s’affiche est donc **Secret\Juridique**. Les métadonnées de ce fichier incluent une propriété de texte personnalisée pour **Secret**, une propriété de texte personnalisée pour **Juridique** et une autre qui contient les deux valeurs (**Secret Juridique**). 

Lorsque vous utilisez des étiquettes secondaires, ne configurez pas de marquages visuels, de protection ou de conditions pour l’étiquette principale. Ces paramètres doivent uniquement être définis pour l’étiquette secondaire. Si vous configurez ces paramètres pour l’étiquette principale et l’étiquette secondaire, ce sont les paramètres de l’étiquette secondaire qui seront prioritaires.

## <a name="when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling"></a>Quand un e-mail est étiqueté, les pièces jointes reçoivent-elles automatiquement le même étiquetage ?

Non. Quand vous étiquetez un e-mail comportant des pièces jointes, ces dernières n’héritent pas de la même étiquette. Les pièces jointes peuvent rester sans étiquette ou conserver une étiquette appliquée séparément. Toutefois, si l’étiquette de l’e-mail applique une protection, cette protection est appliquée aux pièces jointes.

## <a name="how-is-azure-information-protection-classification-for-emails-different-from-exchange-message-classification"></a>En quoi la classification Azure Information Protection pour les e-mails est-elle différente de celle des messages Exchange ?

La classification des messages Exchange est une ancienne fonctionnalité permettant de classer des e-mails. Elle est mise en œuvre indépendamment de la classification Azure Information Protection. Toutefois, vous pouvez intégrer les deux solutions pour que, quand les utilisateurs classifient un e-mail à l’aide d’Outlook Web App et de certaines applications de messagerie mobile, la classification Azure Information Protection et ses marquages d’étiquette correspondants soient automatiquement ajoutés. Exchange ajoute la classification et la préversion du client Azure Information Protection applique les paramètres d’étiquette correspondant à cette classification.

Même si Outlook Web App ne prend pas encore en charge la classification et la protection Azure Information Protection, vous pouvez utiliser cette même technique pour utiliser vos étiquettes avec ce client de messagerie en plus du client Outlook de bureau.

Pour obtenir cette solution : 

1. Utilisez l’applet de commande PowerShell Exchange [New-MessageClassification](https://technet.microsoft.com/library/bb124400) pour créer des classifications des messages avec la propriété Name qui correspond à vos noms d’étiquette dans votre stratégie Azure Information Protection. 

2. Créez une règle de transport Exchange pour chaque étiquette : appliquez la règle quand les propriétés de message incluent la classification que vous avez configurée, puis modifiez les propriétés de message pour définir un en-tête de message. 

    Pour l’en-tête de message, vous trouverez les informations à spécifier en inspectant les propriétés d’un fichier Office que vous avez classifié à l’aide de votre étiquette Azure Information Protection. Identifiez la propriété de fichier au format **MSIP_Label_<GUID>_Enabled** et spécifiez cette chaîne pour l’en-tête de message, puis spécifiez **True** pour la valeur de l’en-tête. Par exemple, votre en-tête de message peut ressembler à cette chaîne : **MSIP_Label_132616b8-f72d-5d1e-aec1-dfd89eb8c5b2_Enabled**


Voici ce qui se produit quand les utilisateurs utilisent Outlook Web Access ou un client d’appareil mobile qui prend en charge la protection de la gestion des droits : 

- Les utilisateurs sélectionnent la classification des messages Exchange et envoient l’e-mail.

- La règle Exchange détecte la classification Exchange et modifie en conséquence l’en-tête de message pour ajouter la classification Azure Information Protection.

- Quand les destinataires exécutant la préversion du client Azure Information Protection affichent l’e-mail dans Outlook, ils voient l’étiquette Azure Information Protection attribuée et tout en-tête, pied de page ou filigrane correspondants. 

Si vos étiquettes Azure Information Protection appliquent la protection de la gestion des droits, ajoutez-la à la configuration de la règle en sélectionnant l’option permettant de modifier la sécurité des messages, appliquez la protection des droits, puis sélectionnez le modèle RMS ou l’option Ne pas transférer.

Vous pouvez également configurer des règles de transport pour effectuer le mappage inverse : quand une étiquette Azure Information Protection est détectée, définissez la classification de messages Exchange correspondante. Pour effectuer cette opération :

- Pour chaque étiquette Azure Information Protection, créez une règle de transport devant être appliquée lorsque l’en-tête **msip_labels** inclut le nom de votre étiquette (par exemple, **Confidentiel**), puis appliquez une classification de messages qui corresponde à cette étiquette.

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>Comment faire pour intégrer les solutions DLP et autres applications avec Azure Information Protection ?

Azure Information Protection utilisant des métadonnées persistantes pour la classification, notamment une étiquette de texte en clair, ces informations peuvent être lues par les solutions DLP et d’autres applications. Dans les fichiers, ces métadonnées sont stockées dans des propriétés personnalisées. Dans les e-mails, ces informations figurent dans les en-têtes.

## <a name="how-does-document-tracking-and-revocation-work-for-azure-information-protection"></a>Comment fonctionnent le suivi des documents et la révocation pour Azure Information Protection ?

Le suivi des documents pour les fichiers que vous classifiez et protégez à l’aide d’Azure Information Protection fonctionne avec la protection Azure Rights Management et l’application de partage RMS. Vous pouvez également accéder au site de suivi des documents à l’aide du client Azure Information Protection (version 1.0.233 ou ultérieure) : 

- Dans une application Office, sous l’onglet **Accueil**, dans le groupe **Protection**, cliquez sur **Protéger** > **Suivre l’utilisation**. 

Pour plus d’informations, consultez [Suivre et révoquer vos documents lorsque vous utilisez l’application de partage RMS](../rms-client/sharing-app-track-revoke.md).

## <a name="can-i-control-which-users-can-use-azure-information-protection-to-classify-and-protect-content"></a>Puis-je contrôler quels utilisateurs peuvent utiliser Azure Information Protection pour classifier et protéger le contenu ?

Vous pouvez limiter les utilisateurs qui classifient et protègent les données en contrôlant la distribution du client Azure Information Protection. Vous ajoutez de nouvelles étiquettes uniquement pour les utilisateurs spécifiés quand vous configurez une [stratégie délimitée](../deploy-use\configure-policy-scope.md). 

Les fichiers et les e-mails classés par Azure Information Protection peuvent être consommés ou modifiés par n’importe quel utilisateur, qu’il ait installé ou non le client Azure Information Protection. 

## <a name="how-do-i-sign-in-as-a-different-user"></a>Comment se connecter avec l'identité d'un autre utilisateur ?

Dans un environnement de production, vous ne devez généralement pas vous connecter sous un autre nom lorsque vous utilisez le client Azure Information Protection. Toutefois, vous devrez peut-être le faire si vous disposez de plusieurs locataires. Par exemple, vous disposez d’un locataire test en plus du locataire Office 365 ou Azure utilisé par votre organisation.

Vous pouvez vérifier le compte auquel vous êtes actuellement connecté à l’aide de la boîte de dialogue **Microsoft Azure Information Protection** : ouvrez une application Office et, dans l’onglet **Accueil**, dans le groupe **Protection**, cliquez sur **Protéger**, puis sur **Aide et commentaires**. Votre nom de votre compte s’affiche dans la section **État du client**.

Vérifiez le nom de domaine du compte connecté qui s’affiche, en particulier lorsque vous utilisez un compte d’administrateur. Par exemple, si vous avez un compte d’administrateur dans deux locataires différents, il peut être facile d’oublier que vous êtes connecté avec un nom du compte correct mais dans un domaine incorrect. Vous pouvez vous en apercevoir en cas d’échec du téléchargement de la stratégie Azure Information Protection ou si vous ne voyez pas les étiquettes ou le comportement que vous attendez.

Pour ouvrir une session sous un autre nom d’utilisateur, vous devez actuellement modifier le Registre :

1. À l’aide d’un éditeur du Registre, accédez à **HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP** et supprimez la clé **TokenCache**.

2. Redémarrez les applications Office ouvertes et connectez-vous avec votre autre compte d’utilisateur. Si l’invite de connexion au service Azure Information Protection n’apparaît pas dans votre application Office, revenez à la boîte de dialogue **Microsoft Azure Information Protection** et cliquez sur **Connexion** depuis la section mise à jour **État du Client**.

En outre :

- Si vous souhaitez réinitialiser l’environnement pour le service Azure Rights Management (également appelé amorçage), vous pouvez utiliser l’option **Réinitialiser** depuis [l’outil d’analyse RMS](https://www.microsoft.com/en-us/download/details.aspx?id=46437).

- Si vous souhaitez supprimer la stratégie Azure Information Protection actuellement téléchargée, vous pouvez supprimer le fichier **Policy.msip** du dossier %localappdata%\Microsoft\MSIP.

## <a name="how-can-i-report-a-problem-or-send-feedback-for-azure-information-protection"></a>Comment puis-je signaler un problème ou envoyer des commentaires pour Azure Information Protection ?

Si vous avez un problème avec Azure Information Protection et que vous utilisez la version actuelle du client : dans votre application Office, sous l’onglet **Accueil**, dans le groupe **Protection**, cliquez sur **Protéger**, puis cliquez sur **Aide et commentaires**. Dans la boîte de dialogue **Microsoft Azure Information Protection**, cliquez sur **Envoyer des commentaires**. Un e-mail est envoyé à l’équipe Information Protection et les fichiers journaux de votre ordinateur sont joints automatiquement pour aider à diagnostiquer le problème. 

Si vous avez des questions ou des commentaires, rendez-vous sur le [site Yammer Azure Information Protection](https://www.yammer.com/askipteam/). 


<!--HONumber=Dec16_HO2-->


