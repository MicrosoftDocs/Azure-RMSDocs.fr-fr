---
title: Configurer une étiquette Azure Information Protection à des fins de protection – AIP
description: Vous pouvez protéger vos documents et e-mails les plus sensibles lorsque vous configurez une étiquette, de façon à utiliser la protection offerte par Rights Management.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: df26430b-315a-4012-93b5-8f5f42e049cc
ms.openlocfilehash: 1e37b45cb6894ddee9630f53c52018f8a0956357
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "62772577"
---
# <a name="how-to-configure-a-label-for-rights-management-protection"></a>Comment configurer une étiquette pour la protection offerte par Rights Management

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Instructions pour : [Client Azure Information Protection pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Vous pouvez protéger vos documents et e-mails les plus sensibles à l’aide d’un service Rights Management. Ce service utilise des stratégies de chiffrement, d’identité et d’autorisation pour vous aider à éviter les pertes de données. La protection est appliquée quand une étiquette est configurée de manière à utiliser la protection Rights Management pour les documents et les e-mails. Les utilisateurs peuvent aussi sélectionner l’option **Ne pas transférer** dans Outlook.

Quand votre étiquette est configurée avec le paramètre de protection **Azure (clé cloud)**, en arrière-plan, cette action crée et configure un modèle de protection qui est ensuite accessible pour les services et applications qui sont intégrés aux modèles Rights Management. Par exemple, Exchange Online et les règles de flux d’e-mail et Outlook sur le web. 

## <a name="how-the-protection-works"></a>Fonctionnement de la protection

Quand un document ou un e-mail est protégé par un service Rights Management, il est chiffré au repos et en transit. Il peut ensuite être uniquement déchiffré par les utilisateurs autorisés. Ce chiffrement est conservé avec le document ou l’e-mail, même si ce dernier est renommé. En outre, vous pouvez configurer des droits d’utilisation et des restrictions, comme dans les exemples suivants :

- Seuls les utilisateurs de votre organisation peuvent ouvrir le document ou l’e-mail confidentiel de l’entreprise.

- Seuls les utilisateurs du service marketing peuvent modifier et imprimer le document ou l’e-mail d’annonce de la promotion. Tous les autres utilisateurs de votre organisation peuvent uniquement lire le document ou l’e-mail.

- Les utilisateurs ne peuvent pas transférer un e-mail ou copier des informations s’y trouvant si des informations sur une réorganisation interne s’y trouvent.

- Il est impossible d’ouvrir la liste de prix actuelle envoyée à des partenaires commerciaux après une date spécifiée.

Pour plus d’informations sur la protection Azure Rights Management et son fonctionnement, consultez [Qu’est-ce qu’Azure Rights Management ?](what-is-azure-rms.md)

> [!IMPORTANT]
> Pour configurer une étiquette pour appliquer cette protection, le service Azure Rights Management doit être activé pour votre organisation. Pour plus d’informations, consultez [Activation d’Azure Rights Management](activate-service.md).

Quand l’étiquette applique une protection, il n’est pas approprié d’enregistrer un document protégé sur SharePoint ou OneDrive. Ces emplacements ne prennent pas en charge les fonctionnalités suivantes pour les fichiers protégés : Co-création, Office Online, recherche, aperçu du document, miniature, eDiscovery et protection contre la perte de données. 

Exchange ne doit pas être configuré pour Azure Information Protection avant que les utilisateurs ne puissent appliquer des étiquettes dans Outlook pour protéger leurs e-mails. Toutefois, tant qu’Exchange n’est pas configuré pour Azure Information Protection, vous n’obtenez pas toutes les fonctionnalités de la protection Azure Rights Management avec Exchange. Par exemple, les utilisateurs ne peuvent pas afficher des e-mails protégés sur un téléphone mobile ou dans la version web d’Outlook. Les e-mails protégés ne peuvent pas être indexés pour la recherche et vous ne pouvez pas configurer la DLP Exchange Online pour la protection Rights Management. Pour qu’Exchange puisse prendre en charge ces scénarios supplémentaires, consultez les ressources suivantes :

- Pour Exchange Online, consultez les instructions figurant dans [Exchange Online : Configuration de la Gestion des droits relatifs à l’information](configure-office365.md#exchangeonline-irm-configuration).

- Pour Exchange sur site, vous devez déployer le [connecteur RMS et configurer vos serveurs Exchange](deploy-rms-connector.md). 

## <a name="to-configure-a-label-for-protection-settings"></a>Pour configurer une étiquette pour les paramètres de protection

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au panneau **Azure Information Protection**. 
    
    Par exemple, dans le menu hub, cliquez sur **Tous les services** et tapez **Informations** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. À partir de l’option de menu **Classifications** > **Étiquettes** : Dans le panneau **Azure Information Protection - Étiquettes**, sélectionnez l’étiquette que vous voulez changer. 

3. Dans le panneau **Étiquette**, recherchez la zone **Définir des autorisations pour les documents et les e-mails contenant cette étiquette**, puis sélectionnez une des options suivantes :
    
    - **Non configuré** : Sélectionnez cette option si l’étiquette est actuellement configurée pour appliquer la protection et que vous ne voulez plus qu’elle le fasse. Passez ensuite à l'étape 11.
        
        Les paramètres de protection précédemment configurés sont conservés sous la forme de modèle de protection archivé et réapparaissent si vous redéfinissez l’option sur **Protéger**. Vous ne voyez pas ce modèle dans le portail Azure, mais si besoin, vous pouvez toujours le gérer à l’aide de [PowerShell](configure-templates-with-powershell.md). Ce comportement signifie que le contenu reste accessible s’il a cette étiquette avec les paramètres de protection appliqués précédemment.
        
        Quand une étiquette avec ce paramètre de protection **Non configuré** est appliqué :
        
         - Si le contenu a été précédemment protégé sans utiliser une étiquette, cette protection est conservée. 
         
         - Si le contenu a été précédemment protégé avec une étiquette, cette protection est supprimée si l’utilisateur appliquant l’étiquette a les autorisations pour supprimer la protection Rights Management. Cela signifie que l’utilisateur doit avoir le [droit d’utilisation](configure-usage-rights.md) **Exporter** ou **Contrôle total**, ou qu’il doit être le propriétaire Rights Management (ce qui accorde automatiquement le droit d’utilisation Contrôle total), ou être un [super utilisateur dans Azure Rights Management](configure-super-users.md).
             
             Si l’utilisateur ne dispose des autorisations pour supprimer la protection, l’étiquette ne peut pas être appliquée et le message suivant s’affiche : **Azure Information Protection ne peut pas appliquer cette étiquette. Si ce problème persiste, contactez votre administrateur**. 
    
    - **Protéger** : Sélectionnez cette option pour appliquer la protection, puis passez à l’étape 4.
    
    - **Supprimer la protection** : Sélectionnez cette option pour supprimer la protection si un document ou un e-mail est protégé. Passez ensuite à l'étape 11.
        
        Si la protection a été appliquée avec un modèle d’étiquette ou de protection, les paramètres de protection sont conservés sous la forme d’un modèle de protection archivé et réapparaissent si vous redéfinissez l’option sur **Protéger**. Vous ne voyez pas ce modèle dans le portail Azure, mais si besoin, vous pouvez toujours le gérer à l’aide de [PowerShell](configure-templates-with-powershell.md). Ce comportement signifie que le contenu reste accessible s’il a cette étiquette avec les paramètres de protection appliqués précédemment.
        
        Notez que pour qu’un utilisateur puisse appliquer une étiquette avec cette option, il doit avoir les autorisations nécessaires pour supprimer la protection Rights Management. Cela signifie que l’utilisateur doit avoir le [droit d’utilisation](configure-usage-rights.md) **Exporter** ou **Contrôle total**, ou qu’il doit être le propriétaire Rights Management (ce qui accorde automatiquement le droit d’utilisation Contrôle total), ou être un [super utilisateur dans Azure Rights Management](configure-super-users.md). 
        
        Si l’utilisateur appliquant l’étiquette avec ce paramètre n’a pas les autorisations pour supprimer la protection Rights Management, l’étiquette ne peut pas être appliquée et le message suivant s’affiche : **Azure Information Protection ne peut pas appliquer cette étiquette. Si le problème persiste, contactez votre administrateur.**

4. Si vous avez sélectionné **Protéger**, le panneau **Protection** s’ouvre automatiquement si une des autres options a été sélectionnée précédemment. Si ce nouveau panneau ne s’ouvre pas automatiquement, sélectionnez **Protection** :
    
    ![Configurer la protection d’une étiquette Azure Information Protection](./media/info-protect-protection-bar-configured.png)

5. Dans le panneau **Protection**, sélectionnez **Azure (clé du cloud)** ou **HYOK (AD RMS)**.
    
    Dans la plupart des cas, sélectionnez **Azure (clé du cloud)** pour vos paramètres d’autorisation. Ne sélectionnez **HYOK (AD RMS)** que si vous avez lu et compris les prérequis et les restrictions qui accompagnent cette configuration « *conservez votre propre clé* » (HYOK, hold your own key). Pour plus d’informations, consultez [HYOK (conservez votre propre clé) : exigences et restrictions pour la protection AD RMS](configure-adrms-restrictions.md). Pour poursuivre la configuration de la fonction HYOK (AD RMS), passez à l’étape 9.
    
6. Sélectionnez l’une des options suivantes :
    
   - **Définir des autorisations** : Permet de définir de nouveaux paramètres de protection dans ce portail.
    
   - **Configurer les autorisations définies par l’utilisateur (préversion)** : Permet aux utilisateurs de spécifier qui doit avoir des autorisations et quelles sont ces autorisations. Vous pouvez ensuite affiner cette option et choisir Outlook uniquement ou Word, Excel, PowerPoint et l’Explorateur de fichiers. Cette option n’est pas prise en charge et ne fonctionne pas quand une étiquette est configurée pour une [classification automatique](configure-policy-classification.md).
        
       Si vous choisissez l’option pour Outlook : L’étiquette est affichée dans Outlook et le comportement obtenu lorsque les utilisateurs appliquent l’étiquette est identique à celui de l’option [Ne pas transférer](configure-usage-rights.md#do-not-forward-option-for-emails).
        
       Si vous choisissez l’option pour Word, Excel, PowerPoint et l’Explorateur de fichiers : Lorsque cette option est définie, l’étiquette est affichée dans ces applications. Le comportement obtenu quand les utilisateurs appliquent l’étiquette affiche la boîte de dialogue pour permettre aux utilisateurs de sélectionner des autorisations personnalisées. Dans cette boîte de dialogue, les utilisateurs choisissent l’un des [niveaux d’autorisation prédéfinis](configure-usage-rights.md#rights-included-in-permissions-levels), accèdent aux utilisateurs ou groupes, ou les spécifient, et s’ils le souhaitent, définissent une date d’expiration. Vérifiez que les utilisateurs disposent des instructions et des conseils qui permettent de fournir ces valeurs.
    
   - **Sélectionner un modèle prédéfini** : Utilisez un des modèles par défaut ou un modèle personnalisé que vous avez configuré. Notez que cette option ne s’affiche pas pour les nouvelles étiquettes si vous modifiez une étiquette qui utilisait l’option **Définir les autorisations**.
    
     Pour sélectionner un modèle prédéfini, le modèle doit être publié (pas archivé) et ne pas être déjà lié à une autre étiquette. Quand vous sélectionnez cette option, vous pouvez utiliser un bouton **Modifier le modèle** pour [convertir le modèle en étiquette](configure-policy-templates.md#to-convert-templates-to-labels).
    
     Si vous avez l’habitude de créer et de modifier des modèles personnalisés, il peut s’avérer utile de consulter [Tâches que vous aviez l’habitude d’effectuer avec le portail Azure Classic](migrate-portal.md).

7. Si vous avez sélectionné **Définir les autorisations** pour **Azure (clé cloud)**, cette option vous permet de sélectionner des utilisateurs et droits d’utilisation. 
    
    Si vous ne sélectionnez pas d’utilisateurs, puis cliquez successivement sur **OK** dans ce panneau et sur **Enregistrer** dans le panneau **Étiquette** : L’étiquette est configurée pour appliquer une protection telle que seule la personne qui applique l’étiquette peut ouvrir le document ou l’e-mail sans aucune restriction. Cette configuration est parfois appelée « Pour moi uniquement » et peut être le résultat requis, afin qu’un utilisateur puisse enregistrer un fichier à n’importe quel emplacement et être assuré d’être le seul à pouvoir l’ouvrir. Si ce résultat correspond à vos besoins et qu’aucun autre utilisateur n’est tenu de collaborer sur le contenu protégé, ne sélectionnez pas **Ajouter des autorisations**. Après que vous avez enregistré l’étiquette, à la prochaine ouverture de ce panneau **Protection**, **IPC_USER_ID_OWNER** est affiché pour **Utilisateurs**, et **Copropriétaire** est affiché pour **Autorisations** afin de refléter cette configuration.
    
    Pour spécifier les utilisateurs que vous souhaitez voir en mesure d’ouvrir des documents et e-mails protégés, sélectionnez **Ajouter des autorisations**. Dans le panneau **Ajouter des autorisations**, sélectionnez le premier ensemble d’utilisateurs et de groupes qui disposeront des droits d’utilisation du contenu qui sera protégé par l’étiquette sélectionnée :
    
   - Choisissez **Sélectionner dans la liste**, où vous pouvez alors ajouter tous les utilisateurs de votre organisation en sélectionnant **Ajouter \<nom de l’organisation > - Tous les membres**. Ce paramètre exclut les comptes invités. Vous pouvez également sélectionner **Ajouter tous les utilisateurs authentifiés** ou parcourir le répertoire.
        
       Lorsque vous choisissez tous les membres ou que vous parcourez le répertoire, les utilisateurs ou les groupes doivent avoir une adresse e-mail. Dans un environnement de production, les utilisateurs et les groupes ont presque toujours une adresse e-mail, mais dans un simple environnement de test, vous devrez peut-être ajouter des adresses e-mail aux comptes d’utilisateur ou aux groupes.
        
       ###### <a name="more-information-about-add-any-authenticated-users"></a>Informations supplémentaires sur **Ajouter tous les utilisateurs authentifiés** 
       Ce paramètre ne restreint pas l’accès au contenu protégé par l’étiquette, tout en chiffrant le contenu et en vous proposant des options permettant de limiter la façon d’accéder au contenu (expiration et l’accès hors connexion) et l’utilisation qui peut en être faite (autorisations). Toutefois, l’application qui ouvre le contenu protégé doit être en mesure de prendre en charge l’authentification utilisée. Pour cette raison, les fournisseurs de réseaux sociaux fédérés, tels que Google, et l’authentification unique par code secret doivent être utilisés uniquement pour les e-mails, et seulement lorsque vous utilisez Exchange Online et les nouvelles fonctionnalités de chiffrement de messages Office 365. Les comptes Microsoft peuvent être utilisées avec la visionneuse Azure Information Protection et avec les applications Office 365 (Démarrer en un clic). 
          
       Quelques scénarios classiques pour la définition des utilisateurs authentifiés :
       - Tout le monde peut consulter le contenu, mais vous souhaitez imposer des restrictions à son utilisation. Par exemple, vous ne souhaitez pas que le contenu soit modifié, copié ou imprimé.
       - Vous n’avez pas besoin de restreindre l’accès au contenu, mais vous souhaitez savoir qui l’ouvre et, éventuellement, le révoquer.
       - Vous voulez que le contenu soit chiffré au repos et en transit, mais aucun contrôle d’accès n’est nécessaire.
        
   - Choisissez **Entrer les détails** pour spécifier manuellement des adresses e-mail pour les utilisateurs individuels ou les groupes (internes ou externes). Vous pouvez utiliser cette option pour spécifier tous les utilisateurs d’une autre organisation en entrant un nom de domaine de cette organisation. Vous pouvez aussi utiliser cette option pour les fournisseurs de réseaux sociaux, en entrant leur nom de domaine comme **gmail.com**, **hotmail.com** ou **outlook.com**.
        
     >[!NOTE]
     >Si une adresse e-mail est modifiée une fois que vous avez sélectionné l’utilisateur ou le groupe, consultez la section [Éléments à prendre en considération en cas de modification des adresses de messagerie](prepare.md#considerations-for-azure-information-protection-if-email-addresses-change) de la documentation relative à la planification.
    
     Au titre de bonne pratique, utilisez des groupes plutôt que des utilisateurs. Cette stratégie permet d’avoir une configuration plus simple et rend moins probable le besoin de mettre à jour par la suite votre configuration d’étiquettes et la reprotection du contenu. Toutefois, si vous apportez des modifications à ce groupe, n’oubliez pas que pour des raisons de performances, Azure Rights Management [met en cache l’appartenance au groupe](prepare.md#group-membership-caching-by-azure-information-protection). 
    
     Quand vous avez spécifié le premier ensemble d’utilisateurs et de groupes, sélectionnez les autorisations à leur accorder. Pour plus d’informations sur les autorisations disponibles, consultez [Configuration des droits d’utilisation pour Azure Rights Management](configure-usage-rights.md). Cependant, la manière dont les applications qui prennent en charge cette protection implémentent ces autorisations peut varier. Consultez la documentation des applications et testez vous-mêmes celles dont les utilisateurs se servent afin de vérifier leur comportement avant de déployer le modèle pour les utilisateurs.
    
     Si nécessaire, vous pouvez maintenant ajouter un deuxième ensemble d’utilisateurs et de groupes avec des droits d’utilisation. Répétez cette opération jusqu’à avoir spécifié tous les utilisateurs et les groupes avec leurs autorisations respectives.

     >[!TIP]
     >Ajoutez l’autorisation personnalisée **Enregistrer sous, Exporter (EXPORTER)** et accordez-la à des administrateurs de récupération de données ou à d’autres personnes dans l’entreprise ayant la responsabilité de récupérer des informations. Si nécessaire, ces utilisateurs peuvent alors supprimer la protection des fichiers et des e-mails qui seront protégés à l’aide de cette étiquette ou de ce modèle. Cette possibilité de supprimer la protection au niveau des autorisations pour un document ou un e-mail offre un contrôle plus précis que la [fonctionnalité de super utilisateur](configure-super-users.md).
    
     Pour tous les utilisateurs et les groupes que vous avez spécifiés dans le panneau **Protection**, vérifiez maintenant si des modifications doivent être apportées aux paramètres suivants. Notez que ces paramètres, comme avec les autorisations, ne s’appliquent pas à [l’émetteur ou au propriétaire de Rights Management](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner), ou n’importe quel [super utilisateur](configure-super-users.md) que vous avez affecté.
    
     ###### <a name="information-about-the-protection-settings"></a>Informations sur les paramètres de protection
    
     |Paramètre|Plus d’informations|Paramètre recommandé
     |-----------|--------------------|--------------------|
     |**Expiration du contenu du fichier**|Définissez une date ou un nombre de jours limite pour l’ouverture par les utilisateurs sélectionnés des documents protégés par ces paramètres. Pour les e-mails, l’expiration n’est pas toujours appliquée en raison des mécanismes de mise en cache utilisés par certains clients de messagerie.<br /><br />Vous pouvez spécifier une date ou un nombre de jours à partir du moment où la protection est appliquée au contenu.<br /><br />Lorsque vous spécifiez une date, celle-ci prend effet à minuit, dans votre fuseau horaire actuel.|**Le contenu n’expire jamais**, sauf s'il comporte une spécification de durée.|
     |**Autoriser l’accès hors connexion**|Utilisez ce paramètre pour équilibrer les éventuelles exigences de sécurité que vous avez (dont l’accès après la révocation) avec la possibilité pour les utilisateurs sélectionnés d’ouvrir du contenu protégé lorsqu’ils ne disposent pas d’une connexion Internet.<br /><br />Si vous spécifiez que le contenu n’est pas disponible sans connexion Internet ou que ce contenu est disponible seulement pour un nombre de jours spécifié, quand ce seuil est atteint, ces utilisateurs doivent se réauthentifier et leur accès est journalisé. Dans ce cas, si leurs informations d’identification ne sont pas mises en cache, les utilisateurs sont invités à se connecter préalablement pour pouvoir ouvrir le ou e-mail.<br /><br />En plus de la réauthentification, la stratégie et l’appartenance au groupe d’utilisateurs sont réévaluées. Cela signifie que les utilisateurs peuvent accéder de nouveau ou ne plus accéder à un même document ou e-mail si des modifications ont été apportées à la stratégie ou à l'appartenance au groupe depuis leur dernier accès. Cela peut inclure l’absence d’accès si le document a été [révoqué](./rms-client/client-track-revoke.md).|En fonction de la sensibilité du contenu :<br /><br />- **Nombre de jours pendant lesquels le contenu est disponible sans connexion Internet** = **7** pour les données métier sensibles pouvant nuire à l’entreprise si elles sont partagées avec des personnes non autorisées. Cette recommandation offre un compromis entre sécurité et flexibilité. Il peut s’agir entre autres de contrats, de rapports de sécurité, de résumés de prévision et de données commerciales.<br /><br />- **Jamais** pour les données d’entreprise très sensibles qui pourraient provoquer des dommages à l’activité si elles étaient partagées avec des personnes non autorisées. Cette recommandation donne la priorité à la sécurité par rapport à la souplesse et garantit que si le document est révoqué, tous les utilisateurs autorisés perdent instantanément la possibilité d’ouvrir le document. Il s'agit entre autres d'informations sur les clients et les employés, les mots de passe, le code source et des rapports financiers préalablement annoncés.|
    
     Une fois terminée la configuration des autorisations et des paramètres, cliquez sur **OK**. 
    
     Ce regroupement de paramètres crée un modèle personnalisé pour le service Azure Rights Management. Ces modèles peuvent être utilisés avec les applications et services qui s’intègrent à Azure Rights Management. Pour plus d’informations sur la façon dont les ordinateurs et les services téléchargent et actualisent ces modèles, consultez [Actualisation des modèles pour les utilisateurs et services](refresh-templates.md).

8. Si vous avez choisi **Sélectionner un modèle prédéfini** pour **Azure (clé du cloud)**, cliquez sur la zone de liste déroulante, puis sélectionnez le [modèle](configure-policy-templates.md) à utiliser pour protéger les documents et les e-mails avec cette étiquette. Vous ne voyez pas les modèles archivés ou les modèles qui sont déjà sélectionnés pour une autre étiquette.
    
    Si vous sélectionnez un **modèle de service** ou que vous avez configuré des [contrôles d’intégration](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) :
    
    - Les utilisateurs en dehors de l’étendue configurée du modèle ou qui sont exemptés de l’application de la protection Azure Rights Management continuent de voir l’étiquette, mais ne peuvent pas l’appliquer. S’ils sélectionnent l’étiquette, ils voient le message suivant : **Azure Information Protection ne peut pas appliquer cette étiquette. Si le problème persiste, contactez votre administrateur.**
        
        Notez que tous les modèles publiés sont toujours affichés, même si vous configurez une stratégie délimitée. Par exemple, vous configurez une stratégie délimitée au groupe Marketing. Les modèles que vous pouvez sélectionner ne se limitent pas aux modèles délimités au groupe Marketing, et il est possible de sélectionner un modèle de service que les utilisateurs sélectionnés ne peuvent pas utiliser. Pour faciliter la configuration et minimiser la résolution des problèmes, envisagez d’attribuer le même nom au modèle de service et à l’étiquette de votre stratégie délimitée. 

9. Si vous avez sélectionné **HYOK (AD RMS)**, sélectionnez **Définir les détails des modèles AD RMS** ou **Configurer des autorisations définies par l’utilisateur (préversion)**. Ensuite, spécifiez l’URL de licence de votre cluster AD RMS.
    
    Pour obtenir des instructions afin de spécifier un GUID de modèle et votre URL de licence, consultez [Recherche d’informations pour spécifier la protection AD RMS avec une étiquette Azure Information Protection](configure-adrms-restrictions.md#locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label).
    
    L’option de configuration des autorisations définies par l’utilisateur permet aux utilisateurs de spécifier qui doit avoir des autorisations et quelles sont ces autorisations. Vous pouvez ensuite affiner cette option et choisir Outlook uniquement (la valeur par défaut) ou Word, Excel, PowerPoint et l’Explorateur de fichiers. Cette option n’est pas prise en charge et ne fonctionne pas quand une étiquette est configurée pour une [classification automatique](configure-policy-classification.md).
    
    Si vous choisissez l’option pour Outlook : L’étiquette est affichée dans Outlook et le comportement obtenu lorsque les utilisateurs appliquent l’étiquette est identique à celui de l’option [Ne pas transférer](configure-usage-rights.md#do-not-forward-option-for-emails).
    
    Si vous choisissez l’option pour Word, Excel, PowerPoint et l’Explorateur de fichiers : Lorsque cette option est définie, l’étiquette est affichée dans ces applications. Le comportement obtenu quand les utilisateurs appliquent l’étiquette affiche la boîte de dialogue pour permettre aux utilisateurs de sélectionner des autorisations personnalisées. Dans cette boîte de dialogue, les utilisateurs choisissent l’un des [niveaux d’autorisation prédéfinis](configure-usage-rights.md#rights-included-in-permissions-levels), accèdent aux utilisateurs ou groupes, ou les spécifient, et s’ils le souhaitent, définissent une date d’expiration. Vérifiez que les utilisateurs disposent des instructions et des conseils qui permettent de fournir ces valeurs.

10. Cliquez sur **OK** pour fermer le panneau **Protection** et voir apparaître la valeur que vous avez choisie pour **Ne pas transférer** ou le modèle que vous avez sélectionné pour l’option **Protection** dans le panneau **Étiquette**.

11. Dans le panneau **Étiquette**, cliquez sur **Enregistrer**.

12. Dans le panneau **Azure Information Protection**, utilisez la colonne **PROTECTION** pour vérifier que votre étiquette affiche maintenant le paramètre de protection souhaité :
    
    - Une coche si vous avez configuré la protection. 
    
    - Une croix (x) pour désigner l’annulation si vous avez configuré une étiquette pour supprimer la protection.
    
    - Champ vide quand la protection n’est pas définie. 

Une fois que vous avez cliqué sur **Enregistrer**, vos modifications sont automatiquement disponibles pour les utilisateurs et les services. Il n’y a plus d’option de publication distincte.


## <a name="example-configurations"></a>Exemples de configurations

Les sous-étiquettes **Tous les employés** et **Destinataires uniquement** des étiquettes **Confidentiel** et **Hautement confidentiel** de la [stratégie par défaut](configure-policy-default.md) fournissent des exemples de configurations d’étiquettes qui appliquent une protection. Vous pouvez également utiliser les exemples suivants pour vous aider à configurer la protection pour différents scénarios. 

Pour chaque exemple qui suit, dans votre panneau \<*nom d’étiquette*>, sélectionnez **Protéger**. Si le panneau **Protection** ne s’ouvre pas automatiquement, sélectionnez **Protection** pour l’ouvrir afin de sélectionner les options de configuration de protection :

![Configuration d’une étiquette Azure Information Protection à des fins de protection](./media/info-protect-protection-bar-configured.png)

### <a name="example-1-label-that-applies-do-not-forward-to-send-a-protected-email-to-a-gmail-account"></a>Exemple 1 : Étiquette qui applique Ne pas transférer pour envoyer un e-mail protégé à un compte Gmail

Cette étiquette est uniquement disponible dans Outlook et convient quand Exchange Online est configuré pour les [nouvelles fonctionnalités dans Chiffrement de messages Office 365](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e). Demandez aux utilisateurs de sélectionner cette étiquette quand ils ont besoin d’envoyer un e-mail protégé à des personnes qui utilisent un compte Gmail (ou tout autre compte e-mail à l’extérieur de votre organisation). 

Vos utilisateurs tapent l’adresse e-mail Gmail dans la zone **À**.  Ensuite, ils sélectionnent l’étiquette et l’option Ne pas transférer est automatiquement ajoutée à l’e-mail. Par conséquent, les destinataires ne peuvent pas transférer l’e-mail, ni l’imprimer, le copier, enregistrer des pièces jointes ou enregistrer l’e-mail sous un autre nom. 

1. Dans le panneau **Protection**, vérifiez que l’option **Azure (clé du cloud)** est sélectionnée.
    
2. Sélectionnez **Configurer les autorisations définies par l’utilisateur (préversion)**.

3. Vérifiez que l’option suivante est sélectionnée : **Dans Outlook appliquer Ne pas transférer**.

4. Si l’option suivante est cochée, décochez-la : **Dans Word, Excel, PowerPoint et l’Explorateur de fichiers, demander à l’utilisateur des autorisations personnalisées**.

5. Cliquez sur **OK** dans le panneau **Protection**, puis sur **Enregistrer** dans le panneau **Étiquette**.


### <a name="example-2-label-that-restricts-read-only-permission-to-all-users-in-another-organization-and-that-supports-immediate-revocation"></a>Exemple 2 : Étiquette qui limite l’autorisation de lecture seule à tous les utilisateurs d’une autre organisation et qui prend en charge une révocation immédiate

Cette étiquette convient au partage des documents très sensibles (en lecture seule) qui exigent toujours une connexion Internet pour les afficher. Si l’autorisation est révoquée, les utilisateurs ne sont plus en mesure d’afficher le document la prochaine fois qu’ils tentent de l’ouvrir.

Cette étiquette ne convient pas aux e-mails.

1. Dans le panneau **Protection**, vérifiez que l’option **Azure (clé du cloud)** est sélectionnée.
    
2. Vérifiez que l’option **Définir les autorisations** est sélectionnée, puis sélectionnez **Ajouter des autorisations**.

3. Dans le panneau **Ajouter des autorisations**, sélectionnez **Entrez les détails**.

4. Entrez le nom d’un domaine de l’autre organisation, par exemple, **fabrikam.com**. Puis sélectionnez **Ajouter**.

5. Dans **Choisir des autorisations à partir des autorisations prédéfinies**, sélectionnez **Observateur**, puis sélectionnez **OK**.

6. De retour dans le panneau **Protection**, pour le **paramètre Autoriser l’accès hors connexion**, sélectionnez **Jamais**.

7. Cliquez sur **OK** dans le panneau **Protection**, puis sur **Enregistrer** dans le panneau **Étiquette**.


### <a name="example-3-add-external-users-to-an-existing-label-that-protects-content"></a>Exemple 3 : Ajouter des utilisateurs externes à une étiquette existante qui protège le contenu

Les nouveaux utilisateurs que vous ajoutez seront en mesure d’ouvrir les documents et e-mails qui ont déjà été protégés avec cette étiquette. Les autorisations que vous accordez à ces utilisateurs peuvent être différentes de celles des utilisateurs existants.

1. Dans le panneau **Protection**, vérifiez que l’option **Azure (clé cloud)** est sélectionnée.
    
2. Vérifiez que l’option **Définir les autorisations** est sélectionnée, puis sélectionnez **Ajouter des autorisations**.

3. Dans le panneau **Ajouter des autorisations**, sélectionnez **Entrez les détails**.

4. Entrez l’adresse e-mail du premier utilisateur (ou groupe) à ajouter, puis sélectionnez **Ajouter**.

5. Sélectionnez les autorisations de cet utilisateur (ou groupe).

6. Répétez les étapes 4 et 5 pour chaque utilisateur (ou groupe) à ajouter à cette étiquette. Cliquez sur **OK**.

7. Cliquez sur **OK** dans le panneau **Protection**, puis sur **Enregistrer** dans le panneau **Étiquette**.

### <a name="example-4-label-for-protected-email-that-supports-less-restrictive-permissions-than-do-not-forward"></a>Exemple 4 : Étiquette pour des e-mails protégés qui prend en charge des autorisations moins restrictives que l’option Ne pas transférer

Cette étiquette ne peut pas être limitée à Outlook, mais elle fournit des contrôles moins restrictifs que l’option Ne pas transférer. Par exemple, vous voulez que les destinataires puissent copier du contenu de l’e-mail ou d’une pièce jointe, ou qu’ils puissent enregistrer et modifier une pièce jointe.

Si vous spécifiez des utilisateurs externes ne possédant pas de compte dans Azure AD :

- Cette étiquette peut être utilisée pour les-mails si Exchange Online utilise les [nouvelles fonctionnalités dans Chiffrement des messages Office 365](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e). 
 
- Les pièces jointes Office qui sont protégées automatiquement peuvent être affichées dans un navigateur. Pour modifier ces documents, après les avoir téléchargés, modifiez-les à l’aide des applications Office 365 (Démarrer en un clic) et d’un compte Microsoft qui utilise la même adresse e-mail. [Plus d’informations](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)


> [!NOTE]
> Exchange Online déploie actuellement une nouvelle option appelée [Chiffrement seul](configure-usage-rights.md#encrypt-only-option-for-emails). Cette option n'est pas disponible pour la configuration des étiquettes. Toutefois, lorsque vous savez qui seront les destinataires, vous pouvez utiliser cet exemple pour configurer une étiquette avec le même ensemble de droits d’utilisation. 

Lorsque vos utilisateurs spécifient les adresses e-mail dans la zone **À**, celles-ci doivent correspondre aux mêmes utilisateurs que ceux que vous spécifiez pour cette configuration d’étiquette. Étant donné que les utilisateurs peuvent appartenir à des groupes et avoir plusieurs adresses e-mail, celle qu’ils spécifient ne doit pas nécessairement correspondre exactement à l’adresse e-mail que vous spécifiez pour les autorisations. Toutefois, l’utilisation de la même adresse e-mail est le moyen le plus simple d’être sûr que le destinataire est autorisé. Pour plus d’informations sur la façon dont les utilisateurs reçoivent les autorisations, consultez [Préparation des utilisateurs et groupes pour Azure Information Protection](prepare.md). 

1. Dans le panneau **Protection**, vérifiez que l’option **Azure (clé du cloud)** est sélectionnée.
    
2. Vérifiez que l’option **Définir les autorisations** est sélectionnée, puis sélectionnez **Ajouter des autorisations**.

3. Dans le panneau **Ajouter des autorisations** : Pour accorder des autorisations aux utilisateurs de votre organisation, sélectionnez **Ajouter \<nom de l’organisation> - Tous les membres** pour sélectionner tous les utilisateurs de votre locataire. Ce paramètre exclut les comptes invités. Ou sélectionnez **Parcourir le répertoire** pour sélectionner un groupe spécifique. Pour accorder des autorisations à des utilisateurs externes ou si vous préférez taper l’adresse e-mail, sélectionnez **Entrer les détails** et tapez l’adresse e-mail de l’utilisateur, le groupe Azure AD ou un nom de domaine.
    
    Répétez cette étape pour spécifier des utilisateurs supplémentaires qui doivent avoir les mêmes autorisations.

4. Pour **Choisir des autorisations à partir des autorisations prédéfinies**, sélectionnez **Copropriétaire**, **Co-auteur**, **Réviseur** ou **Personnalisé** pour sélectionner les autorisations à accorder.
    
    Remarque : Ne sélectionnez pas **Observateur** pour les e-mails et, si vous sélectionnez **Personnalisé**, veillez à inclure **Modifier et enregistrer**.
    
    Pour sélectionner les autorisations qui correspondent à la nouvelle option **Chiffrement seul** d’Exchange Online, sélectionnez **Personnalisé**. Ensuite, sélectionnez toutes les autorisations sauf **Enregistrer sous, Exporter (EXPORT)** et **Contrôle total (OWNER)**.

5. Pour spécifier des utilisateurs supplémentaires qui doivent disposer d’autorisations différentes, répétez les étapes 3 et 4.

6. Cliquez sur **OK** dans le panneau **Ajouter des autorisations**.

7. Cliquez sur **OK** dans le panneau **Protection**, puis sur **Enregistrer** dans le panneau **Étiquette**.


### <a name="example-5-label-that-encrypts-content-but-doesnt-restrict-who-can-access-it"></a>Exemple 5 : Étiquette qui chiffre le contenu, mais n’en restreint pas l’accès

L’avantage de cette configuration est que vous n’avez pas besoin de spécifier des utilisateurs, des groupes ou des domaines pour protéger un e-mail ou un document. Le contenu sera toujours chiffré, et vous pouvez toujours spécifier des droits d’utilisation, une date d’expiration et un accès hors connexion. Utilisez cette configuration uniquement lorsque vous n’avez pas besoin de restreindre qui peut ouvrir le document ou l’e-mail protégé. [Pour plus d'informations sur ce paramètre](#more-information-about-add-any-authenticated-users)

1. Dans le panneau **Protection**, vérifiez que l’option **Azure (clé cloud)** est sélectionnée.
    
2. Vérifiez que l’option **Définir les autorisations** est sélectionnée, puis sélectionnez **Ajouter des autorisations**.

3. Dans le panneau **Ajouter des permissions**, sur l’onglet **Sélectionner dans la liste**, sélectionnez **Ajoutez des utilisateurs authentifiés**.

4. Sélectionnez les autorisations souhaitées, puis cliquez sur **OK**.

5. De retour dans le panneau **Protection**, si nécessaire, configurez les paramètres pour **Expiration du contenu du fichier** et **Autoriser l’accès hors connexion**, puis cliquez sur **OK**.

6. Dans le panneau **Étiquette**, sélectionnez **Enregistrer**.


### <a name="example-6-label-that-applies-just-for-me-protection"></a>Exemple 6 : Étiquette qui applique une protection « Pour moi uniquement »

Cette configuration offre l’opposé de la collaboration sécurisée pour les documents : À l’exception d’un [super utilisateur](configure-super-users.md), seule la personne qui applique l’étiquette peut ouvrir le contenu protégé, sans aucune restriction. Cette configuration est souvent appelée « Pour moi uniquement » et convient quand un utilisateur veut enregistrer un fichier à n’importe quel emplacement et être assuré d’être le seul à pouvoir l’ouvrir.

La configuration de l’étiquette est extrêmement simple :

1. Dans le panneau **Protection**, vérifiez que l’option **Azure (clé cloud)** est sélectionnée.
    
2. Sélectionnez **OK** sans sélectionner aucun utilisateur ou sans configurer aucun paramètre dans ce panneau.
    
    Même si vous pouvez configurer des paramètres pour **Expiration du contenu du fichier** et **Autoriser l’accès hors connexion**, quand vous ne spécifiez pas d’utilisateurs et leurs autorisations, ces paramètres d’accès ne sont pas applicables. La raison en est que la personne qui applique la protection est l’[émetteur Rights Management](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner) pour le contenu et que ce rôle est exempté de ces restrictions d’accès.

3. Dans le panneau **Étiquette**, sélectionnez **Enregistrer**.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy). 

Les règles de flux de messagerie Exchange peuvent également appliquer une protection, en fonction de vos étiquettes. Pour plus d’informations et d’exemples, consultez [Configuration des règles de flux de messagerie Exchange Online pour les étiquettes Azure Information Protection](configure-exo-rules.md).  
