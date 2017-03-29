---
title: "Stratégie Azure Information Protection par défaut"
description: "Comprendre le processus de configuration de la stratégie par défaut pour Azure Information Protection. Si vous modifiez la stratégie par défaut, vous pouvez référencer ces valeurs de manière à réinitialiser votre stratégie sur les valeurs par défaut."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/21/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 671281c8-f0d1-42b6-aae3-681d1821e2cf
ms.openlocfilehash: 40a6c3eed95ef30b7540e31478257b1c851ae9b6
ms.sourcegitcommit: f0402cf14506b4c61a156a2baf7e69b7b16883a1
translationtype: HT
---
# <a name="the-default-azure-information-protection-policy"></a>La stratégie Azure Information Protection par défaut

>*S’applique à : Azure Information Protection*

Utilisez les informations suivantes pour comprendre la configuration de la stratégie par défaut pour Azure Information Protection.

Quand un administrateur se connecte pour la première fois au service Azure Information Protection en utilisant le portail Azure, la stratégie par défaut pour ce locataire est créée. Microsoft peut parfois apporter des modifications à la stratégie par défaut, mais si vous utilisiez déjà le service avant que la stratégie par défaut ait été révisée, votre version précédente de la stratégie par défaut n’est pas mise à jour, car vous pouvez l’avoir configurée et déployée en production.

Vous pouvez référencer les valeurs suivantes pour rétablir votre stratégie aux valeurs par défaut ou mettre à jour votre stratégie avec les valeurs les plus récentes.

## <a name="current-default-policy"></a>Stratégie par défaut actuelle

Cette version de la stratégie par défaut date du 21 mars 2017.

Notez que les descriptions de cette stratégie font référence aux données qui nécessitent une protection, ainsi qu’au suivi et à la révocation des données. La stratégie ne configure pas cette protection pour ces étiquettes : vous devez donc effectuer des étapes supplémentaires pour compléter cette description. Par exemple, configurez l’étiquette pour appliquer la protection Azure RMS ou utilisez une solution de protection contre la perte de données. Avant de pouvoir suivre et révoquer un document en utilisant le site de suivi des documents, ce document doit être protégé par Azure RMS. 


### <a name="labels"></a>Étiquettes

|Étiquette|Info-bulle|Paramètres|
|-------------------------------|---------------------------|-----------------|
|Personnel|Données autres que les données d’entreprise, uniquement pour une utilisation personnelle.|**Activé** : Oui <br /><br />**Couleur** : Vert clair<br /><br />**Marquages visuels** : Désactivés <br /><br />**Conditions** : Aucune<br /><br />**Protection** : Aucune|
|Public|Données d’entreprise qui sont spécifiquement préparées et approuvées pour une consommation publique.|**Activé** : Oui <br /><br />**Couleur** : vert<br /><br />**Marquages visuels** : Désactivés<br /><br />**Conditions** : Aucune<br /><br />**Protection** : Aucune|
|Général|Données d’entreprise qui ne sont pas destinées à la consommation publique. Cependant, elles peuvent être partagées avec des partenaires externes, en fonction des besoins. Il peut s’agir par exemple d’un annuaire téléphonique interne d’une entreprise, d’organigrammes, de normes internes et de la plupart des communications internes.|**Activé** : Oui <br /><br />**Couleur** : Bleu <br /><br />**Marquages visuels** : Désactivés<br /><br />**Conditions** : Aucune<br /><br />**Protection** : Aucune|
|Confidentiel|Données d’entreprise sensibles qui pourraient provoquer des dommages à l’activité si elles étaient partagées avec des personnes non autorisées. Il peut s’agir entre autres de contrats, de rapports de sécurité, de résumés de prévision et de données commerciales.|**Activé** : Oui <br /><br />**Couleur** : Orange<br /><br />**Marquages visuels** : Désactivés<br /><br />**Conditions** : Aucune<br /><br />**Protection** : Aucune|
|Hautement confidentiel|Données d’entreprise très sensibles qui pourraient provoquer des dommages à l’activité si elles étaient partagées avec des personnes non autorisées. Il s'agit entre autres d'informations sur les clients et les employés, les mots de passe, le code source et des rapports financiers préalablement annoncés.|**Activé** : Oui <br /><br />**Couleur** : Rouge<br /><br />**Marquages visuels** : Désactivés<br /><br />**Conditions** : Aucune<br /><br />**Protection** : Aucune|


### <a name="sub-labels"></a>Sous-étiquettes

|Étiquette|Info-bulle|Paramètres|
|-------------------------------|---------------------------|-----------------|
|Confidentiel \ Tous les employés|Données confidentielles qui nécessitent une protection, qui permettent toutes les autorisations complètes des employés. Les propriétaires des données peuvent suivre et révoquer le contenu.|**Activé** : Oui <br /><br />**Marquages visuels** : Pied de page (document et e-mail)<br /><br />Classé comme confidentiel<br /><br />**Conditions** : Aucune<br /><br />**Protection** : Aucune|
|Confidentiel \ Tout le monde (sans protection)|Données ne nécessitant pas de protection. Utilisez cette option avec précaution et avec une justification métier appropriée.|**Activé** : Oui <br /><br />**Marquages visuels** : Pied de page (document et e-mail)<br /><br />Classé comme confidentiel <br /><br />**Conditions** : Aucune<br /><br />**Protection** : Aucune|
|Hautement confidentiel \ Tous les employés|Données hautement confidentielles, qui permettent les autorisations d’afficher, de modifier et de répondre de tous les employés sur ce contenu. Les propriétaires des données peuvent suivre et révoquer le contenu.|**Activé** : Oui <br /><br />**Marquages visuels** : Pied de page (document et e-mail)<br /><br />Classé hautement confidentiel<br /><br />**Conditions** : Aucune<br /><br />**Protection** : Aucune|
|Hautement confidentiel \ Tout le monde (sans protection)|Données ne nécessitant pas de protection. Utilisez cette option avec précaution et avec une justification métier appropriée.|**Activé** : Oui <br /><br />**Marquages visuels** : Pied de page (document et e-mail)<br /><br />Classé hautement confidentiel<br /><br />**Conditions** : Aucune<br /><br />**Protection** : Aucune|

### <a name="information-protection-bar"></a>Barre Information Protection

|Paramètre|Valeur|
|-------------------------------|---------------------------|
|Titre|Sensibilité|
|Info-bulle|L’étiquette actuelle pour ce contenu. Ce paramètre identifie les risques pour l’entreprise si ce contenu est partagé avec des personnes non autorisées à l’intérieur ou à l’extérieur de l’organisation.|


### <a name="settings"></a>Paramètres

|Paramètre|Valeur|
|-------------------------------|---------------------------|
|Tous les documents et e-mails doivent avoir une étiquette (appliquée automatiquement ou par les utilisateurs)|Désactivé|
|Sélectionner l’étiquette par défaut|Aucune|
|Les utilisateurs doivent fournir une justification pour définir une étiquette de classification moins élevée, supprimer une étiquette ou supprimer la protection|Désactivé|
|Pour les e-mails avec des pièces jointes, appliquez une étiquette qui correspond à la classification la plus élevée de ces pièces jointes|Désactivé|
|Spécifiez une URL personnalisée pour la page web « En savoir plus » du client Azure Information Protection|Vide|

## <a name="default-policy-before-march-21-2017"></a>Stratégie par défaut avant le 21 mars 2017

### <a name="labels"></a>Étiquettes

|Étiquette|Info-bulle|Paramètres|
|-------------------------------|---------------------------|-----------------|
|Personnel|Réservé à un usage personnel. Ces données ne sont pas surveillées par l’organisation. Les informations personnelles ne doivent inclure aucune donnée professionnelle.|**Activé** : Oui <br /><br />**Couleur** : Vert clair<br /><br />**Marquages visuels** : Désactivés <br /><br />**Conditions** : Aucune<br /><br />**Protection** : Aucune|
|Public|Ces informations sont internes et peuvent être utilisées par tout le monde à l’intérieur ou à l’extérieur de l’entreprise.|**Activé** : Oui <br /><br />**Couleur** : vert<br /><br />**Marquages visuels** : Désactivés<br /><br />**Conditions** : Aucune<br /><br />**Protection** : Aucune|
|Interne|Ces informations comprennent une grande variété de données métier internes qui peuvent être utilisées par tous les employés et peuvent être partagées avec des clients et des partenaires commerciaux autorisés. Les informations internes sont, par exemple, des stratégies de l’entreprise et la plupart des communications internes.|**Activé** : Oui <br /><br />**Couleur** : Bleu <br /><br />**Marquages visuels** : Pied de page (document et e-mail) : <br /><br />Sensibilité : Interne<br /><br />**Conditions** : Aucune<br /><br />**Protection** : Aucune|
|Confidentiel|Ces données incluent des informations métier sensibles. Une exposition de ces données à des utilisateurs non autorisés peut nuire à l’organisation. Les informations confidentielles sont, par exemple, des informations sur les employés, des projets ou des contrats de clients, ainsi que des données de comptes de vente.|**Activé** : Oui <br /><br />**Couleur** : Orange<br /><br />**Marquages visuels** : Pied de page (document et e-mail) :<br /><br /> Sensibilité : Confidentiel<br /><br />**Conditions** : Aucune<br /><br />**Protection** : Aucune|
|Secret|Ces données incluent des informations hautement confidentielles de l’entreprise qui doivent être protégées. Une exposition de ces données secrètes à des utilisateurs non autorisés peut nuire gravement à l’organisation. Les informations secrètes sont, par exemple, des informations d’identification personnelles, des enregistrements de clients, des codes source et des rapports financiers préalablement annoncés.|**Activé** : Oui <br /><br />**Couleur** : Rouge<br /><br />**Marquages visuels** : Pied de page (document et e-mail) :<br /><br /> Sensibilité : Secret<br /><br />**Conditions** : Aucune<br /><br />**Protection** : Aucune|


### <a name="sub-labels"></a>Sous-étiquettes

|Étiquette|Info-bulle|Paramètres|
|-------------------------------|---------------------------|-----------------|
|Secret \ Toute l’entreprise|Ces données incluent des informations métier sensibles pour lesquelles les employés de la société ont une autorisation.|**Activé** : Oui <br /><br />**Marquages visuels** : Désactivés<br /><br />**Conditions** : Aucune<br /><br />**Protection** : Aucune|
|Secret > Mon groupe|Ces données incluent des informations métier sensibles pour lesquelles des groupes d’employés ont une autorisation.|**Activé** : Oui <br /><br />**Marquages visuels** : Désactivés<br /><br />**Conditions** : Aucune<br /><br />**Protection** : Aucune|

### <a name="information-protection-bar"></a>Barre Information Protection

|Paramètre|Valeur|
|-------------------------------|---------------------------|
|Titre|Sensibilité|
|Info-bulle|La confidentialité des informations est composée de quatre niveaux distincts (public, interne, confidentiel, secret), qui permettent à l’utilisateur d’identifier le risque d’exposition d’informations à des utilisateurs non autorisés à l’intérieur ou à l’extérieur de l’entreprise.|


### <a name="settings"></a>Paramètres

|Paramètre|Valeur|
|-------------------------------|---------------------------|
|Tous les documents et e-mails doivent avoir une étiquette (appliquée automatiquement ou par les utilisateurs)|Désactivé|
|Sélectionner l’étiquette par défaut|Aucune|
|Les utilisateurs doivent fournir une justification pour définir une étiquette de classification moins élevée, supprimer une étiquette ou supprimer la protection|Désactivé|
|Spécifiez une URL personnalisée pour la page web « En savoir plus » du client Azure Information Protection|Vide|


## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy). 

[!INCLUDE[Commenting house rules](../includes/houserules.md)]