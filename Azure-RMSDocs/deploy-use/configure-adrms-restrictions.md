---
title: "Restrictions liées à HYOK | Azure Information Protection"
description: Identify the limitations, prerequisites, and recommendations if you select AD RMS protection with Azure Information Protection. This solution is sometimes referred to as "hold your own key" (HYOK).
manager: mbaldwin
ms.date: 10/10/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 7667b5b0-c2e9-4fcf-970f-05577ba51126
translationtype: Human Translation
ms.sourcegitcommit: 821f4c0bfbad4c88bea0fbe26807f8e50677069b
ms.openlocfilehash: 44a7dc786b678844e58f2a60204853d86c8750a7


---

# HYOK (conservez votre propre clé) : exigences et restrictions pour la protection AD RMS

>*S’applique à : Azure Information Protection*

**[Cette fonctionnalité est toujours à un stade préliminaire, et les informations sont susceptibles d’évoluer. ]**

La protection de vos documents et e-mails les plus sensibles passe généralement par l’application d’une protection Azure Rights Management. Cette dernière offre les avantages suivants :

- Aucune infrastructure serveur n’est exigée, ce qui rend la solution plus rapide et plus économique à déployer et à gérer qu’une solution locale.

- Simplification du partage avec les partenaires et les utilisateurs d’autres organisations à l’aide de l’authentification basée sur le cloud.

- Intégration étroite aux services Office 365, notamment la recherche, les visionneuses de web, les vues croisées dynamiques, les logiciels anti-programme malveillant, eDiscovery et Delve.

- Suivi et révocation des documents, et notification par e-mail en cas de partage de documents sensibles.

Azure RMS protège les documents et e-mails de votre organisation à l’aide d’une clé privée qui est gérée par Microsoft (défaut) ou vous-même (scénario « apportez votre propre clé » ou BYOK). Les informations que vous protégez avec Azure RMS ne sont jamais envoyées dans le cloud. Les documents et e-mails ne sont pas stockés dans Azure, sauf si vous les stockez explicitement dans Azure ou que vous utilisez un autre service cloud qui les stocke dans Azure. Pour plus d’informations sur les options de clé de locataire, consultez [Planification et implémentation de la clé de locataire Azure Rights Management](../plan-design/plan-implement-tenant-key.md). 

Toutefois, il peut être nécessaire pour certains clients de protéger une partie de leurs documents et e-mails à l’aide d’une clé hébergée localement, par exemple pour des raisons de conformité et de respect de la réglementation. 

Cette configuration, parfois appelée HYOK (« conservez votre propre clé »), est prise en charge par Azure Information Protection quand vous avez un déploiement Active Directory Rights Management Services (AD RMS) fonctionnel qui répond aux exigences décrites dans la section suivante. Cette fonctionnalité se trouve toujours à un stade préliminaire.

Dans ce scénario HYOK, les stratégies de droits et la clé privée de l’organisation qui protège ces stratégies sont gérées et conservées au niveau local, tandis que la stratégie Azure Information Protection pour l’étiquetage et la classification est gérée et stockée dans Azure. Comme pour la protection Azure RMS, les informations que vous protégez avec AD RMS ne sont jamais envoyées dans le cloud.

> [!NOTE]
> Utilisez uniquement cette configuration quand cela est nécessaire et limitez-la aux documents et e-mails qui l’exigent. La protection AD RMS ne fournit pas les avantages associés à la protection Azure RMS. Son objectif est plutôt d’offrir « l’opacité des données à tout prix ».

Les utilisateurs ne peuvent pas faire la distinction entre une étiquette qui utilise la protection AD RMS et une autre qui utilise la protection Azure RMS. En raison des restrictions associées à la protection AD RMS, veillez à indiquer clairement quand les utilisateurs doivent sélectionner des étiquettes qui appliquent la protection AD RMS.

## Limitations lors de l’utilisation de HYOK

En plus de ne pas prendre en charge les avantages associés à l’utilisation de la protection Azure RMS, l’utilisation conjuguée d’AD RMS et d’Azure Information Protection s’accompagne des limitations suivantes :

- Absence de prise en charge d’Office 2010 ou Office 2007.

- Si vous utilisez aussi la protection Azure RMS : n’utilisez pas l’option **Ne pas transférer** quand vous configurez une étiquette pour la protection Azure RMS. Vous devez aussi demander aux utilisateurs de ne pas sélectionner manuellement cette option dans Outlook. 

    Si l’option Ne pas transférer est appliquée par une étiquette ou manuellement par les utilisateurs, l’option risque d’être appliquée par votre déploiement AD RMS, et non par le service de gestion des droits Azure voulu. Dans ce scénario, les personnes extérieures avec qui vous partagez ne pourront pas ouvrir les messages électroniques auxquels cette option Ne pas transférer a été appliquée.

## Exigences liées à HYOK

Vérifiez que votre déploiement AD RMS répond aux exigences suivantes pour fournir la protection AD RMS pour Azure Information Protection.

- Configuration d’AD RMS :
    
    - Version minimale de Windows Server 2012 R2 : obligatoire pour les environnements de production, mais à des fins de test ou d’évaluation, vous pouvez utiliser une version minimale de Windows Server 2008 R2 avec Service Pack 1.
    
    - Cluster racine AD RMS unique.
    
    - [Mode de chiffrement 2](https://technet.microsoft.com/library/hh867439.aspx) : vous pouvez vérifier la version du mode de chiffrement du cluster AD RMS et son intégrité globale en utilisant l’outil [RMS Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=46437).   
    
    - Les serveurs AD RMS sont configurés pour utiliser SSL/TLS avec un certificat x.509 valide qui est approuvé par les clients qui se connectent : obligatoire pour les environnements de production, mais non obligatoire à des fins de test ou d’évaluation.
    
    - Modèles de droits configurés.

- La synchronisation d’annuaires est configurée entre votre annuaire Active Directory local et votre annuaire Azure Active Directory, et les utilisateurs qui utilisent la protection AD RMS sont configurés pour l’authentification unique.

- Si vous partagez des documents ou des e-mails protégés par AD RMS avec des personnes extérieures à votre organisation : AD RMS est configuré pour des approbations définies explicitement dans une relation de point à point directe avec les autres organisations à l’aide de domaines d’utilisateurs approuvés ou d’approbations fédérées créés à l’aide des services de fédération Active Directory (AD FS).

- Les utilisateurs exécutent Office 2013 Pro Plus avec Service 1 ou Office 2016 Pro Plus sur Windows 7 Service Pack 1 ou version ultérieure. Notez qu’Office 2010 et Office 2007 ne sont pas pris en charge dans ce scénario.

> [!IMPORTANT]
> Pour assurer le haut niveau de garantie de ce scénario, placez de préférence vos serveurs AD RMS à l’extérieur de votre réseau de périmètre et faites-en sorte qu’ils soient uniquement utilisés par des ordinateurs bien gérés (et non, par exemple, par des appareils mobiles ou des ordinateurs de groupe de travail). 
> 
> Nous recommandons également que votre cluster AD RMS utilise un HSM, pour que la clé privée de votre certificat de licence serveur ne puisse pas être exposée ou volée en cas de violation ou de compromission de la sécurité de votre déploiement AD RMS. 

Pour obtenir des informations et des instructions sur le déploiement pour AD RMS, consultez [Services AD RMS (Active Directory Rights Management Services)](https://technet.microsoft.com/library/hh831364.aspx) dans la bibliothèque Windows Server. 


## Recherche d’informations pour spécifier la protection AD RMS avec une étiquette Azure Information Protection

Quand vous configurez une étiquette pour la protection AD RMS, vous devez spécifier le GUID du modèle et l’URL de licence de votre cluster AD RMS. Vous trouverez ces deux valeurs dans la console AD RMS (Active Directory Rights Management Services) :

- Pour trouver le GUID du modèle : développez le cluster, puis cliquez sur **Modèles de stratégies de droits**. Vous pouvez ensuite copier le GUID des informations **Modèles de stratégies de droits distribués** à partir du modèle à utiliser. Par exemple : 82bf3474-6efe-4fa1-8827-d1bd93339119

- Pour trouver l’URL de licence : cliquez sur le nom du cluster. Dans **Détails du cluster**, copiez la valeur **Gestion des licences** valeur sans la chaîne **/_wmcs/licensing**. Par exemple : https://rmscluster.contoso.com 
    
    Si vous disposez d’une valeur de licence extranet et d’une valeur de licence intranet qui sont différentes : spécifiez uniquement la valeur extranet si vous souhaitez partager des documents ou des e-mails protégés avec des partenaires définis avec des approbations point à point explicites. Sinon, utilisez la valeur intranet et vérifiez que tous les ordinateurs clients qui utilisent la protection AD RMS avec Azure Information Protection se connectent au moyen d’une connexion intranet (par exemple, les ordinateurs distants utilisent une connexion VPN).

## Étapes suivantes

Pour plus d’informations sur cette fonctionnalité en préversion, consultez l’annonce sur le billet de blog [Azure Information Protection with HYOK (Hold Your Own Key)](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/10/azure-information-protection-with-hyok-hold-your-own-key/).

Pour configurer une étiquette pour la protection AD RMS, consultez [Comment configurer une étiquette pour appliquer la protection Rights Management](../deploy-use/configure-policy-protection.md). 



<!--HONumber=Oct16_HO2-->


