---
title: "Stratégie par défaut | Azure Information Protection"
description: "Comprendre le processus de configuration de la stratégie par défaut pour Azure Information Protection. Si vous modifiez la stratégie par défaut, vous pouvez référencer ces valeurs de manière à réinitialiser votre stratégie sur les valeurs par défaut."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/04/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 671281c8-f0d1-42b6-aae3-681d1821e2cf
translationtype: Human Translation
ms.sourcegitcommit: d5b3f3fc473661022a4f17b6587d58a252d07d1a
ms.openlocfilehash: 5c3d3962d72a0dc3d08bdb869f6b00f4524477b5


---

# <a name="the-default-azure-information-protection-policy"></a>La stratégie Azure Information Protection par défaut

>*S’applique à : Azure Information Protection*

Utilisez les informations suivantes pour comprendre la configuration de la stratégie par défaut pour Azure Information Protection. Si vous modifiez la stratégie par défaut, vous pouvez référencer ces valeurs de manière à réinitialiser votre stratégie sur les valeurs par défaut.

## <a name="information-protection-bar"></a>Barre Information Protection

|Paramètre|Valeur|
|-------------------------------|---------------------------|
|Titre|Sensibilité|
|Info-bulle|La confidentialité des informations est composée de quatre niveaux distincts (public, interne, confidentiel, secret), qui permettent à l’utilisateur d’identifier le risque d’exposition d’informations à des utilisateurs non autorisés à l’intérieur ou à l’extérieur de l’entreprise.|

## <a name="labels"></a>Étiquettes

|Étiquette|Info-bulle|Paramètres|
|-------------------------------|---------------------------|-----------------|
|Personnel|Réservé à un usage personnel. Ces données ne sont pas surveillées par l’organisation. Les informations personnelles ne doivent inclure aucune donnée professionnelle.|**Activé** : Oui <br /><br />**Couleur** : Vert clair<br /><br />**Marquages visuels** : Désactivés <br /><br />**Conditions** : Aucune<br /><br />**Protection** : Aucune|
|Public|Ces informations sont internes et peuvent être utilisées par tout le monde à l’intérieur ou à l’extérieur de l’entreprise.|**Activé** : Oui <br /><br />**Couleur** : vert<br /><br />**Marquages visuels** : Désactivés<br /><br />**Conditions** : Aucune<br /><br />**Protection** : Aucune|
|Interne|Ces informations comprennent une grande variété de données métier internes qui peuvent être utilisées par tous les employés et peuvent être partagées avec des clients et des partenaires commerciaux autorisés. Les informations internes sont, par exemple, des stratégies de l’entreprise et la plupart des communications internes.|**Activé** : Oui <br /><br />**Couleur** : Bleu <br /><br />**Marquages visuels** : Pied de page (document et e-mail)<br /><br />**Conditions** : Aucune<br /><br />**Protection** : Aucune|
|Confidentiel|Ces données incluent des informations métier sensibles. Une exposition de ces données à des utilisateurs non autorisés peut nuire à l’organisation. Les informations confidentielles sont, par exemple, des informations sur les employés, des projets ou des contrats de clients, ainsi que des données de comptes de vente.|**Activé** : Oui <br /><br />**Couleur** : Orange<br /><br />**Marquages visuels** : Pied de page (document et e-mail)<br /><br />**Conditions** : Aucune<br /><br />**Protection** : Aucune|
|Secret|Ces données incluent des informations hautement confidentielles de l’entreprise qui doivent être protégées. Une exposition de ces données secrètes à des utilisateurs non autorisés peut nuire gravement à l’organisation. Les informations secrètes sont, par exemple, des informations d’identification personnelles, des enregistrements de clients, des codes source et des rapports financiers préalablement annoncés.|**Activé** : Oui <br /><br />**Couleur** : Rouge<br /><br />**Marquages visuels** : Pied de page (document et e-mail)<br /><br />**Conditions** : Aucune<br /><br />**Protection** : Aucune|

## <a name="sublabels"></a>Sous-étiquettes

|Étiquette|Info-bulle|Paramètres|
|-------------------------------|---------------------------|-----------------|
|Secret \ Toute l’entreprise|Ces données incluent des informations métier sensibles pour lesquelles les employés de la société ont une autorisation.|**Activé** : Oui <br /><br />**Marquages visuels** : Désactivés<br /><br />**Conditions** : Aucune<br /><br />**Protection** : Aucune|
|Secret > Mon groupe|Ces données incluent des informations métier sensibles pour lesquelles des groupes d’employés ont une autorisation.|**Activé** : Oui <br /><br />**Marquages visuels** : Désactivés<br /><br />**Conditions** : Aucune<br /><br />**Protection** : Aucune|

## <a name="global-settings"></a>Paramètres globaux

|Paramètre|Valeur|
|-------------------------------|---------------------------|
|Tous les documents et e-mails doivent avoir une étiquette (appliquée automatiquement ou par les utilisateurs)|Désactivé|
|Sélectionner l’étiquette par défaut|Aucune|
|Users must provide justification to set a lower classification label, remove a label, or remove protection (Les utilisateurs doivent fournir une justification pour définir une étiquette de classification d’un niveau inférieur, supprimer une étiquette ou enlever la protection)|Désactivé|


## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy). 



<!--HONumber=Nov16_HO1-->


