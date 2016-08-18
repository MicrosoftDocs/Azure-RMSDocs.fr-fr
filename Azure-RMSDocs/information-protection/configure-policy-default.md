---
title: "La stratégie Azure Information Protection par défaut | Azure Rights Management"
description: 
author: cabailey
manager: mbaldwin
ms.date: 07/21/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 671281c8-f0d1-42b6-aae3-681d1821e2cf
translationtype: Human Translation
ms.sourcegitcommit: 93444affe94b280db2c9e4e2960c6902e491dec6
ms.openlocfilehash: 977cbf2f45cab75aaca9c2a16dd1564c2af2fe4a


---

# La stratégie Azure Information Protection par défaut

>*S’applique à : Azure Information Protection (préversion)*

**[ Cette information est préliminaire et susceptible d'être modifiée. ]**

Utilisez les informations suivantes pour comprendre la configuration de la stratégie par défaut pour Azure Information Protection. Si vous modifiez la stratégie par défaut, vous pouvez référencer ces valeurs de manière à réinitialiser votre stratégie sur les valeurs par défaut.

## Barre Information Protection

Titre : **Confidentialité**

Info-bulle : **la confidentialité des informations est composée de quatre niveaux distincts (public, interne, confidentiel, secret), qui permettent à l’utilisateur d’identifier le risque d’exposition d’informations à des utilisateurs non autorisés à l’intérieur ou à l’extérieur de l’entreprise.**


## Étiquettes

Il existe 5 étiquettes par défaut qui ont les paramètres suivants :

### **Personnel**

Info-bulle : **Réservé à un usage personnel. Ces données ne sont pas surveillées par l’organisation. Les informations personnelles ne doivent inclure aucune donnée professionnelle.**

Couleur : vert clair

Marquages visuels : aucun

Conditions : aucune

Protection : non

----


### **Public**

Info-bulle : **Cette information est interne et peut être utilisée par tout le monde à l’intérieur ou à l’extérieur de l’entreprise.**

Couleur : Vert

Marquages visuels : aucun

Conditions : aucune

Protection : non

----

### **Interne**

Info-bulle : **Ces informations comprennent une grande variété de données métier internes qui peuvent être utilisées par tous les employés et peuvent être partagées avec des clients et des partenaires commerciaux autorisés. Les informations internes sont, par exemple, des stratégies de l’entreprise et la plupart des communications internes.**

Couleur : bleu

Marquages visuels : pied de page (document et e-mail)

Conditions : aucune

Protection : non

----

### **Confidentiel**

Info-bulle : **Ces données incluent des informations métier sensibles. Une exposition de ces données à des utilisateurs non autorisés peut nuire à l’organisation. Les informations confidentielles sont, par exemple, des informations sur les employés, des projets ou des contrats de clients, ainsi que des données de comptes de vente.**

Couleur : orange

Marquages visuels : pied de page (document et e-mail)

Conditions : aucune

Protection : non

----

### **Secret**

Info-bulle : **Ces données incluent des informations hautement confidentielles de l’entreprise qui doivent être protégées. Une exposition de ces données secrètes à des utilisateurs non autorisés peut nuire gravement à l’organisation. Les informations secrètes sont, par exemple, des informations d’identification personnelles, des enregistrements de clients, des codes source et des rapports financiers préalablement annoncés.**

Couleur : rouge

Marquages visuels : pied de page (document et e-mail)

Conditions : aucune

Protection : non

----


## Sous-étiquettes

Il existe 2 sous-étiquettes par défaut qui ont les paramètres suivants :

### Secret > **Toute l’entreprise**

Info-bulle : **Ces données incluent des informations métier sensibles pour lesquelles les employés de la société ont une autorisation.**

Marquages visuels : aucun

Conditions : aucune

Protection : non

----

### Secret > **Mon groupe**

Info-bulle : **Ces données incluent des informations métier sensibles pour lesquelles des groupes d’employés ont une autorisation.**

Marquages visuels : aucun

Conditions : aucune

Protection : non

## Paramètres globaux

**Tous les documents et e-mails doivent avoir une étiquette (appliquée automatiquement ou par les utilisateurs)** : désactivé

**Sélectionnez l’étiquette par défaut** : aucune

**Les utilisateurs doivent fournir une justification quand ils abaissent le niveau de confidentialité (par exemple, de Confidentiel à Public)** : désactivé

## Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organization-s-policy). 



<!--HONumber=Jul16_HO5-->


