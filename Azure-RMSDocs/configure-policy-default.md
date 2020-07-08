---
title: Stratégie Azure Information Protection par défaut – AIP
description: Comprendre le processus de configuration de la stratégie par défaut pour Azure Information Protection. Si vous modifiez la stratégie par défaut, vous pouvez référencer ces valeurs de manière à réinitialiser votre stratégie sur les valeurs par défaut.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 9cbfea73a667c0d7b96c0daddb9efbb5cf97b78b
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/07/2020
ms.locfileid: "86048287"
---
# <a name="the-default-azure-information-protection-policy"></a>La stratégie Azure Information Protection par défaut

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Instructions pour : [Client Azure Information Protection pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Pour fournir une expérience client unifiée et rationalisée, **Azure Information Protection client (Classic)** et **Gestion des étiquettes** dans le Portail Azure sont **dépréciées** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

> [!NOTE]
> La stratégie de Azure Information Protection s’applique au client Azure Information Protection (Classic) et non au client d’étiquetage unifié Azure Information Protection. Vous ne connaissez pas trop la différence entre ces clients ? Consultez ce [FAQ](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients).
> 
> Si vous recherchez des informations sur la configuration des étiquettes de sensibilité et des paramètres de stratégie pour le client d’étiquetage unifié, consultez [en savoir plus sur les étiquettes de sensibilité](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels) dans la documentation relative à la conformité de Microsoft 365.

Utilisez les informations suivantes pour comprendre la configuration de la stratégie par défaut pour Azure Information Protection.

Quand un administrateur se connecte pour la première fois au service Azure Information Protection à l’aide du Portail Azure, la stratégie Azure Information Protection par défaut de ce locataire est créée. Il peut arriver que Microsoft apporte des modifications à cette stratégie par défaut ; cependant, si vous utilisiez déjà le service avant cette révision, votre version antérieure de la stratégie Azure Information Protection par défaut n’est pas mise à jour, car vous pouvez l’avoir configurée et déployée en production.

Vous pouvez référencer les valeurs suivantes pour rétablir les valeurs par défaut de votre stratégie Azure Information Protection ou la mettre à jour avec les dernières valeurs.

> [!IMPORTANT]
> À compter du 2019 avril, les étiquettes par défaut ne sont pas créées automatiquement pour les nouveaux clients. Ces locataires sont automatiquement provisionnés pour la plateforme d’étiquetage unifié, il n’est donc pas nécessaire de migrer les étiquettes après les avoir configurées dans le portail Azure.
> 
> Pour ces locataires, s’il n’existe pas d’étiquettes de sensibilité déjà créées dans le Centre de sécurité et de conformité Office 365, le centre de sécurité Microsoft 365 ou le centre de conformité Microsoft 365, vous pouvez créer les étiquettes par défaut à partir de la stratégie par défaut pour Azure Information Protection. Pour ce faire, sélectionnez **générer des étiquettes par défaut** dans le volet **étiquettes** et ajoutez les étiquettes à la stratégie globale. Si vous ne voyez pas l’option permettant de générer des étiquettes par défaut, vous devrez peut-être d’abord activer l’étiquetage unifié à partir du volet **gérer**l'  >  **étiquetage unifié** . Pour des instructions détaillées, consultez le démarrage rapide [Bien démarrer avec Azure Information Protection sur le portail Azure](quickstart-viewpolicy.md).


## <a name="current-default-policy"></a>Stratégie par défaut actuelle

Cette version de la stratégie Azure Information Protection par défaut date du 31 juillet 2017.

Cette stratégie Azure Information Protection par défaut est créée lorsque le service Azure Rights Management est activé, ce qui est le cas pour les nouveaux locataires à partir de février 2018. Pour plus d’informations, consultez le billet de blog de lancement [Improvements to the protection stack in Azure Information Protection](https://cloudblogs.microsoft.com/enterprisemobility/2018/03/08/improvements-to-the-protection-stack-in-azure-information-protection) (Améliorations de la pile de protection dans Azure Information Protection).

Cette stratégie Azure Information Protection par défaut est également créée si vous avez [activé manuellement le service](activate-service.md) avant la création de la stratégie Azure Information Protection. 

Si le service n’a pas été activé, la stratégie Azure Information Protection par défaut ne configure pas de protection pour les sous-étiquettes suivantes :

- **Confidentiel \ Tous les employés**

- **Confidentiel \ Destinataires uniquement**

- **Hautement confidentiel \ Tous les employés** 

- **Hautement confidentiel \ Destinataires uniquement** 

Quand ces sous-étiquettes ne sont pas configurées automatiquement pour la protection, la stratégie Azure Information Protection par défaut reste identique à la [stratégie par défaut précédente](#default-policy-before-july-31-2017).

Quand la protection est appliquée aux sous-étiquettes **Tous les employés**, la protection est configurée à l’aide des modèles par défaut qui sont convertis automatiquement en étiquettes dans le portail Azure. Pour plus d’informations sur ces modèles, consultez [Configuration et gestion des modèles pour Azure Information Protection](configure-policy-templates.md).

Depuis le 30 août 2017, cette version de la stratégie Azure Information Protection par défaut comporte les versions multilingues des noms et des descriptions d’étiquettes. 

#### <a name="more-information-about-the-recipients-only-sublabel"></a>Plus d’informations sur les sous-étiquettes Destinataires uniquement

Les utilisateurs voient cette étiquette seulement dans Outlook. Ils ne voient pas cette étiquette dans Word, Excel et PowerPoint, ni depuis l’Explorateur de fichiers. 

Quand les utilisateurs sélectionnent cette étiquette, l’option Outlook Ne pas transférer est appliquée automatiquement à l’e-mail. Les destinataires spécifiés par les utilisateurs ne peuvent pas transférer l’e-mail, et ils ne peuvent pas copier ou en imprimer le contenu, ni enregistrer les pièces jointes.


### <a name="labels"></a>Étiquettes

|Etiquette|Info-bulle|Paramètres|
|-------------------------------|---------------------------|-----------------|
|Personnel|Données autres que les données d’entreprise, uniquement pour une utilisation personnelle.|**Activé** : Oui <br /><br />**Couleur**: vert clair<br /><br />**Marquages visuels** : Désactivés <br /><br />**Conditions**: aucune<br /><br />**Protection** : Aucune|
|Public|Données d’entreprise qui sont spécifiquement préparées et approuvées pour une consommation publique.|**Activé** : Oui <br /><br />**Couleur**: vert<br /><br />**Marquages visuels** : Désactivés<br /><br />**Conditions**: aucune<br /><br />**Protection** : Aucune|
|Général|Données d’entreprise qui ne sont pas destinées à la consommation publique. Cependant, elles peuvent être partagées avec des partenaires externes, en fonction des besoins. Il peut s’agir par exemple d’un annuaire téléphonique interne d’une entreprise, d’organigrammes, de normes internes et de la plupart des communications internes.|**Activé** : Oui <br /><br />**Couleur**: bleu <br /><br />**Marquages visuels** : Désactivés<br /><br />**Conditions**: aucune<br /><br />**Protection** : Aucune|
|Confidentiel|Données d’entreprise sensibles qui pourraient provoquer des dommages à l’activité si elles étaient partagées avec des personnes non autorisées. Elle peut concerner les contrats, les rapports de sécurité, les synthèses de prévision et les données commerciales, par exemple.|**Activé** : Oui <br /><br />**Couleur** : Orange<br /><br />**Marquages visuels** : Désactivés<br /><br />**Conditions**: aucune<br /><br />**Protection** : Aucune|
|Hautement confidentiel|Données d’entreprise très sensibles qui pourraient provoquer des dommages à l’activité si elles étaient partagées avec des personnes non autorisées. Elle peut concerner les informations relatives aux employés et aux clients, les mots de passe, le code source et les rapports financiers préannoncés, par exemple.|**Activé** : Oui <br /><br />**Couleur**: rouge<br /><br />**Marquages visuels** : Désactivés<br /><br />**Conditions**: aucune<br /><br />**Protection** : Aucune|


### <a name="sublabels"></a>Sous-étiquettes

|Etiquette|Info-bulle|Paramètres|
|-------------------------------|---------------------------|-----------------|
|Confidentiel \ Tous les employés|Données confidentielles qui nécessitent une protection, qui permettent toutes les autorisations complètes des employés. Les propriétaires des données peuvent suivre et révoquer le contenu.|**Activé** : Oui <br /><br />**Marquages visuels** : Pied de page (document et e-mail)<br /><br />Classé comme confidentiel<br /><br />**Conditions**: aucune<br /><br />**Protection** : Azure (clé cloud) [[1]](#footnote-1)|
|Confidentiel \ Tout le monde (sans protection)|Données ne nécessitant pas de protection. Utilisez cette option avec précaution et avec une justification métier appropriée.|**Activé** : Oui <br /><br />**Marquages visuels** : Pied de page (document et e-mail)<br /><br />Classé comme confidentiel <br /><br />**Conditions**: aucune<br /><br />**Protection** : Aucune|
|Confidentiel \ Destinataires uniquement|Données confidentielles qui nécessitent la protection et qui peuvent être visualisées seulement par les destinataires.|**Activé** : Oui <br /><br />**Marquages visuels** : Pied de page (e-mail)<br /><br />Classé comme confidentiel <br /><br />**Conditions**: aucune<br /><br />**Protection** : Configurer des autorisations définies par l’utilisateur (préversion), dans Outlook appliquer Ne pas transférer|
|Hautement confidentiel \ Tous les employés|Données hautement confidentielles, qui permettent les autorisations d’afficher, de modifier et de répondre de tous les employés sur ce contenu. Les propriétaires des données peuvent suivre et révoquer le contenu.|**Activé** : Oui <br /><br />**Marquages visuels** : Pied de page (document et e-mail)<br /><br />Classé hautement confidentiel<br /><br />**Conditions**: aucune<br /><br />**Protection** : Azure (clé cloud) [[2]](#footnote-2)|
|Hautement confidentiel \ Tout le monde (sans protection)|Données ne nécessitant pas de protection. Utilisez cette option avec précaution et avec une justification métier appropriée.|**Activé** : Oui <br /><br />**Marquages visuels** : Pied de page (document et e-mail)<br /><br />Classé hautement confidentiel<br /><br />**Conditions**: aucune<br /><br />**Protection** : Aucune|
|Hautement confidentiel \ Destinataires uniquement|Données hautement confidentielles qui nécessitent la protection et qui peuvent être visualisées seulement par les destinataires.|**Activé** : Oui <br /><br />**Marquages visuels** : Pied de page (e-mail)<br /><br />Classé hautement confidentiel <br /><br />**Conditions**: aucune<br /><br />**Protection** : Configurer des autorisations définies par l’utilisateur (préversion), dans Outlook appliquer Ne pas transférer|

###### <a name="footnote-1"></a>Note 1
Les autorisations de protection sont celles définies dans le [modèle par défaut](configure-policy-templates.md#default-templates), **Confidentiel\Tous les employés**.

###### <a name="footnote-2"></a>Note 2 
Les autorisations de protection sont celles définies dans le [modèle par défaut](configure-policy-templates.md#default-templates), **Hautement confidentiel\Tous les employés**.


### <a name="information-protection-bar"></a>Barre Information Protection

|Paramètre|Valeur|
|-------------------------------|---------------------------|
|Intitulé|Sensibilité|
|Info-bulle|L’étiquette actuelle pour ce contenu. Ce paramètre identifie les risques pour l’entreprise si ce contenu est partagé avec des personnes non autorisées à l’intérieur ou à l’extérieur de l’organisation.|


### <a name="settings"></a>Paramètres

Certains paramètres ont été ajoutés après le 31 juillet 2017.

|Paramètre|Valeur|
|-------------------------------|---------------------------|
|Sélectionner l’étiquette par défaut|None|
|Envoyer des données d’audit à l’analytique Azure Information Protection|Désactivé|
|Tous les documents et e-mails doivent avoir une étiquette (appliquée automatiquement ou par les utilisateurs)|Désactivé|
|Les utilisateurs doivent fournir une justification pour définir une étiquette de classification moins élevée, supprimer une étiquette ou supprimer la protection|Désactivé|
|Pour les e-mails avec des pièces jointes, appliquez une étiquette qui correspond à la classification la plus élevée de ces pièces jointes|Désactivé|
|Afficher la barre Information Protection dans les applications Office|Désactivé|
|Ajouter le bouton Ne pas transférer au ruban Outlook|Désactivé|
|Activer les options d’autorisations personnalisées pour les utilisateurs|Désactivé|
|Spécifiez une URL personnalisée pour la page web « En savoir plus » du client Azure Information Protection|Vide|

## <a name="default-policy-before-july-31-2017"></a>Stratégie par défaut avant le 31 juillet 2017

Notez que les descriptions de cette stratégie font référence aux données qui nécessitent une protection, ainsi qu’au suivi et à la révocation des données. La stratégie ne configure pas cette protection pour ces étiquettes : vous devez donc effectuer des étapes supplémentaires pour compléter cette description. Par exemple, configurez l’étiquette pour appliquer la protection ou utilisez une solution de protection contre la perte de données. Avant de pouvoir suivre et révoquer un document en utilisant le site de suivi des documents, ce document doit être protégé par le service Azure Rights Management et suivi par la personne qui l’a protégé. 


### <a name="labels"></a>Étiquettes

|Etiquette|Info-bulle|Paramètres|
|-------------------------------|---------------------------|-----------------|
|Personnel|Données autres que les données d’entreprise, uniquement pour une utilisation personnelle.|**Activé** : Oui <br /><br />**Couleur**: vert clair<br /><br />**Marquages visuels** : Désactivés <br /><br />**Conditions**: aucune<br /><br />**Protection** : Aucune|
|Public|Données d’entreprise qui sont spécifiquement préparées et approuvées pour une consommation publique.|**Activé** : Oui <br /><br />**Couleur**: vert<br /><br />**Marquages visuels** : Désactivés<br /><br />**Conditions**: aucune<br /><br />**Protection** : Aucune|
|Général|Données d’entreprise qui ne sont pas destinées à la consommation publique. Cependant, elles peuvent être partagées avec des partenaires externes, en fonction des besoins. Il peut s’agir par exemple d’un annuaire téléphonique interne d’une entreprise, d’organigrammes, de normes internes et de la plupart des communications internes.|**Activé** : Oui <br /><br />**Couleur**: bleu <br /><br />**Marquages visuels** : Désactivés<br /><br />**Conditions**: aucune<br /><br />**Protection** : Aucune|
|Confidentiel|Données d’entreprise sensibles qui pourraient provoquer des dommages à l’activité si elles étaient partagées avec des personnes non autorisées. Elle peut concerner les contrats, les rapports de sécurité, les synthèses de prévision et les données commerciales, par exemple.|**Activé** : Oui <br /><br />**Couleur** : Orange<br /><br />**Marquages visuels** : Désactivés<br /><br />**Conditions**: aucune<br /><br />**Protection** : Aucune|
|Hautement confidentiel|Données d’entreprise très sensibles qui pourraient provoquer des dommages à l’activité si elles étaient partagées avec des personnes non autorisées. Elle peut concerner les informations relatives aux employés et aux clients, les mots de passe, le code source et les rapports financiers préannoncés, par exemple.|**Activé** : Oui <br /><br />**Couleur**: rouge<br /><br />**Marquages visuels** : Désactivés<br /><br />**Conditions**: aucune<br /><br />**Protection** : Aucune|


### <a name="sublabels"></a>Sous-étiquettes

|Etiquette|Info-bulle|Paramètres|
|-------------------------------|---------------------------|-----------------|
|Confidentiel \ Tous les employés|Données confidentielles qui nécessitent une protection, qui permettent toutes les autorisations complètes des employés. Les propriétaires des données peuvent suivre et révoquer le contenu.|**Activé** : Oui <br /><br />**Marquages visuels** : Pied de page (document et e-mail)<br /><br />Classé comme confidentiel<br /><br />**Conditions**: aucune<br /><br />**Protection** : Aucune|
|Confidentiel \ Tout le monde (sans protection)|Données ne nécessitant pas de protection. Utilisez cette option avec précaution et avec une justification métier appropriée.|**Activé** : Oui <br /><br />**Marquages visuels** : Pied de page (document et e-mail)<br /><br />Classé comme confidentiel <br /><br />**Conditions**: aucune<br /><br />**Protection** : Aucune|
|Hautement confidentiel \ Tous les employés|Données hautement confidentielles, qui permettent les autorisations d’afficher, de modifier et de répondre de tous les employés sur ce contenu. Les propriétaires des données peuvent suivre et révoquer le contenu.|**Activé** : Oui <br /><br />**Marquages visuels** : Pied de page (document et e-mail)<br /><br />Classé hautement confidentiel<br /><br />**Conditions**: aucune<br /><br />**Protection** : Aucune|
|Hautement confidentiel \ Tout le monde (sans protection)|Données ne nécessitant pas de protection. Utilisez cette option avec précaution et avec une justification métier appropriée.|**Activé** : Oui <br /><br />**Marquages visuels** : Pied de page (document et e-mail)<br /><br />Classé hautement confidentiel<br /><br />**Conditions**: aucune<br /><br />**Protection** : Aucune|

### <a name="information-protection-bar"></a>Barre Information Protection

|Paramètre|Valeur|
|-------------------------------|---------------------------|
|Intitulé|Sensibilité|
|Info-bulle|L’étiquette actuelle pour ce contenu. Ce paramètre identifie les risques pour l’entreprise si ce contenu est partagé avec des personnes non autorisées à l’intérieur ou à l’extérieur de l’organisation.|


### <a name="settings"></a>Paramètres

|Paramètre|Valeur|
|-------------------------------|---------------------------|
|Tous les documents et e-mails doivent avoir une étiquette (appliquée automatiquement ou par les utilisateurs)|Désactivé|
|Sélectionner l’étiquette par défaut|None|
|Les utilisateurs doivent fournir une justification pour définir une étiquette de classification moins élevée, supprimer une étiquette ou supprimer la protection|Désactivé|
|Pour les e-mails avec des pièces jointes, appliquez une étiquette qui correspond à la classification la plus élevée de ces pièces jointes|Désactivé|
|Spécifiez une URL personnalisée pour la page web « En savoir plus » du client Azure Information Protection|Vide|

## <a name="default-policy-before-march-21-2017"></a>Stratégie par défaut avant le 21 mars 2017

### <a name="labels"></a>Étiquettes

|Etiquette|Info-bulle|Paramètres|
|-------------------------------|---------------------------|-----------------|
|Personnel|Réservé à un usage personnel. Ces données ne sont pas surveillées par l’organisation. Les informations personnelles ne doivent inclure aucune donnée professionnelle.|**Activé** : Oui <br /><br />**Couleur**: vert clair<br /><br />**Marquages visuels** : Désactivés <br /><br />**Conditions**: aucune<br /><br />**Protection** : Aucune|
|Public|Ces informations sont internes et peuvent être utilisées par tout le monde à l’intérieur ou à l’extérieur de l’entreprise.|**Activé** : Oui <br /><br />**Couleur**: vert<br /><br />**Marquages visuels** : Désactivés<br /><br />**Conditions**: aucune<br /><br />**Protection** : Aucune|
|Interne|Ces informations comprennent une grande variété de données métier internes qui peuvent être utilisées par tous les employés et peuvent être partagées avec des clients et des partenaires commerciaux autorisés. Les informations internes sont, par exemple, des stratégies de l’entreprise et la plupart des communications internes.|**Activé** : Oui <br /><br />**Couleur**: bleu <br /><br />**Marquages visuels**: pied de page (document et e-mail) : <br /><br />Sensibilité : Interne<br /><br />**Conditions**: aucune<br /><br />**Protection** : Aucune|
|Confidentiel|Ces données incluent des informations métier sensibles. Une exposition de ces données à des utilisateurs non autorisés peut nuire à l’organisation. Les informations confidentielles sont, par exemple, des informations sur les employés, des projets ou des contrats de clients, ainsi que des données de comptes de vente.|**Activé** : Oui <br /><br />**Couleur** : Orange<br /><br />**Marquages visuels**: pied de page (document et e-mail) :<br /><br /> Sensibilité : Confidentiel<br /><br />**Conditions**: aucune<br /><br />**Protection** : Aucune|
|Secret|Ces données incluent des informations hautement confidentielles de l’entreprise qui doivent être protégées. Une exposition de ces données secrètes à des utilisateurs non autorisés peut nuire gravement à l’organisation. Les informations secrètes sont, par exemple, des informations d’identification personnelles, des enregistrements de clients, des codes source et des rapports financiers préalablement annoncés.|**Activé** : Oui <br /><br />**Couleur**: rouge<br /><br />**Marquages visuels**: pied de page (document et e-mail) :<br /><br /> Sensibilité : Secret<br /><br />**Conditions**: aucune<br /><br />**Protection** : Aucune|


### <a name="sublabels"></a>Sous-étiquettes

|Etiquette|Info-bulle|Paramètres|
|-------------------------------|---------------------------|-----------------|
|Secret \ Toute l’entreprise|Ces données incluent des informations métier sensibles pour lesquelles les employés de la société ont une autorisation.|**Activé** : Oui <br /><br />**Marquages visuels** : Désactivés<br /><br />**Conditions**: aucune<br /><br />**Protection** : Aucune|
|Secret > Mon groupe|Ces données incluent des informations métier sensibles pour lesquelles des groupes d’employés ont une autorisation.|**Activé** : Oui <br /><br />**Marquages visuels** : Désactivés<br /><br />**Conditions**: aucune<br /><br />**Protection** : Aucune|

### <a name="information-protection-bar"></a>Barre Information Protection

|Paramètre|Valeur|
|-------------------------------|---------------------------|
|Intitulé|Sensibilité|
|Info-bulle|La confidentialité des informations est composée de quatre niveaux distincts (public, interne, confidentiel, secret), qui permettent à l’utilisateur d’identifier le risque d’exposition d’informations à des utilisateurs non autorisés à l’intérieur ou à l’extérieur de l’entreprise.|


### <a name="settings"></a>Paramètres

|Paramètre|Valeur|
|-------------------------------|---------------------------|
|Tous les documents et e-mails doivent avoir une étiquette (appliquée automatiquement ou par les utilisateurs)|Désactivé|
|Sélectionner l’étiquette par défaut|None|
|Les utilisateurs doivent fournir une justification pour définir une étiquette de classification moins élevée, supprimer une étiquette ou supprimer la protection|Désactivé|
|Spécifiez une URL personnalisée pour la page web « En savoir plus » du client Azure Information Protection|Vide|


## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy). 
