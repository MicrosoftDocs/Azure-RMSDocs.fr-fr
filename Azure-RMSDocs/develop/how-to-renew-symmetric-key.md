---
title: Guide pratique pour renouveler la clé symétrique dans Azure Information Protection
description: Cet article décrit le processus de renouvellement d’une clé symétrique dans Azure Information Protection.
keywords: ''
author: msmbaldwin
manager: barbkess
ms.author: mbaldwin
ms.date: 03/27/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: a0b8c8f0-6ed5-48bb-8155-ac4f319ec178
ms.custom: dev
ms.openlocfilehash: 539ad36df7d2c74a00650347abb8ed067dd743c7
ms.sourcegitcommit: 6b159e050176a2cc1b308b1e4f19f52bb4ab1340
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/30/2020
ms.locfileid: "95567822"
---
# <a name="how-to-renew-the-symmetric-key-in-azure-information-protection"></a>Guide pratique pour renouveler la clé symétrique dans Azure Information Protection

Une **clé symétrique** est un secret qui chiffre et déchiffre un message dans le chiffrement par clé symétrique.  

Dans Azure AD (Azure Active Directory), quand vous créez un objet principal de service pour représenter une application, le processus génère également une clé symétrique 256 bits pour vérifier l’application. Par défaut, cette clé symétrique est valable un an. 

Les étapes suivantes montrent comment renouveler la clé symétrique. 

## <a name="prerequisites"></a>Prérequis

* Vous devez installer le module Azure AD (Azure Active Directory) PowerShell comme indiqué dans [Référence Azure AD PowerShell](/powershell/msonline/).


## <a name="renewing-the-symmetric-key-after-expiry"></a>Renouvellement de la clé symétrique après expiration

Vous n’êtes pas obligé de créer un principal de service quand la clé symétrique associée à votre application a expiré. En effet, vous pouvez utiliser les [applets de commande PowerShell](/powershell/module/msonline) fournies par MSol (Microsoft Online Services) qui vous permettront d’émettre une nouvelle clé symétrique pour un principal de service existant.

Pour illustrer ce processus, supposons que vous avez déjà créé un principal de service à l’aide de la [`New-MsolServicePrincipal`](/powershell/msonline/v1/new-msolserviceprincipalcredential) commande.

```
New-MsolServicePrincipalCredential -ServicePrincipalName "SupportExampleApp"
```

Le processus de création crée une clé symétrique et un **AppPrincipalId** comme indiqué.

```
The following symmetric key was created as one was not supplied
ZYbF/lTtwE28qplQofCpi2syWd11D83+A3DRlb2Jnv8=

DisplayName : SupportExampleApp
ServicePrincipalNames : {7d9c1f38-600c-4b4d-8249-22427f016963}
ObjectId : 0ee53770-ec86-409e-8939-6d8239880518
AppPrincipalId : 7d9c1f38-600c-4b4d-8249-22427f016963
TrustedForDelegation : False
AccountEnabled : True
Addresses : []
KeyType : Symmetric
KeyId : acb9ad1b-36ce-4a7d-956c-40e5ac29dcbe
StartDate : 3/22/2017 3:27:53 PM
EndDate : 3/22/2018 3:27:53 PM
Usage : Verify
```

Cette clé symétrique expire le 22/03/2018 à 15:27:53. Pour utiliser le principal de service après cette date, vous devez renouveler la clé symétrique. Pour ce faire, utilisez la [`New-MsolServicePrincipalCredential`](/powershell/msonline/v1/new-msolserviceprincipalcredential) commande. 

```
New-MsolServicePrincipalCredential -AppPrincipalId 7d9c1f38-600c-4b4d-8249-22427f016963
```

Elle crée une clé symétrique pour l’élément **AppPrincipalId** spécifié.

```
The following symmetric key was created as one was not supplied ON8YYaMYNmwSfMX625Ei4eC6N1zaeCxbc219W090v28-
```
Vous pouvez utiliser la [`GetMsolServicePrincipalCredential`](/powershell/msonline/v1/get-msolserviceprincipalcredential) commande pour vérifier que la nouvelle clé symétrique est associée au principal du service approprié, comme indiqué. Notez que la commande liste toutes les clés actuellement associées au principal de service.

```
Get-MsolServicePrincipalCredential -AppPrincipalId 7d9c1f38-600c-4b4d-8249-22427f016963 -ReturnKeyValues $true

Type : Symmetric
Value :
KeyId : c1ac145f-e899-4c90-8a02-2cef40054fc5
StartDate : 3/24/2017 10:11:07 PM
EndDate : 3/24/2018 10:11:07 PM
Usage : Verify

Type : Symmetric
Value :
KeyId : acb9ad1b-36ce-4a7d-956c-40e5ac29dcbe
StartDate : 3/22/2017 3:27:53 PM
EndDate : 3/22/2018 3:27:53 PM
Usage : Verify
```

Une fois que vous avez vérifié que la clé symétrique est effectivement associée au principal de service approprié, vous pouvez mettre à jour les paramètres d’authentification du principal de service avec la nouvelle clé. 

Vous pouvez ensuite supprimer l’ancienne clé symétrique à l’aide de la [`Remove-MsolServicePrincipalCredential`](/powershell/msonline/v1/remove-msolserviceprincipalcredential) commande et vérifier que la clé est supprimée à l’aide de la `Get-MsolServicePrincipalCredential` commande.

```
Remove-MsolServicePrincipalCredential -KeyId acb9ad1b-36ce-4a7d-956c-40e5ac29dcbe -ObjectId 0ee53770-ec86-409e-8939-6d8239880518
```

## <a name="related-topics"></a>Rubriques connexes

* [Comment : permettre à votre application de service de fonctionner avec le service RMS cloud](how-to-use-file-api-with-aadrm-cloud.md)
* [Référence Azure Active Directory MSOnline PowerShell](/powershell/msonline/)