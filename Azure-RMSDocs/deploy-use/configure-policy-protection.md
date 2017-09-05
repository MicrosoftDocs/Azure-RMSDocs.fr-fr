---
title: "Configurer une étiquette Azure Information Protection à des fins de protection"
description: "Vous pouvez protéger vos documents et e-mails les plus sensibles lorsque vous configurez une étiquette, de façon à utiliser la protection offerte par Rights Management."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/30/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: df26430b-315a-4012-93b5-8f5f42e049cc
ms.openlocfilehash: 2f6bc027353f38e272a6765c10e770643b739d26
ms.sourcegitcommit: 13e95906c24687eb281d43b403dcd080912c54ec
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/30/2017
---
# <a name="how-to-configure-a-label-for-rights-management-protection"></a>Comment configurer une étiquette pour la protection offerte par Rights Management

>*S’applique à : Azure Information Protection*

Vous pouvez protéger vos documents et e-mails les plus sensibles à l’aide d’un service Rights Management. Ce service utilise des stratégies de chiffrement, d’identité et d’autorisation pour vous aider à éviter les pertes de données. La protection est appliquée quand vous configurez une étiquette de façon la protection Rights Management pour des documents et des e-mails, ou l’option **Ne pas transférer** pour les e-mails Outlook. 

## <a name="how-the-protection-works"></a>Fonctionnement de la protection

Quand un document ou un e-mail est protégé par Rights Management, il est chiffré au repos et en transit et peut uniquement être déchiffré par les utilisateurs autorisés. Ce chiffrement est conservé avec le document ou l’e-mail, même si ce dernier est renommé. En outre, vous pouvez configurer des droits d’utilisation et des restrictions, comme dans les exemples suivants :

- Seuls les utilisateurs de votre organisation peuvent ouvrir le document ou l’e-mail confidentiel de l’entreprise.

- Seuls les utilisateurs du service marketing peuvent modifier et imprimer le document ou l’e-mail d’annonce de la promotion. Tous les autres utilisateurs de votre organisation peuvent uniquement lire le document ou l’e-mail.

- Les utilisateurs ne peuvent pas transférer un e-mail ou copier des informations s’y trouvant si des informations sur une réorganisation interne s’y trouvent.

- Il est impossible d’ouvrir la liste de prix actuelle envoyée à des partenaires commerciaux après une date spécifiée.

Pour plus d’informations sur la protection Azure Rights Management et son fonctionnement, consultez [Qu’est-ce qu’Azure Rights Management ?](../understand-explore/what-is-azure-rms.md)

> [!IMPORTANT]
> Pour configurer une étiquette pour appliquer cette protection, le service Azure Rights Management doit être activé pour votre organisation. Si vous ne le n’avez pas déjà fait, consultez [Activation d'Azure Rights Management](../deploy-use/activate-service.md).

Quand l’étiquette applique une protection, il n’est pas approprié d’enregistrer un document protégé sur SharePoint ou OneDrive. Ces emplacements ne prennent pas en charge les fonctionnalités suivantes pour les fichiers protégés : co-édition, Office Online, recherche, aperçu du document, miniature et eDiscovery. 

Exchange ne doit pas être configuré pour IRM (Information Rights Management, Gestion des droits relatifs à l'information) avant que les utilisateurs ne puissent appliquer des étiquettes dans Outlook pour protéger leurs e-mails. Toutefois, vous n’obtiendrez pas toutes les fonctionnalités de la protection Azure Rights Management avec Exchange jusqu'à ce qu’Exchange soit configuré pour IRM. Par exemple, les utilisateurs ne seront pas en mesure d’afficher des e-mails protégés sur un téléphone mobile ou la version web d’Outlook. Les e-mails protégés ne peuvent pas être indexés pour la recherche, et vous ne pourrez pas configurer DLP Exchange Online pour la protection Rights Management. Consultez les ressources suivantes pour configurer Exchange de manière à prendre en charge ces scénarios supplémentaires :

- Pour Exchange Online, consultez les instructions figurant dans [Exchange Online : configuration de la gestion des droits relatifs à l'information](../deploy-use/configure-office365.md#exchange-online-irm-configuration).

- Pour Exchange sur site, vous devez déployer le [connecteur RMS et configurer vos serveurs Exchange](../deploy-use/deploy-rms-connector.md). 

## <a name="to-configure-a-label-for-rights-management-protection"></a>Configurer une étiquette pour la protection Rights Management

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur de la sécurité ou administrateur général. Accédez ensuite au panneau **Azure Information Protection**. 
    
    Par exemple, dans le menu du hub, cliquez sur **Autres services** et commencez à taper **Information** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. Si l’étiquette à configurer s’applique à tous les utilisateurs, restez dans le panneau **Azure Information Protection - Stratégie globale**. Toutefois, si l’étiquette à configurer se trouve dans une [stratégie délimitée](configure-policy-scope.md) pour s’appliquer uniquement aux utilisateurs sélectionnés, dans la sélection de menu **STRATÉGIES**, sélectionnez **Stratégies délimitées**. Sélectionnez ensuite votre stratégie délimitée dans le panneau **Azure Information Protection - Stratégies délimitées**.

3. Sélectionnez l’étiquette à configurer. Le panneau **Étiquette** s’ouvre. 

4. Dans le panneau **Étiquette**, recherchez la zone **Définir des autorisations pour les documents et les e-mails contenant cette étiquette** et sélectionnez une des options suivantes :
    
    - **Non configuré** : sélectionnez cette option si l’étiquette est actuellement configurée pour appliquer la protection et que vous ne voulez plus qu’elle le fasse. Passez ensuite à l'étape 11.
    
    - **Protéger** : sélectionnez cette option pour appliquer la protection, puis passez à l’étape 5.
    
    - **Supprimer la protection** : Sélectionnez cette option pour supprimer la protection si un document ou un e-mail est protégé. Passez ensuite à l'étape 11.
        
        Notez que pour que les utilisateurs puissent appliquer une étiquette avec cette option, ils doivent avoir les autorisations nécessaires pour supprimer la protection Rights Management. Cela signifie que les utilisateurs doivent avoir le [droit d’utilisation](../deploy-use/configure-usage-rights.md) **Exporter** ou **Contrôle total**. ou ils doivent être propriétaires de Rights Management (ce qui accorde automatiquement le droit d’utilisation Contrôle total), ou être un [super utilisateur dans Azure Rights Management](../deploy-use/configure-super-users.md). Les modèles Azure Rights Management par défaut n’incluent pas les droits d’utilisation qui permettent aux utilisateurs de supprimer la protection. 
        
        Si les utilisateurs n’ont pas les autorisations nécessaires pour supprimer la protection Rights Management et qu’ils sélectionnent une étiquette configurée avec l’option **Supprimer la protection**, ils reçoivent le message suivant : **Azure Information Protection ne peut pas appliquer cette étiquette. Si le problème persiste, contactez votre administrateur.**

5. Si vous avez sélectionné **Protéger**, sélectionnez maintenant **Protection** pour ouvrir le panneau **Protection** :
    
    ![Configurer la protection d’une étiquette Azure Information Protection](../media/info-protect-protection-bar-configured.png)

6. Dans le panneau **Protection**, sélectionnez **Azure RMS** ou **HYOK (AD RMS)**.     
    Pour la plupart des cas, sélectionnez **Azure RMS** pour vos paramètres d’autorisation. Ne sélectionnez **HYOK (AD RMS)** que si vous avez lu et compris les prérequis et les restrictions qui accompagnent cette configuration « *conservez votre propre clé* » (HYOK, hold your own key). Pour plus d’informations, consultez [HYOK (conservez votre propre clé) : exigences et restrictions pour la protection AD RMS](configure-adrms-restrictions.md). Pour poursuivre la configuration de la fonction HYOK (AD RMS), passez à l’étape 10.
    
7. Sélectionnez l’une des options suivantes :
    
    - **Sélectionner un modèle prédéfini** : utilisez un des modèles par défaut ou un modèle personnalisé que vous avez configuré. Ce modèle doit être publié (pas archivé) et ne doit pas être déjà lié à une autre étiquette. Quand vous sélectionnez cette option, vous pouvez utiliser le bouton **Modifier le modèle** pour [convertir le modèle en étiquette](configure-policy-templates.md#to-convert-templates-to-labels).
    
    - **Définir des autorisations** : Permet de définir de nouveaux paramètres de protection dans ce portail.
    
    - **Configurer des autorisations définies par l’utilisateur (préversion)** : Permet aux utilisateurs de spécifier qui doit avoir des autorisations et quelles sont ces autorisations. Vous pouvez ensuite affiner cette option et choisir Outlook uniquement (la valeur par défaut) ou Word, Excel, PowerPoint et l’Explorateur de fichiers. 
        
        Si vous choisissez l’option pour Outlook : l’étiquette est affichée dans Outlook et le comportement obtenu quand les utilisateurs appliquent l’étiquette est identique à celui de l’option Ne pas transférer.
        
        Si vous choisissez l’option pour Word, Excel, PowerPoint et l’Explorateur de fichiers : cette option nécessite la préversion du client Azure Information Protection. Quand cette option est définie et que les utilisateurs ont la préversion du client, l’étiquette est affichée dans ces applications. Le comportement obtenu quand les utilisateurs appliquent l’étiquette affiche la boîte de dialogue pour permettre aux utilisateurs de sélectionner des autorisations personnalisées. Dans cette boîte de dialogue, les utilisateurs doivent spécifier les autorisations, les utilisateurs ou les groupes et une date d’expiration. Vérifiez que les utilisateurs disposent des instructions et des conseils qui permettent de fournir ces valeurs.

8. Si vous avez choisi **Sélectionner un modèle prédéfini** pour **Azure RMS**, cliquez sur la zone de liste déroulante et sélectionnez le [modèle](../deploy-use/configure-policy-templates.md) à utiliser pour protéger les documents et les e-mails avec cette étiquette. Vous ne voyez pas les modèles archivés ou les modèles qui sont déjà sélectionnés pour une autre étiquette.
    
    Si vous sélectionnez un **modèle de service** ou que vous avez configuré des [contrôles d’intégration](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) :
    
    - Les utilisateurs en dehors de l’étendue configurée du modèle ou qui sont exclus de l’application de la protection d’Azure Rights Management continuent de voir l’étiquette, mais ne peuvent pas l’appliquer. S’ils sélectionnent l’étiquette, ils voient le message suivant : **Azure Information Protection ne peut pas appliquer cette étiquette. Si le problème persiste, contactez votre administrateur.**
        
        Notez que tous les modèles publiés sont toujours affichés, même si vous configurez une stratégie délimitée. Par exemple, vous configurez une stratégie délimitée au groupe Marketing. Les modèles Azure RMS que vous pouvez sélectionner ne se limitent pas aux modèles délimités au groupe Marketing, et il est possible de sélectionner un modèle de service que les utilisateurs sélectionnés ne peuvent pas utiliser. Pour faciliter la configuration et minimiser la résolution des problèmes, envisagez d’attribuer le même nom au modèle de service et à l’étiquette de votre stratégie délimitée. 
            
9. Si vous avez sélectionné **Définir les autorisations** pour **Azure RMS**, cette option vous permet de configurer les mêmes paramètres que ceux que vous pouvez configurer dans un modèle. 
    
    Sélectionnez **Ajouter des autorisations** puis, dans le panneau **Ajouter des autorisations**, sélectionnez le premier ensemble d’utilisateurs et de groupes qui auront des droits d’utilisation du contenu à protéger par l’étiquette sélectionnée :
    
    - Choisissez **Sélectionner dans la liste** pour ajouter tous les utilisateurs de votre organisation ou parcourez l’annuaire.
        
        Les utilisateurs ou les groupes doivent avoir une adresse e-mail. Dans un environnement de production, ce sera presque toujours le cas, mais dans un simple environnement de test, il peut être nécessaire d’ajouter des adresses e-mails aux comptes d’utilisateur ou aux groupes.
        
    - Choisissez **Entrer les détails** pour spécifier manuellement des adresses e-mail pour les utilisateurs individuels ou les groupes (internes ou externes). Vous pouvez aussi spécifier tous les utilisateurs d’une autre organisation en entrant un nom de domaine de cette organisation. 
        
    >[!NOTE]
    >Si une adresse e-mail est modifiée une fois que vous avez sélectionné l’utilisateur ou le groupe, consultez la section [Éléments à prendre en considération en cas de modification des adresses de messagerie](../plan-design/prepare.md#considerations-for-azure-information-protection-if-email-addresses-change) de la documentation relative à la planification.
    
    Au titre de bonne pratique, utilisez des groupes plutôt que des utilisateurs. Cette stratégie conserve votre configuration plus simple et rend moins probable la nécessité de mettre à jour ultérieurement votre configuration d’étiquettes puis de reprotéger le contenu. Toutefois, si vous apportez des modifications à ce groupe, n’oubliez pas que pour des raisons de performances, Azure Rights Management [met en cache l’appartenance au groupe](../plan-design/prepare.md#group-membership-caching-by-azure-rights-management ). 
    
    Quand vous avez spécifié le premier ensemble d’utilisateurs et de groupes, sélectionnez les autorisations à leur accorder. Pour plus d’informations sur les autorisations disponibles, consultez [Configuration des droits d’utilisation pour Azure Rights Management](configure-usage-rights.md). Cependant, la manière dont les applications qui prennent en charge cette protection implémentent ces autorisations peut varier. Consultez la documentation des applications et testez vous-mêmes celles dont les utilisateurs se servent afin de vérifier leur comportement avant de déployer le modèle pour les utilisateurs.
    
    Si nécessaire, vous pouvez maintenant ajouter un deuxième ensemble d’utilisateurs et de groupes avec des droits d’utilisation. Répétez cette opération jusqu’à avoir spécifié tous les utilisateurs et les groupes avec leurs autorisations respectives.

    >[!TIP]
    >Vous pouvez ajouter l’autorisation personnalisée **Copier et extraire le contenu** et l’accorder à des administrateurs de récupération de données ou à du personnel occupant une autre fonction qui a la responsabilité de récupérer des informations. Si nécessaire, ces utilisateurs peuvent alors supprimer la protection des fichiers et des e-mails qui seront protégés à l’aide de cette étiquette ou de ce modèle. Cette possibilité de supprimer la protection au niveau des autorisations pour un document ou un e-mail offre un contrôle plus précis que la [fonctionnalité de super utilisateur](configure-super-users.md).
    
    Pour tous les utilisateurs et les groupes que vous avez spécifiés dans le panneau **Protection**, vérifiez maintenant si des modifications doivent être apportées aux paramètres suivants. Notez que ces paramètres, comme avec les autorisations, ne s’appliquent pas à [l’émetteur ou au propriétaire de Rights Management](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner), ou n’importe quel [super utilisateur](configure-super-users.md) que vous avez affecté.
    
    |Paramètre|Plus d'informations|Paramètre recommandé
    |-----------|--------------------|--------------------|
    |**expiration du contenu**|Définissez une date ou un nombre de jours après lesquels les documents ou messages protégés par le modèle ne devront plus s'ouvrir. Vous pouvez spécifier une date ou un nombre de jours à partir du moment où la protection est appliquée au contenu.<br /><br />Lorsque vous spécifiez une date, celle-ci prend effet à minuit, dans votre fuseau horaire actuel.|**Le contenu n’expire jamais**, sauf s'il comporte une spécification de durée.|
    |**Autoriser l’accès hors connexion**|Utilisez ce paramètre pour équilibrer les éventuelles exigences de sécurité que vous avez (dont l’accès après la révocation) avec la possibilité pour les utilisateurs sélectionnés d’ouvrir du contenu protégé lorsqu’ils ne disposent pas d’une connexion Internet.<br /><br />Si vous spécifiez que le contenu n’est pas disponible sans connexion Internet ou que ce contenu est disponible seulement pour un nombre de jours spécifié, quand ce seuil est atteint, ces utilisateurs doivent se réauthentifier et leur accès est journalisé. Dans ce cas, si leurs informations d’identification ne sont pas mises en cache, les utilisateurs sont invités à se connecter préalablement pour pouvoir ouvrir le ou e-mail.<br /><br />En plus de la réauthentification, la stratégie et l’appartenance au groupe d’utilisateurs sont réévaluées. Cela signifie que les utilisateurs peuvent accéder de nouveau ou ne plus accéder à un même document ou e-mail si des modifications ont été apportées à la stratégie ou à l'appartenance au groupe depuis leur dernier accès. Cela peut inclure l’absence d’accès si le document a été [révoqué](../rms-client/client-track-revoke.md).|En fonction de la sensibilité du contenu :<br /><br />- **Nombre de jours pendant lesquels le contenu est disponible sans connexion Internet** = **7** pour les données métier sensibles pouvant nuire à l’entreprise si elles sont partagées avec des personnes non autorisées. Cette recommandation offre un compromis entre sécurité et flexibilité. Il peut s’agir entre autres de contrats, de rapports de sécurité, de résumés de prévision et de données commerciales.<br /><br />- **Jamais** pour les données d’entreprise très sensibles qui pourraient provoquer des dommages à l’activité si elles étaient partagées avec des personnes non autorisées. Cette recommandation donne la priorité à la sécurité par rapport à la souplesse et garantit que si le document est révoqué, tous les utilisateurs autorisés perdent instantanément la possibilité d’ouvrir le document. Il s'agit entre autres d'informations sur les clients et les employés, les mots de passe, le code source et des rapports financiers préalablement annoncés.|
    
    Une fois terminée la configuration des autorisations, cliquez sur **OK**. 
    
    Ce regroupement de paramètres crée un modèle personnalisé pour le service Azure Rights Management. Ces modèles peuvent être utilisés avec les applications et services qui s’intègrent à Azure Rights Management. Pour plus d’informations sur la façon dont les ordinateurs et les services téléchargent et actualisent ces modèles, consultez [Actualisation des modèles pour les utilisateurs et services](refresh-templates.md).

10. Si vous avez sélectionné **HYOK (AD RMS)**, sélectionnez **Définir les détails des modèles AD RMS** ou **Configurer des autorisations définies par l’utilisateur (préversion)**, puis spécifiez l’URL de licence de votre cluster AD RMS.
    
    Pour obtenir des instructions afin de spécifier un GUID de modèle et votre URL de licence, consultez [Recherche d’informations pour spécifier la protection AD RMS avec une étiquette Azure Information Protection](configure-adrms-restrictions.md#locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label).
    
    Pour utiliser l’option des autorisations définies par l’utilisateur, vous devez disposer de la préversion du client Azure Information Protection. Cette option permet aux utilisateurs de spécifier qui doit avoir des autorisations et quelles sont ces autorisations. Vous pouvez ensuite affiner cette option et choisir Outlook uniquement (la valeur par défaut) ou Word, Excel, PowerPoint et l’Explorateur de fichiers. 
    
    Si vous choisissez l’option pour Outlook : l’étiquette est affichée dans Outlook et le comportement obtenu quand les utilisateurs appliquent l’étiquette est identique à celui de l’option Ne pas transférer.
    
    Si vous choisissez l’option pour Word, Excel, PowerPoint et l’Explorateur de fichiers : l’étiquette est affichée dans ces applications. Le comportement obtenu quand les utilisateurs appliquent l’étiquette affiche la boîte de dialogue pour permettre aux utilisateurs de sélectionner des autorisations personnalisées. Dans cette boîte de dialogue, les utilisateurs doivent spécifier les autorisations, les utilisateurs ou les groupes et une date d’expiration. Vérifiez que les utilisateurs disposent des instructions et des conseils qui permettent de fournir ces valeurs. Actuellement, cette option dans l’Explorateur de fichiers utilise toujours la protection Azure RMS au lieu de la protection HYOK (AD RMS).

11. Cliquez sur **Terminé** pour fermer le panneau **Protection** et voir apparaître la valeur que vous avez choisie pour **Ne pas transférer** ou le modèle que vous avez sélectionné pour l’option **Protection** dans le panneau **Étiquette**.

12. Dans le panneau **Étiquette**, cliquez sur **Enregistrer**.

13. Pour que les utilisateurs puissent voir ces modifications, cliquez dans le panneau **Azure Information Protection** sur **Publier**.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]