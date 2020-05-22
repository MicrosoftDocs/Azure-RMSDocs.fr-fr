---
title: Active Directory l’extension d’appareil mobile Rights Management Services pour AIP
description: En savoir plus sur les extensions d’appareils mobiles Active Directory pour AIP
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 04/28/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 6dc8a5aa43b6f5d3dc53c014dd770fa87ff683a5
ms.sourcegitcommit: 8499602fba94fbfa28d7682da2027eeed6583c61
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/21/2020
ms.locfileid: "83746375"
---
# <a name="active-directory-rights-management-services-mobile-device-extension"></a>Extension Appareils mobiles AD RMS (Active Directory Rights Management Services)

 
S’applique à : Windows Server 2019, 2016, 2012 R2 et 2012

Vous pouvez télécharger l’extension d’appareil mobile (AD RMS) services AD RMS (Active Directory Rights Management Services) à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=43738) et installer cette extension sur un déploiement de AD RMS existant. Cela permet aux utilisateurs de protéger et de consommer des données sensibles quand leur appareil prend en charge les dernières applications compatibles avec l’API. Par exemple, les utilisateurs peuvent effectuer les opérations suivantes :
- Utilisez l’application Azure Information Protection pour consommer des fichiers texte protégés dans différents formats (y compris. txt,. csv et. Xml).
- Utilisez l’application Azure Information Protection pour consommer des fichiers image protégés (y compris. jpg,. gif et. TIF).
- Utilisez l’application Azure Information Protection pour ouvrir un fichier qui a été protégé de façon générique (format. pfile).
- Utilisez l’application Azure Information Protection pour ouvrir un fichier Office (Word, Excel, PowerPoint) qui est une copie PDF (format. pdf et. ppdf).
- Utilisez l’application Azure Information Protection pour ouvrir des messages électroniques protégés (. rpmsg) et des fichiers PDF protégés sur Microsoft SharePoint.
- Utilisez une visionneuse PDF à l’aide d’AIP pour l’affichage multiplateforme ou pour ouvrir des fichiers PDF protégés par des applications compatibles AIP.
- Utilisez vos applications développées en interne et compatibles AIP qui ont été écrites à l’aide du [Kit de développement logiciel (SDK) MIP](https://aka.ms/mipsdkdocs).

> [!NOTE]
> Vous pouvez télécharger l’application Azure Information Protection à partir de la page [microsoft Rights Management](https://go.microsoft.com/fwlink/?linkid=303970) du site Web Microsoft. Pour plus d’informations sur les autres applications prises en charge avec l’extension d’appareil mobile, consultez le tableau dans la page [applications](https://docs.microsoft.com/azure/information-protection/requirements-applications) de cette documentation. Pour plus d’informations sur les différents types de fichiers pris en charge par RMS, consultez la section types de fichiers [et extensions de nom de fichier pris en charge](https://docs.microsoft.com/rights-management/rms-client/sharing-app-admin-guide-technical%23supported-file-types-and-file-name-extensions) dans le Guide de l’administrateur de l’application de partage Rights Management.

> [!IMPORTANT]
> Veillez à lire et à configurer les composants requis avant d’installer l’extension d’appareil mobile.

Pour plus d’informations, téléchargez le livre blanc « Microsoft Azure Information Protection » et les scripts qui l’accompagnent à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=40333).

## <a name="prerequisites-for-ad-rms-mobile-device-extension"></a>Conditions préalables pour AD RMS extension d’appareil mobile

Avant d’installer l’extension de périphérique mobile AD RMS, assurez-vous que les dépendances suivantes sont en place.


|Condition requise|Informations complémentaires|
|---------------|------------------------|
|Un déploiement de AD RMS existant sur Windows Server 2019, 2016, 2012 R2 ou 2012, qui comprend les éléments suivants :<br /><br /> -Votre cluster AD RMS doit être accessible à partir d’Internet. <br /><br /> -AD RMS devez utiliser une base de données Microsoft SQL Server complète sur un serveur distinct, et non sur la base de données interne Windows qui est souvent utilisée pour le test sur le même serveur. <br /><br />-Le compte que vous allez utiliser pour installer l’extension d’appareil mobile doit disposer des droits d’administrateur système pour l’instance de SQL Server que vous utilisez pour AD RMS. <br /><br />-Les serveurs AD RMS doivent être configurés pour utiliser SSL/TLS avec un certificat x. 509 valide qui est approuvé par les clients de périphériques mobiles.<br /><br /> -Si les serveurs AD RMS se trouvent derrière un pare-feu ou publiés à l’aide d’un proxy inverse, en plus de la publication du dossier **/_wmcs** sur Internet, vous devez également publier le dossier/My (par exemple : **_https : \/ \/ RMSserver.contoso.com/my**).|Pour plus d’informations sur les conditions préalables et les informations de déploiement de AD RMS, consultez la section conditions préalables de cet article.|
|AD FS déployé sur votre serveur Windows :<br /><br /> -Votre batterie de serveurs AD FS doit être accessible à partir d’Internet (vous avez déployé des serveurs proxys de Fédération). <br /><br />-L’authentification basée sur les formulaires n’est pas prise en charge. vous devez utiliser l’authentification intégrée de Windows <br /><br /> **Important**: AD FS devez exécuter un ordinateur différent de l’ordinateur exécutant AD RMS et l’extension d’appareil mobile.|Pour obtenir de la documentation sur AD FS, consultez le [Guide de déploiement de Windows server AD FS](https://docs.microsoft.com/office365/troubleshoot/active-directory/set-up-adfs-for-single-sign-on) dans la bibliothèque Windows Server.<br /><br /> Les services AD FS doivent être configurés pour l'extension Appareils mobiles. Pour obtenir des instructions, voir la section **configuration de AD FS pour l’extension de périphérique mobile AD RMS** de cette rubrique.|
|Les appareils mobiles doivent approuver les certificats PKI sur le ou les serveurs RMS.|Lorsque vous achetez vos certificats de serveur auprès d’une autorité de certification publique, telle que VeriSign ou Comodo, il est probable que les appareils mobiles approuvent déjà l’autorité de certification racine pour ces certificats, afin que ces appareils approuvent les certificats de serveur sans configuration supplémentaire.<br /><br /> Toutefois, si vous utilisez votre propre autorité de certification interne pour déployer les certificats de serveur pour RMS, vous devez prendre des mesures supplémentaires pour installer le certificat d’autorité de certification racine sur les périphériques mobiles. Si vous ne le faites pas, les périphériques mobiles ne seront pas en mesure d’établir une connexion avec le serveur RMS.|
|Enregistrements SRV dans DNS|Créez un ou plusieurs enregistrements SRV dans le ou les domaines de votre entreprise :<br /><br />1 : créer un enregistrement pour chaque suffixe de domaine de messagerie qui sera utilisé par les utilisateurs <br /><br />2 : créer un enregistrement pour chaque nom de domaine complet utilisé par vos clusters RMS pour protéger du contenu, à l’exclusion du nom du cluster <br /><br />Ces enregistrements doivent pouvoir être résolus à partir de tout réseau utilisé par les périphériques mobiles qui se connectent, y compris l’intranet si vos appareils mobiles se connectent via l’intranet.<br /><br /> Lorsque les utilisateurs fournissent leur adresse de messagerie à partir de leur appareil mobile, le suffixe de domaine est utilisé pour déterminer s’ils doivent utiliser une infrastructure AD RMS ou Azure AIP. Quand l'enregistrement SRV est trouvé, les clients sont redirigés vers le serveur AD RMS qui répond à cette URL.<br /><br /> Quand les utilisateurs consomment du contenu protégé avec un appareil mobile, l’application cliente recherche dans DNS un enregistrement qui correspond au nom de domaine complet dans l’URL du cluster qui a protégé le contenu (sans le nom du cluster). L'appareil est ensuite dirigé vers le cluster AD RMS spécifié dans l'enregistrement DNS et obtient une licence pour ouvrir le contenu. Dans la plupart des cas, le cluster RMS sera le même cluster RMS qui a protégé le contenu.<br /><br /> Pour plus d’informations sur la façon de spécifier les enregistrements SRV, consultez la section **spécification des enregistrements SRV DNS pour l’extension de périphérique mobile AD RMS** dans cette rubrique.|
|Clients pris en charge qui utilisent des applications développées à l’aide du kit de développement logiciel (SDK) MIP pour cette plateforme. |Téléchargez les applications prises en charge pour les appareils que vous utilisez à l’aide des liens de la page de téléchargement [Microsoft Azure information protection](https://www.microsoft.com/download/details.aspx?id=40333) .|

### <a name="configuring-ad-fs-for-the-ad-rms-mobile-device-extension"></a>Configuration des services AD FS pour l'extension Appareils mobiles AD RMS

Vous devez d’abord configurer AD FS, puis autoriser l’application AIP pour les appareils que vous souhaitez utiliser.

#### <a name="step-1-to-configure-ad-fs"></a>Étape 1 : configurer AD FS

- Vous pouvez exécuter un script Windows PowerShell pour configurer automatiquement les services AD FS pour prendre en charge l'extension Appareils mobiles AD RMS, ou vous pouvez spécifier manuellement les valeurs et options de configuration :
    - Pour configurer automatiquement AD FS pour l’extension d’appareil mobile AD RMS, copiez et collez le code suivant dans un fichier de script Windows PowerShell, puis exécutez-le :

```powershell
# This Script Configures the Microsoft Rights Management Mobile Device Extension and Claims used in the ADFS Server

# Check if Microsoft Rights Management Mobile Device Extension is configured on the Server
$CheckifConfigured = Get-AdfsRelyingPartyTrust -Identifier "api.rms.rest.com"
if ($CheckifConfigured)
{
Write-Host "api.rms.rest.com Identifer used for Microsoft Rights Management Mobile Device Extension is already configured on this Server"
Write-Host $CheckifConfigured
}
else
{
Write-Host "Configuring  Microsoft Rights Management Mobile Device Extension "

# TransformaRules used by Microsoft Rights Management Mobile Device Extension
# Claims: E-mail, UPN and ProxyAddresses
$TransformRules = @"
@RuleTemplate = "LdapClaims"
@RuleName = "Jwt Token"
c:[Type ==
"https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname",
Issuer == "AD AUTHORITY"]
 => issue(store = "Active Directory", types =
("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress",
"http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn",
"http://schemas.xmlsoap.org/claims/ProxyAddresses"), query =
";mail,userPrincipalName,proxyAddresses;{0}", param = c.Value);

@RuleTemplate = "PassThroughClaims"
@RuleName = "JWT pass through"
c:[Type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"]
 => issue(claim = c);

@RuleTemplate = "PassThroughClaims"
@RuleName = "JWT pass through"
c:[Type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"]
 => issue(claim = c);

@RuleTemplate = "PassThroughClaims"
@RuleName = "JWT pass through Proxy addresses"
c:[Type == "http://schemas.xmlsoap.org/claims/ProxyAddresses"]
 => issue(claim = c);
"@

# AuthorizationRules used by Microsoft Rights Management Mobile Device Extension
# Allow All users
$AuthorizationRules = @"
@RuleTemplate = "AllowAllAuthzRule"
 => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit",
Value = "true");
"@

# Add a Relying Part Truest with Name -"Microsoft Rights Management Mobile Device Extension" Identifier "api.rms.rest.com"
Add-ADFSRelyingPartyTrust -Name "Microsoft Rights Management Mobile Device Extension" -Identifier "api.rms.rest.com" -IssuanceTransformRules $TransformRules -IssuanceAuthorizationRules  $AuthorizationRules

Write-Host "Microsoft Rights Management Mobile Device Extension Configured"
}
```

- Pour configurer manuellement AD FS pour l’extension d’appareil mobile AD RMS, utilisez les paramètres suivants :

|**Configuration**|**Valeur**|
|-----|-----|
|**Approbation de partie de confiance**|_api. RMS. Rest. com|
|**Règle de revendication**|**Magasin d’attributs** : Active Directory <br /><br />**Adresses de messagerie**: adresse de messagerie<br /><br>**User-principal-name**: UPN<br /><br /> **Adresse proxy**: _https : \/ \/ schemas.xmlsoap.org/claims/proxyAddresses|

> [!TIP]
> Pour obtenir des instructions pas à pas pour un exemple de déploiement de AD RMS avec AD FS, consultez [déploiement de services AD RMS (Active Directory Rights Management Services) avec services ADFS](https://docs.microsoft.com/office365/troubleshoot/active-directory/set-up-adfs-for-single-sign-on).

#### <a name="step-2-authorize-apps-for-your-devices"></a>Étape 2 : autoriser les applications pour vos appareils

1. Exécutez la commande Windows PowerShell suivante après avoir remplacé les variables pour ajouter la prise en charge de l’application Azure Information Protection :


```powershell
Add-AdfsClient -Name "R<your application name> " -ClientId "<YOUR CLIENT ID >" -RedirectUri @("<YOUR REDIRECT URI >")
```

**Exemple PowerShell**
```powershell
Add-AdfsClient -Name "Fabrikam application for MIP" -ClientId "96731E97-2204-4D74-BEA5-75DCA53566C3" -RedirectUri @("com.fabrikam.MIPAPP://authorize")
```

### <a name="specifying-the-dns-srv-records-for-the-ad-rms-mobile-device-extension"></a>Spécification des enregistrements SRV DNS pour l’extension d’appareil mobile AD RMS

Vous devez créer des enregistrements SRV DNS pour chaque domaine de messagerie employé par les utilisateurs. Si tous vos utilisateurs emploient des domaines enfants depuis un domaine parent unique et que tous les utilisateurs de cet espace de noms contigu emploient le même cluster RMS, vous pouvez utiliser un seul enregistrement SRV dans le domaine parent et RMS trouvera les enregistrements DNS appropriés.
Les enregistrements SRV ont le format suivant : _rmsdisco. _http. _tcp. \<emailsuffix>\< numéro_port>\< RMSClusterFQDN>

> [!NOTE]
> Spécifiez 443 pour le \< numéro_port>. Bien que vous puissiez spécifier un numéro de port différent dans DNS, les appareils qui utilisent l’extension d’appareil mobile utilisent toujours 443.

Par exemple, si votre organisation a des utilisateurs avec les adresses de messagerie suivantes :
  - _user@contoso.com
  - _user@sales.contoso.com
  - _user@fabrikam.comS’il n’existe aucun autre domaine enfant pour _contoso. com qui utilise un cluster RMS différent de celui nommé _rmsserver. contoso. com, créez deux enregistrements SRV DNS qui ont les valeurs suivantes :
- _rmsdisco. _http. _tcp. contoso. com 443 _rmsserver. contoso. com
- _rmsdisco. _http. _tcp. fabrikam. com 443 _rmsserver. contoso. com

Si vous utilisez le rôle serveur DNS sur Windows Server, utilisez les tableaux suivants comme guide pour les propriétés de l’enregistrement SRV dans la console du Gestionnaire DNS :

|Champ|Valeur|
|------|------|
|Domain|_tcp. contoso. com
|Service|_rmsdisco
|Protocol|_http
|Priority|0
|Poids|0
|Numéro de port|443
|Hôte offrant ce service|_rmsserver. contoso. com

|Champ|Valeur|
|------|------|
|Domain|_tcp. fabrikam. com
|Service|_rmsdisco
|Protocol|_http
|Priority|0
|Poids|0
|Numéro de port|443
|Hôte offrant ce service|_rmsserver. contoso. com|

En plus de ces enregistrements SRV DNS pour votre domaine de messagerie, vous devez créer un autre enregistrement DNS SRV dans le domaine de cluster RMS. Cet enregistrement doit spécifier les noms de domaine complets de votre cluster RMS qui protègent le contenu. Chaque fichier qui est protégé par RMS inclut une URL vers le cluster qui a protégé ce fichier. Les appareils mobiles utilisent l'enregistrement SRV DNS et le nom de domaine complet de l'URL spécifié dans l'enregistrement pour trouver le cluster RMS correspondant qui peut prendre en charge des appareils mobiles.

Par exemple, si votre cluster RMS est **_rmsserver. contoso. com**, créez un enregistrement SRV DNS qui a les valeurs suivantes : **_rmsdisco. _http. _tcp. contoso. com 443 _rmsserver. contoso. com**

Si vous utilisez le rôle serveur DNS sur Windows Server, utilisez le tableau suivant comme guide pour les propriétés de l’enregistrement SRV dans la console du Gestionnaire DNS :

|Champ|Valeur|
|------|------|
|Domain|_tcp. contoso. com
|Service|_rmsdisco
|Protocol|_http
|Priority|0
|Poids|0
|Numéro de port|443
|Hôte offrant ce service|_rmsserver. contoso. com|

## <a name="deploying-the-ad-rms-mobile-device-extension"></a>Déploiement de l'extension Appareils mobiles AD RMS

Avant d’installer l’extension d’appareil mobile AD RMS, assurez-vous que les conditions préalables de la section précédente sont en place et que vous connaissez l’URL de votre serveur de AD FS. Faites ensuite ce qui suit :

1. Téléchargez l’extension d’appareil mobile AD RMS (ADRMS. MobileDeviceExtension. exe) à partir du centre de téléchargement Microsoft.
1. Exécutez **ADRMS. MobileDeviceExtension. exe** pour démarrer services AD RMS (Active Directory Rights Management Services) l’Assistant Installation d’une extension de périphérique mobile.
Quand vous y êtes invité, entrez l'URL du serveur AD FS que vous avez configuré précédemment.
1. Effectuez toutes les étapes de l'Assistant.

Exécutez cet Assistant sur tous les nœuds de votre cluster RMS.

Si vous avez un serveur proxy entre le cluster AD RMS et les serveurs AD FS, par défaut, votre cluster AD RMS ne pourra pas contacter le service fédéré. Dans ce cas, AD RMS ne peut pas vérifier le jeton reçu du client mobile et rejette la demande. Si vous avez un serveur proxy qui bloque cette communication, vous devez mettre à jour le fichier Web. config à partir du site Web d’extension de périphérique mobile AD RMS, afin que AD RMS puisse contourner le serveur proxy lorsqu’il doit contacter les serveurs de AD FS.

#### <a name="updating-proxy-settings-for-the-ad-rms-mobile-device-extension"></a>Mise à jour des paramètres de proxy pour l’extension d’appareil mobile AD RMS

1. Ouvrez le fichier Web. config qui se trouve dans **\Program Files\Active Directory Rights Management Services Mobile Device Extension\Web service**.

1. Ajoutez le nœud suivant au fichier :

```powershell
   <system.net>
    <defaultProxy>
        <proxy  proxyaddress="http://<proxy server>:<port>"
                bypassonlocal="true"
        />
        <bypasslist>
            <add address="<AD FS URL>" />
        </bypasslist>
    </defaultProxy>
<system.net>
```
1. Apportez les modifications suivantes, puis enregistrez le fichier :
- Remplacez \< proxy-server> par le nom ou l’adresse de votre serveur proxy.
- Remplacez le \< port> par le numéro de port que le serveur proxy est configuré pour utiliser.
- Remplacez \< AD FS url> par l’URL du service de Fédération. N’incluez pas le préfixe HTTP.

    > [!NOTE]
    > Pour en savoir plus sur le remplacement des paramètres de proxy, consultez la documentation sur la [configuration du proxy](https://msdn.microsoft.com/library/dkwyc043(v=vs.110).aspx) .

1. Réinitialisez IIS, par exemple, en exécutant **IISReset** en tant qu’administrateur à partir d’une invite de commandes.

Répétez cette procédure sur tous les nœuds de votre cluster RMS.


## <a name="see-also"></a>Voir aussi

Pour en savoir plus sur les Azure Information Protection, contactez les autres clients AIP et les responsables de produit AIP à l’aide du [groupe Yammer d’API](https://www.yammer.com/askipteam/). 

