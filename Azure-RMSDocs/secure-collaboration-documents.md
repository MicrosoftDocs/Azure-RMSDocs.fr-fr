---
title: Configuration d’une collaboration sécurisée autour de documents à l’aide d’Azure Information Protection
description: Flux de travail de bout en bout pour la collaboration autour de documents protégés par Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/19/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4895c429-959f-47c7-9007-b8f032f6df6f
ms.subservice: aiplabels
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: bbb085aa7de8555594d33bc0b2e0ea4d06034aa2
ms.sourcegitcommit: 72694afc0e74fd51662e40db2844cdb322632428
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/19/2020
ms.locfileid: "95568560"
---
# <a name="configuring-secure-document-collaboration-by-using-azure-information-protection"></a>Configuration d’une collaboration sécurisée autour de documents à l’aide d’Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

>[!NOTE] 
> Pour fournir une expérience client unifiée et rationalisée, **Azure Information Protection client (Classic)** et **Gestion des étiquettes** dans le Portail Azure sont **dépréciées** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Lorsque vous utilisez Azure Information Protection, vous pouvez protéger vos documents sans pour autant devoir renoncer à la collaboration avec des utilisateurs autorisés. Les documents créés par un utilisateur puis partagés avec d’autres afin que ceux-ci puissent les consulter et les modifier sont en majorité des documents Office Word, Excel et PowerPoint. Ces documents prennent en charge la protection native, autrement dit, en plus des fonctionnalités de protection que sont le chiffrement et l’autorisation, ils prennent également en charge l’autorisation restreinte pour un contrôle plus précis. 

Ces autorisations sont appelées des droits d’utilisation et incluent des autorisations comme afficher, modifier et imprimer. Vous pouvez définir des droits d’utilisation individuels lorsqu’un document est protégé, ou vous pouvez définir un groupe de droits d’utilisation, appelé niveau d’autorisation. Les niveaux d’autorisation facilitent la sélection de droits d’utilisation qui sont généralement utilisés ensemble, par exemple, réviseur et coauteur. Pour plus d’informations sur les droits d’utilisation et les niveaux d’autorisation, consultez [Configuration des droits d’utilisation pour Azure information protection](configure-usage-rights.md).

Lorsque vous configurez ces autorisations, vous pouvez spécifier les utilisateurs auxquels elles s’adressent :

- **Pour les utilisateurs de votre organisation ou d’une autre organisation qui utilisent Azure Active Directory** : vous pouvez spécifier des comptes d’utilisateur Azure AD, des groupes Azure AD ou tous les utilisateurs de cette organisation. 

- **Pour les utilisateurs n’ayant pas de compte Azure Active Directory** : spécifiez une adresse e-mail qui sera utilisée avec un compte Microsoft. Ce compte peut déjà exister, ou les utilisateurs peuvent le créer au moment de l’ouverture du document protégé. 
    
    Pour ouvrir des documents avec un compte Microsoft, les utilisateurs doivent utiliser des applications Microsoft 365 (démarrer en un clic). Les autres éditions et versions de Microsoft Office ne prennent pas encore en charge l’ouverture de documents Office protégés avec un compte Microsoft.

- **Pour tout utilisateur authentifié** : cette option est appropriée lorsque vous n’avez pas besoin de contrôler l’accès au document protégé, à condition que l’utilisateur puisse être authentifié. L’authentification peut avoir lieu via Azure AD, à l’aide d’un compte Microsoft, ou même via un fournisseur de réseaux sociaux fédérés ou un code secret à usage unique quand le contenu est protégé par les nouvelles fonctionnalités d’Office 365 Message Encryption. 

En tant qu’administrateur, vous pouvez configurer une étiquette Azure Information Protection pour appliquer les autorisations et les utilisateurs autorisés. Avec cette configuration, les utilisateurs et autres administrateurs peuvent facilement appliquer les paramètres de protection corrects, car il leur suffit d’appliquer l’étiquette, sans avoir à indiquer les détails. Les sections suivantes fournissent un exemple de procédure pour protéger un document qui prend en charge la collaboration sécurisée avec des utilisateurs internes et externes.


## <a name="example-configuration-for-a-label-to-apply-protection-to-support-internal-and-external-collaboration"></a>Exemple de configuration d’une étiquette afin d’appliquer une protection prenant en charge la collaboration interne et externe


Cet exemple montre comment configurer une étiquette existante pour appliquer la protection afin que les utilisateurs de votre organisation puissent collaborer sur des documents avec tous les utilisateurs d’une autre organisation disposant d’Microsoft 365 ou d’Azure AD, d’un groupe d’une autre organisation possédant Microsoft 365 ou Azure AD, et d’un utilisateur qui n’a pas de compte dans Azure AD et qui utilisera à la place son adresse e-mail gmail.

Étant donné que le scénario restreint l’accès de personnes spécifiques, il n’inclut pas le paramètre pour tous les utilisateurs authentifiés. Pour obtenir un exemple de la manière dont vous pouvez configurer une étiquette avec ce paramètre, consultez [Exemple 5 : étiquette qui crypte le contenu, mais n’en restreint pas l’accès](configure-policy-protection.md#example-5-label-that-encrypts-content-but-doesnt-restrict-who-can-access-it).  

1. Sélectionnez l’étiquette qui existe déjà dans la stratégie globale ou la stratégie délimitée. Dans le volet **Protection**, vérifiez que l’option **Azure (clé cloud)** est sélectionnée.
    
2. Assurez-vous que l’option **Définir les autorisations** est sélectionnée, puis sélectionnez **Ajouter des autorisations**.

3. Dans le volet **Ajouter des autorisations** : 
    
   - Pour votre groupe interne : sélectionnez **Parcourir les répertoires** pour sélectionner le groupe qui doit être à extension messagerie.
    
   - Pour tous les utilisateurs de la première organisation externe : sélectionnez **Entrez les détails** et tapez le nom d’un domaine dans le locataire de l’organisation. Par exemple, fabrikam.com.
    
   - Pour le groupe dans la seconde organisation externe : sous l’onglet **Entrez les détails**, tapez l’adresse e-mail du groupe dans le locataire de l’organisation. Par exemple : sales@contoso.com.
    
   - Pour l’utilisateur qui n’a pas de compte Azure AD : sous l’onglet **Entrez les détails**, tapez l’adresse e-mail de l’utilisateur. Par exemple : bengi.turan@gmail.com. 

4. Pour accorder les mêmes autorisations à tous les utilisateurs : dans **Choisir des autorisations à partir des autorisations prédéfinies**, sélectionnez **Copropriétaire**, **Co-auteur**, **Réviseur** ou **Personnalisé** pour sélectionner les autorisations à accorder.
    
    Par exemple, les autorisations que vous configurez peuvent s’apparenter à ce qui suit :
        
    ![Configuration d’autorisations pour une collaboration sécurisée](./media/collaboration-permissions.png)

5. Cliquez sur **OK** dans le volet **Ajouter des autorisations**.

6. Dans le volet **protection** , cliquez sur **OK**.

7. Dans le volet **Étiquette**, sélectionnez **Enregistrer**. 

## <a name="applying-the-label-that-supports-secure-collaboration"></a>Application de l’étiquette qui prend en charge la collaboration sécurisée

Maintenant que cette étiquette est configurée, elle peut être appliquée aux documents de différentes manières, notamment :

|Différentes manières d’appliquer l’étiquette|Autres informations|
|---------------|----------|
|Un utilisateur sélectionne manuellement l’étiquette lorsque le document est créé dans l’application Office.|Les utilisateurs sélectionnent l’étiquette à partir du bouton **Protéger** du ruban Office ou à partir de la barre Azure Information Protection.|
|Les utilisateurs sont invités à sélectionner une étiquette au moment de l’enregistrement d’un nouveau document.|Vous avez configuré le [paramètre de stratégie](configure-policy-settings.md) Azure Information Protection nommé **Tous les documents et e-mails doivent avoir une étiquette**.|
|Un utilisateur partage le document par e-mail et sélectionne manuellement l’étiquette dans Outlook.|Les utilisateurs sélectionnent l’étiquette à partir du bouton **Protéger** du ruban Office ou à partir de la barre Azure Information Protection. Le document joint est alors automatiquement protégé avec les mêmes paramètres.|
|Un administrateur applique l’étiquette au document à l’aide de PowerShell.|Utilisez l’applet de commande [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) pour appliquer l’étiquette à un document spécifique ou à tous les documents d’un dossier.|
|Vous avez en plus configuré l’étiquette de sorte qu’elle applique la classification automatique. Celle-ci peut désormais être appliquée à l’aide du scanneur Azure Information Protection ou de PowerShell.|Consultez [Comment configurer des conditions pour la classification automatique et recommandée pour Azure Information Protection](configure-policy-classification.md).|

Pour effectuer cette procédure pas à pas, appliquez manuellement l’étiquette lorsque vous créez le document dans l’application Office : 

1. Sur un ordinateur client, si l’application Office est déjà ouverte, commencez par la fermer et la rouvrir afin d’appliquer les dernières modifications de stratégie qui incluent l’étiquette que vous venez de configurer. 

2. Appliquez l’étiquette à un document, puis enregistrez-le.

Partagez le document protégé en le joignant à un e-mail et envoyez-le aux personnes que vous avez autorisé à modifier le document.

## <a name="opening-and-editing-the-protected-document"></a>Ouverture et modification du document protégé

Lorsque les utilisateurs que vous avez autorisés ouvrent le document en vue de le modifier, le document s’ouvre avec une bannière d’informations qui les avertit que les autorisations sont limitées. Par exemple :

![Exemple de bannière d’informations Azure Information Protection pour les autorisations](./media/example-restricted-access-banner.png)

S’ils sélectionnent **Afficher l’autorisation**, ils voient les autorisations dont ils disposent. Dans l’exemple suivant, l’utilisateur peut afficher et modifier le document :

![Exemple de boîte de dialogue Azure Information Protection pour les autorisations](./media/example-permisisons-popup.png)

Remarque : Si le document est ouvert par des utilisateurs externes qui utilisent également Azure Information Protection, l’application Office n’affiche pas votre étiquette de classification pour le document, bien que les marquages visuels de l’étiquette restent. Au lieu de cela, les utilisateurs externes peuvent appliquer leur propre étiquette conformément à la taxonomie de classification de leur organisation. Si ces utilisateurs externes renvoient ensuite le document modifié, Office affiche votre étiquette de classification d’origine lorsque vous rouvrez le document.

Avant l’ouverture du document protégé, un des flux d’authentification suivants se produit :

- Les utilisateurs ayant un compte Azure AD utilisent les informations d’identification de ce compte pour être authentifiés par Azure AD, puis le document s’ouvre. 

- Pour les utilisateurs qui n’ont pas de compte Azure AD et qui ne sont pas connectés à Office avec un compte autorisé à ouvrir le document, la page **Comptes** s’affiche. 
    
   Dans la page **Comptes**, sélectionnez **Ajouter un compte** :
   
    ![Ajout d’un compte Microsoft pour ouvrir un document protégé](./media/add-account-msa.png)

   À la page de **Connexion**, sélectionnez **Créez-en un !** et suivez les invites afin de créer un compte Microsoft avec l’adresse e-mail utilisée pour accorder les autorisations :
    
    ![Création d’un compte Microsoft pour ouvrir un document protégé](./media/create-account-msa.png)
    
    Lorsque le nouveau compte Microsoft est créé, le compte local bascule vers ce nouveau compte Microsoft et l’utilisateur peut alors ouvrir le document.


### <a name="supported-scenarios-for-opening-protected-documents"></a>Scénarios pris en charge pour l’ouverture de documents protégés

Le tableau suivant récapitule les différentes méthodes d’authentification qui sont prises en charge pour afficher et modifier des documents protégés.

En outre, les scénarios suivants prennent en charge l’affichage de documents :

- La visionneuse Azure Information Protection pour Windows ainsi que pour iOS et Android peut ouvrir des fichiers à l’aide d’un compte Microsoft. 

- Un navigateur peut ouvrir des pièces jointes protégées lorsque des fournisseurs de réseaux sociaux et des codes secrets à usage unique sont utilisés pour l’authentification avec Exchange Online et avec les nouvelles fonctionnalités d’Office 365 Message Encryption. 

|Plateformes pour l’affichage et la modification de documents : <br />Word, Excel, PowerPoint|Méthode d'authentification :<br />Azure AD|Méthode d'authentification :<br />Compte Microsoft|
|---------------|----------|-----------|-----------|
|Windows|Oui [[1]](#footnote-1)|Oui [[2]](#footnote-2)|
|iOS|Oui [[1]](#footnote-1)|Oui (version 1385219 et versions ultérieures) |
|Android|Oui [[1]](#footnote-1)|Oui (version 13029 et versions ultérieures)|
|MacOS|Oui [[1]](#footnote-1)|No|

###### <a name="footnote-1"></a>Note 1
Prend en charge les comptes d’utilisateur, les groupes à extension messagerie, tous les membres. Les comptes d’utilisateur et les groupes à extension messagerie peuvent inclure des comptes Invité. Tous les membres sauf les comptes Invité.

###### <a name="footnote-2"></a>Note 2
Actuellement pris en charge par les applications Microsoft 365 uniquement.

## <a name="next-steps"></a>Étapes suivantes

Consultez d’autres [exemples de configuration](configure-policy-protection.md#example-configurations) pour que les étiquettes appliquent une protection dans des scénarios courants. Cet article contient également des informations supplémentaires sur les paramètres de protection.

Pour plus d’informations sur les autres options et paramètres que vous pouvez configurer pour votre étiquette, consultez [Configuration de la stratégie Azure Information Protection](configure-policy.md). 

L’étiquette qui a été configurée dans cet article crée également un modèle de protection portant le même nom. Si vous avez des applications et services qui s’intègrent aux modèles de protection d’Azure Information Protection, ils peuvent appliquer ce modèle. Par exemple, les solutions DLP et les règles de flux de messagerie. Outlook sur le web affiche automatiquement des modèles de protection de la stratégie globale Azure Information Protection. 




