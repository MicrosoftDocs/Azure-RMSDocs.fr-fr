---
title: "Restrictions liées à HYOK pour Azure Information Protection"
description: "Identifiez les limitations, conditions préalables et recommandations associées à la sélection de la protection HYOK (AD RMS) avec Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/13/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 7667b5b0-c2e9-4fcf-970f-05577ba51126
ms.openlocfilehash: ef39c5489e63a67e0880e4faab4d9675a49f5f90
ms.sourcegitcommit: 4e31a4797eb8df64af3ae8932d2b49839e7a4524
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/13/2017
---
# <a name="hold-your-own-key-hyok-requirements-and-restrictions-for-ad-rms-protection"></a>HYOK (conservez votre propre clé) : exigences et restrictions pour la protection AD RMS

>*S’applique à : Azure Information Protection*

Pour protéger vos documents et e-mails les plus sensibles, vous appliquez généralement une protection Azure Rights Management (Azure RMS), qui offre les avantages suivants :

- Aucune infrastructure serveur n’est exigée, ce qui rend la solution plus rapide et plus économique à déployer et à gérer qu’une solution locale.

- Simplification du partage avec les partenaires et les utilisateurs d’autres organisations à l’aide de l’authentification basée sur le cloud.

- Intégration étroite aux services Office 365, notamment la recherche, les visionneuses de web, les vues croisées dynamiques, les logiciels anti-programme malveillant, eDiscovery et Delve.

- Suivi et révocation des documents, et notification par e-mail en cas de partage de documents sensibles.

Azure RMS protège les documents et e-mails de votre organisation à l’aide d’une clé privée qui est gérée par Microsoft (défaut) ou vous-même (scénario « apportez votre propre clé » ou BYOK). Les informations que vous protégez avec Azure RMS ne sont jamais envoyées dans le cloud. Les documents et e-mails ne sont pas stockés dans Azure, sauf si vous les stockez explicitement dans Azure ou que vous utilisez un autre service cloud qui les stocke dans Azure. Pour plus d’informations sur les options de clé de locataire, consultez [Planification et implémentation de la clé de locataire Azure Rights Management](../plan-design/plan-implement-tenant-key.md). 

Toutefois, il peut être nécessaire pour certaines organisations de protéger une partie de leurs documents et e-mails à l’aide d’une clé hébergée en local, par exemple pour des raisons de conformité et de respect de la réglementation.  

Cette configuration, parfois appelée HYOK (« conservez votre propre clé »), est prise en charge par Azure Information Protection quand vous avez un déploiement Active Directory Rights Management Services (AD RMS) fonctionnel qui répond aux exigences décrites dans la section suivante.

Dans ce scénario HYOK, les stratégies de droits et la clé privée de l’organisation qui protège ces stratégies sont gérées et conservées au niveau local, tandis que la stratégie Azure Information Protection pour l’étiquetage et la classification est gérée et stockée dans Azure. Comme pour la protection Azure RMS, les informations que vous protégez avec AD RMS ne sont jamais envoyées dans le cloud.

> [!NOTE]
> Utilisez uniquement cette configuration quand cela est nécessaire et limitez-la aux documents et e-mails qui l’exigent. La protection AD RMS ne fournit pas les avantages associés à la protection Azure RMS. Son objectif est plutôt d’offrir une « opacité des données à tout prix ».
>
> En général, cette protection convient à moins de 10 % de l’ensemble du contenu devant être protégé, même pour les organisations qui utilisent cette configuration. Nous vous conseillons de l’utiliser uniquement pour les documents ou e-mails qui correspondent à tous les critères suivants :
> 
> - Le contenu est soumis au niveau de classification le plus élevé au sein de votre organisation (« Top Secret ») et l’accès est limité à quelques personnes.
> 
> - Le contenu n’est jamais partagé en dehors de l’organisation.
> 
> - Le contenu est uniquement utilisé sur le réseau interne.
> 
> - Le contenu n’a pas besoin d’être utilisé sur des ordinateurs Mac ou des appareils mobiles.

Les utilisateurs ne sont pas en mesure de déterminer si une étiquette utilise la protection AD RMS ou la protection Azure RMS. En raison des restrictions et limitations associées à la protection AD RMS, veillez à fournir des informations précises sur les exceptions applicables lorsque les utilisateurs doivent sélectionner des étiquettes qui exécutent la protection AD RMS. 

Les [stratégies délimitées](configure-policy-scope.md) constituent un bon moyen de vous assurer que les utilisateurs qui ont besoin d’appliquer la protection AD RMS sont les seuls à voir les étiquettes configurées pour la protection AD RMS. 

## <a name="additional-limitations-when-using-hyok"></a>Limitations supplémentaires lors de l’utilisation de la solution HYOK

En plus de ne pas prendre en charge les avantages associés à l’utilisation de la protection Azure RMS, l’utilisation conjuguée d’AD RMS et d’Azure Information Protection s’accompagne des limitations suivantes :

- Absence de prise en charge d’Office 2010 ou Office 2007.

- Demandez aux utilisateurs de ne pas sélectionner **Ne pas transférer** dans Outlook ou fournissez des instructions spécifiques. 

    Même si vous pouvez configurer une étiquette pour **Ne pas transférer** afin d’utiliser HYOK ou le service Azure Rights Management, les utilisateurs peuvent également sélectionner Ne pas transférer eux-mêmes. Ils peuvent sélectionner cette option à l’aide du bouton **Ne pas transférer** sous l’onglet **Message** du ruban Office ou à l’aide des options de menu d’Outlook. Les options de menu **Ne pas transférer** sont situées sous **Fichier** > **Autorisations** et en cliquant sur le bouton **Autorisations** de l’onglet **Options** sur le ruban. 
    
    Quand les utilisateurs sélectionnent le bouton Ne pas transférer, Azure RMS ou AD RMS peut être utilisé et le choix n’est pas déterminant. Quand les utilisateurs sélectionnent **Ne pas transférer** à partir d’une option de menu Outlook, ils peuvent choisir Azure RMS ou AD RMS, mais risquent de ne pas savoir quelle option choisir pour leur e-mail. Dans les deux scénarios, si AD RMS est utilisé par erreur à la place d’Azure RMS, les personnes externes avec qui vous partagez du contenu ne peuvent pas ouvrir ces e-mails.
    
    La préversion actuelle du client Azure Information Protection utilise toujours Azure RMS quand les utilisateurs sélectionnent le bouton **Ne pas transférer** dans Outlook. Si vous ne souhaitez pas voir ce comportement, vous pouvez masquer le bouton **Ne pas transférer** dans Outlook en configurant un [paramètre client avancé](../rms-client/client-admin-guide-customizations.md#hide-the-do-not-forward-button-in-outlook). 

- Pour la version actuelle de disponibilité générale du client Azure Information Protection : si les utilisateurs configurent des autorisations personnalisées quand vous utilisez les protections Azure RMS et AD RMS (HYOK), le document ou l’e-mail est toujours protégé par Azure Rights Management. Cette limitation ne s’applique pas à la préversion actuelle du client.

- Si vous configurez des autorisations définies par l’utilisateur pour Word, Excel, PowerPoint et l’Explorateur de fichiers, ce qui est pris en charge dans la préversion actuelle du client Azure Information Protection : dans l’Explorateur de fichiers, la protection est toujours appliquée à l’aide d’Azure RMS au lieu de la protection HYOK (AD RMS). 

- Si un utilisateur choisit dans Outlook une étiquette qui applique la protection AD RMS, puis change d’avis avant d’envoyer l’e-mail et sélectionne une étiquette qui applique la protection Azure RMS, la dernière étiquette sélectionnée ne peut pas s’appliquer. Les utilisateurs voient apparaître le message d’erreur suivant : **Azure Information Protection ne peut pas appliquer cette étiquette. Vous n’avez pas l’autorisation requise pour effectuer cette action.**
    
    La seule solution de contournement consiste à fermer l’e-mail et à recommencer. La même restriction s’applique lorsque les utilisateurs commencent par choisir une étiquette qui applique la protection Azure RMS, puis la remplacent par une étiquette qui applique la protection AD RMS.

## <a name="requirements-for-hyok"></a>Exigences liées à HYOK

Vérifiez que votre déploiement AD RMS répond aux exigences suivantes pour fournir la protection AD RMS pour Azure Information Protection.

- Configuration d’AD RMS :
    
    - Version minimale de Windows Server 2012 R2 : obligatoire pour les environnements de production, mais à des fins de test ou d’évaluation, vous pouvez utiliser une version minimale de Windows Server 2008 R2 avec Service Pack 1.
    
    - Une des topologies suivantes :
        
        - Forêt unique avec un seul cluster racine AD RMS. 
        
        - Plusieurs forêts avec des clusters racines AD RMS indépendants, les utilisateurs n’ayant pas accès au contenu protégé par les utilisateurs des autres forêts.
        
        - Plusieurs forêts avec des clusters AD RMS dans chacune d’elles. Chaque cluster AD RMS partage une URL de licence qui pointe vers le même cluster AD RMS. Sur ce cluster AD RMS, vous devez importer tous les certificats de domaine utilisateur approuvé à partir de tous les autres clusters AD RMS. Pour plus d’informations concernant cette topologie, consultez [Domaine utilisateur approuvé](https://technet.microsoft.com/library/dd983944(v=ws.10\).aspx).
        
    Quand vous avez plusieurs clusters AD RMS dans des forêts distinctes, supprimez toutes les étiquettes de la stratégie globale qui appliquent la protection HYOK (AD RMS) et qui configurent une [stratégie délimitée](configure-policy-scope.md) pour chaque cluster. Affectez ensuite les utilisateurs de chaque cluster à leur stratégie délimitée, en vous assurant que vous n’utilisez pas des groupes qui entraîneraient l’affectation d’un utilisateur à plusieurs stratégies délimitées. Chaque utilisateur doit avoir des étiquettes pour un seul cluster AD RMS. 
    
    - [Mode de chiffrement 2](https://technet.microsoft.com/library/hh867439.aspx) : vous pouvez confirmer le mode en vérifiant les propriétés du cluster AD RMS, onglet **Général**.
    
    - Un point de connexion de service (SCP) n’est pas inscrit dans Active Directory : aucun SCP n’est utilisé quand vous appliquez la protection AD RMS avec Azure Information Protection. Si vous avez inscrit un SCP pour votre déploiement AD RMS, vous devez le supprimer pour que la [découverte du service](../rms-client/client-deployment-notes.md#rms-service-discovery) fonctionne pour la protection Azure Rights Management.
    
    - Les serveurs AD RMS sont configurés pour utiliser SSL/TLS avec un certificat x.509 valide qui est approuvé par les clients qui se connectent : obligatoire pour les environnements de production, mais non obligatoire à des fins de test ou d’évaluation.
    
    - Modèles de droits configurés.

- La synchronisation d’annuaires est configurée entre votre annuaire Active Directory local et votre annuaire Azure Active Directory, et les utilisateurs qui utilisent la protection AD RMS sont configurés pour l’authentification unique.

- Si vous partagez des documents ou des e-mails protégés par AD RMS avec des personnes extérieures à votre organisation : AD RMS est configuré pour des approbations définies explicitement dans une relation de point à point directe avec les autres organisations à l’aide de domaines d’utilisateurs approuvés ou d’approbations fédérées créés au moyen des services de fédération Active Directory (AD FS).

- Les utilisateurs exécutent Office 2013 Pro Plus avec Service Pack 1 ou Office 2016 Pro Plus sur Windows 7 Service Pack 1 ou version ultérieure. Notez qu’Office 2010 et Office 2007 ne sont pas pris en charge dans ce scénario.

> [!IMPORTANT]
> Pour assurer le haut niveau de garantie de ce scénario, placez de préférence vos serveurs AD RMS à l’extérieur de votre réseau de périmètre et faites-en sorte qu’ils soient uniquement utilisés par des ordinateurs bien gérés (et non, par exemple, par des appareils mobiles ou des ordinateurs de groupe de travail). 
> 
> Nous recommandons également que votre cluster AD RMS utilise un HSM, pour que la clé privée de votre certificat de licence serveur ne puisse pas être exposée ou volée en cas de violation ou de compromission de la sécurité de votre déploiement AD RMS. 

Pour obtenir des informations et des instructions sur le déploiement pour AD RMS, consultez [Services AD RMS (Active Directory Rights Management Services)](https://technet.microsoft.com/library/hh831364.aspx) dans la bibliothèque Windows Server. 


## <a name="locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label"></a>Recherche d’informations pour spécifier la protection AD RMS avec une étiquette Azure Information Protection

Quand vous configurez une étiquette pour la protection **HYOK (AD RMS)**, vous devez spécifier l’URL de licence de votre cluster AD RMS. Par ailleurs, vous devez spécifier un modèle que vous avez configuré pour les autorisations à accorder aux utilisateurs ou permettre aux utilisateurs de définir les autorisations et les utilisateurs. 

Les valeurs du GUID de modèle et de l’URL de licence sont disponibles dans la console des services AD RMS (Active Directory Rights Management Services) :

- Pour rechercher le GUID du modèle : développez le cluster, puis cliquez sur **Modèles de stratégies de droits**. Vous pouvez ensuite copier le GUID des informations **Modèles de stratégies de droits distribués** à partir du modèle à utiliser. Par exemple : 82bf3474-6efe-4fa1-8827-d1bd93339119

- Pour trouver l’URL de licence : cliquez sur le nom du cluster. Dans **Détails du cluster**, copiez la valeur **Gestion des licences** valeur sans la chaîne **/_wmcs/licensing**. Par exemple : https://rmscluster.contoso.com 
    
    Si vous disposez d’une valeur de licence extranet et d’une valeur de licence intranet différentes : spécifiez la valeur extranet uniquement si vous voulez partager des documents ou des e-mails protégés avec des partenaires qui ont été définis avec des approbations point à point explicites. Sinon, utilisez la valeur intranet et vérifiez que tous les ordinateurs clients qui utilisent la protection AD RMS avec Azure Information Protection se connectent au moyen d’une connexion intranet (par exemple, les ordinateurs distants utilisent une connexion VPN).

## <a name="next-steps"></a>Étapes suivantes

Pour en savoir plus sur cette fonctionnalité et obtenir des conseils sur son utilisation, consultez l’annonce sur le billet de blog [Azure Information Protection with HYOK (Hold Your Own Key)](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/10/azure-information-protection-with-hyok-hold-your-own-key/).

Pour savoir comment configurer une étiquette pour la protection AD RMS, voir [Comment configurer une étiquette pour la protection offerte par Rights Management](../deploy-use/configure-policy-protection.md). 

[!INCLUDE[Commenting house rules](../includes/houserules.md)]