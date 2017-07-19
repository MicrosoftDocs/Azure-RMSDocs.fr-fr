---
title: "Préparer des utilisateurs et groupes pour Azure Information Protection"
description: "Vérifiez que vous disposez des comptes d’utilisateur et de groupe dont vous avez besoin pour démarrer la classification, l’étiquetage et la protection des documents et e-mails de votre organisation."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/13/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: afbca2d6-32a7-4bda-8aaf-9f93f5da5abc
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: f49d00317503f23d03ae64aa3608375b871b3854
ms.sourcegitcommit: 1dee39e5e3b222b4aab2b6c4284b82927148407e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/13/2017
---
# <a name="preparing-users-and-groups-for-azure-information-protection"></a>Préparation des utilisateurs et groupes pour Azure Information Protection

>*S’applique à : Azure Information Protection, Office 365*

Avant de déployer Azure Information Protection dans votre organisation, vérifiez que vous avez des comptes pour les utilisateurs et groupes dans Azure AD pour le locataire de votre organisation.

Il existe différentes façons de créer ces comptes pour les utilisateurs et groupes, notamment :

- Créez les utilisateurs dans le centre d’administration Office 365 et les groupes dans le centre d’administration Exchange Online.

- Créez les utilisateurs et groupes dans le portail Azure.

- Créez les utilisateurs et groupes à l’aide des applets de commande Azure AD PowerShell et Exchange Online.

- Créez les utilisateurs et groupes dans votre annuaire Active Directory local et synchronisez-les avec Azure AD.

- Créez les utilisateurs et groupes dans un autre annuaire et synchronisez-les avec Azure AD.

Quand vous créez des utilisateurs et groupes à l’aide des trois premières méthodes de cette liste, ils sont automatiquement créés dans Azure AD et Azure Information Protection peut utiliser ces comptes directement. Toutefois, de nombreux réseaux d’entreprise utilisent un annuaire local pour créer et gérer les utilisateurs et groupes. Azure Information Protection ne peut pas utiliser ces comptes directement. Vous devez les synchroniser avec Azure AD.

## <a name="how-users-and-groups-are-used-by-azure-information-protection"></a>Comment les utilisateurs et groupes sont utilisés par Azure Information Protection

Il existe trois scénarios d’utilisation des utilisateurs et des groupes avec Azure Information Protection :

**Pour affecter des étiquettes aux utilisateurs** quand vous configurez la stratégie Azure Information Protection afin que les étiquettes puissent être appliquées à des documents et e-mails. Seuls les administrateurs peuvent sélectionner ces utilisateurs et groupes :

- La stratégie Azure Information Protection par défaut est automatiquement attribuée à tous les utilisateurs de l’annuaire Azure AD de votre locataire. Toutefois, vous pouvez également affecter d’autres étiquettes à des utilisateurs ou groupes spécifiés à l’aide de stratégies délimitées.     

**Pour affecter des droits d’utilisation et des contrôles d’accès** quand vous utilisez le service Azure Rights Management pour protéger les documents et e-mails. Les administrateurs et utilisateurs peuvent sélectionner ces utilisateurs et groupes :

- Les droits d’utilisation déterminent si un utilisateur peut ouvrir un document ou e-mail et comment il peut l’utiliser, par exemple s’il peut uniquement le lire, le lire et l’imprimer, ou le lire et le modifier. 

- Les contrôles d’accès incluent une date d’expiration et indiquent si une connexion à Internet est nécessaire pour l’accès. 

**Pour configurer le service Azure Rights Management** afin de prendre en charge des scénarios spécifiques. Par conséquent, seuls les administrateurs sélectionnent ces groupes. Les exemples incluent la configuration des éléments suivants :

- Super utilisateurs, afin que les personnes ou services désignés puissent ouvrir le contenu chiffré si cela est nécessaire pour la récupération de données ou découverte électronique (eDiscovery).

- Administration déléguée du service Azure Rights Management.

- Contrôles d’intégration pour prendre en charge un déploiement à plusieurs phases.

## <a name="azure-information-protection-requirements-for-user-accounts"></a>Configuration requise d’Azure Information Protection pour les comptes d’utilisateur

Pour affecter des étiquettes :

- Tous les comptes d’utilisateur dans Azure AD peuvent être utilisés pour configurer des stratégies délimitées qui affectent des étiquettes supplémentaires aux utilisateurs.

Pour affecter des droits d’utilisation et des contrôles d’accès, et configurer le service Azure Rights Management :

- Pour autoriser les utilisateurs, deux attributs dans Azure AD sont utilisés : **proxyAddresses** et **userPrincipalName**.

- L’attribut **proxyAddresses d’Azure AD** stocke toutes les adresses e-mail pour un compte et peut être rempli de différentes façons. Par exemple, un utilisateur dans Office 365 avec une boîte aux lettres Exchange Online a automatiquement une adresse e-mail stockée dans cet attribut. Si vous attribuez une autre adresse e-mail pour un utilisateur Office 365, elle est également enregistrée dans cet attribut. Il peut également être rempli par les adresses e-mail qui sont synchronisées à partir de comptes locaux. 
    
    Azure Information Protection peut utiliser n’importe quelle valeur dans cet attribut proxyAddresses d’Azure AD si le domaine a été ajouté à votre locataire (un « domaine vérifié »). Pour plus d’informations sur la vérification des domaines :
    
    - Pour Azure AD : [Ajouter un nom de domaine personnalisé à Azure Active Directory](/active-directory/active-directory-add-domain)
    
    - Pour Office 365 : [Ajouter un domaine et des utilisateurs à Office 365](https://go.microsoft.com/fwlinkid/?linkid=847121)

- L’attribut **userPrincipalName d’Azure AD** est utilisé uniquement quand un compte dans votre locataire n’a aucune valeur dans l’attribut proxyAddresses d’Azure AD. Par exemple, vous créez un utilisateur dans le portail Azure, ou créez un utilisateur pour Office 365 qui n’a pas de boîte aux lettres.

### <a name="assigning-usage-rights-and-access-controls-to-external-users"></a>Affectation des droits d’utilisation et des contrôles d’accès à des utilisateurs externes

En plus d’utiliser les attributs proxyAddresses et userPrincipalName d’Azure AD pour les utilisateurs dans votre locataire, Azure Information Protection utilise également ces attributs de la même manière pour autoriser les utilisateurs d’un autre locataire.

## <a name="azure-information-protection-requirements-for-group-accounts"></a>Configuration requise d’Azure Information Protection pour les comptes de groupe

Pour affecter des étiquettes :

- Pour configurer des stratégies avec étendue qui attribuent des étiquettes supplémentaires aux membres du groupe, vous pouvez utiliser n’importe quel type de groupe dans Azure AD ayant une adresse e-mail avec un domaine vérifié pour le locataire de l’utilisateur. Un groupe qui possède une adresse e-mail est souvent appelé groupe à extension messagerie.
    
    Par exemple, vous pouvez utiliser un groupe de sécurité à extension messagerie, un groupe de distribution (qui peut être statique ou dynamique) et un groupe Office 365. Vous ne pouvez pas utiliser un groupe de sécurité (dynamique ou statique), car ce type de groupe n’a pas d’adresse e-mail.

Pour affecter des droits d’utilisation et des contrôles d’accès :

- Vous pouvez utiliser n’importe quel type de groupe dans Azure AD qui a une adresse e-mail contenant un domaine vérifié pour le locataire de l’utilisateur. Un groupe qui possède une adresse e-mail est souvent appelé groupe à extension messagerie. 

Pour configurer le service Azure Rights Management :

- Vous pouvez utiliser n’importe quel type de groupe dans Azure AD qui a une adresse e-mail à partir d’un domaine vérifié dans votre locataire, à une exception près : quand vous configurez des contrôles d’intégration pour utiliser un groupe, qui doit être un groupe de sécurité dans Azure AD pour votre locataire.
    
- Vous pouvez utiliser n’importe quel type de groupe dans Azure AD (avec ou sans adresse e-mail) à partir d’un domaine vérifié dans votre locataire pour l’administration déléguée du service Azure Rights Management.

### <a name="assigning-usage-rights-and-access-controls-to-external-groups"></a>Affectation des droits d’utilisation et des contrôles d’accès à des groupes externes

En plus d’utiliser l’attribut proxyAddresses d’Azure AD pour les groupes dans votre locataire, Azure Information Protection utilise également cet attribut de la même manière pour autoriser les groupes d’un autre locataire.

## <a name="using-accounts-from-active-directory-on-premises-for-azure-information-protection"></a>Utilisation de comptes de l’annuaire Active Directory local pour Azure Information Protection

Si vous disposez de comptes qui sont gérés en local et que vous souhaitez utiliser avec Azure Information Protection, vous devez les synchroniser avec Azure AD. Pour faciliter le déploiement, nous vous recommandons d’utiliser [Azure AD Connect](/azure/active-directory/connect/active-directory-aadconnect). Toutefois, vous pouvez utiliser toute méthode de synchronisation d’annuaires qui aboutit au même résultat.

Quand vous synchronisez vos comptes, il est inutile de synchroniser tous les attributs. Pour obtenir la liste des attributs qui doivent être synchronisés, consultez la [section relative à Azure RMS](/azure/active-directory/connect/active-directory-aadconnectsync-attributes-synchronized#azure-rms) dans la documentation d’Azure Active Directory. 

Dans la liste d’attributs d’Azure Rights Management, pour les utilisateurs, les attributs AD locaux **mail**, **proxyAddresses** et **userPrincipalName** sont nécessaires pour la synchronisation. Les valeurs pour **mail** et **proxyAddresses** sont synchronisées avec l’attribut proxyAddresses d’Azure AD. Pour plus d’informations, consultez [Comment l’attribut proxyAddresses est rempli dans Azure AD](https://support.microsoft.com/help/3190357/how-the-proxyaddresses-attribute-is-populated-in-azure-ad)

## <a name="confirming-your-users-and-groups-are-prepared-for-azure-information-protection"></a>Confirmation que vos utilisateurs et groupes sont préparés pour Azure Information Protection

Vous pouvez utiliser Azure AD PowerShell pour confirmer que les utilisateurs et groupes peuvent être employés avec Azure Information Protection. Vous pouvez également utiliser PowerShell pour confirmer les valeurs qui peuvent être utilisées pour les autoriser. 

Par exemple, à l’aide du module PowerShell V1 pour Azure Active Directory, [MSOnline](/powershell/module/msonline/?view=azureadps-1.0), dans une session PowerShell, connectez-vous tout d’abord au service et indiquez vos informations d’identification d’administrateur général :

    Connect-MsolService
    

Remarque : Si cette commande ne fonctionne pas, vous pouvez exécuter `Install-Module MSOnline` pour installer le module MSOnline.

Configurez ensuite votre session PowerShell afin de ne pas tronquer les valeurs :

    $Formatenumerationlimit =-1

### <a name="confirm-user-accounts-are-ready-for-azure-information-protection"></a>Confirmez que les comptes d’utilisateur sont prêts pour Azure Information Protection

Pour confirmer les comptes d’utilisateur, exécutez la commande suivante :

    Get-Msoluser | select DisplayName, UserPrincipalName, ProxyAddresses
        
Votre première vérification consiste à vous assurer que les utilisateurs que vous souhaitez utiliser avec Azure Information Protection sont affichés. 

Vérifiez ensuite si la colonne **ProxyAddresses** est remplie. Si tel est le cas, les valeurs de messagerie dans cette colonne peuvent être utilisées pour autoriser l’utilisateur à se servir du service Azure Rights Management. 

Si la colonne **ProxyAddresses** n’est pas remplie, la valeur **UserPrincipalName** sert à autoriser l’utilisation du service Azure Rights Management.

Exemple : 
    
|Nom d’affichage|UserPrincipalName|ProxyAddresses
|-------------------|-----------------|--------------------|
|Jagannath Reddy |jagannathreddy@contoso.com|{}|
|Ankur Roy|ankurroy@contoso.com|{SMTP:ankur.roy@contoso.com, smtp : ankur.roy@onmicrosoft.contoso.com}|

Exemple :

- Le compte d’utilisateur pour Jagannath Reddy est autorisé par **jagannathreddy@contoso.com**.

-  Le compte d’utilisateur pour Ankur Roy peut être autorisé en utilisant **ankur.roy@contoso.com** et **ankur.roy@onmicrosoft.contoso.com**, mais pas **ankurroy@contoso.com**.

Dans la plupart des cas, la valeur de UserPrincipalName correspond à une valeur du champ ProxyAddresses. Cette configuration est recommandée, mais si vous ne pouvez pas changer votre valeur UPN pour qu’elle corresponde à l’adresse e-mail, vous devez suivre les étapes ci-après :

1. Si le nom de domaine dans la valeur UPN est un domaine vérifié pour votre locataire Azure AD, ajoutez la valeur UPN comme une autre adresse e-mail dans Azure AD afin que la valeur UPN puisse maintenant être utilisée pour autoriser le compte d’utilisateur pour Azure Information Protection.
    
    Si le nom de domaine dans la valeur UPN n’est pas un domaine vérifié pour votre locataire, il ne peut pas être utilisé avec Azure Information Protection. Toutefois, l’utilisateur peut toujours être autorisé en tant que membre d’un groupe quand l’adresse e-mail de groupe utilise un nom de domaine vérifié.

2. Si la valeur UPN n’est pas routable (par exemple, **ankurroy@contoso.local**), configurez un autre ID de connexion pour les utilisateurs et indiquez-leur comment se connecter à Office à l’aide de cette connexion de remplacement. Vous devez également définir une clé de Registre pour Office.
    
    Pour plus d’informations, consultez [Configuration d’un autre ID de connexion](/windows-server/identity/ad-fs/operations/configuring-alternate-login-id) et [Les applications Office demandent régulièrement des informations d’identification pour SharePoint Online, OneDrive et Lync Online](https://support.microsoft.com/help/2913639/office-applications-periodically-prompt-for-credentials-to-sharepoint-online,-onedrive,-and-lync-online).

> [!TIP]
> Vous pouvez utiliser l’applet de commande Export-Csv afin d’exporter les résultats dans une feuille de calcul pour faciliter la gestion, comme la recherche et la modification en bloc pour l’importation. 
> 
> Par exemple : `Get-MsolGroup | select DisplayName, ProxyAddresses | Export-Csv -Path UserAccounts.csv`

### <a name="confirm-group-accounts-are-ready-for-azure-information-protection"></a>Confirmer que les comptes de groupe sont prêts pour Azure Information Protection

Pour confirmer les comptes de groupe, utilisez la commande suivante :
         
    Get-MsolGroup | select DisplayName, ProxyAddresses

Vérifiez que les groupes que vous souhaitez utiliser avec Azure Information Protection sont affichés. Pour les groupes affichés, les adresses e-mail dans la colonne **ProxyAddresses** peuvent servir à autoriser les membres du groupe à utiliser le service Azure Rights Management.

Vérifiez ensuite que les groupes contiennent les utilisateurs (ou autres groupes) que vous souhaitez utiliser pour Azure Information Protection. Pour ce faire, vous pouvez utiliser PowerShell (par exemple, [Get-MsolGroupMember](/powershell/module/msonline/Get-MsolGroupMember?view=azureadps-1.0)) ou le portail de gestion. 

Pour les deux scénarios de configuration du service Azure Rights Management qui utilisent des groupes de sécurité, vous pouvez utiliser la commande PowerShell suivante pour trouver l’ID d’objet et le nom d’affichage permettant d’identifier ces groupes. Vous pouvez également utiliser le portail Azure pour rechercher ces groupes et copier les valeurs de l’ID d’objet et du nom d’affichage :

    Get-MsolGroup | where {$_.GroupType -eq "Security"}

## <a name="considerations-for-azure-information-protection-if-email-addresses-change"></a>Considérations relatives à Azure Information Protection en cas de changement des adresses e-mail

Si vous modifiez l’adresse e-mail d’un utilisateur ou d’un groupe, nous vous recommandons d’ajouter l’ancienne adresse e-mail comme une deuxième adresse e-mail (également appelée adresse proxy, alias ou autre adresse e-mail) à l’utilisateur ou au groupe. Quand vous effectuez cette opération, l’ancienne adresse e-mail est ajoutée à l’attribut proxyAddresses d’Azure AD. Cette administration des comptes permet d’assurer la continuité d’activité pour les droits d’utilisation ou d’autres configurations enregistrées quand l’ancienne adresse e-mail était utilisée. 

Si vous ne pouvez pas le faire, l’utilisateur ou le groupe avec la nouvelle adresse e-mail peut se voir refuser l’accès aux documents et e-mails qui étaient précédemment protégés, et peut être confronté à d’autres erreurs de configuration dues à l’utilisation de l’ancienne valeur. Dans ce cas, vous devez répéter la configuration pour enregistrer la nouvelle adresse e-mail. 

Notez qu’il est rare qu’un groupe change son adresse e-mail et, si vous attribuez des droits d’utilisation à un groupe plutôt qu’à des utilisateurs individuels, peu importe si l’adresse e-mail de l’utilisateur est modifiée. Dans ce scénario, les droits d’utilisation sont affectés à l’adresse e-mail de groupe et non aux adresses e-mail des utilisateurs individuels. Il s’agit de la méthode la plus probable (et recommandée) pour un administrateur qui souhaite configurer des droits d’utilisation qui protègent des documents et e-mails. Toutefois, les utilisateurs peuvent attribuer plus généralement des autorisations personnalisées aux utilisateurs individuels. Comme vous ne pouvez pas toujours savoir si un compte d’utilisateur ou un groupe a été utilisé pour accorder l’accès, il est plus sûr de toujours ajouter l’ancienne adresse e-mail comme une deuxième adresse e-mail.

## <a name="group-membership-caching-by-azure-rights-management"></a>Mise en cache de l’appartenance au groupe par Azure Rights Management

Pour des raisons de performances, l’appartenance au groupe est mise en cache par le service Azure Rights Management. Cela signifie que les modifications apportées à l’appartenance au groupe dans Azure AD peuvent prendre jusqu’à 3 heures pour entrer en vigueur quand ces groupes sont utilisés par Azure Rights Management, et cette durée est susceptible de changer. 

N’oubliez pas de tenir compte de ce délai dans l’ensemble des modifications ou tests que vous effectuez quand vous utilisez des groupes pour Azure Rights Management, par exemple quand vous attribuez des droits d’utilisation ou configurez le service Azure Rights Management. 


## <a name="next-steps"></a>Étapes suivantes

Après avoir confirmé que vos utilisateurs et groupes peuvent être utilisés avec Azure Information Protection et que vous êtes prêt à commencer à protéger des documents et des e-mails, lancez le service Rights Management pour activer ce service de protection des données. Pour plus d’informations, consultez [Activation d’Azure Rights Management](../deploy-use/activate-service.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


