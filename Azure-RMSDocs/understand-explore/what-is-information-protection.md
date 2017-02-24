---
title: "Qu’est-ce qu’Azure Information Protection ?"
description: "Présentation du service Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/16/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: cd8a88e2-3555-4be2-9637-3cdee992f2c8
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: 7d5c759a6b7e206f30588926a8d480b50be20bc4


---

# <a name="what-is-azure-information-protection"></a>Qu’est-ce qu’Azure Information Protection ?

>*S’applique à : Azure Information Protection*

Azure Information Protection est une solution basée sur le cloud qui permet à une organisation de classifier, d’étiqueter et de protéger ses documents et les e-mails. Ces opérations peuvent être effectuées automatiquement par les administrateurs qui définissent des règles et des conditions ou manuellement par les utilisateurs, qui peuvent éventuellement se voir proposer des recommandations. 

L’image suivante illustre Azure Information Protection en action. L’administrateur a configuré des règles pour détecter les données sensibles (dans ce cas, des informations de carte de crédit). Quand un utilisateur enregistre un document Word qui contient des informations de carte de crédit, il voit une info-bulle personnalisée qui lui recommande d’appliquer une étiquette spécifique que l’administrateur a configurée, qui classifie et éventuellement protège le document. 

![Exemple de classification recommandée pour Azure Information Protection](../media/info-protect-recommend-callouts.png)

Une fois que votre contenu est classifié (et éventuellement protégé), vous pouvez suivre et contrôler son utilisation. Vous pouvez analyser les flux de données pour obtenir des informations sur vos activités, détecter les comportements à risque et prendre des mesures correctives, suivre l’accès aux documents, empêcher la fuite de données ou une mauvaise utilisation des données, etc.

## <a name="how-labels-apply-classification"></a>Comment les étiquettes appliquent la classification

Les étiquettes Azure Information Protection vous permettent d’appliquer une classification aux documents et e-mails. Ainsi, la classification est identifiable à tout moment, quel que soit l’endroit où les données sont stockées ou avec qui elles sont partagées. Les étiquettes persistantes incluent des marquages visuels comme des en-têtes, des pieds de page ou des filigranes. Des métadonnées sont ajoutées aux fichiers et aux en-têtes des messages en texte clair afin que les autres services (tels que les solutions de prévention de perte de données) puissent identifier la classification et prendre les mesures appropriées. 

Par exemple, le message suivant a été classifié comme « Interne ». Cette étiquette est ajoutée à l’e-mail en tant que pied de page ; grâce à cet indicateur visuel, tous les destinataires savent que l’e-mail est destiné à un usage interne et qu’il ne doit pas être envoyé à l’extérieur de l’organisation. Cette étiquette est également incorporée aux en-têtes d’e-mail afin que les services d’e-mail puissent inspecter cette valeur et éventuellement créer une entrée d’audit ou empêcher son envoi à l’extérieur de l’organisation.

![Exemple d’en-têtes et de pied de page d’e-mail montrant la classification Azure Information Protection](../media/example-email-footer-header.png)


## <a name="how-data-is-protected"></a>Comment les données sont protégées

La technologie de protection utilise *Azure Rights Management* (ou Azure RMS, dans sa forme abrégée courante). Cette technologie est intégrée à d’autres services cloud et applications Microsoft, tels qu’Office 365 et Azure Active Directory. Vous pouvez aussi l’utiliser avec vos propres applications métier et avec les solutions de protection des informations d’autres éditeurs de logiciels, que ces applications et solutions soient locales ou dans le cloud.

Cette technologie de protection utilise des stratégies de chiffrement, d’identité et d’autorisation. À l’image des étiquettes permanentes, la protection appliquée avec Rights Management reste associée aux documents et aux e-mails, indépendamment de leur emplacement, dans ou en dehors de votre organisation, de vos réseaux, de vos serveurs de fichiers et de vos applications. Cette solution de protection des informations vous permet de garder le contrôle de vos données, même quand vous les partagez avec d'autres personnes.

Par exemple, vous pouvez configurer un document (rapport, feuille de calcul de prévision de ventes, etc.) pour qu’il soit accessible uniquement par les personnes de votre organisation et déterminer s’il peut être modifié, s’il est disponible en lecture seule uniquement ou empêcher son impression. Vous pouvez configurer des messages électroniques de la même façon, et de plus, empêcher leur transfert ou l'utilisation de l'option Répondre à tous. Ces tâches de protection peuvent être simplifiées et rationalisées à l’aide de *modèles de gestion des droits*.

### <a name="rights-management-templates"></a>Modèles de gestion des droits

Dès que vous activez le service Azure Rights Management, deux modèles par défaut sont automatiquement créés qui restreignent l’accès aux données aux utilisateurs appartenant à votre organisation. Vous pouvez utiliser ces modèles pour empêcher immédiatement une fuite des données hors de votre organisation. Vous pouvez également compléter ces modèles par défaut en configurant vos propres modèles personnalisés qui appliquent des contrôles plus restrictifs.

Ces modèles peuvent faire partie de la configuration d’une étiquette ; ainsi, quand une étiquette spécifique est appliquée à un document (ou à un e-mail), les données sont automatiquement classifiées et protégées. Les modèles peuvent également être sélectionnés par les utilisateurs ou les administrateurs dans les produits et services qui prennent en charge la technologie Azure Rights Management.

Cet exemple montre comment vous pouvez sélectionner un modèle pour une étiquette quand vous configurez la stratégie Azure Information Protection à partir du portail Azure :

![Exemple de sélection de modèles dans le portail Azure](../media/info-protect-template-callout.png)

Les mêmes modèles peuvent être sélectionnés à partir du centre d’administration Exchange pour configurer des règles de flux de messagerie Exchange Online, qui prennent en charge la technologie Azure Rights Management :

![Exemple de sélection de modèles pour Exchange Online](../media/templates-exchangeonline-callouts.png)

Pour plus d’informations sur la protection Azure Rights Management, consultez [Qu’est-ce qu’Azure Rights Management ?](what-is-azure-rms.md)

## <a name="integration-with-end-user-workflows"></a>Intégration aux workflows de l’utilisateur final

Azure Information Protection s’intègre aux workflows existants des utilisateurs finaux quand le client Azure Information Protection est installé. Ce client installe la barre Information Protection dans les applications Office, illustrée dans la première image. La même barre est ajoutée à Excel, PowerPoint et Outlook. Exemple :

![Exemple de la barre Azure Information Protection dans Excel](../media/excel2016-infoprotect-bar.png)

Cette barre Information Protection permet aux utilisateurs finaux de sélectionner des étiquettes pour définir la classification adéquate et, si nécessaire, ces étiquettes peuvent protéger automatiquement leurs documents et e-mails.

Pour classifier et protéger d’autres types de fichiers et pour prendre en charge plusieurs fichiers à la fois, les utilisateurs peuvent cliquer avec le bouton droit sur les fichiers ou sur un dossier à partir de l’Explorateur de fichiers Windows :

![Menu contextuel de l’Explorateur de fichiers, Classifier et protéger avec Azure Information Protection](../media/right-click-classify-protect-folder.png)

Lorsque les utilisateurs sélectionnent l’option **Classifier et protéger**dans l’Explorateur de fichiers, ils peuvent ensuite sélectionner une étiquette de la même façon qu’ils utilisent la barre Information Protection dans leurs applications de bureau Office. Ils peuvent également définir leurs propres autorisations personnalisées, si nécessaire.

Les utilisateurs avancés (et administrateurs) peuvent trouver l’utilisation des commandes PowerShell plus efficace pour la gestion et la configuration de la classification et de la protection de plusieurs fichiers. Les commandes PowerShell correspondantes sont incluses automatiquement avec le client, bien que vous puissiez également installer le module PowerShell séparément.

Après qu’un document a été protégé, les utilisateurs et administrateurs peuvent utiliser un site de suivi des documents pour surveiller qui accède à ces documents et à quel moment. En outre, s’ils suspectent une utilisation incorrecte, ils peuvent révoquer l’accès à ces documents :

![Icône Révoquer l’accès du site de suivi de document](../media/tracking-site-revoke-access-icon.png)


## <a name="resources-for-azure-information-protection"></a>Ressources pour Azure Information Protection

- Annonce : [Azure Information Protection est maintenant mis à la disposition générale](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/04/azure-information-protection-is-now-generally-available/)

- Version d’évaluation gratuite : [Enterprise Mobility + Security E5](https://portal.office.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)

- Téléchargement du client : [Client Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018)

- FAQ : [Forum aux questions sur Azure Information Protection](../get-started/faqs.md)

- Yammer : [Azure Information Protection](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all)

- Vidéo de présentation

    <iframe width="560" height="315" src="https://www.youtube.com/embed/N9Ip0m6d3G0" frameborder="0" allowfullscreen></iframe>

    De plus, Microsoft Ignite 2016 propose plusieurs sessions à la demande pour Azure Information Protection :

    - [BRK2127: Adopt a comprehensive identity-driven solution for protecting and sharing data securely (Adopter une solution complète basée sur les identités pour protéger et partager des données en toute sécurité)](https://myignite.microsoft.com/videos?q=BRK2127)
    
    - [THR2107: Collaborate securely using Azure Information Protection (Collaborer en toute sécurité à l’aide d’Azure Information Protection)](https://myignite.microsoft.com/videos?q=THR2107)
    
    - [THR2108: Ensure comprehensive protection of your data with Azure Information Protection (Garantir une protection complète de vos données avec Azure Information Protection)](https://myignite.microsoft.com/videos?q=THR2108)
    
    - [BRK3095: Learn how classification, labeling, and protection delivers persistent data protection (Découvrir comment la classification, l’étiquetage et la protection offrent une protection des données persistantes)](https://myignite.microsoft.com/videos?q=BRK3095)
    
    - [BRK2128: Send secure email to anyone with the power of Microsoft Office 365 and Azure Information Protection (Envoyer un e-mail sécurisé à l’aide de la puissance de Microsoft Office 365 et d’Azure Information Protection)](https://myignite.microsoft.com/videos?q=BRK2128)


## <a name="next-steps"></a>Étapes suivantes

Configurez et découvrez Azure Information Protection par vous-même avec notre [Didacticiel de démarrage rapide pour Azure Information Protection](../get-started/infoprotect-quick-start-tutorial.md) en cinq étapes.

Vous connaissez Azure Information Protection ou Azure Rights Management sous un autre nom ? Consultez [notre liste d’autres termes pour le service](azure-rms-aka.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Feb17_HO4-->


