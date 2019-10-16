---
title: MIP::P rotectionHandler::P ublishingSettings
description: Documente la classe MIP::p rotectionhandler du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: ec5c7860c7804e30ee3ab8ae9df29f8ab9a5a112
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70057612"
---
# <a name="class-mipprotectionhandlerpublishingsettings"></a>MIP::P rotectionHandler::P ublishingSettings 
Paramètres utilisés pour créer un [ProtectionHandler](class_mip_protectionhandler.md) pour protéger un nouveau contenu.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public PublishingSettings (const std:: shared_ptr\<ProtectionDescriptor\>& ProtectionDescriptor)  |  ProtectionHandler:: Settings, constructeur pour la création d’un nouveau moteur.
public std:: shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor () const  | _Pas encore documenté._
public bool GetIsAuditedExtractionAllowed () const  |  Obtient une valeur indiquant si des applications prenant en charge les non-MIP sont autorisées ou non pour ouvrir du contenu protégé.
public void SetIsAuditedExtractionAllowed (bool isAuditedExtractionAllowed)  |  Définit si les applications prenant en charge non MIP sont autorisées ou non pour ouvrir du contenu protégé.
public bool GetIsDeprecatedAlgorithmPreferred () const  |  Obtient une valeur indiquant si l’algorithme de chiffrement (ECB) déconseillé est préféré pour la compatibilité descendante.
public void SetIsDeprecatedAlgorithmPreferred (bool isDeprecatedAlgorithmPreferred)  |  Définit si l’algorithme de chiffrement déconseillé (ECB) est préféré pour la compatibilité descendante.
public void SetDelegatedUserEmail (const std:: String & delegatedUserEmail)  |  Définit l’utilisateur délégué.
public const std:: String & GetDelegatedUserEmail () const  |  Obtient l’utilisateur délégué.
  
## <a name="members"></a>Membres
  
### <a name="publishingsettings-function"></a>PublishingSettings fonction)
ProtectionHandler:: Settings, constructeur pour la création d’un nouveau moteur.

Paramètres :  
* **protectionDescriptor**: Détails de la protection


  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor fonction)
_Pas encore documenté._

  
### <a name="getisauditedextractionallowed-function"></a>GetIsAuditedExtractionAllowed fonction)
Obtient une valeur indiquant si des applications prenant en charge les non-MIP sont autorisées ou non pour ouvrir du contenu protégé.

  
**Retourne**: Si des applications prenant en charge non MIP sont autorisées à ouvrir du contenu protégé
  
### <a name="setisauditedextractionallowed-function"></a>SetIsAuditedExtractionAllowed fonction)
Définit si les applications prenant en charge non MIP sont autorisées ou non pour ouvrir du contenu protégé.

Paramètres :  
* **isAuditedExtractionAllowed**: Si des applications prenant en charge non MIP sont autorisées à ouvrir du contenu protégé


  
### <a name="getisdeprecatedalgorithmpreferred-function"></a>GetIsDeprecatedAlgorithmPreferred fonction)
Obtient une valeur indiquant si l’algorithme de chiffrement (ECB) déconseillé est préféré pour la compatibilité descendante.

  
**Retourne**: Si l’algorithme de chiffrement deprectated est préféré
  
### <a name="setisdeprecatedalgorithmpreferred-function"></a>SetIsDeprecatedAlgorithmPreferred fonction)
Définit si l’algorithme de chiffrement déconseillé (ECB) est préféré pour la compatibilité descendante.

Paramètres :  
* **Si**: l’algorithme de chiffrement deprectated est préféré


  
### <a name="setdelegateduseremail-function"></a>SetDelegatedUserEmail fonction)
Définit l’utilisateur délégué.

Paramètres :  
* **delegatedUserEmail**: e-mail de délégation.


Un utilisateur délégué est spécifié quand l’utilisateur ou l’application d’authentification agit au nom d’un autre utilisateur
  
### <a name="getdelegateduseremail-function"></a>GetDelegatedUserEmail fonction)
Obtient l’utilisateur délégué.

  
**Retourne**: Utilisateur délégué un utilisateur délégué est spécifié quand l’utilisateur ou l’application d’authentification agit au nom d’un autre utilisateur