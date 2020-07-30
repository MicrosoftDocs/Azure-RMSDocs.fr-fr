---
title: Configurer une étiquette Azure Information Protection à des fins de protection – AIP
description: Lorsque vous configurez une étiquette pour utiliser la protection de Rights Management, vous pouvez protéger vos documents et vos e-mails les plus sensibles.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: df26430b-315a-4012-93b5-8f5f42e049cc
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 141a8e6642745dc36dfd596d11b8153e20c09e69
ms.sourcegitcommit: 58e7d6e5c1cd3f21af03fe873076f282b684fd98
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87334162"
---
# <a name="how-to-configure-a-label-for-rights-management-protection"></a>Comment configurer une étiquette pour la protection de Rights Management

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Instructions pour : [Client Azure Information Protection pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Pour fournir une expérience client unifiée et rationalisée, **Azure Information Protection client (Classic)** et **Gestion des étiquettes** dans le Portail Azure sont **dépréciées** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

> [!NOTE]
> Ces instructions s’appliquent au client Azure Information Protection (classique) et pas au client d’étiquetage unifié Azure Information Protection. Vous ne connaissez pas trop la différence entre ces clients ? Consultez ce [FAQ](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients).
> 
> Si vous recherchez des informations sur la configuration d’une étiquette de sensibilité pour appliquer Rights Management protection, consultez la documentation relative à la conformité des Microsoft 365. Par exemple, [Restriction de l’accès au contenu à l’aide du chiffrement dans les étiquettes de sensibilité](/microsoft-365/compliance/encryption-sensitivity-labels).

Vous pouvez protéger vos documents et vos e-mails les plus sensibles avec le service Rights Management. Ce service utilise des stratégies de chiffrement, d’identité et d’autorisation pour empêcher la perte de données. La protection est appliquée à une étiquette qui est configurée afin d’utiliser la protection de Rights Management pour les documents et les e-mails, et les utilisateurs peuvent également cliquer sur le bouton **Ne pas transférer** dans Outlook.

Quand votre étiquette est configurée avec le paramètre de protection **Azure (clé cloud)**, en arrière-plan, cette action crée et configure un modèle de protection qui est ensuite accessible pour les services et applications qui sont intégrés aux modèles Rights Management. Par exemple, Exchange Online et les règles de flux d’e-mail et Outlook sur le web. 

## <a name="how-the-protection-works"></a>Fonctionnement de la protection

Quand un document ou un e-mail est protégé par un service Rights Management, il est chiffré au repos et en transit. Il peut ensuite être déchiffré uniquement par les utilisateurs autorisés. Ce chiffrement est conservé avec le document ou l’e-mail, même ce dernier est renommé. En outre, vous pouvez configurer les droits et restrictions d’utilisation, comme dans les exemples suivants :

- Seuls les utilisateurs au sein de votre organisation peuvent ouvrir le document ou l’e-mail confidentiel.

- Seuls les utilisateurs du service marketing peuvent modifier et imprimer le document ou l’e-mail d’annonce de promotion. Les autres utilisateurs de votre organisation peuvent uniquement lire ce document ou cet e-mail.

- Les utilisateurs ne peuvent pas transférer un e-mail ou copier des informations tirées de cet e-mail s’il contient des informations relatives à une réorganisation interne.

- La liste de tarifs en cours qui est envoyée aux partenaires commerciaux ne peut pas être ouverte après une date spécifique.

Pour plus d’informations sur la protection d’Azure Rights Management et sur son fonctionnement, consultez [Qu’est-ce qu’Azure Rights Management ?](what-is-azure-rms.md)

> [!IMPORTANT]
> Si vous souhaitez configurer une étiquette afin d’appliquer cette protection, le service Azure Rights Management doit être activé pour votre organisation. Pour plus d’informations, consultez [Activation du service de protection à partir d’Azure Information Protection](activate-service.md).

Lorsque l’étiquette applique la protection, il est impossible d’enregistrer un document protégé sur OneDrive ou SharePoint. Ces emplacements ne prennent pas en charge les fonctionnalités suivantes pour les fichiers protégés : co-création, Office pour le Web, recherche, aperçu du document, miniature, eDiscovery et protection contre la perte de données (DLP).

> [!TIP]
> Lorsque vous [migrez vos étiquettes](configure-policy-migrate-labels.md) vers des étiquettes de confidentialité unifiées et que vous les publiez à partir d’un des centres d’administration d’étiquetage tels que le Centre de conformité Microsoft 365, les étiquettes qui appliquent la protection sont alors prises en charge pour ces emplacements. Pour plus d’informations, consultez [activer les étiquettes de sensibilité pour les fichiers Office dans SharePoint et OneDrive](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files).

Exchange ne doit pas être configuré pour Azure Information Protection avant que les utilisateurs ne puissent appliquer des étiquettes dans Outlook pour protéger leurs e-mails. Toutefois, tant qu’Exchange n’est pas configuré pour Azure Information Protection, vous n’obtenez pas toutes les fonctionnalités de la protection Azure Rights Management avec Exchange. Par exemple, les utilisateurs ne peuvent pas afficher les e-mails protégés sur un téléphone mobile ou avec Outlook sur le web, les e-mails protégés ne peuvent pas être indexés pour la recherche, et vous ne pouvez pas configurer Exchange Online DLP pour la protection de Rights Management. Pour qu’Exchange puisse prendre en charge ces scénarios supplémentaires, consultez les ressources suivantes :

- Pour Exchange Online, consultez les instructions décrites dans [Exchange Online : configuration de la gestion des droits relatifs à l’information](configure-office365.md#exchangeonline-irm-configuration).

- Pour Exchange sur site, vous devez déployer le [connecteur RMS et configurer vos serveurs Exchange](deploy-rms-connector.md). 

## <a name="to-configure-a-label-for-protection-settings"></a>Pour configurer une étiquette pour les paramètres de protection

1. Si ce n’est pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au Portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au volet **Azure Information Protection**. 
    
    Par exemple, dans la zone de recherche de ressources, services et documents : Commencez à taper **Information** et sélectionnez **Azure Information Protection**.

2. À partir de l’option de menu **classifications**  >  **étiquettes** : dans le volet **Azure information protection-étiquettes** , sélectionnez l’étiquette que vous souhaitez modifier. 

3. Dans le volet **Étiquette**, recherchez la zone **Définir les autorisations pour les documents et les e-mails contenant cette étiquette**, puis sélectionnez une des options suivantes :
    
    - **Non configuré** : sélectionnez cette option si l’étiquette est actuellement configurée pour appliquer la protection et si vous ne voulez plus que l’étiquette sélectionnée applique la protection. Passez ensuite à l’étape 11.
        
        Les paramètres de protection précédemment configurés sont conservés sous la forme de modèle de protection archivé et réapparaissent si vous redéfinissez l’option sur **Protéger**. Vous ne voyez pas ce modèle dans le portail Azure, mais si besoin, vous pouvez toujours le gérer à l’aide de [PowerShell](configure-templates-with-powershell.md). Ce comportement signifie que le contenu reste accessible s’il a cette étiquette avec les paramètres de protection appliqués précédemment.
        
        Quand une étiquette avec ce paramètre de protection **Non configuré** est appliqué :
        
         - Si le contenu a été précédemment protégé sans utiliser une étiquette, cette protection est conservée. 
         
         - Si le contenu a été précédemment protégé avec une étiquette, cette protection est supprimée si l’utilisateur appliquant l’étiquette a les autorisations pour supprimer la protection Rights Management. Cette exigence signifie que l’utilisateur doit disposer du [droit d’utilisation](configure-usage-rights.md) **exportation** ou **contrôle total** . ou qu’il doit être le propriétaire Rights Management (ce qui accorde automatiquement le droit d’utilisation Contrôle total), ou être un [super utilisateur dans Azure Rights Management](configure-super-users.md).
             
             Si l’utilisateur ne dispose pas des autorisations nécessaires pour supprimer la protection, l’étiquette ne peut pas être appliquée et le message suivant s’affiche : **Azure information protection ne pouvez pas appliquer cette étiquette. Si ce problème persiste, contactez votre administrateur**. 
    
    - **Protéger** : sélectionnez cette option pour appliquer la protection, puis passez à l’étape 4.
    
    - **Supprimer la protection** : sélectionnez cette option pour supprimer la protection si un document ou un e-mail est protégé. Passez ensuite à l’étape 11.
        
        Si la protection a été appliquée avec un modèle d’étiquette ou de protection, les paramètres de protection sont conservés sous la forme d’un modèle de protection archivé et réapparaissent si vous redéfinissez l’option sur **Protéger**. Vous ne voyez pas ce modèle dans le portail Azure, mais si besoin, vous pouvez toujours le gérer à l’aide de [PowerShell](configure-templates-with-powershell.md). Ce comportement signifie que le contenu reste accessible s’il a cette étiquette avec les paramètres de protection appliqués précédemment.
        
        Notez que pour qu’un utilisateur puisse appliquer une étiquette avec cette option, il doit avoir les autorisations nécessaires pour supprimer la protection Rights Management. Cette exigence signifie que l’utilisateur doit disposer du [droit d’utilisation](configure-usage-rights.md) **exportation** ou **contrôle total** . ou qu’il doit être le propriétaire Rights Management (ce qui accorde automatiquement le droit d’utilisation Contrôle total), ou être un [super utilisateur dans Azure Rights Management](configure-super-users.md). 
        
        Si l’utilisateur appliquant l’étiquette avec ce paramètre ne dispose pas des autorisations nécessaires pour supprimer Rights Management protection, l’étiquette ne peut pas être appliquée et le message suivant s’affiche : **Azure information protection ne pouvez pas appliquer cette étiquette. Si ce problème persiste, contactez votre administrateur.**

4. Si vous avez sélectionné **Protéger**, le volet **Protection** s’ouvre automatiquement si une des autres options a été sélectionnée précédemment. Si ce nouveau volet ne s’ouvre pas automatiquement, sélectionnez **Protection** :
    
    ![Configurer la protection pour une étiquette Azure Information Protection](./media/info-protect-protection-bar-configured.png)

5. Dans le volet **Protection**, sélectionnez **Azure (clé cloud)** ou **HYOK (AD RMS)**.
    
    Dans la plupart des cas, sélectionnez **Azure (clé cloud)** pour vos paramètres d’autorisation. Ne sélectionnez pas **HYOK (AD RMS)** , sauf si vous avez lu et compris les conditions préalables et les restrictions qui accompagnent cette configuration *Hold Your Own Key* (HYOK, Conserver votre propre clé). Pour plus d’informations, consultez [HYOK (conservez votre propre clé) : exigences et restrictions pour la protection AD RMS](configure-adrms-restrictions.md). Pour poursuivre la configuration de la fonction HYOK (AD RMS), passez à l’étape 9.
    
6. Sélectionnez l’une des options suivantes :
    
   - **Définir les autorisations** : pour définir de nouveaux paramètres de protection dans ce portail.
    
   - **Configurer des autorisations définies par l’utilisateur (préversion)**  : permet aux utilisateurs de spécifier qui doit avoir des autorisations et quelles sont ces autorisations. Vous pouvez ensuite affiner cette option et choisir Outlook uniquement, ou Word, Excel, PowerPoint et l’Explorateur de fichiers. Cette option n’est pas prise en charge, et ne fonctionne pas, lorsqu’une étiquette est configurée pour la [classification automatique](configure-policy-classification.md).
        
       Si vous choisissez l’option pour Outlook : l’étiquette est affichée dans Outlook et le comportement résultant lorsque les utilisateurs appliquent l’étiquette est le même que l’option [ne pas transférer](configure-usage-rights.md#do-not-forward-option-for-emails) .
        
       Si vous choisissez l’option pour Word, Excel, PowerPoint et l’Explorateur de fichiers : lorsque cette option est définie, l’étiquette est affichée dans ces applications. Le comportement lorsque les utilisateurs appliquent l’étiquette consiste à afficher la boîte de dialogue pour que les utilisateurs sélectionnent les autorisations personnalisées. Dans cette boîte de dialogue, les utilisateurs choisissent l’un des [niveaux d’autorisation prédéfinis](configure-usage-rights.md#rights-included-in-permissions-levels), accèdent aux utilisateurs ou groupes, ou les spécifient, et s’ils le souhaitent, définissent une date d’expiration. Assurez-vous que les utilisateurs disposent des instructions et des conseils nécessaires pour fournir ces valeurs.
    
   - **Sélectionner un modèle prédéfini** : pour utiliser l’un des modèles par défaut ou un modèle personnalisé que vous avez configuré. Notez que cette option ne s’affiche pas pour les nouvelles étiquettes si vous modifiez une étiquette qui utilisait l’option **Définir les autorisations**.
    
     Pour sélectionner un modèle prédéfini, le modèle doit être publié (pas archivé) et il ne doit pas déjà être lié à une autre étiquette. Lorsque vous sélectionnez cette option, vous pouvez utiliser un bouton **Modifier le modèle** pour [convertir le modèle en étiquette](configure-policy-templates.md#to-convert-templates-to-labels).
    
     Si vous avez l’habitude de créer et de modifier des modèles personnalisés, il peut s’avérer utile de consulter [Tâches que vous aviez l’habitude d’effectuer avec le portail Azure Classic](migrate-portal.md).

7. Si vous avez sélectionné **Définir les autorisations** pour **Azure (clé cloud)**, cette option vous permet de sélectionner des utilisateurs et droits d’utilisation. 
    
    Si vous ne sélectionnez aucun utilisateur et que vous sélectionnez **OK** dans ce volet, suivi de **Enregistrer** dans le volet **étiquette** : l’étiquette est configurée pour appliquer la protection, de sorte que seule la personne qui applique l’étiquette peut ouvrir le document ou l’e-mail sans aucune restriction. Cette configuration est parfois appelée « Pour moi uniquement » et peut être le résultat requis, afin qu’un utilisateur puisse enregistrer un fichier à n’importe quel emplacement et être assuré d’être le seul à pouvoir l’ouvrir. Si ce résultat correspond à vos besoins et qu’aucun autre utilisateur n’est tenu de collaborer sur le contenu protégé, ne sélectionnez pas **Ajouter des autorisations**. Une fois que vous avez enregistré l’étiquette, à la prochaine ouverture de ce volet **Protection**, **IPC_USER_ID_OWNER** est affiché pour **Utilisateurs**, et **Copropriétaire** est affiché pour **Autorisations** afin de refléter cette configuration.
    
    Pour spécifier les utilisateurs que vous souhaitez voir en mesure d’ouvrir des documents et e-mails protégés, sélectionnez **Ajouter des autorisations**. Dans le volet **Ajouter des autorisations**, sélectionnez le premier ensemble d’utilisateurs et de groupes qui disposeront des droits d’utilisation du contenu qui sera protégé par l’étiquette sélectionnée :
    
   - Choisissez **Sélectionner dans la liste** pour ajouter tous les utilisateurs de votre organisation en sélectionnant **ajouter \<organization name> -tous les membres**. Ce paramètre exclut les comptes invités. Vous pouvez également sélectionner **Ajouter tous les utilisateurs authentifiés** ou parcourir le répertoire.
        
       Lorsque vous choisissez tous les membres ou que vous parcourez le répertoire, les utilisateurs ou les groupes doivent avoir une adresse e-mail. Dans un environnement de production, les utilisateurs et les groupes ont presque toujours une adresse e-mail, mais dans un environnement de test simple, vous devrez peut-être ajouter des adresses e-mail aux comptes d’utilisateur ou aux groupes.
        
       ###### <a name="more-information-about-add-any-authenticated-users"></a>Informations supplémentaires sur **Ajouter tous les utilisateurs authentifiés** 
       Ce paramètre ne restreint pas l’accès au contenu protégé par l’étiquette, tout en chiffrant le contenu et en vous proposant des options permettant de limiter la façon d’accéder au contenu (expiration et l’accès hors connexion) et l’utilisation qui peut en être faite (autorisations). Toutefois, l’application qui ouvre le contenu protégé doit être en mesure de prendre en charge l’authentification utilisée. Pour cette raison, les fournisseurs de réseaux sociaux fédérés, tels que Google, et l’authentification unique par code secret doivent être utilisés uniquement pour les e-mails, et seulement lorsque vous utilisez Exchange Online et les nouvelles fonctionnalités de chiffrement de messages Office 365. Les comptes Microsoft peuvent être utilisées avec la visionneuse Azure Information Protection et avec les applications Office 365 (Démarrer en un clic). 
          
       Quelques scénarios classiques pour la définition des utilisateurs authentifiés :
       - Tout le monde peut consulter le contenu, mais vous souhaitez imposer des restrictions à son utilisation. Par exemple, vous ne souhaitez pas que le contenu soit modifié, copié ou imprimé.
       - Vous n’avez pas besoin de restreindre l’accès au contenu, mais vous souhaitez savoir qui l’ouvre et, éventuellement, le révoquer.
       - Vous voulez que le contenu soit chiffré au repos et en transit, mais aucun contrôle d’accès n’est nécessaire.
        
   - Sélectionnez **Entrez les détails** pour spécifier manuellement les adresses e-mail relatives aux utilisateurs individuels ou aux groupes (internes ou externes). Vous pouvez utiliser cette option pour spécifier tous les utilisateurs d’une autre organisation en entrant un nom de domaine de cette organisation. Vous pouvez aussi utiliser cette option pour les fournisseurs de réseaux sociaux, en entrant leur nom de domaine comme **gmail.com**, **hotmail.com** ou **outlook.com**.
        
     >[!NOTE]
     >Si une adresse e-mail est modifiée une fois que vous avez sélectionné l’utilisateur ou le groupe, consultez la section [Considérations relatives à Azure Information Protection en cas de changement des adresses e-mail](prepare.md#considerations-for-azure-information-protection-if-email-addresses-change) dans la documentation de planification.
    
     Une meilleure pratique consiste à utiliser des groupes plutôt que des utilisateurs. Cette stratégie préserve la simplicité de votre configuration et rend moins probable la nécessité de mettre à jour ultérieurement votre configuration d’étiquette, puis de protéger à nouveau le contenu. Toutefois, si vous apportez des modifications au groupe, n’oubliez pas que pour des raisons de performances, Azure Rights Management [met en cache l’appartenance au groupe](prepare.md#group-membership-caching-by-azure-information-protection). 
    
    Une fois que vous avez spécifié le premier ensemble d’utilisateurs et de groupes, sélectionnez les autorisations à accorder à ces utilisateurs et à ces groupes. Pour plus d’informations sur les autorisations disponibles, consultez [Configuration des droits d’utilisation pour Azure Information Protection](configure-usage-rights.md). Toutefois, l’implémentation de ces autorisations peut varier selon les applications qui prennent en charge cette protection. Consultez leur documentation et faites vos propres tests avec les applications dont les utilisateurs se servent pour vérifier le comportement avant de déployer le modèle pour les utilisateurs.
    
     Si nécessaire, vous pouvez désormais ajouter un deuxième ensemble d’utilisateurs et de groupes avec des droits d’utilisation. Répétez l’opération jusqu’à ce que vous ayez spécifié tous les utilisateurs et les groupes avec leurs autorisations respectives.

     >[!TIP]
     >Ajoutez l’autorisation personnalisée **Enregistrer sous, Exporter (EXPORTER)** et accordez-la à des administrateurs de récupération de données ou à d’autres personnes dans l’entreprise ayant la responsabilité de récupérer des informations. Si nécessaire, ces utilisateurs peuvent ensuite supprimer la protection des fichiers et des e-mails qui seront protégés au moyen de cette étiquette ou de ce modèle. Cette possibilité de supprimer la protection au niveau de l’autorisation pour un document ou un e-mail offre un contrôle plus précis que la [fonctionnalité de super utilisateur](configure-super-users.md).
    
     Pour tous les utilisateurs et les groupes que vous avez spécifiés dans le volet **Protection**, vérifiez maintenant si des modifications doivent être apportées aux paramètres suivants. Ces paramètres, comme les autorisations, ne s’appliquent pas à [l’émetteur de Rights Management ni au propriétaire de Rights Management](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner), ni à tout [super utilisateur](configure-super-users.md) que vous avez assigné.
    
     ###### <a name="information-about-the-protection-settings"></a>Informations sur les paramètres de protection
    
     |Paramètre|Plus d’informations|Paramètre recommandé
     |-----------|--------------------|--------------------|
     |**Expiration du contenu du fichier**|Définissez une date ou un nombre de jours limite pour l’ouverture par les utilisateurs sélectionnés des documents protégés par ces paramètres. Pour les e-mails, l’expiration n’est pas toujours appliquée en raison des mécanismes de mise en cache utilisés par certains clients de messagerie.<br /><br />Vous pouvez spécifier une date ou un nombre de jours à partir du moment où la protection est appliquée au contenu.<br /><br />Lorsque vous spécifiez une date, cette dernière prend effet à minuit, dans votre fuseau horaire actuel.|**Le contenu n’expire jamais** sauf s’il est associé à une exigence temporelle spécifique.|
     |**Autoriser l’accès hors connexion**|Utilisez ce paramètre pour équilibrer les éventuelles exigences de sécurité que vous avez (dont l’accès après la révocation) avec la possibilité pour les utilisateurs sélectionnés d’ouvrir du contenu protégé lorsqu’ils ne disposent pas d’une connexion Internet.<br /><br />Si vous spécifiez que le contenu n’est pas disponible sans connexion Internet ou que ce contenu est disponible seulement pour un nombre de jours spécifié, quand ce seuil est atteint, ces utilisateurs doivent se réauthentifier et leur accès est journalisé. Dans ce cas, si leurs informations d’identification ne sont pas mises en cache, les utilisateurs sont invités à se connecter avant de pouvoir ouvrir le document ou l’e-mail.<br /><br />En plus de la réauthentification, la stratégie et l’appartenance au groupe d’utilisateurs sont réévaluées. Cela signifie que les utilisateurs peuvent obtenir des résultats d’accès différents pour le même document ou e-mail si la stratégie ou l’appartenance au groupe a changé par rapport au moment où ils ont accédé au contenu pour la dernière fois. Cela peut inclure le refus d’accès à un document si ce dernier a été [révoqué](./rms-client/client-track-revoke.md).|Selon la sensibilité du contenu :<br /><br />- **Nombre de jours pendant lesquels le contenu est disponible sans connexion Internet**  =  **7** pour les données sensibles de l’entreprise qui pourraient nuire à l’entreprise si elles sont partagées avec des personnes non autorisées. Cette recommandation est un bon compromis entre flexibilité et sécurité. Elle peut concerner les contrats, les rapports de sécurité, les synthèses de prévision et les données commerciales, par exemple.<br /><br />- **Jamais** pour les données d’entreprise très sensibles qui pourraient nuire à l’entreprise si elles étaient partagées avec des personnes non autorisées. Cette recommandation privilégie la sécurité par rapport à la flexibilité, et elle garantit qu’en cas de révocation du document, tous les utilisateurs autorisés sont dans l’incapacité d’ouvrir le document immédiatement. Elle peut concerner les informations relatives aux employés et aux clients, les mots de passe, le code source et les rapports financiers préannoncés, par exemple.|
    
     Une fois terminée la configuration des autorisations et des paramètres, cliquez sur **OK**. 
    
     Ce regroupement de paramètres crée un modèle personnalisé pour le service Azure Rights Management. Ces modèles peuvent être utilisés avec les applications et les services qui s’intègrent dans Azure Rights Management. Pour plus d’informations sur la manière dont les ordinateurs et les services téléchargent et actualisent ces modèles, consultez [Actualisation des modèles pour les utilisateurs et services](refresh-templates.md).

8. Si vous avez sélectionné **Sélectionner un modèle prédéfini** pour **Azure (clé cloud)**, cliquez sur la zone de liste déroulante et sélectionnez le [modèle](configure-policy-templates.md) que vous souhaitez utiliser pour protéger les documents et les e-mails avec cette étiquette. Vous ne voyez pas les modèles archivés ni les modèles qui sont déjà sélectionnés pour une autre étiquette.
    
    Si vous sélectionnez un **modèle de service**, ou si vous avez configuré des [contrôles d’intégration](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) :
    
    - Les utilisateurs qui se trouvent en dehors de l’étendue configurée du modèle ou qui sont exclus de l’application de la protection d’Azure Rights Management voient toujours l’étiquette, mais ils ne peuvent pas l’appliquer. S’ils sélectionnent l’étiquette, ils voient le message suivant : **Azure information protection ne pouvez pas appliquer cette étiquette. Si ce problème persiste, contactez votre administrateur.**
        
        Tous les modèles publiés sont toujours affichées, même si vous configurez une stratégie étendue. Par exemple, vous configurez une stratégie étendue pour le groupe Marketing. Les modèles que vous pouvez sélectionner ne se limitent pas aux modèles étendus au groupe Marketing, et il est possible de sélectionner un modèle de service que les utilisateurs sélectionnés ne peuvent pas employer. Pour faciliter la configuration et réduire le dépannage, pensez à faire correspondre le modèle de service à l’étiquette de votre stratégie étendue. 

9. Si vous avez sélectionné **HYOK (AD RMS)**, sélectionnez **Définir les détails du modèle AD RMS** ou **Configurer les autorisations définies par l’utilisateur (aperçu)**. Ensuite, spécifiez l’URL de licence de votre cluster AD RMS.
    
    Pour savoir comment spécifier un GUID de modèle et votre URL de licence, consultez [Recherche d’informations pour spécifier la protection AD RMS avec une étiquette Azure Information Protection](configure-adrms-restrictions.md#locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label).
    
    L’option de configuration des autorisations définies par l’utilisateur permet aux utilisateurs de spécifier qui doit avoir des autorisations et quelles sont ces autorisations. Vous pouvez ensuite affiner cette option et choisir Outlook uniquement (par défaut), ou Word, Excel, PowerPoint et l’Explorateur de fichiers. Cette option n’est pas prise en charge, et ne fonctionne pas, lorsqu’une étiquette est configurée pour la [classification automatique](configure-policy-classification.md).
    
    Si vous choisissez l’option pour Outlook : l’étiquette est affichée dans Outlook et le comportement résultant lorsque les utilisateurs appliquent l’étiquette est le même que l’option [ne pas transférer](configure-usage-rights.md#do-not-forward-option-for-emails) .
    
    Si vous choisissez l’option pour Word, Excel, PowerPoint et l’Explorateur de fichiers : lorsque cette option est définie, l’étiquette est affichée dans ces applications. Le comportement lorsque les utilisateurs appliquent l’étiquette consiste à afficher la boîte de dialogue pour que les utilisateurs sélectionnent les autorisations personnalisées. Dans cette boîte de dialogue, les utilisateurs choisissent l’un des [niveaux d’autorisation prédéfinis](configure-usage-rights.md#rights-included-in-permissions-levels), accèdent aux utilisateurs ou groupes, ou les spécifient, et s’ils le souhaitent, définissent une date d’expiration. Assurez-vous que les utilisateurs disposent des instructions et des conseils nécessaires pour fournir ces valeurs.

10. Cliquez sur **OK** pour fermer le volet **Protection** et voir apparaître la valeur que vous avez choisie pour **Ne pas transférer** ou le modèle que vous avez sélectionné pour l’option **Protection** dans le volet **Étiquette**.

11. Dans le volet **Étiquette**, cliquez sur **Enregistrer**.

12. Dans le volet **Azure Information Protection**, utilisez la colonne **PROTECTION** pour vérifier que votre étiquette affiche maintenant le paramètre de protection souhaité :
    
    - Une coche si vous avez configuré la protection. 
    
    - Un X pour désigner l’annulation, si vous avez configuré une étiquette pour la suppression de la protection.
    
    - Un champ vide lorsque la protection n’est pas définie. 

Une fois que vous avez cliqué sur **Enregistrer**, vos modifications sont automatiquement disponibles pour les utilisateurs et les services. Il n’y a plus d’option de publication distincte.


## <a name="example-configurations"></a>Exemples de configurations

Les sous-étiquettes **Tous les employés** et **Destinataires uniquement** découlant des étiquettes **Confidentiel** et **Hautement confidentiel** dans la [stratégie par défaut](configure-policy-default.md) fournissent des exemples de configuration d’étiquettes qui appliquent la protection. Vous pouvez également vous appuyer sur les exemples suivants pour configurer la protection dans différents scénarios. 

Pour chaque exemple qui suit, dans votre \<*label name*> volet, sélectionnez **protéger**. Si le volet **Protection** ne s’ouvre pas automatiquement, sélectionnez **Protection** pour l’ouvrir afin de sélectionner les options de configuration de protection :

![Configuration d’une étiquette Azure Information Protection à des fins de protection](./media/info-protect-protection-bar-configured.png)

### <a name="example-1-label-that-applies-do-not-forward-to-send-a-protected-email-to-a-gmail-account"></a>Exemple 1 : Étiquette qui applique l’option Ne pas transférer pour envoyer un e-mail protégé vers un compte Gmail

Cette étiquette est uniquement disponible dans Outlook et convient lorsque Exchange Online est configuré pour les [nouvelles fonctionnalités de chiffrement de messages Office 365](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e). Demandez aux utilisateurs de sélectionner cette étiquette lorsqu’ils doivent envoyer un e-mail protégé à des personnes qui utilisent un compte Gmail (ou tout autre compte de messagerie externe à votre organisation). 

Vos utilisateurs saisissent l’adresse e-mail Gmail dans le champ **À**.  Ensuite, ils sélectionnent l’étiquette : l’option Ne pas transférer est automatiquement ajoutée à l’e-mail. Le résultat est que les destinataires ne peuvent pas transférer l’e-mail ou l’imprimer, le copier ou enregistrer l’e-mail en dehors de sa boîte aux lettres à l’aide de l’option **Enregistrer sous** . 

1. Dans le volet **Protection**, vérifiez que l’option **Azure (clé cloud)** est sélectionnée.
    
2. Sélectionnez **Configurer les autorisations définies par l’utilisateur (préversion)**.

3. Assurez-vous que l’option suivante est sélectionnée : **Dans Outlook appliquer Ne pas transférer**.

4. Si cette option est sélectionnée, désélectionnez l’option suivante : **Dans Word, Excel, PowerPoint et l’Explorateur de fichiers, demander à l’utilisateur des autorisations personnalisées**.

5. Cliquez sur **OK** dans le volet **Protection**, puis sur **Enregistrer** dans le volet **Étiquette**.


### <a name="example-2-label-that-restricts-read-only-permission-to-all-users-in-another-organization-and-that-supports-immediate-revocation"></a>Exemple 2 : Étiquette qui limite l’autorisation en lecture seule à tous les utilisateurs d’une autre organisation, et qui prend en charge la révocation immédiate

Cette étiquette convient au partage des documents très sensibles (en lecture seule) qui exigent toujours une connexion Internet pour les afficher. Si le document est révoqué, les utilisateurs ne seront pas en mesure de l’afficher la prochaine fois qu’ils tenteront de l’ouvrir.

Cette étiquette ne convient pas aux e-mails.

1. Dans le volet **Protection**, vérifiez que l’option **Azure (clé cloud)** est sélectionnée.
    
2. Assurez-vous que l’option **Définir les autorisations** est sélectionnée, puis sélectionnez **Ajouter des autorisations**.

3. Dans le volet **Ajouter des autorisations**, sélectionnez **Entrez les détails**.

4. Entrez le nom d’un domaine à partir de l’autre organisation, comme **fabrikam.com**. Sélectionnez ensuite **Ajouter**.

5. Dans **Choisir des autorisations à partir des autorisations prédéfinies**, sélectionnez **Visionneuse**, puis sélectionnez **OK**.

6. De retour dans le volet **Protection**, pour le **paramètre Autoriser l’accès hors connexion**, sélectionnez **Jamais**.

7. Cliquez sur **OK** dans le volet **Protection**, puis sur **Enregistrer** dans le volet **Étiquette**.


### <a name="example-3-add-external-users-to-an-existing-label-that-protects-content"></a>Exemple 3 : Ajouter des utilisateurs externes à une étiquette existante qui protège le contenu

Les nouveaux utilisateurs que vous ajoutez seront en mesure d’ouvrir des documents et des e-mails déjà protégés avec cette étiquette. Les autorisations que vous accordez à ces utilisateurs peuvent être différentes des autorisations dont les utilisateurs existants disposent.

1. Dans le volet **Protection**, vérifiez que l’option **Azure (clé cloud)** est sélectionnée.
    
2. Assurez-vous que l’option **Définir les autorisations** est sélectionnée, puis sélectionnez **Ajouter des autorisations**.

3. Dans le volet **Ajouter des autorisations**, sélectionnez **Entrez les détails**.

4. Entrez l’adresse e-mail du premier utilisateur (ou groupe) à ajouter, puis sélectionnez **Ajouter**.

5. Sélectionnez les autorisations pour cet utilisateur (ou groupe).

6. Répétez les étapes 4 et 5 pour chaque utilisateur (ou groupe) que vous souhaitez ajouter à cette étiquette. Cliquez ensuite sur **OK**.

7. Cliquez sur **OK** dans le volet **Protection**, puis sur **Enregistrer** dans le volet **Étiquette**.

### <a name="example-4-label-for-protected-email-that-supports-less-restrictive-permissions-than-do-not-forward"></a>Exemple 4 : Étiquette pour un e-mail protégé qui prend en charge des autorisations moins restrictives que Ne pas transférer

Cette étiquette ne peut pas être limitée à Outlook, mais elle fournit des contrôles moins restrictifs que Ne pas transférer. Par exemple, vous voulez que les destinataires puissent copier du contenu de l’e-mail ou d’une pièce jointe, ou qu’ils puissent enregistrer et modifier une pièce jointe.

Si vous spécifiez des utilisateurs externes ne possédant pas de compte dans Azure AD :

- Cette étiquette peut être utilisée pour les-mails si Exchange Online utilise les [nouvelles fonctionnalités dans Chiffrement des messages Office 365](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e). 
 
- Les pièces jointes Office qui sont protégées automatiquement peuvent être affichées dans un navigateur. Pour modifier ces documents, après les avoir téléchargés, modifiez-les à l’aide des applications Office 365 (Démarrer en un clic) et d’un compte Microsoft qui utilise la même adresse e-mail. [Plus d’informations](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)


> [!NOTE]
> Exchange Online déploie actuellement une nouvelle option appelée [Chiffrement seul](configure-usage-rights.md#encrypt-only-option-for-emails). Cette option n'est pas disponible pour la configuration des étiquettes. Toutefois, lorsque vous savez qui seront les destinataires, vous pouvez utiliser cet exemple pour configurer une étiquette avec le même ensemble de droits d’utilisation. 

Lorsque vos utilisateurs spécifient les adresses e-mail dans le champ **À**, les adresses doivent correspondre aux utilisateurs que vous spécifiez pour cette configuration d’étiquette. Étant donné que les utilisateurs peuvent appartenir à des groupes et avoir plusieurs adresses e-mail, l’adresse e-mail qu’ils spécifient ne doit pas nécessairement correspondre à l’adresse e-mail que vous spécifiez pour les autorisations. Toutefois, il est plus simple de spécifier la même adresse e-mail pour s’assurer que le destinataire sera autorisé. Pour plus d’informations sur la façon dont les utilisateurs sont autorisés, consultez [Préparation des utilisateurs et des groupes pour Azure Information Protection](prepare.md). 

1. Dans le volet **Protection**, vérifiez que l’option **Azure (clé cloud)** est sélectionnée.
    
2. Assurez-vous que l’option **Définir les autorisations** est sélectionnée, puis sélectionnez **Ajouter des autorisations**.

3. Dans le volet **Ajouter des autorisations** : pour accorder des autorisations aux utilisateurs de votre organisation, sélectionnez **ajouter \<organization name> -tous les membres** pour sélectionner tous les utilisateurs de votre locataire. Ce paramètre exclut les comptes invités. Ou sélectionnez **Parcourir le répertoire** pour sélectionner un groupe spécifique. Pour accorder des autorisations à des utilisateurs externes ou si vous préférez taper l’adresse e-mail, sélectionnez **Entrer les détails** et tapez l’adresse e-mail de l’utilisateur, le groupe Azure AD ou un nom de domaine.
    
    Répétez cette étape pour spécifier les utilisateurs supplémentaires qui doivent disposer des mêmes autorisations.

4. Pour **Choisir des autorisations à partir des autorisations prédéfinies**, sélectionnez **Copropriétaire**, **Coauteur**, **Réviseur** ou **Personnalisé** afin de sélectionner les autorisations que vous souhaitez accorder.
    
    Remarque : ne sélectionnez pas **Visionneuse** pour les e-mails, et si vous sélectionnez **Personnalisé**, assurez-vous d’inclure **Modifier et enregistrer**.
    
    Pour sélectionner les autorisations qui correspondent à la nouvelle option **Chiffrement seul** d’Exchange Online, sélectionnez **Personnalisé**. Ensuite, sélectionnez toutes les autorisations sauf **Enregistrer sous, Exporter (EXPORT)** et **Contrôle total (OWNER)**.

5. Pour spécifier les utilisateurs supplémentaires qui doivent disposer d’autorisations différentes, répétez les étapes 3 et 4.

6. Cliquez sur **OK** dans le volet **Ajouter des autorisations**.

7. Cliquez sur **OK** dans le volet **Protection**, puis sur **Enregistrer** dans le volet **Étiquette**.


### <a name="example-5-label-that-encrypts-content-but-doesnt-restrict-who-can-access-it"></a>Exemple 5 : Étiquette qui chiffre le contenu, mais n’en restreint pas l’accès

L’avantage de cette configuration est que vous n’avez pas besoin de spécifier des utilisateurs, des groupes ou des domaines pour protéger un e-mail ou un document. Le contenu sera toujours chiffré, et vous pouvez toujours spécifier des droits d’utilisation, une date d’expiration et un accès hors connexion. Utilisez cette configuration uniquement lorsque vous n’avez pas besoin de restreindre qui peut ouvrir le document ou l’e-mail protégé. [Pour plus d'informations sur ce paramètre](#more-information-about-add-any-authenticated-users)

1. Dans le volet **Protection**, vérifiez que l’option **Azure (clé cloud)** est sélectionnée.
    
2. Vérifiez que l’option **Définir les autorisations** est sélectionnée, puis sélectionnez **Ajouter des autorisations**.

3. Dans le volet **Ajouter des autorisations**, sur l’onglet **Sélectionner dans la liste**, sélectionnez **Ajouter les utilisateurs authentifiés**.

4. Sélectionnez les autorisations souhaitées, puis cliquez sur **OK**.

5. De retour dans le volet **Protection**, si nécessaire, configurez les paramètres pour **Expiration du contenu du fichier** et **Autoriser l’accès hors connexion**, puis cliquez sur **OK**.

6. Dans le volet **Étiquette**, sélectionnez **Enregistrer**.


### <a name="example-6-label-that-applies-just-for-me-protection"></a>Exemple 6 : étiquette qui applique la protection « juste pour moi »

Cette configuration offre l’inverse de la collaboration sécurisée pour les documents : à l’exception d’un [super utilisateur](configure-super-users.md), seule la personne qui applique l’étiquette peut ouvrir le contenu protégé, sans aucune restriction. Cette configuration est souvent appelée « Pour moi uniquement » et convient quand un utilisateur veut enregistrer un fichier à n’importe quel emplacement et être assuré d’être le seul à pouvoir l’ouvrir.

La configuration de l’étiquette est extrêmement simple :

1. Dans le volet **Protection**, vérifiez que l’option **Azure (clé cloud)** est sélectionnée.
    
2. Sélectionnez **OK** sans sélectionner aucun utilisateur ou sans configurer aucun paramètre dans ce volet.
    
    Même si vous pouvez configurer des paramètres pour **Expiration du contenu du fichier** et **Autoriser l’accès hors connexion**, quand vous ne spécifiez pas d’utilisateurs et leurs autorisations, ces paramètres d’accès ne sont pas applicables. La raison en est que la personne qui applique la protection est l’[émetteur Rights Management](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner) pour le contenu et que ce rôle est exempté de ces restrictions d’accès.

3. Dans le volet **Étiquette**, sélectionnez **Enregistrer**.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy). 

Les règles de flux de messagerie Exchange peuvent également appliquer une protection, en fonction de vos étiquettes. Pour plus d’informations et d’exemples, consultez [Configuration des règles de flux de messagerie Exchange Online pour les étiquettes Azure Information Protection](configure-exo-rules.md).  
