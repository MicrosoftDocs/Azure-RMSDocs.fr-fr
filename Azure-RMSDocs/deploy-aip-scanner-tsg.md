---
title: Résoudre les problèmes de déploiement d’un analyseur local
description: Instructions pour la résolution des problèmes liés au déploiement d’un analyseur local d’étiquetage local
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 12/27/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: d9eadd907059bd128ac08c761128e0f1926c9f81
ms.sourcegitcommit: 0ac52ea741f205692406f0f82c74c65c23ee3467
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/27/2020
ms.locfileid: "97792294"
---
# <a name="troubleshooting-your-unified-labeling-on-premises-scanner-deployment"></a>Résolution des problèmes liés au déploiement d’un analyseur local d’étiquetage local

>***S’applique à**: [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 *
>
>***Concerne**: [client d’étiquetage unifié AIP uniquement](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). *

Utilisez le contenu de cet article pour vous aider à résoudre les problèmes liés à votre déploiement de l’analyseur local.

## <a name="troubleshooting-using-the-scanner-diagnostic-tool"></a>Résolution des problèmes à l’aide de l’outil de diagnostic du scanneur

Si vous rencontrez des problèmes avec Azure information scanner, vérifiez que votre déploiement est sain à l’aide de la commande PowerShell [Start-AIPScannerDiagnostics](/powershell/module/azureinformationprotection/start-aipscannerdiagnostics) :

```powershell
Start-AIPScannerDiagnostics
```

L’outil de diagnostic vérifie les détails suivants, puis exporte un fichier journal avec les résultats :

- Si la base de données est à jour
- Si les URL réseau sont accessibles
- Indique s’il existe un jeton d’authentification valide et si la stratégie peut être acquise
- Si le profil est défini dans le Portail Azure
- Indique si la configuration en ligne/hors connexion existe et peut être acquise
- Indique si les règles configurées sont valides

> [!TIP]
> Si vous exécutez la commande sous un utilisateur qui n’est pas l’utilisateur du scanneur, veillez à ajouter le paramètre **-OnBehalf** . 
>

> [!NOTE]
> La commande **Start-AIPScannerDiagnostics** n’exécute pas une vérification de la configuration requise complète. Si vous rencontrez des problèmes avec le scanneur, vérifiez également que votre système est conforme aux [exigences du scanneur](deploy-aip-scanner-prereqs.md)et que la [configuration et l’installation de votre scanneur](deploy-aip-scanner-configure-install.md) sont terminées.
>

## <a name="troubleshooting-a-scan-that-timed-out"></a>Résolution des problèmes d’une analyse ayant expiré

Si le scanneur s’arrête de manière inattendue et ne termine pas l’analyse d’un grand nombre de fichiers dans un référentiel, vous devrez peut-être modifier l’un des paramètres suivants :

- **Nombre de ports dynamiques**. Vous devrez peut-être augmenter le nombre de ports dynamiques pour le système d’exploitation hébergeant les fichiers. Le renforcement du serveur pour SharePoint peut être l’une des raisons expliquant pourquoi le scanneur dépasse le nombre de connexions réseau autorisées et s’arrête.

    Pour plus d’informations sur l’affichage de la plage de ports actuelle et l’augmentation de la plage, consultez [Paramètres modifiables pour améliorer les performances du réseau](/biztalk/technical-guides/settings-that-can-be-modified-to-improve-network-performance).

- **Seuil du mode liste**. Pour les batteries de serveurs SharePoint de grande taille, vous devrez peut-être augmenter le seuil d’affichage de liste. Par défaut, le seuil d’affichage de liste est défini sur **5 000**.

    Pour plus d’informations, consultez [gérer des listes et des bibliothèques de grande taille dans SharePoint](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server).


## <a name="scanner-error-reference"></a>Référence des erreurs du scanneur

Utilisez les sections suivantes pour comprendre les messages d’erreur spécifiques générés par le scanneur, ainsi que les actions de résolution des problèmes ou des solutions pour résoudre le problème :

|Type d’erreur |Résolution des problèmes  |
|---------|---------|
|**Erreurs d'authentification**     |  - [Jeton d’authentification non accepté](#authentication-token-not-accepted) <br>  - [Jeton d’authentification manquant](#authentication-token-missing)|
|**Erreurs de stratégie**     |  - [Stratégie manquante](#policy-missing) <br>- [La stratégie n’inclut aucune condition d’étiquetage automatique](#policy-doesnt-include-any-automatic-labeling-condition)      |
|**Erreurs de base de BD/schéma**     |  - [Erreurs de base de données](#database-errors) <br> - [Schéma incompatible ou obsolète](#mismatched-or-outdated-schema)  |
|**Autres erreurs**     |  - [Processus de scanneur bloqués](#stuck-scanner-processes) <br>- [Impossible de se connecter au serveur distant](#unable-to-connect-to-remote-server) <br>- [Une erreur s’est produite lors de l’envoi de la demande](#error-occurred-while-sending-the-request) <br>- [Travail ou profil d’analyse de contenu manquant](#missing-content-scan-job-or-profile) <br>- [Aucun référentiel configuré](#no-repositories-configured) <br>- [Aucun cluster trouvé](#no-cluster-found)   |
|     |         |


<!--Authentication errors-->

### <a name="authentication-token-not-accepted"></a>Jeton d’authentification non accepté

**Message d’erreur**

`Microsoft.InformationProtection.Exceptions.AccessDeniedException: The service didn't accept the auth token.`

**Solution**

Si la commande [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) a échoué, veillez à définir correctement les autorisations dans le portail Azure.

Pour plus d’informations, consultez [créer et configurer les applications de Azure AD pour Set-AIPAuthentication](rms-client/clientv2-admin-guide-powershell.md#to-create-and-configure-the-azure-ad-applications-for-set-aipauthentication).

### <a name="authentication-token-missing"></a>Jeton d’authentification manquant

**Message d’erreur**

Celui-ci peut avoir l'une des valeurs suivantes :

- `NoAuthTokenException: Client application failed to provide authentication token for HTTP request`

- `Microsoft.InformationProtection.Exceptions.NoAuthTokenException: Client application failed to provide authentication token for HTTP request. Failed with: System.AggregateException: One or more errors occurred. ---> Microsoft.IdentityModel.Clients.ActiveDirectory.AdalException: user_interaction_required: One of two conditions was encountered: 1. The PromptBehavior.Never flag was passed, but the constraint could not be honored, because user interaction was required. 2. An error occurred during a silent web authentication that prevented the http authentication flow from completing in a short enough time frame`

- `Failed to acquire a token using windows integrated authentication (No SSO)`

- Dans la Portail Azure, sur la page **nœuds** : `Policy does not include any automatic labeling condition`

**Solution**

Pour que le scanneur s’exécute de manière non interactive, vous devez vous authentifier à l’aide d’un jeton. 

Quand vous exécutez la commande [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) , veillez à utiliser le paramètre Token pour le compte de l’utilisateur du scanneur.

Par exemple :

```powershell
$pscreds = Get-Credential CONTOSO\scanner
Set-AIPAuthentication -AppId "77c3c1c3-abf9-404e-8b2b-4652836c8c66" -AppSecret "OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4" -DelegatedUser scanner@contoso.com -TenantId "9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a" -OnBehalfOf $pscreds
Acquired application access token on behalf of CONTOSO\scanner.
```

Pour plus d’informations, consultez [obtenir un jeton de Azure AD pour le scanneur](deploy-aip-scanner-configure-install.md#get-an-azure-ad-token-for-the-scanner).

<!--Policy errors-->

### <a name="policy-missing"></a>Stratégie manquante

**Message d’erreur**

`Policy is missing`

**Description**

Le scanneur ne parvient pas à trouver votre fichier de stratégie Microsoft Information Protection (MIP).

**Solution**

Pour vérifier que votre fichier de stratégie existe comme prévu, vérifiez l’emplacement suivant : **% LocalAppData% \Microsoft\MSIP\mip\MSIP.Scanner.exe \mip\mip.Policies.sqlite3**

Pour plus d’informations sur les étiquettes MIP et les stratégies d’étiquette, consultez [créer et configurer des étiquettes de sensibilité et leurs stratégies](/microsoft-365/compliance/create-sensitivity-labels) dans la documentation Microsoft 365.

### <a name="policy-doesnt-include-any-automatic-labeling-condition"></a>La stratégie n’inclut aucune condition d’étiquetage automatique

**Error**

Les erreurs indiquent que des conditions d’étiquetage automatique sont manquantes pour votre stratégie d’étiquetage

**Solution**

Vérifiez les problèmes suivants :

|Solution  |Détails  |
|---------|---------|
|**Vérifiez les paramètres de votre travail d’analyse de contenu**     | Dans le portail Azure, procédez comme suit : <br> <br>- [Définir les **types d’informations à découvrir** pour **tous**](deploy-aip-scanner-configure-install.md#identify-all-custom-conditions-and-known-sensitive-information-types)  <br>- [Définir une étiquette par défaut à appliquer lors de l’analyse](deploy-aip-scanner-configure-install.md#apply-a-default-label-to-all-files-in-a-data-repository)      |
|**Vérifiez les paramètres de votre stratégie d’étiquetage**     |  Dans le centre d’administration d’étiquetage, comme le centre de conformité Microsoft 365 Security &, procédez comme suit : <br> <br>- [Définir une étiquette de sensibilité par défaut](/microsoft-365/compliance/create-sensitivity-labels#publish-sensitivity-labels-by-creating-a-label-policy)  <br> - [Définir les règles d’étiquetage automatique/recommandé](/microsoft-365/compliance/apply-sensitivity-label-automatically)       |
|**Vérifier que votre stratégie est accessible**     | Si vos paramètres sont définis comme prévu, le fichier de stratégie lui-même peut être manquant ou inaccessible, par exemple en cas de délai d’expiration dans le centre de conformité Microsoft 365 Security &. <br>  <br>Pour vérifier votre fichier de stratégie, vérifiez que le fichier suivant existe : **% LocalAppData% \Microsoft\MSIP\mip\MSIP.Scanner.exe \mip\mip.Policies.sqlite3**        |
| | |

Pour plus d’informations, consultez [qu’est-ce que le Azure information protection scanneur d’étiquetage unifié ?](deploy-aip-scanner.md) et [en savoir plus sur les étiquettes de sensibilité](/microsoft-365/compliance/sensitivity-labels).

<!--DB / Schema errors-->

### <a name="database-errors"></a>Erreurs de base de données

**Message d’erreur**

`DB error`

**Description**

Le scanneur peut ne pas être en mesure de se connecter à la base de données.

**Solution**

Vérifiez la connectivité réseau entre l’ordinateur du scanneur et la base de données. 

En outre, assurez-vous que le compte de service utilisé pour exécuter les processus du scanneur dispose des autorisations nécessaires pour accéder à la base de données.

### <a name="mismatched-or-outdated-schema"></a>Schéma incompatible ou obsolète

**Message d’erreur**

Celui-ci peut avoir l'une des valeurs suivantes :

- `SchemaMismatchException`

- Dans la Portail Azure, sur la page **nœuds** : `DB schema is not up to date. Run Update-AIPScanner command to update the DB schema` ou `Error: DB schema is not up to date`

**Solution**

Exécutez la commande [Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner) pour resynchroniser votre schéma et assurez-vous qu’il est à jour avec les modifications récentes.


<!--Other errors-->

### <a name="stuck-scanner-processes"></a>Processus de scanneur bloqués

**Message d’erreur**

Le scanneur traite un fichier unique plus longtemps que prévu. Le processus est peut-être bloqué.

**Solution**

Vérifiez le rapport détaillé pour voir si le fichier est toujours en croissance. 

Si le fichier continue à croître, cela signifie que le scanneur continue de traiter les données et que vous devez attendre la fin de l’opération.

Toutefois, si le fichier n’augmente plus, procédez comme suit :

1. Effectuez une des actions suivantes ou les deux :

    - Exécutez l’applet de commande [Start-AIPScannerDiagnostics](/powershell/module/azureinformationprotection/start-aipscannerdiagnostics) pour exécuter les vérifications de diagnostic sur votre scanneur, puis exportez et compressez les fichiers journaux pour toutes les erreurs détectées.
    - Exécutez l’applet de commande [Export-AIPLogs](/powershell/module/azureinformationprotection/export-aiplogs) pour exporter et compresser les fichiers journaux à partir du répertoire **%LocalAppData%\Microsoft\MSIP\Logs** .

1. Créez un fichier de vidage pour le service d’analyse MSIP. Dans le gestionnaire des tâches de Windows, cliquez avec le bouton droit sur le **service du scanneur MSIP**, puis sélectionnez **créer un fichier de vidage**.

1. Dans le Portail Azure, arrêtez l’analyse. 

1. Sur l’ordinateur du scanneur, redémarrez le service.

1. Ouvrez un ticket de support et attachez les fichiers de vidage à partir du processus du scanneur.

Pour plus d’informations, consultez [Dépannage d’une analyse qui a expiré](#troubleshooting-a-scan-that-timed-out). 

### <a name="unable-to-connect-to-remote-server"></a>Impossible de se connecter au serveur distant

**Error**

Dans le fichier **% *LocalAppData*% \ Microsoft\MSIP\Logs\MSIPScanner.Iplog** ,`Unable to connect to the remote server ---> System.Net.Sockets.SocketException: Only one usage of each socket address (protocol/network address/port) is normally permitted IP:port`    

> [!NOTE]
> Ce fichier sera compressé s’il existe plusieurs journaux.

**Description**

Le scanneur a dépassé le nombre de connexions réseau autorisées.

**Solution**

Augmentez le nombre de ports dynamiques pour le système d’exploitation hébergeant les fichiers.

Pour plus d’informations sur l’affichage de la plage de ports actuelle et l’augmentation de la plage, consultez [Paramètres modifiables pour améliorer les performances du réseau](/biztalk/technical-guides/settings-that-can-be-modified-to-improve-network-performance).


Voir aussi : [Dépannage d’une analyse qui a expiré](#troubleshooting-a-scan-that-timed-out).
### <a name="error-occurred-while-sending-the-request"></a>Une erreur s’est produite lors de l’envoi de la demande

**Message d’erreur**

`[System.Net.Http.HttpRequestException: An error occurred while sending the request. ---> System.Net.WebException: The underlying connection was closed: An unexpected error occurred on a send. ---> System.IO.IOException: Unable to read data from the transport connection: An existing connection was forcibly closed by the remote host. ---> System.Net.Sockets.SocketException: An existing connection was forcibly closed by the remote host`

**Solution**

Cette erreur signifie généralement que TLS 1,2 n’est pas activé.

Pour plus d’informations, consultez [pare-feu et infrastructure réseau](requirements.md#firewalls-and-network-infrastructure). 

Pour activer TLS 1,2, consultez [Comment activer tls 1,2](/mem/configmgr/core/plan-design/security/enable-tls-1-2-client) dans la documentation Enterprise Mobility + Security.


### <a name="missing-content-scan-job-or-profile"></a>Travail ou profil d’analyse de contenu manquant

**Error**

Les erreurs indiquent que votre travail ou profil d’analyse de contenu est introuvable.

Par exemple, l’erreur suivante dans la Portail Azure sur la page **nœuds** : `No content scan job found`

**Solution**

Vérifiez la configuration de votre scanneur dans le Portail Azure.

Pour plus d’informations, consultez [configuration et installation du scanneur d’étiquetage unifié Azure information protection](deploy-aip-scanner-configure-install.md). 

> [!NOTE]
> Un *Profil* est un terme de scanneur hérité qui a été remplacé par le cluster de scanneur et le travail d’analyse de contenu dans les versions plus récentes du scanneur.
> 
### <a name="no-repositories-configured"></a>Aucun référentiel configuré

**Message d’erreur**

Dans la Portail Azure, sur la page **nœuds** : `No repositories are configured`

**Description**

Vous pouvez avoir un travail d’analyse de contenu sans référentiel configuré. 

**Solution**

Vérifiez les paramètres de votre travail d’analyse de contenu et ajoutez au moins un référentiel. 

Pour plus d’informations, consultez [créer un travail d’analyse du contenu](deploy-aip-scanner-configure-install.md#create-a-content-scan-job).

### <a name="no-cluster-found"></a>Aucun cluster trouvé

**Message d’erreur**

Dans la Portail Azure, sur la page **nœuds** : `No cluster found`

**Description**

Aucune correspondance réelle n’a été trouvée pour l’un des clusters de scanneurs que vous avez définis.

**Solution**

Vérifiez la configuration de votre cluster et vérifiez-la par rapport à vos propres Détails système pour les erreurs de frappe et les erreurs.

Pour plus d’informations, consultez [créer un cluster de scanneur](deploy-aip-scanner-configure-install.md#create-a-scanner-cluster).

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations, consultez notre blog sur [les meilleures pratiques pour le déploiement et l’utilisation du scanneur UL AIP](https://techcommunity.microsoft.com/t5/microsoft-security-and/best-practices-for-deploying-and-using-the-aip-ul-scanner/ba-p/1878168).