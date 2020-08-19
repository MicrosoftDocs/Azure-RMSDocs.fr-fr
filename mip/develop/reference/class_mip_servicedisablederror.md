---
title: ServiceDisabledError de classe
description: 'Documente la classe servicedisablederror :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 3dc6d73f12dc1512d1850d465a966e99d13b52c9
ms.sourcegitcommit: dc50f9a6c2f66544893278a7fd16dff38eef88c6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2020
ms.locfileid: "88564451"
---
# <a name="class-servicedisablederror"></a>ServiceDisabledError de classe

L’utilisateur n’a pas pu accéder au contenu en raison de la désactivation d’un service.
  
## <a name="summary"></a>Récapitulatif

| Membres                          | Descriptions
|----------------------------------|--------------------------------------------------------
| const GetExtent () d’étendue publique  | Obtient l’étendue pour laquelle le service est désactivé.
| Étendue d’énumération                      | Décrit l’étendue pour laquelle le service est désactivé.
  
## <a name="members"></a>Membres
  
### <a name="getextent-function"></a>GetExtent fonction)
Obtient l’étendue pour laquelle le service est désactivé.

**Retourne**: l’étendue pour laquelle le service est désactivé
  
### <a name="extent-enum"></a>Énumération d’étendue

Décrit l’étendue pour laquelle le service est désactivé.

| Valeurs   | Descriptions
|----------|---------------------------------------
| Utilisateur     | Le service est désactivé pour l’utilisateur.
| Appareil   | Le service est désactivé pour l’appareil.
| Plateforme | Le service est désactivé pour la plateforme.
| Locataire   | Le service est désactivé pour le locataire.
