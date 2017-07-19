---
title: "Configurer une étiquette Azure Information Protection à des fins de protection"
description: "Vous pouvez protéger vos documents et e-mails les plus sensibles lorsque vous configurez une étiquette, de façon à utiliser la protection offerte par Rights Management."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/05/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: df26430b-315a-4012-93b5-8f5f42e049cc
ms.openlocfilehash: f5c4e2f7513832a884820ec0c57c7da2dec5f04e
ms.sourcegitcommit: 8b768e7e249e124f24acdf630d165eaf743f9c21
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/05/2017
---
# <a name="how-to-configure-a-label-for-rights-management-protection"></a>Comment configurer une étiquette pour la protection offerte par Rights Management

>*S’applique à : Azure Information Protection*

Vous pouvez protéger vos documents et e-mails les plus sensibles à l’aide d’un service Rights Management qui utilise des stratégies de chiffrement, d’identité et d’autorisation pour éviter la perte de données. Cette protection est appliquée lorsque vous configurez une étiquette de manière à utiliser un modèle Rights Management pour les documents et e-mails, ou l’option **Ne pas transférer** pour les messages électroniques de Microsoft Outlook. 

Il peut s’agir de l’un des modèles par défaut créés automatiquement lorsque vous activez Azure Rights Management, ou d’un modèle personnalisé. Les modèles pour services Azure Rights Management sont pris en charge, mais appliquent la protection uniquement lorsque l’auteur du document ou de l’e-mail figure dans l’étendue configurée du modèle. Si l’utilisateur n’y figure pas, il reçoit un message indiquant qu’Azure Information Protection ne peut pas appliquer l’étiquette.

## <a name="how-the-protection-works"></a>Fonctionnement de la protection

Quand un document ou un e-mail est protégé par Rights Management, il est chiffré au repos et en transit et peut uniquement être déchiffré par les utilisateurs autorisés. Ce chiffrement est conservé avec le document ou l’e-mail, même si ce dernier est renommé. En outre, vous pouvez configurer des droits d’utilisation et des restrictions, comme dans les exemples suivants :

- Seuls les utilisateurs de votre organisation peuvent ouvrir le document ou l’e-mail confidentiel de l’entreprise.

- Seuls les utilisateurs du service marketing peuvent modifier et imprimer le document ou l’e-mail d’annonce de la promotion. Tous les autres utilisateurs de votre organisation peuvent uniquement lire le document ou l’e-mail.

- Les utilisateurs ne peuvent pas transférer un e-mail ou copier des informations s’y trouvant si des informations sur une réorganisation interne s’y trouvent.

- Il est impossible d’ouvrir la liste de prix actuelle envoyée à des partenaires commerciaux après une date spécifiée.

Pour plus d’informations sur les modèles Azure Rights Management et la façon de les configurer dans le portail Azure Classic, consultez [Configuration de modèles personnalisés pour le service Azure Rights Management](../deploy-use/configure-custom-templates.md).

Pour plus d’informations sur Azure Rights Management et son fonctionnement, consultez [Qu'est-ce qu'Azure Rights Management ?](../understand-explore/what-is-azure-rms.md)

> [!IMPORTANT]
> Pour configurer une étiquette pour appliquer la protection Azure Rights Management, le service Azure Rights Management doit être activé pour votre organisation. Si vous ne le n’avez pas déjà fait, consultez [Activation d'Azure Rights Management](../deploy-use/activate-service.md).

Exchange ne doit pas être configuré pour IRM (Information Rights Management, Gestion des droits relatifs à l'information) avant que les utilisateurs ne puissent appliquer des étiquettes dans Outlook pour protéger leurs e-mails. Toutefois, vous n’obtiendrez pas toutes les fonctionnalités de la protection Azure Rights Management avec Exchange jusqu'à ce qu’Exchange soit configuré pour IRM. Par exemple, les utilisateurs ne seront pas en mesure d’afficher des e-mails protégés sur un téléphone mobile ou la version web d’Outlook. Les e-mails protégés ne peuvent pas être indexés pour la recherche, et vous ne pourrez pas configurer DLP Exchange Online pour la protection Rights Management. Consultez les ressources suivantes pour configurer Exchange de manière à prendre en charge ces scénarios supplémentaires :

- Pour Exchange Online, consultez les instructions figurant dans [Exchange Online : configuration de la gestion des droits relatifs à l'information](../deploy-use/configure-office365.md#exchange-online-irm-configuration).

- Pour Exchange sur site, vous devez déployer le [connecteur RMS et configurer vos serveurs Exchange](../deploy-use/deploy-rms-connector.md). 


## <a name="to-configure-a-label-for-rights-management-protection"></a>Configurer une étiquette pour la protection Rights Management

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur de la sécurité ou administrateur général, puis accédez au panneau **Azure Information Protection**. 

    Par exemple, dans le menu du hub, cliquez sur **Autres services** et commencez à taper **Information** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. Si l’étiquette à configurer s’applique à tous les utilisateurs, sélectionnez **Global** dans le panneau **Azure Information Protection**. Par contre, si l’étiquette à configurer se trouve dans une [stratégie délimitée](configure-policy-scope.md) pour qu’elle s’applique uniquement aux utilisateurs sélectionnés, choisissez plutôt la stratégie délimitée en question.

3. Dans le panneau **Stratégie**, sélectionnez l’étiquette que vous souhaitez configurer. Le panneau **Étiquette** s’ouvre. 

4. Dans le panneau **Étiquette**, recherchez la zone **Définir des autorisations pour les documents et les e-mails contenant cette étiquette** et sélectionnez l’une des options suivantes.
    
    - **Non configuré** : sélectionnez cette option si l’étiquette est actuellement configurée pour appliquer la protection et que vous ne voulez plus qu’elle le fasse. Passez ensuite à l'étape 11.
    
    - **Protéger** : sélectionnez cette option pour appliquer la protection, puis passez à l’étape 5.
    
    - **Supprimer la protection** : sélectionnez cette option pour supprimer la protection si elle est configurée pour un document ou un e-mail. Passez ensuite à l'étape 11.
        
        Remarque : les utilisateurs doivent disposer des autorisations nécessaires pour pouvoir supprimer la protection Rights Management et appliquer une étiquette associée à cette option. Cette option implique que l’utilisateur dispose du [droit d’utilisation](../deploy-use/configure-usage-rights.md) **Exporter** ou **Contrôle total**, ou qu’il soit propriétaire de Rights Management (ce qui accorde automatiquement le droit d’utilisation Contrôle total), ou encore qu’il soit un [super utilisateur dans Azure Rights Management](../deploy-use/configure-super-users.md). Les modèles Azure Rights Management par défaut n’incluent pas les droits d’utilisation qui permettent aux utilisateurs de supprimer la protection. 
        
        Si les utilisateurs ne disposent pas des autorisations nécessaires pour supprimer la protection Rights Management et qu’ils sélectionnent une étiquette configurée avec l’option **Supprimer la protection**, ils reçoivent le message suivant : **Azure Information Protection ne peut pas appliquer cette étiquette. Si le problème persiste, contactez votre administrateur.**

5. Si vous avez sélectionné **Protéger**, sélectionnez maintenant **Protection** pour ouvrir le panneau **Protection** :
    
    ![Configurer la protection d’une étiquette Azure Information Protection](../media/info-protect-protection-bar.png)

6. Dans le panneau **Protection**, sélectionnez **Azure RMS** ou **HYOK (AD RMS)**. 
    
    Dans la plupart des cas, vous devrez sélectionner **Azure RMS** pour vos paramètres d’autorisation. Ne sélectionnez **HYOK (AD RMS)** que si vous avez lu et compris les prérequis et les restrictions qui accompagnent cette configuration « *conservez votre propre clé* » (HYOK, hold your own key). Pour plus d’informations, consultez [HYOK (conservez votre propre clé) : exigences et restrictions pour la protection AD RMS](configure-adrms-restrictions.md). Pour poursuivre la configuration de la fonction HYOK (AD RMS), passez à l’étape 10.
    
7. Sélectionnez l’une des options suivantes :
    
    - **Ne pas transférer** : pour définir cette option d’Outlook pour les messages électroniques.
    
    - **Sélectionner un modèle prédéfini** : utilisez un des modèles par défaut ou un modèle personnalisé que vous avez configuré.
    
    - **Définir des autorisations (version préliminaire)** pour définir de nouveaux paramètres de protection dans ce portail.

8. Si vous avez choisi **Sélectionner un modèle prédéfini** pour **Azure RMS**, cliquez sur la zone de liste déroulante et sélectionnez le [modèle](../deploy-use/configure-custom-templates.md) à utiliser pour protéger les documents et les e-mails avec cette étiquette.
    
    Si vous sélectionnez un **modèle de service** ou que vous avez configuré des [contrôles d’intégration](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) :
    
    - Les utilisateurs en dehors de l’étendue configurée du modèle ou qui sont exclus de l’application de la protection d’Azure Rights Management continuent de voir l’étiquette, mais ne peuvent pas l’appliquer. S’ils sélectionnent l’étiquette, ils voient le message suivant : **Azure Information Protection ne peut pas appliquer cette étiquette. Si le problème persiste, contactez votre administrateur.**
    
        Notez que tous les modèles sont toujours affichés, même si vous configurez une stratégie délimitée. Par exemple, vous configurez une stratégie délimitée au groupe Marketing. Les modèles Azure RMS que vous pouvez sélectionner ne se limitent pas aux modèles délimités au groupe Marketing et il est possible de sélectionner un modèle de service que les utilisateurs sélectionnés ne peuvent pas utiliser. Pour faciliter la configuration et minimiser la résolution des problèmes, envisagez d’attribuer le même nom au modèle de service et à l’étiquette de votre stratégie délimitée. 
            
9. Si vous avez sélectionné **Définir des autorisations (version préliminaire)** pour **Azure RMS**, cette option a la plupart des options de configuration pour les [modèles personnalisés](configure-custom-templates.md) que vous pouvez configurer dans le portail Azure Classic. Par ailleurs, vous pouvez facilement ajouter tous les utilisateurs de votre organisation, et spécifier les adresses e-mail externes pour des utilisateurs individuels ou des groupes, ou pour tous les utilisateurs d’une autre organisation quand vous spécifiez un nom de domaine. 
    
    Pour plus d’informations sur la configuration de cette préversion, consultez le billet de blog [Azure Information Protection unified administration now in Preview](https://blogs.technet.microsoft.com/enterprisemobility/2017/04/26/azure-information-protection-unified-administration-now-in-preview/). 
    
    Pour plus d’informations sur les autorisations disponibles, consultez [Configuration des droits d’utilisation pour Azure Rights Management](configure-usage-rights.md).
    
    Avec l’option **Définir les autorisations (version préliminaire)**, vérifiez si vous voulez apporter des modifications aux paramètres suivants. Notez que ces paramètres, comme avec les autorisations, ne s’appliquent pas à [l’émetteur ou au propriétaire de Rights Management](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner), ou n’importe quel [superutilisateur](configure-super-users.md) que vous avez affecté.
    
    |Paramètre|Plus d'informations|Paramètre recommandé
    |-----------|--------------------|--------------------|
    |**expiration du contenu**|Définissez une date ou un nombre de jours après lesquels les documents ou messages protégés par le modèle ne devront plus s'ouvrir. Vous pouvez spécifier une date ou un nombre de jours à partir du moment où la protection est appliquée au contenu.<br /><br />Lorsque vous spécifiez une date, celle-ci prend effet à minuit, dans votre fuseau horaire actuel.|**Le contenu n’expire jamais**, sauf s'il comporte une spécification de durée.|
    |**Autoriser l’accès hors connexion**|Utilisez ce paramètre pour équilibrer les éventuelles exigences de sécurité que vous avez (dont l’accès après la révocation) avec la possibilité pour les utilisateurs sélectionnés d’ouvrir du contenu protégé lorsqu’ils ne disposent pas d’une connexion Internet.<br /><br />Si vous spécifiez que le contenu n’est pas disponible sans connexion Internet ou que ce contenu est uniquement disponible pendant un nombre de jours spécifié, quand ce seuil est atteint, ces utilisateurs doivent s’authentifier à nouveau et leur accès est journalisé. Dans ce cas, si leurs informations d’identification ne sont pas mises en cache, les utilisateurs sont invités à se connecter préalablement pour pouvoir ouvrir le ou e-mail.<br /><br />En plus d’une nouvelle authentification, la stratégie et l’appartenance au groupe d’utilisateurs sont réévaluées. Cela signifie que les utilisateurs peuvent accéder de nouveau ou ne plus accéder à un même document ou e-mail si des modifications ont été apportées à la stratégie ou à l'appartenance au groupe depuis leur dernier accès. Cela peut inclure l’absence d’accès si le document a été [révoqué](../rms-client/client-track-revoke.md).|En fonction de la sensibilité du contenu :<br /><br />- **Nombre de jours pendant lesquels le contenu est disponible sans connexion Internet** = **7** pour les données métier sensibles pouvant nuire à l’entreprise si elles sont partagées avec des personnes non autorisées. Cette recommandation offre un compromis entre sécurité et flexibilité. Il peut s’agir entre autres de contrats, de rapports de sécurité, de résumés de prévision et de données commerciales.<br /><br />- **Jamais** pour les données d’entreprise très sensibles qui pourraient provoquer des dommages à l’activité si elles étaient partagées avec des personnes non autorisées. Cette recommandation donne la priorité à la sécurité par rapport à la souplesse et garantit que si le document est révoqué, tous les utilisateurs autorisés perdent instantanément la possibilité d’ouvrir le document. Il s'agit entre autres d'informations sur les clients et les employés, les mots de passe, le code source et des rapports financiers préalablement annoncés.|
    
    Ce regroupement de paramètres crée un modèle personnalisé pour le service Azure Rights Management. Ces modèles peuvent être utilisés avec les applications et services qui s’intègrent à Azure Rights Management. Pour plus d’informations sur la façon dont les ordinateurs et les services téléchargent et actualisent ces modèles, consultez [Actualisation des modèles pour les utilisateurs et services](refresh-templates.md).

10. Si vous avez sélectionné **Sélectionner un modèle** pour **HYOK (AD RMS)** : indiquez le GUID du modèle et l’URL de licence de votre cluster AD RMS. [Plus d’informations](configure-adrms-restrictions.md#locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label)

11. Cliquez sur **Terminé** pour fermer le panneau **Protection** et voir apparaître la valeur que vous avez choisie pour **Ne pas transférer** ou le modèle que vous avez sélectionné pour l’option **Protection** dans le panneau **Étiquette**.

12. Dans le panneau **Étiquette**, cliquez sur **Enregistrer**.

13. Pour que les utilisateurs puissent voir ces modifications, cliquez dans le panneau **Azure Information Protection** sur **Publier**.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]