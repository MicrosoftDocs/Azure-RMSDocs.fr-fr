---
title: "Préparer des utilisateurs et des groupes pour Azure Information Protection"
description: "Vérifiez que vous disposez des comptes d’utilisateur et de groupe dont vous avez besoin pour démarrer la classification, l’étiquetage et la protection des documents et des e-mails de votre organisation."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/18/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: afbca2d6-32a7-4bda-8aaf-9f93f5da5abc
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: de06bc202ff60e6850ba217fe7ded79c0753d925
ms.sourcegitcommit: 972acdb468ac32a28e3e24c90694aff4b75206fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/29/2018
---
# <a name="preparing-users-and-groups-for-azure-information-protection"></a>Préparation des utilisateurs et des groupes pour Azure Information Protection

>*S’applique à : Azure Information Protection, Office 365*

Avant de déployer Azure Information Protection pour votre organisation, assurez-vous de disposer de comptes pour les utilisateurs et les groupes d’Azure AD pour le locataire de votre organisation.

Voici les différentes façons de créer ces comptes pour les utilisateurs et les groupes :

- Vous créez les utilisateurs dans le centre d’administration Office 365 et les groupes dans le centre d’administration Exchange Online.

- Vous créez les utilisateurs et les groupes dans le portail Azure.

- Vous créez le groupe et les utilisateurs à l’aide des applets de commande Azure AD PowerShell et Exchange Online.

- Vous créez les utilisateurs et les groupes dans votre répertoire Active Directory local et les synchronisez sur Azure AD.

- Vous créez les utilisateurs et les groupes dans un autre répertoire et les synchronisez sur Azure AD.

Lorsque vous créez des utilisateurs et des groupes à l’aide des trois premières méthodes de cette liste, ils sont automatiquement créés dans Azure AD et Azure Information Protection peut les utiliser directement. Toutefois, plusieurs réseaux d’entreprise utilisent un répertoire local pour créer et gérer les utilisateurs et les groupes. Azure Information Protection ne peut pas utiliser ces comptes directement. Vous devez les synchroniser sur Azure AD.

## <a name="how-users-and-groups-are-used-by-azure-information-protection"></a>Utilisation des utilisateurs et des groupes par Azure Information Protection

Il existe trois scénarios d’utilisation des utilisateurs et des groupes avec Azure Information Protection :

- **Pour attribuer des étiquettes aux utilisateurs** lorsque vous utilisez l’étiquetage et la classification. Seuls les administrateurs sélectionnent ces groupes :

    - La stratégie Azure Information Protection par défaut est automatiquement attribuée à tous les utilisateurs du Azure AD de votre locataire. Cependant, vous pouvez également affecter des étiquettes supplémentaires aux utilisateurs ou aux groupes spécifiés à l’aide de stratégies étendues.     

- **Pour affecter des droits d’utilisation et des contrôles d’accès** lorsque vous utilisez le service Azure Rights Management pour protéger des documents et des e-mails. Les administrateurs et les utilisateurs peuvent sélectionner ces utilisateurs et ces groupes :

    - Les droits d’utilisation déterminent si un utilisateur peut ouvrir un document ou un e-mail et comment il peut l’utiliser. Par exemple, ils indiquent s’il est en lecture seule, s’il peut le lire et l’imprimer ou le lire et le modifier uniquement.

    - Les contrôles d’accès incluent une date d’expiration et indiquent si une connexion à Internet est nécessaire pour l’accès.

- **Pour configurer le service Azure Rights Management**  afin de prendre en charge des scénarios spécifiques, et par conséquent, uniquement les administrateurs, sélectionnez ces groupes. Les exemples comprennent la configuration des éléments suivants :

    - Les super utilisateurs, afin que les services désignés ou les personnes puissent ouvrir du contenu chiffré si nécessaire pour la récupération de données ou eDiscovery.

    - L’administration déléguée du service Azure Rights Management.

    - Les contrôles d’intégration pour la prise en charge d’un déploiement échelonné.

**Pour attribuer des étiquettes aux utilisateurs** lorsque vous configurez la stratégie Azure Information Protection afin que les étiquettes puissent être appliquées à des documents et des e-mails. Seuls les administrateurs peuvent sélectionner ces utilisateurs et ces groupes :

- La stratégie Azure Information Protection par défaut est automatiquement attribuée à tous les utilisateurs du Azure AD de votre locataire. Cependant, vous pouvez également affecter des étiquettes supplémentaires aux utilisateurs ou aux groupes spécifiés à l’aide de stratégies étendues.     

**Pour affecter des droits d’utilisation et des contrôles d’accès** lorsque vous utilisez le service Azure Rights Management pour protéger des documents et des e-mails. Les administrateurs et les utilisateurs peuvent sélectionner ces utilisateurs et ces groupes :

- Les droits d’utilisation déterminent si un utilisateur peut ouvrir un document ou un e-mail et comment il peut l’utiliser. Par exemple, ils indiquent s’il est en lecture seule, s’il peut le lire et l’imprimer ou le lire et le modifier uniquement. 

- Les contrôles d’accès incluent une date d’expiration et indiquent si une connexion à Internet est nécessaire pour l’accès. 

**Pour configurer le service Azure Rights Management**  afin de prendre en charge des scénarios spécifiques, et par conséquent, uniquement les administrateurs, sélectionnez ces groupes. Les exemples comprennent la configuration des éléments suivants :

- Les super utilisateurs, afin que les services désignés ou les personnes puissent ouvrir du contenu chiffré si nécessaire pour la récupération de données ou eDiscovery.

- L’administration déléguée du service Azure Rights Management.

- Les contrôles d’intégration pour la prise en charge d’un déploiement échelonné.

## <a name="azure-information-protection-requirements-for-user-accounts"></a>Configuration requise d’Azure Information Protection pour les comptes d’utilisateurs

Pour affecter des étiquettes :

- Tous les comptes d’utilisateur dans Azure AD peuvent être utilisés pour configurer les stratégies étendues qui affectent des étiquettes supplémentaires aux utilisateurs.

Pour affecter des droits d’utilisation et des contrôles d’accès et configurer le service Azure Rights Management :

- Pour autoriser les utilisateurs, deux attributs dans Azure AD sont utilisés : **proxyAddresses** et **userPrincipalName**.

- L’attribut **AD Azure proxyAddresses** stocke toutes les adresses de messagerie d’un compte et peut être rempli de différentes façons. Par exemple, un utilisateur dans Office 365 possédant une boîte aux lettres Exchange Online dispose automatiquement d’une adresse de messagerie stockée dans cet attribut. Si vous attribuez une adresse de messagerie de secours pour un utilisateur Office 365, celle-ci est également enregistrée dans cet attribut. Il peut également être alimenté par les adresses de messagerie synchronisées à partir de comptes locaux. 
    
    Azure Information Protection peut utiliser n’importe quelle valeur de cet attribut proxyAddresses Azure AD, à condition que le domaine ait été ajouté à votre locataire (un « domaine vérifié »). Pour en savoir plus sur la vérification des domaines :
    
    - Pour Azure AD : [Ajouter un nom de domaine personnalisé à Azure Active Directory](/active-directory/active-directory-add-domain)

    - Pour office 365 : [Ajouter des utilisateurs et un domaine à Office 365](https://go.microsoft.com/fwlinkid/?linkid=847121)

- L’attribut **AD Azure userPrincipalName** est utilisé uniquement lorsque le compte de votre locataire n’a aucune valeur dans l’attribut proxyAddresses Azure AD. Par exemple, vous créez un utilisateur dans le portail Azure, ou un utilisateur pour Office 365 n’ayant pas de boîte aux lettres.

### <a name="assigning-usage-rights-and-access-controls-to-external-users"></a>Attribution de droits d’utilisation et de contrôles d’accès à des utilisateurs externes

Outre l’utilisation des attributs proxyAddresses Azure AD et userPrincipalName Azure AD pour les utilisateurs de votre locataire, Azure Information Protection utilise également ces attributs de la même manière pour autoriser les utilisateurs issus d’un autre locataire.

Quand un e-mail est envoyé à l’aide du chiffrement de messages Office 365 avec de nouvelles fonctionnalités à un utilisateur ne possédant pas de compte dans Azure AD, l’utilisateur est tout d’abord authentifié à l’aide de la fédération avec un fournisseur d’identité sociale ou à l’aide d’un code secret à usage unique. Ensuite, l’adresse de messagerie spécifiée dans l’e-mail protégé est utilisée pour autoriser l’utilisateur.

## <a name="azure-information-protection-requirements-for-group-accounts"></a>Configuration requise d’Azure Information Protection pour les comptes de groupe

Pour affecter des étiquettes :

- Pour configurer des stratégies étendues qui affectent des étiquettes supplémentaires aux membres du groupe, vous pouvez utiliser n’importe quel type de groupe dans Azure AD disposant d’une adresse de messagerie contenant un domaine vérifié pour le locataire de l’utilisateur. Un groupe possédant une adresse de messagerie est souvent appelé groupe à extension de messagerie.
    
    Par exemple, vous pouvez utiliser un groupe de sécurité à extension de messagerie, un groupe de distribution (qui peut être statique ou dynamique) et un groupe Office 365. Vous ne pouvez pas utiliser de groupe de sécurité (dynamique ou statique), car ce type de groupe n’a pas d’adresse de messagerie.

Pour attribuer des droits d’utilisation et des contrôles d’accès :

- Vous pouvez utiliser n’importe quel type de groupe dans Azure AD disposant d’une adresse de messagerie qui contient un domaine vérifié pour le locataire de l’utilisateur. Un groupe possédant une adresse de messagerie est souvent appelé groupe à extension de messagerie. 

Pour configurer le service Azure Rights Management :

- Vous pouvez utiliser n’importe quel type de groupe dans Azure AD disposant d’une adresse de messagerie provenant d’un domaine vérifié de votre locataire, à une exception. Cette exception s’applique lorsque vous configurez des contrôles d’intégration pour utiliser un groupe, qui doit être un groupe de sécurité dans Azure AD pour votre locataire.

- Vous pouvez utiliser n’importe quel groupe dans Azure AD (avec ou sans adresse de messagerie) à partir d’un domaine vérifié de votre locataire pour l’administration déléguée du service Azure Rights Management.

### <a name="assigning-usage-rights-and-access-controls-to-external-groups"></a>Attribution de droits d’utilisation et de contrôles d’accès à des groupes externes

Outre l’utilisation des attributs proxyAddresses Azure AD pour les groupes de votre locataire, Azure Information Protection utilise également cet attribut de la même manière pour autoriser les groupes issus d’un autre locataire.

## <a name="using-accounts-from-active-directory-on-premises-for-azure-information-protection"></a>Utilisation de comptes à partir d’Active Directory en local pour Azure Information Protection

Si vous souhaitez utiliser des comptes gérés en local avec Azure Information Protection, vous devez les synchroniser avec Azure AD. Pour faciliter le déploiement, nous vous recommandons d’utiliser [Azure AD Connect](/azure/active-directory/connect/active-directory-aadconnect). Toutefois, vous pouvez utiliser n’importe quelle méthode de synchronisation d’annuaires permettant d’obtenir le même résultat.

Lorsque vous synchronisez vos comptes, vous n’avez pas besoin de synchroniser tous les attributs. Pour obtenir la liste des attributs qui doivent être synchronisés, consultez la section [Azure RMS](/azure/active-directory/connect/active-directory-aadconnectsync-attributes-synchronized#azure-rms) dans la documentation relative à Azure Active Directory.

Dans la liste des attributs pour Azure Rights Management, vous constatez que pour les utilisateurs, les attributs AD locaux de **mail**, **proxyAddresses**, et **userPrincipalName** sont requis pour la synchronisation. Les valeurs pour **mail** et **proxyAddresses** sont synchronisées avec l’attribut proxyAddresses Azure AD. Pour en savoir plus, consultez [Comment l’attribut proxyAddresses est rempli dans Azure AD](https://support.microsoft.com/help/3190357/how-the-proxyaddresses-attribute-is-populated-in-azure-ad)

## <a name="confirming-your-users-and-groups-are-prepared-for-azure-information-protection"></a>Confirmation de la préparation de vos utilisateurs et groupes pour Azure Information Protection

Vous pouvez utiliser Azure AD PowerShell pour confirmer que les utilisateurs et les groupes sont utilisables avec Azure Information Protection. Vous pouvez également utiliser PowerShell pour vérifier les valeurs pouvant être utilisées pour les autoriser. 

Par exemple, à l’aide du module PowerShell V1 pour Azure Active Directory, [MSOnline](/powershell/module/msonline/?view=azureadps-1.0), dans une session PowerShell, commencez par vous connecter au service et renseignez vos informations d’identification d’administrateur global :

    Connect-MsolService


Remarque : si cette commande ne fonctionne pas, vous pouvez exécuter `Install-Module MSOnline` pour installer le module MSOnline.

Ensuite, configurez votre session PowerShell afin que les valeurs ne soient pas tronquées :

    $Formatenumerationlimit =-1

### <a name="confirm-user-accounts-are-ready-for-azure-information-protection"></a>Confirmer que les comptes d’utilisateur sont prêts pour Azure Information Protection

Pour confirmer les comptes d’utilisateur, exécutez la commande suivante :

    Get-Msoluser | select DisplayName, UserPrincipalName, ProxyAddresses

La première vérification consiste à s’assurer que les utilisateurs que vous souhaitez utiliser avec Azure Information Protection sont affichés.

Vérifiez ensuite que la colonne **ProxyAddresses** est remplie. Si c’est le cas, les valeurs d’e-mail de cette colonne peuvent être utilisées pour autoriser l’utilisateur pour Azure Information Protection.

Si la colonne **ProxyAddresses** n’est pas remplie, la valeur de l’attribut **UserPrincipalName** est utilisée pour autoriser l’utilisateur pour le service Azure Rights Management.

Exemple :

|Nom complet|UserPrincipalName|ProxyAddresses
|-------------------|-----------------|--------------------|
|Jagannath Reddy |jagannathreddy@contoso.com|{}|
|Ankur Roy|ankurroy@contoso.com|{SMTP:ankur.roy@contoso.com, smtp: ankur.roy@onmicrosoft.contoso.com}|

Dans cet exemple :

- Le compte d’utilisateur pour Jagannath Reddy sera autorisé par **jagannathreddy@contoso.com**.

-  Le compte d’utilisateur pour Ankur Roy peut être autorisé à l’aide de **ankur.roy@contoso.com** et **ankur.roy@onmicrosoft.contoso.com**, mais pas **ankurroy@contoso.com**.

Dans la plupart des cas, la valeur pour UserPrincipalName correspond à une des valeurs du champ ProxyAddresses. Il s’agit de la configuration recommandée, mais si vous ne pouvez pas modifier votre UPN pour qu’il corresponde à l’adresse de messagerie, vous devez procéder comme suit :

1. Si le nom de domaine de la valeur de l’UPN est un domaine vérifié pour votre locataire Azure AD, ajoutez la valeur de l’UPN en tant qu’autre adresse de messagerie dans Azure AD afin qu’elle puisse maintenant être utilisée pour autoriser le compte d’utilisateur pour Azure Information Protection.

    Si le nom de domaine de la valeur de l’UPN n’est pas un domaine vérifié pour votre locataire, il ne peut pas être utilisé avec Azure Information Protection. Toutefois, l’utilisateur peut encore être autorisé en tant que membre d’un groupe lorsque l’adresse de messagerie du groupe utilise un nom de domaine vérifié.

2. Si l’UPN n’est pas routable (par exemple, **ankurroy@contoso.local**), Configurez un ID de connexion de secours pour les utilisateurs et expliquez-leur comment se connecter à Office à l’aide de cette connexion de secours. Vous devez également définir une clé de Registre pour Office.

    Pour plus d’informations, consultez [Configuring Alternate Login ID](/windows-server/identity/ad-fs/operations/configuring-alternate-login-id) (Configuration d’un ID de connexion de secours) et [Office applications periodically prompt for credentials to SharePoint Online, OneDrive, and Lync Online](https://support.microsoft.com/help/2913639/office-applications-periodically-prompt-for-credentials-to-sharepoint-online,-onedrive,-and-lync-online) (Les applications Office invitent régulièrement à saisir les informations d’identification pour SharePoint Online, OneDrive et Lync Online).

> [!TIP]
> Vous pouvez utiliser l’applet de commande Export-Csv pour exporter les résultats dans une feuille de calcul pour faciliter les tâches de gestion, telles que la recherche et la modification en bloc pour l’importation.
>
> Par exemple : `Get-MsolGroup | select DisplayName, ProxyAddresses | Export-Csv -Path UserAccounts.csv`

### <a name="confirm-group-accounts-are-ready-for-azure-information-protection"></a>Confirmer que les comptes de groupe sont prêts pour Azure Information Protection

Pour confirmer les comptes de groupe, utilisez la commande suivante :

    Get-MsolGroup | select DisplayName, ProxyAddresses

Assurez-vous que les groupes que vous souhaitez utiliser avec Azure Information Protection sont affichés. Pour les groupes affichés, les adresses de messagerie figurant dans la colonne **ProxyAddresses** peuvent être utilisées pour autoriser les membres du groupe pour le service Azure Rights Management.

Vérifiez ensuite que les groupes contiennent les utilisateurs (ou les autres groupes) que vous souhaitez utiliser pour Azure Information Protection. Vous pouvez utiliser PowerShell pour ce faire (par exemple, [Get-MsolGroupMember](/powershell/module/msonline/Get-MsolGroupMember?view=azureadps-1.0)), ou utiliser votre portail de gestion.

Pour les deux scénarios de configuration du service Azure Rights Management utilisant des groupes de sécurité, vous pouvez utiliser la commande PowerShell suivante pour rechercher l’ID d’objet et le nom d’affichage qui peut être utilisé pour identifier ces groupes. Vous pouvez également utiliser le portail Azure pour rechercher ces groupes et copier les valeurs pour l’ID d’objet et le nom d’affichage :

    Get-MsolGroup | where {$_.GroupType -eq "Security"}

## <a name="considerations-for-azure-information-protection-if-email-addresses-change"></a>Éléments à prendre en compte pour Azure Information Protection en cas de modification de l’adresse de messagerie

Si vous modifiez l’adresse de messagerie d’un utilisateur ou d’un groupe, nous recommandons d’ajouter l’ancienne adresse de messagerie comme deuxième adresse de messagerie (également appelée adresse proxy, alias ou adresse de messagerie de secours) à l’utilisateur ou au groupe. Lorsque vous effectuez cette opération, l’ancienne adresse de messagerie est ajoutée à l’attribut proxyAddresses Azure AD. L’administration de ce compte permet de garantir la continuité d’activité pour les droits d’utilisation ou les autres configurations enregistrées lors de l’utilisation de l’ancienne adresse de messagerie. 

Si vous ne pouvez pas effectuer cette opération, l’utilisateur ou le groupe associé à la nouvelle adresse de messagerie risque de se voir refuser l’accès aux documents et e-mails précédemment protégés avec l’ancienne adresse de messagerie. Dans ce cas, vous devez répéter la configuration de la protection pour enregistrer la nouvelle adresse de messagerie. Par exemple, si l’utilisateur ou le groupe a obtenu des droits d’utilisation dans des modèles ou des étiquettes, modifiez ces derniers et affectez à la nouvelle adresse de messagerie les mêmes droits d’utilisation que l’ancienne adresse.

Notez qu’il est rare qu’un groupe modifie son adresse de messagerie et que si vous attribuez des droits d’utilisation à un groupe plutôt qu’à des utilisateurs individuels, peu importe si l’adresse de messagerie de l’utilisateur change. Dans ce scénario, les droits d’utilisation sont attribués à l’adresse de messagerie du groupe et non à celle de chaque utilisateur. Il s’agit de la méthode la plus probable (et recommandée) qui permet à un administrateur de configurer des droits d’utilisation protégeant des documents et e-mails. Toutefois, il se peut que les utilisateurs attribuent plus généralement des autorisations personnalisées à des utilisateurs individuels. Dans la mesure où vous ne pouvez pas toujours savoir si un compte d’utilisateur ou un groupe a été utilisé pour accorder un accès, il est plus sûr de toujours ajouter l’ancienne adresse de messagerie comme une deuxième adresse de messagerie.

## <a name="group-membership-caching-by-azure-information-protection"></a>Mise en cache de l’appartenance à un groupe par Azure Information Protection

Pour des raisons de performances, Azure Information Protection met en cache l’appartenance au groupe. Cela signifie que toute mise en application d’une modification apportée à l’appartenance au groupe dans Azure AD peut prendre jusqu’à trois heures lorsque ces groupes sont utilisés par Azure Information Protection et que cette période est susceptible d’être modifiée. 

N’oubliez pas de tenir compte de ce délai pour les modifications ou les tests effectués lorsque vous utilisez des groupes pour accorder des droits d’utilisation ou configurer le service Azure Rights Management, ou lorsque vous configurez des stratégies étendues.


## <a name="next-steps"></a>Étapes suivantes

Après avoir vérifié que vos utilisateurs et groupes peuvent être utilisés avec Azure Information Protection et que vous êtes prêt à démarrer la protection des documents et des e-mails, activez le service Azure Rights Management pour lancer ce service de protection des données. Pour plus d’informations, consultez [Activer Azure Rights Management](../deploy-use/activate-service.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
