---
title: "Configurer une étiquette Azure Information Protection pour la protection"
description: "Lorsque vous configurez une étiquette pour utiliser la protection de Rights Management, vous pouvez protéger vos documents et vos e-mails les plus sensibles."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/29/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: df26430b-315a-4012-93b5-8f5f42e049cc
ms.openlocfilehash: d42a561e61991a6299e83c5054ceb2ed8151ebf6
ms.sourcegitcommit: 972acdb468ac32a28e3e24c90694aff4b75206fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/29/2018
---
# <a name="how-to-configure-a-label-for-rights-management-protection"></a>Comment configurer une étiquette pour la protection de Rights Management

>*S’applique à : Azure Information Protection*

Vous pouvez protéger vos documents et vos e-mails les plus sensibles avec le service Rights Management. Ce service utilise des stratégies de chiffrement, d’identité et d’autorisation pour empêcher la perte de données. La protection est appliquée à une étiquette qui est configurée afin d’utiliser la protection de Rights Management pour les documents et les e-mails, et les utilisateurs peuvent également cliquer sur le bouton **Ne pas transférer** dans Outlook. 

## <a name="how-the-protection-works"></a>Fonctionnement de la protection

Quand un document ou un e-mail est protégé par un service Rights Management, il est chiffré au repos et en transit. Il peut ensuite être déchiffré uniquement par les utilisateurs autorisés. Ce chiffrement est conservé avec le document ou l’e-mail, même ce dernier est renommé. En outre, vous pouvez configurer les droits et restrictions d’utilisation, comme dans les exemples suivants :

- Seuls les utilisateurs au sein de votre organisation peuvent ouvrir le document ou l’e-mail confidentiel.

- Seuls les utilisateurs du service marketing peuvent modifier et imprimer le document ou l’e-mail d’annonce de promotion. Les autres utilisateurs de votre organisation peuvent uniquement lire ce document ou cet e-mail.

- Les utilisateurs ne peuvent pas transférer un e-mail ou copier des informations tirées de cet e-mail s’il contient des informations relatives à une réorganisation interne.

- La liste de tarifs en cours qui est envoyée aux partenaires commerciaux ne peut pas être ouverte après une date spécifique.

Pour plus d’informations sur la protection d’Azure Rights Management et sur son fonctionnement, consultez [Qu’est-ce qu’Azure Rights Management ?](../understand-explore/what-is-azure-rms.md)

> [!IMPORTANT]
> Si vous souhaitez configurer une étiquette afin d’appliquer cette protection, le service Azure Rights Management doit être activé pour votre organisation. Pour plus d’informations, consultez [Activer Azure Rights Management](../deploy-use/activate-service.md).

Lorsque l’étiquette applique la protection, il est impossible d’enregistrer un document protégé sur OneDrive ou SharePoint. Ces emplacements ne prennent pas en charge les fonctionnalités suivantes pour les fichiers protégés : cocréation, Office Online, recherche, aperçu de document, miniature, eDiscovery et protection contre la perte de données (DLP). 

Il n’est pas nécessaire de configurer Exchange pour la gestion des droits relatifs à l’information avant que les utilisateurs ne puissent appliquer des étiquettes dans Outlook pour protéger leurs e-mails. Toutefois, jusqu’à ce qu’Exchange soit configuré pour la gestion des droits relatifs à l’information, vous ne pouvez pas bénéficier des fonctionnalités complètes d’utilisation de la protection d’Azure Rights Management avec Exchange. Par exemple, les utilisateurs ne peuvent pas afficher les e-mails protégés sur un téléphone mobile ou avec Outlook sur le web, les e-mails protégés ne peuvent pas être indexés pour la recherche, et vous ne pouvez pas configurer Exchange Online DLP pour la protection de Rights Management. Pour configurer Exchange afin de prendre en charge ces scénarios supplémentaires, consultez les ressources suivantes :

- Pour Exchange Online, consultez les instructions décrites dans [Exchange Online : configuration de la gestion des droits relatifs à l’information](../deploy-use/configure-office365.md#exchange-online-irm-configuration).

- Pour Exchange sur site, vous devez déployer le [connecteur RMS et configurer vos serveurs Exchange](../deploy-use/deploy-rms-connector.md). 

## <a name="to-configure-a-label-for-rights-management-protection"></a>Pour configurer une étiquette dédiée à la protection de Rights Management

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et connectez-vous au [Portail Azure](https://portal.azure.com) en tant qu’administrateur de la sécurité ou administrateur général. Accédez ensuite au panneau **Azure Information Protection**. 
    
    Par exemple, dans le menu hub, cliquez sur **Autres services** et commencez à écrire **Informations** dans la zone de filtre. Sélectionnez **Azure Information Protection**.

2. Si l’étiquette que vous souhaitez configurer s’applique à tous les utilisateurs, restez dans le panneau **Azure Information Protection - Stratégie globale**. Cependant, si l’étiquette que vous souhaitez configurer se trouve dans une [stratégie étendue](configure-policy-scope.md) pour s’appliquer uniquement aux utilisateurs sélectionnés, dans la sélection de menu **STRATÉGIES**, sélectionnez d’abord **Stratégies étendues**. Sélectionnez ensuite votre stratégie étendue à partir du panneau **Azure Information Protection - Stratégies étendues**.

3. Sélectionnez l’étiquette que vous souhaitez configurer afin d’ouvrir le panneau **Étiquette**. 

4. Dans le panneau **Étiquette**, recherchez **Définir les autorisations pour les documents et les e-mails contenant cette étiquette** et sélectionnez l’une des options suivantes :
    
    - **Non configuré** : sélectionnez cette option si l’étiquette est actuellement configurée pour appliquer la protection et si vous ne voulez plus que l’étiquette sélectionnée applique la protection. Passez ensuite à l’étape 11.
    
    - **Protéger** : sélectionnez cette option pour appliquer la protection, puis passez à l’étape 5.
    
    - **Supprimer la protection** : sélectionnez cette option pour supprimer la protection si un document ou un e-mail est protégé. Passez ensuite à l’étape 11.
        
        Pour que les utilisateurs puissent appliquer une étiquette disposant de cette option, ils doivent avoir l’autorisation de supprimer la protection de Rights Management. Cela signifie que les utilisateurs doivent disposer d’**Exporter** ou de **Contrôle total** comme [droit d’utilisation](../deploy-use/configure-usage-rights.md). Ou ils doivent être le propriétaire de Rights Management (ce qui leur accorde automatiquement le droit d’utilisation Contrôle total) ou bien être un [super utilisateur pour Azure Rights Management](../deploy-use/configure-super-users.md). Les modèles Azure Rights Management par défaut n’incluent pas les droits d’utilisation qui permettent aux utilisateurs de supprimer la protection. 
        
        Si les utilisateurs n’ont pas les autorisations nécessaires pour supprimer la protection de Rights Management, et s’ils sélectionnent une étiquette configurée avec cette option **Supprimer la protection**, le message suivant s’affiche : **Azure Information Protection ne peut pas appliquer cette étiquette. Si ce problème persiste, contactez votre administrateur.**

5. Si vous avez sélectionné **Protéger**, sélectionnez à présent **Protection** pour ouvrir le panneau **Protection** :
    
    ![Configurer la protection pour une étiquette Azure Information Protection](../media/info-protect-protection-bar-configured.png)

6. Dans le panneau **Protection**, sélectionnez **Azure (clé cloud)** ou **HYOK (AD RMS)**.
    
    Dans la plupart des cas, sélectionnez **Azure (clé cloud)** pour vos paramètres d’autorisation. Ne sélectionnez pas **HYOK (AD RMS)** , sauf si vous avez lu et compris les conditions préalables et les restrictions qui accompagnent cette configuration *Hold Your Own Key* (HYOK, Conserver votre propre clé). Pour plus d’informations, consultez [HYOK (conservez votre propre clé) : exigences et restrictions pour la protection AD RMS](configure-adrms-restrictions.md). Pour poursuivre la configuration HYOK (AD RMS), passez à l’étape 10.
    
7. Sélectionnez l'une des options suivantes :
    
    - **Définir les autorisations** : pour définir de nouveaux paramètres de protection dans ce portail.
    
    - **Configurer les autorisations définies par l’utilisateur (aperçu)** : pour permettre aux utilisateurs de spécifier qui doit disposer d’autorisations et quelles sont ces autorisations. Vous pouvez ensuite affiner cette option et choisir Outlook uniquement, ou Word, Excel, PowerPoint et l’Explorateur de fichiers. Cette option n’est pas prise en charge, et ne fonctionne pas, lorsqu’une étiquette est configurée pour la [classification automatique](configure-policy-classification.md).
        
        Si vous choisissez l’option pour Outlook : l’étiquette est affichée dans Outlook et le comportement lorsque les utilisateurs appliquent l’étiquette est le même que pour l’option Ne pas transférer.
        
        Si vous choisissez l’option pour Word, Excel, PowerPoint et l’Explorateur de fichiers : lorsque cette option est définie, l’étiquette est affichée dans ces applications. Le comportement lorsque les utilisateurs appliquent l’étiquette consiste à afficher la boîte de dialogue pour que les utilisateurs sélectionnent les autorisations personnalisées. Dans cette boîte de dialogue, les utilisateurs doivent spécifier les autorisations, les utilisateurs ou les groupes, ainsi qu’une date d’expiration. Assurez-vous que les utilisateurs disposent des instructions et des conseils nécessaires pour fournir ces valeurs.
    
    - **Sélectionner un modèle prédéfini** : pour utiliser l’un des modèles par défaut ou un modèle personnalisé que vous avez configuré. Cette option ne s’affiche pas si vous modifiez une étiquette qui utilisait précédemment l’option **Définir les autorisations**.
    
    Pour sélectionner un modèle prédéfini, le modèle doit être publié (pas archivé) et il ne doit pas déjà être lié à une autre étiquette. Lorsque vous sélectionnez cette option, vous pouvez utiliser un bouton **Modifier le modèle** pour [convertir le modèle en étiquette](configure-policy-templates.md#to-convert-templates-to-labels).
    
    Conseil : si vous savez créer et modifier les modèles personnalisés, vous pouvez consulter [Tâches que vous aviez l’habitude d’effectuer dans le portail Azure Classic](migrate-portal.md).

8. Si vous avez sélectionné **Définir les autorisations** pour **Azure (clé cloud)**, cette option vous permet de configurer les mêmes paramètres que dans un modèle. 
    
    Sélectionnez **Ajouter des autorisations**, puis dans le panneau **Ajouter des autorisations**, sélectionnez le premier ensemble d’utilisateurs et de groupes ayant des droits d’utilisation du contenu et qui sera protégé par l’étiquette sélectionnée :
    
    - Choisissez **Sélectionner dans la liste** pour ajouter tous les utilisateurs de votre organisation ou parcourir le répertoire.
        
        Les utilisateurs ou les groupes doivent avoir une adresse e-mail. Dans un environnement de production, les utilisateurs et les groupes ont presque toujours une adresse e-mail, mais dans un environnement de test simple, vous devrez peut-être ajouter des adresses e-mail aux comptes d’utilisateur ou aux groupes.
        
    - Sélectionnez **Entrez les détails** pour spécifier manuellement les adresses e-mail relatives aux utilisateurs individuels ou aux groupes (internes ou externes). Ou utilisez cette option pour spécifier tous les utilisateurs d’une autre organisation en entrant un nom de domaine à partir de cette organisation. Lorsque vous entrez uniquement un nom de domaine, n’entrez pas de noms de domaines issus de fournisseurs de réseaux sociaux qui prennent en charge les comptes e-mail personnels. Par exemple, n’entrez pas **gmail.com**, **hotmail.com** ou **outlook.com**.
        
    >[!NOTE]
    >Si une adresse e-mail est modifiée une fois que vous avez sélectionné l’utilisateur ou le groupe, consultez la section [Considérations relatives à Azure Information Protection en cas de changement des adresses e-mail](../plan-design/prepare.md#considerations-for-azure-information-protection-if-email-addresses-change) dans la documentation de planification.
    
    Une meilleure pratique consiste à utiliser des groupes plutôt que des utilisateurs. Cette stratégie préserve la simplicité de votre configuration et rend moins probable la nécessité de mettre à jour ultérieurement votre configuration d’étiquette, puis de protéger à nouveau le contenu. Toutefois, si vous apportez des modifications au groupe, n’oubliez pas que pour des raisons de performances, Azure Rights Management [met en cache l’appartenance au groupe](../plan-design/prepare.md#group-membership-caching-by-azure-information-protection). 
    
    Une fois que vous avez spécifié le premier ensemble d’utilisateurs et de groupes, sélectionnez les autorisations à accorder à ces utilisateurs et à ces groupes. Pour plus d’informations sur les autorisations que vous pouvez sélectionner, consultez [Configuration des droits d’utilisation pour Azure Rights Management](configure-usage-rights.md). Toutefois, l’implémentation de ces autorisations peut varier selon les applications qui prennent en charge cette protection. Consultez leur documentation et faites vos propres tests avec les applications dont les utilisateurs se servent pour vérifier le comportement avant de déployer le modèle pour les utilisateurs.
    
    Si nécessaire, vous pouvez désormais ajouter un deuxième ensemble d’utilisateurs et de groupes avec des droits d’utilisation. Répétez l’opération jusqu’à ce que vous ayez spécifié tous les utilisateurs et les groupes avec leurs autorisations respectives.

    >[!TIP]
    >Envisagez d’ajouter l’autorisation personnalisée **Copier et extraire le contenu** et accordez cette autorisation aux administrateurs de récupération des données ou au personnel également responsable de la récupération d’informations. Si nécessaire, ces utilisateurs peuvent ensuite supprimer la protection des fichiers et des e-mails qui seront protégés au moyen de cette étiquette ou de ce modèle. Cette possibilité de supprimer la protection au niveau de l’autorisation pour un document ou un e-mail offre un contrôle plus précis que la [fonctionnalité de super utilisateur](configure-super-users.md).
    
    Pour tous les utilisateurs et les groupes que vous avez spécifiés, dans le panneau **Protection**, vérifiez à présent si vous souhaitez apporter des modifications aux paramètres suivants. Ces paramètres, comme les autorisations, ne s’appliquent pas à [l’émetteur de Rights Management ni au propriétaire de Rights Management](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner), ni à tout [super utilisateur](configure-super-users.md) que vous avez assigné.
    
    |Paramètre|Informations complémentaires|Paramètre recommandé
    |-----------|--------------------|--------------------|
    |**expiration du contenu**|Définissez une date ou un nombre de jours précisant le moment où les documents ou les e-mails protégés par ces paramètres ne devront plus s’ouvrir pour les utilisateurs sélectionnés. Vous pouvez spécifier une date ou un nombre de jours à partir du moment où la protection est appliquée au contenu.<br /><br />Lorsque vous spécifiez une date, cette dernière prend effet à minuit, dans votre fuseau horaire actuel.|**Le contenu n’expire jamais** sauf s’il est associé à une exigence temporelle spécifique.|
    |**Autoriser l’accès hors connexion**|Utilisez ce paramètre afin de contrebalancer vos éventuelles exigences de sécurité (ce qui inclut l’accès après révocation) avec la possibilité pour les utilisateurs sélectionnés d’ouvrir du contenu protégé lorsqu’ils ne disposent pas d’une connexion Internet.<br /><br />Si vous spécifiez que le contenu n’est pas disponible sans connexion Internet ou que le contenu est uniquement disponible pour un nombre de jours spécifique, lorsque ce seuil est atteint, ces utilisateurs doivent être de nouveau authentifiés et leur accès doit être consigné. Dans ce cas, si leurs informations d’identification ne sont pas mises en cache, les utilisateurs sont invités à se connecter avant de pouvoir ouvrir le document ou l’e-mail.<br /><br />En plus de la réauthentification, la stratégie et l’appartenance au groupe d’utilisateurs sont réévaluées. Cela signifie que les utilisateurs peuvent obtenir des résultats d’accès différents pour le même document ou e-mail si la stratégie ou l’appartenance au groupe a changé par rapport au moment où ils ont accédé au contenu pour la dernière fois. Cela peut inclure le refus d’accès à un document si ce dernier a été [révoqué](../rms-client/client-track-revoke.md).|Selon la sensibilité du contenu :<br /><br />- **Nombre de jours pendant lesquels le contenu est disponible sans connexion Internet** = **7** pour les données sensibles de l’entreprise qui pourraient nuire à l’entreprise si elles étaient partagées avec des personnes non autorisées. Cette recommandation est un bon compromis entre flexibilité et sécurité. Elle peut concerner les contrats, les rapports de sécurité, les synthèses de prévision et les données commerciales, par exemple.<br /><br />- **Jamais** pour les données d’entreprise très sensibles qui pourraient nuire à l’entreprise si elles étaient partagées avec des personnes non autorisées. Cette recommandation privilégie la sécurité par rapport à la flexibilité, et elle garantit qu’en cas de révocation du document, tous les utilisateurs autorisés sont dans l’incapacité d’ouvrir le document immédiatement. Elle peut concerner les informations relatives aux employés et aux clients, les mots de passe, le code source et les rapports financiers préannoncés, par exemple.|
    
    Lorsque vous avez terminé de configurer les autorisations, cliquez sur **OK**. 
    
    Ce regroupement de paramètres crée un modèle personnalisé pour le service Azure Rights Management. Ces modèles peuvent être utilisés avec les applications et les services qui s’intègrent dans Azure Rights Management. Pour plus d’informations sur la manière dont les ordinateurs et les services téléchargent et actualisent ces modèles, consultez [Actualisation des modèles pour les utilisateurs et services](refresh-templates.md).

9. Si vous avez sélectionné **Sélectionner un modèle prédéfini** pour **Azure (clé cloud)**, cliquez sur la zone de liste déroulante et sélectionnez le [modèle](../deploy-use/configure-policy-templates.md) que vous souhaitez utiliser pour protéger les documents et les e-mails avec cette étiquette. Vous ne voyez pas les modèles archivés ni les modèles qui sont déjà sélectionnés pour une autre étiquette.
    
    Si vous sélectionnez un **modèle de service**, ou si vous avez configuré des [contrôles d’intégration](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) :
    
    - Les utilisateurs qui se trouvent en dehors de l’étendue configurée du modèle ou qui sont exclus de l’application de la protection d’Azure Rights Management voient toujours l’étiquette, mais ils ne peuvent pas l’appliquer. S’ils sélectionnent l’étiquette, le message suivant s’affiche : **Azure Information Protection ne peut pas appliquer cette étiquette. Si ce problème persiste, contactez votre administrateur.**
        
        Tous les modèles publiés sont toujours affichées, même si vous configurez une stratégie étendue. Par exemple, vous configurez une stratégie étendue pour le groupe Marketing. Les modèles que vous pouvez sélectionner ne se limitent pas aux modèles étendus au groupe Marketing, et il est possible de sélectionner un modèle de service que les utilisateurs sélectionnés ne peuvent pas employer. Pour faciliter la configuration et réduire le dépannage, pensez à faire correspondre le modèle de service à l’étiquette de votre stratégie étendue. 

10. Si vous avez sélectionné **HYOK (AD RMS)**, sélectionnez **Définir les détails du modèle AD RMS** ou **Configurer les autorisations définies par l’utilisateur (aperçu)**. Ensuite, spécifiez l’URL de licence de votre cluster AD RMS.
    
    Pour savoir comment spécifier un GUID de modèle et votre URL de licence, consultez [Recherche d’informations pour spécifier la protection AD RMS avec une étiquette Azure Information Protection](configure-adrms-restrictions.md#locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label).
    
    L’option d’autorisations définies par l’utilisateur permet aux utilisateurs de spécifier qui doit disposer d’autorisations et quelles sont ces autorisations. Vous pouvez ensuite affiner cette option et choisir Outlook uniquement (par défaut), ou Word, Excel, PowerPoint et l’Explorateur de fichiers. Cette option n’est pas prise en charge, et ne fonctionne pas, lorsqu’une étiquette est configurée pour la [classification automatique](configure-policy-classification.md).
    
    Si vous choisissez l’option pour Outlook : l’étiquette est affichée dans Outlook et le comportement lorsque les utilisateurs appliquent l’étiquette est le même que pour l’option Ne pas transférer.
    
    Si vous choisissez l’option pour Word, Excel, PowerPoint et l’Explorateur de fichiers : l’étiquette est affichée dans ces applications. Le comportement lorsque les utilisateurs appliquent l’étiquette consiste à afficher la boîte de dialogue pour que les utilisateurs sélectionnent les autorisations personnalisées. Dans cette boîte de dialogue, les utilisateurs doivent spécifier les autorisations, les utilisateurs ou les groupes, ainsi qu’une date d’expiration. Assurez-vous que les utilisateurs disposent des instructions et des conseils nécessaires pour fournir ces valeurs. Sauf si vous disposez de la préversion du client, cette option pour l’Explorateur de fichiers utilise toujours la protection Azure RMS plutôt que la protection HYOK (AD RMS).

11. Cliquez sur **OK** pour fermer le panneau **Protection** et vérifiez que vous avez bien sélectionné **Défini par l’utilisateur** ou l’affichage du modèle choisi pour l’option **Protection** dans le panneau **Étiquette**.

12. Dans le panneau **Étiquette**, cliquez sur **Enregistrer**.

13. Dans le panneau **Azure Information Protection**, utilisez la colonne **PROTECTION** pour confirmer que votre étiquette affiche désormais le paramètre de protection que vous souhaitez :
    
    - Une coche si vous avez configuré la protection. 
    
    - Un X pour désigner l’annulation, si vous avez configuré une étiquette pour la suppression de la protection.
    
    - Un champ vide lorsque la protection n’est pas définie. 

13. Pour mettre vos modifications à disposition des utilisateurs, cliquez sur **Publier**.

## <a name="example-configurations"></a>Exemples de configuration

Les sous-étiquettes **Tous les employés** et **Destinataires uniquement** découlant des étiquettes **Confidentiel** et **Hautement confidentiel** dans la [stratégie par défaut](configure-policy-default.md) fournissent des exemples de configuration d’étiquettes qui appliquent la protection. Vous pouvez également vous appuyer sur les exemples suivants pour configurer la protection dans différents scénarios. 

Pour chaque exemple qui suit, dans votre panneau \<*nom d’étiquette*>, sélectionnez **Protéger**, puis sélectionnez **Protection** afin d’ouvrir le panneau **Protection**.

### <a name="example-1-label-that-applies-do-not-forward-to-send-a-protected-email-to-a-gmail-account"></a>Exemple 1 : Étiquette qui applique l’option Ne pas transférer pour envoyer un e-mail protégé vers un compte Gmail

Cette étiquette est uniquement disponible dans Outlook et convient lorsque Exchange Online est configuré pour les [nouvelles fonctionnalités de chiffrement de messages Office 365](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e). Demandez aux utilisateurs de sélectionner cette étiquette lorsqu’ils doivent envoyer un e-mail protégé à des personnes qui utilisent un compte Gmail (ou tout autre compte de messagerie externe à votre organisation). 

Vos utilisateurs saisissent l’adresse e-mail Gmail dans le champ **À**.  Ensuite, ils sélectionnent l’étiquette : l’option Ne pas transférer est automatiquement ajoutée à l’e-mail. De cette manière, les destinataires ne peuvent pas transférer l’e-mail, l’imprimer, effectuer une copie, enregistrer les pièces jointes ni enregistrer l’e-mail sous un autre nom. 

1. Dans le panneau **Protection**, assurez-vous que l’option **Azure (clé cloud)** est bien sélectionnée.
    
2. Sélectionnez **Configurer les autorisations définies par l’utilisateur (aperçu)**.

3. Assurez-vous que l’option suivante est sélectionnée : **Dans Outlook appliquer Ne pas transférer**.

4. Si cette option est sélectionnée, désélectionnez l’option suivante : **Dans Word, Excel, PowerPoint et l’Explorateur de fichiers, demander à l’utilisateur des autorisations personnalisées**.

5. Cliquez sur **OK** dans le panneau **Protection**, puis publiez vos modifications.


### <a name="example-2-label-that-restricts-read-only-permission-to-all-users-in-another-organization-and-that-supports-immediate-revocation"></a>Exemple 2 : Étiquette qui limite l’autorisation en lecture seule à tous les utilisateurs d’une autre organisation, et qui prend en charge la révocation immédiate

Cette étiquette convient au partage de documents très sensibles (en lecture seule) qui nécessitent en permanence une connexion Internet pour l’affichage. Si le document est révoqué, les utilisateurs ne seront pas en mesure de l’afficher la prochaine fois qu’ils tenteront de l’ouvrir.

Cette étiquette ne convient pas aux e-mails.

1. Dans le panneau **Protection**, assurez-vous que l’option **Azure (clé cloud)** est bien sélectionnée.
    
2. Assurez-vous que l’option **Définir les autorisations** est sélectionnée, puis sélectionnez **Ajouter des autorisations**.

3. Dans le panneau **Ajouter des autorisations**, sélectionnez **Entrez les détails**.

4. Entrez le nom d’un domaine à partir de l’autre organisation, comme **fabrikam.com**. Sélectionnez ensuite **Ajouter**.

5. Dans **Choisir des autorisations à partir des autorisations prédéfinies**, sélectionnez **Visionneuse**, puis sélectionnez **OK**.

6. De retour dans le panneau **Protection**, pour le paramètre **Autoriser l’accès hors connexion**, sélectionnez **Jamais**.

7. Cliquez sur **OK** dans le panneau **Protection**, puis publiez vos modifications.


### <a name="example-3-add-external-users-to-an-existing-label"></a>Exemple 3 : Ajout d’utilisateurs externes à une étiquette existante

Les nouveaux utilisateurs que vous ajoutez seront en mesure d’ouvrir des documents et des e-mails déjà protégés avec cette étiquette. Les autorisations que vous accordez à ces utilisateurs peuvent être différentes des autorisations dont les utilisateurs existants disposent.

1. Dans le panneau **Protection**, assurez-vous que l’option **Azure (clé cloud)** est bien sélectionnée.
    
2. Assurez-vous que l’option **Définir les autorisations** est sélectionnée, puis sélectionnez **Ajouter des autorisations**.

3. Dans le panneau **Ajouter des autorisations**, sélectionnez **Entrez les détails**.

4. Entrez l’adresse e-mail du premier utilisateur (ou groupe) à ajouter, puis sélectionnez **Ajouter**.

5. Sélectionnez les autorisations pour cet utilisateur (ou groupe).

6. Répétez les étapes 4 et 5 pour chaque utilisateur (ou groupe) que vous souhaitez ajouter à cette étiquette. Cliquez ensuite sur **OK**.

7. Cliquez sur **OK** dans le panneau **Protection**, puis publiez vos modifications.

### <a name="example-4-label-for-protected-email-that-supports-less-restrictive-permissions-than-do-not-forward"></a>Exemple 4 : Étiquette pour un e-mail protégé qui prend en charge des autorisations moins restrictives que Ne pas transférer

Cette étiquette ne peut pas être limitée à Outlook, mais elle fournit des contrôles moins restrictifs que Ne pas transférer. Exemple : vous voulez que les destinataires soient en mesure de faire une copie à partir de l’e-mail ou d’une pièce jointe, ou d’imprimer et enregistrer une pièce jointe. Si vous spécifiez des utilisateurs externes qui ne disposent pas d’un compte dans Azure AD, veillez à demander à vos utilisateurs de ne pas utiliser cette étiquette pour les documents, mais seulement pour les e-mails. En outre, afin de prendre en charge ces utilisateurs externes, Exchange Online doit être configuré pour les [nouvelles fonctionnalités de chiffrement de messages Office 365](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e).  

Lorsque vos utilisateurs spécifient les adresses e-mail dans le champ **À**, les adresses doivent correspondre aux utilisateurs que vous spécifiez pour cette configuration d’étiquette. Étant donné que les utilisateurs peuvent appartenir à des groupes et avoir plusieurs adresses e-mail, l’adresse e-mail qu’ils spécifient ne doit pas nécessairement correspondre à l’adresse e-mail que vous spécifiez pour les autorisations. Toutefois, il est plus simple de spécifier la même adresse e-mail pour s’assurer que le destinataire sera autorisé. Pour plus d’informations sur la façon dont les utilisateurs sont autorisés, consultez [Préparation des utilisateurs et des groupes pour Azure Information Protection](../plan-design/prepare.md). 

1. Dans le panneau **Protection**, assurez-vous que l’option **Azure (clé cloud)** est bien sélectionnée.
    
2. Assurez-vous que l’option **Définir les autorisations** est sélectionnée, puis sélectionnez **Ajouter des autorisations**.

3. Dans le panneau **Ajouter des autorisations** : pour accorder des autorisations aux utilisateurs de votre organisation, sélectionnez **Ajouter \<nom de l’organisation > - Tous les membres** afin de sélectionner tous les utilisateurs de votre tenant, ou **Parcourir le répertoire** afin de sélectionner un groupe spécifique. Pour accorder des autorisations aux utilisateurs externes, ou si vous préférez saisir l’adresse e-mail, sélectionnez **Entrez les détails** et saisissez l’adresse e-mail de l’utilisateur ou du groupe Azure AD.
    
    Répétez cette étape pour spécifier les utilisateurs supplémentaires qui doivent disposer des mêmes autorisations.

4. Pour **Choisir des autorisations à partir des autorisations prédéfinies**, sélectionnez **Copropriétaire**, **Coauteur**, **Réviseur** ou **Personnalisé** afin de sélectionner les autorisations que vous souhaitez accorder. 
    
    Remarque : ne sélectionnez pas **Visionneuse** pour les e-mails, et si vous sélectionnez **Personnalisé**, assurez-vous d’inclure **Modifier et enregistrer**. 

5. Pour spécifier les utilisateurs supplémentaires qui doivent disposer d’autorisations différentes, répétez les étapes 3 et 4.

6. Cliquez sur **OK** dans le panneau **Ajouter des autorisations**. 

7. Cliquez sur **OK** dans le panneau **Protection**, puis publiez vos modifications.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]