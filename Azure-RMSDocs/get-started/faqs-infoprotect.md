---
title: "FAQ sur la classification et l’étiquetage - AIP"
description: "Vous avez une question au sujet de l’utilisation d’Azure Information Protection pour la classification et l’étiquetage ? Vous trouverez peut-être une réponse ici."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/28/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ccd840fdfc702e209390ed431d24d7e47edf9930
ms.openlocfilehash: 0ce3ba72eb8a201486eaf2ae39f5d7bf99753cad
ms.lasthandoff: 02/28/2017


---

# <a name="frequently-asked-questions-about-classification-and-labeling-in-azure-information-protection"></a>Forum aux questions sur la classification et l’étiquetage dans Azure Information Protection

>*S’applique à : Azure Information Protection, Office 365*

Vous avez une question concernant Azure Information Protection qui porte spécifiquement sur la classification et l’étiquetage ?  Vous trouverez peut-être une réponse ici. 

## <a name="what-can-i-do-with-the-classification-capabilities-in-azure-information-protection"></a>Que puis-je faire avec les fonctionnalités de classification disponibles dans Azure Information Protection ?

Essayez notre didacticiel de démarrage rapide pour obtenir une démonstration en quelques minutes : [Didacticiel de démarrage rapide pour Azure Information Protection](infoprotect-quick-start-tutorial.md).

Pour être informé de la mise à disposition de fonctionnalités de classification supplémentaires, consultez les annonces publiées sur le [blog Enterprise Mobility and Security](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection) et sur notre [site Yammer](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all). La version actuelle présente quelques limites, notamment :

- Les noms des étiquettes et des info-bulles sont pris en charge dans une seule langue uniquement.

- Il n’existe aucun enregistrement centralisé pour la classification et l’étiquetage.

- Les conditions de classification automatique doivent être des expressions ou des modèles.

- L’étiquetage n’est pas pris en charge pour les applications Office pour appareils mobiles (iOS et Android) et les ordinateurs Mac ou pour les applications web Office (Office Online).

- Aucune intégration de classification et d’étiquetage n’est assurée avec Exchange Online ou SharePoint Online.

- Le SDK pour les développeurs et les partenaires n’inclut pas encore la classification et l’étiquetage.

La version de février supprime un grand nombre des limites précédentes. Pour plus d’informations, voir cette [annonce faite dans un billet du blog](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/08/azure-information-protection-december-update-moves-to-general-availability/).

## <a name="do-i-need-to-be-a-global-admin-to-configure-classification-and-labels"></a>Dois-je être un administrateur global pour configurer la classification et les étiquettes ?

Pour configurer la stratégie Azure Information Protection, vous devez vous connecter au portail Azure en tant qu’administrateur général pour Azure Active Directory.

Toutefois, si vous sélectionnez cette option pour installer la stratégie de démonstration au moment de l’installation du [client Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018), vous n’êtes pas obligé de vous connecter au portail pour voir et tester la fonctionnalité d’étiquetage. La stratégie de démonstration installe localement la stratégie par défaut pour Azure Information Protection. Vous pourrez donc essayer l’étiquetage des documents et des e-mails, mais vous ne pourrez pas modifier ni ajouter de nouvelles étiquettes sans vous connecter au portail. 

## <a name="which-options-in-the-azure-portal-are-p1-or-p2"></a>Que sont les options P1 et P2 dans le portail Azure ?

Pour vérifier les fonctionnalités qui sont incluses dans l’abonnement **Azure Information Protection Premium 1** (P1) et l’abonnement **Azure Information Protection Premium 2** (P2), consultez la [liste des fonctionnalités](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features) sur le site Azure Information Protection. Toutefois, en règle générale, les fonctionnalités avancées telles que la classification automatique et HYOK (Hold Your Own Key) sont propres à l’abonnement Azure Information Protection Premium 2.

## <a name="can-a-file-have-more-than-one-classification"></a>Un fichier peut-il avoir plusieurs classifications ?

Les utilisateurs ne peuvent sélectionner qu’une seule étiquette à la fois pour chaque document ou e-mail, ce qui aboutit la plupart du temps à une classification unique pour chaque élément. Vous avez toutefois la possibilité d’appliquer une étiquette principale et une étiquette secondaire (ou sous-étiquette) à chaque document ou e-mail. Les étiquettes secondaires permettent d’attribuer à un fichier deux classifications ayant une relation parent\enfant afin d’obtenir un niveau de contrôle supplémentaire.

Par exemple, l’étiquette **Secret** peut contenir des sous-étiquettes telles que **Juridique** et **Finance**. Vous pouvez appliquer différents marquages de classification visuels et différents modèles Rights Management à ces sous-étiquettes. L’utilisateur ne peut pas sélectionner uniquement l’étiquette **Secret**. Il peut seulement sélectionner les sous-étiquettes, telles que **Juridique**. L’étiquette qui s’affiche est donc **Secret\Juridique**. Les métadonnées de ce fichier incluent une propriété de texte personnalisée pour **Secret**, une propriété de texte personnalisée pour **Juridique** et une autre qui contient les deux valeurs (**Secret Juridique**). 

Lorsque vous utilisez des étiquettes secondaires, ne configurez pas de marquages visuels, de protection ou de conditions pour l’étiquette principale. Ces paramètres doivent uniquement être définis pour l’étiquette secondaire. Si vous configurez ces paramètres pour l’étiquette principale et l’étiquette secondaire, ce sont les paramètres de l’étiquette secondaire qui seront prioritaires.

## <a name="when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling"></a>Quand un e-mail est étiqueté, les pièces jointes reçoivent-elles automatiquement le même étiquetage ?

Non. Quand vous étiquetez un e-mail comportant des pièces jointes, ces dernières n’héritent pas de la même étiquette. Les pièces jointes peuvent rester sans étiquette ou conserver une étiquette appliquée séparément. Toutefois, si l’étiquette de l’e-mail applique une protection, cette protection est appliquée aux pièces jointes.

## <a name="how-is-azure-information-protection-classification-for-emails-different-from-exchange-message-classification"></a>En quoi la classification Azure Information Protection pour les e-mails est-elle différente de celle des messages Exchange ?

La classification des messages Exchange est une ancienne fonctionnalité permettant de classer des e-mails. Elle est mise en œuvre indépendamment de la classification Azure Information Protection. Toutefois, vous pouvez intégrer les deux solutions pour que, quand les utilisateurs classifient un e-mail à l’aide d’Outlook Web App et de certaines applications de messagerie mobile, la classification Azure Information Protection et ses marquages d’étiquette correspondants soient automatiquement ajoutés. Exchange ajoute la classification, et le client Azure Information Protection applique les paramètres d’étiquette correspondant à cette classification.

Même si Outlook Web App ne prend pas encore en charge la classification et la protection Azure Information Protection, vous pouvez utiliser cette même technique pour utiliser vos étiquettes avec ce client de messagerie en plus du client Outlook de bureau.

Pour obtenir cette solution : 

1. Utilisez l’applet de commande PowerShell Exchange [New-MessageClassification](https://technet.microsoft.com/library/bb124400) pour créer des classifications des messages avec la propriété Name qui correspond à vos noms d’étiquette dans votre stratégie Azure Information Protection. 

2. Créez une règle de transport Exchange pour chaque étiquette : appliquez la règle quand les propriétés de message incluent la classification que vous avez configurée, puis modifiez les propriétés de message pour définir un en-tête de message. 

    Pour l’en-tête de message, vous trouverez les informations à spécifier en inspectant les propriétés d’un fichier Office que vous avez classifié à l’aide de votre étiquette Azure Information Protection. Identifiez la propriété de fichier au format **MSIP_Label_<GUID>_Enabled** et spécifiez cette chaîne pour l’en-tête de message, puis spécifiez **True** pour la valeur de l’en-tête. Par exemple, votre en-tête de message peut ressembler à cette chaîne : **MSIP_Label_132616b8-f72d-5d1e-aec1-dfd89eb8c5b2_Enabled**


Voici ce qui se produit quand les utilisateurs utilisent Outlook Web Access ou un client d’appareil mobile qui prend en charge la protection de la gestion des droits : 

- Les utilisateurs sélectionnent la classification des messages Exchange et envoient l’e-mail.

- La règle Exchange détecte la classification Exchange et modifie en conséquence l’en-tête de message pour ajouter la classification Azure Information Protection.

- Quand les destinataires exécutant le client Azure Information Protection affichent l’e-mail dans Outlook, ils voient l’étiquette Azure Information Protection attribuée et tout en-tête, pied de page ou filigrane correspondants. 

Si vos étiquettes Azure Information Protection appliquent la protection de la gestion des droits, ajoutez-la à la configuration de la règle en sélectionnant l’option permettant de modifier la sécurité des messages, appliquez la protection des droits, puis sélectionnez le modèle RMS ou l’option Ne pas transférer.

Vous pouvez également configurer des règles de transport pour effectuer le mappage inverse : quand une étiquette Azure Information Protection est détectée, définissez la classification de messages Exchange correspondante. Pour effectuer cette opération :

- Pour chaque étiquette Azure Information Protection, créez une règle de transport devant être appliquée lorsque l’en-tête **msip_labels** inclut le nom de votre étiquette (par exemple, **Confidentiel**), puis appliquez une classification de messages qui corresponde à cette étiquette.

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>Comment faire pour intégrer les solutions DLP et autres applications avec Azure Information Protection ?

Azure Information Protection utilisant des métadonnées persistantes pour la classification, notamment une étiquette de texte en clair, ces informations peuvent être lues par les solutions DLP et d’autres applications. Dans les fichiers, ces métadonnées sont stockées dans des propriétés personnalisées. Dans les e-mails, ces informations figurent dans les en-têtes.

## <a name="how-do-i-sign-in-as-a-different-user"></a>Comment se connecter avec l'identité d'un autre utilisateur ?

Dans un environnement de production, vous ne devez généralement pas vous connecter sous un autre nom lorsque vous utilisez le client Azure Information Protection. Toutefois, vous devrez peut-être le faire si vous disposez de plusieurs locataires. Par exemple, vous disposez d’un locataire test en plus du locataire Office 365 ou Azure utilisé par votre organisation.

Vous pouvez vérifier le compte auquel vous êtes actuellement connecté à l’aide de la boîte de dialogue **Microsoft Azure Information Protection** : ouvrez une application Office et, dans l’onglet **Accueil**, dans le groupe **Protection**, cliquez sur **Protéger**, puis sur **Aide et commentaires**. Votre nom de votre compte s’affiche dans la section **État du client**.

Vérifiez le nom de domaine du compte connecté qui s’affiche, en particulier lorsque vous utilisez un compte d’administrateur. Par exemple, si vous avez un compte d’administrateur dans deux locataires différents, il peut être facile d’oublier que vous êtes connecté avec un nom du compte correct mais dans un domaine incorrect. Vous pouvez vous en apercevoir en cas d’échec du téléchargement de la stratégie Azure Information Protection ou si vous ne voyez pas les étiquettes ou le comportement que vous attendez.

Pour ouvrir une session sous un autre nom d’utilisateur, vous devez actuellement modifier le Registre :

1. À l’aide d’un éditeur du Registre, accédez à **HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP** et supprimez la valeur **TokenCache**.

2. Redémarrez les applications Office ouvertes et connectez-vous avec votre autre compte d’utilisateur. Si l’invite de connexion au service Azure Information Protection n’apparaît pas dans votre application Office, revenez à la boîte de dialogue **Microsoft Azure Information Protection** et cliquez sur **Connexion** depuis la section mise à jour **État du Client**.

En outre :

- Si vous souhaitez réinitialiser l’environnement pour le service Azure Rights Management (également appelé amorçage), vous pouvez utiliser l’option **Réinitialiser** depuis [l’outil d’analyse RMS](https://www.microsoft.com/en-us/download/details.aspx?id=46437).

- Si vous souhaitez supprimer la stratégie Azure Information Protection actuellement téléchargée, vous pouvez supprimer le fichier **Policy.msip** du dossier %localappdata%\Microsoft\MSIP.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
