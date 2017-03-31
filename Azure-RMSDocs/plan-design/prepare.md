---
title: "Préparer la protection des données Azure Rights Management - AIP"
description: "Vérifiez que tout est en place pour utiliser le service Azure Rights Management afin de permettre à votre organisation de protéger les documents et les e-mails."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/28/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: afbca2d6-32a7-4bda-8aaf-9f93f5da5abc
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 4b074f9a9a3d72b4d1ab5810b69e92b4792b0711
ms.sourcegitcommit: 16fec44713c7064959ebb520b9f0857744fecce9
translationtype: HT
---
# <a name="preparing-for-azure-information-protection"></a>Préparation d’Azure Information Protection

>*S’applique à : Azure Information Protection, Office 365*

Avant de déployer Azure Information Protection dans votre organisation, vérifiez que les éléments suivants sont en place :

-   Les comptes d’utilisateurs et groupes du cloud créés manuellement ou qui sont automatiquement créés et synchronisés par les services de domaine Active Directory (AD DS).

    Lorsque vous synchronisez vos comptes et groupes locaux, certains attributs ne doivent pas être synchronisés. Pour obtenir la liste des attributs qui doivent être synchronisés pour le service Azure Rights Management utilisé par Azure Information Protection, consultez la [section relative à Azure RMS](/active-directory/active-directory-aadconnectsync-attributes-synchronized#azure-rms) dans la documentation Azure Active Directory. Pour faciliter le déploiement, nous vous conseillons d’utiliser [Azure AD Connect](/active-directory/active-directory-aadconnectsync-whatis) pour connecter vos annuaires locaux à Azure Active Directory, mais vous pouvez utiliser toute méthode de synchronisation d’annuaires permettant d’obtenir le même résultat.

-   Les groupes à extension messagerie du cloud que vous utiliserez avec Azure Information Protection. Ceux-ci peuvent être des groupes intégrés ou des groupes créés manuellement contenant les utilisateurs qui utiliseront des documents et e-mails protégés.

    Si vous avez Exchange Online, vous pouvez créer et utiliser des groupes à extension messagerie à l’aide du Centre d’administration Exchange. Si vous disposez d’AD DS et synchronisez sur Azure AD, vous pouvez créer et utiliser des groupes à extension messagerie qui sont des groupes de sécurité ou de distribution.

### <a name="group-membership-caching"></a>Mise en cache de l’appartenance au groupe

Pour des raisons de performances, l’appartenance au groupe est mise en cache par le service Azure Rights Management. Cela signifie que les modifications apportées à l’appartenance au groupe peuvent prendre jusqu’à 3 heures pour entrer en vigueur, et cette période est susceptible de changer. N’oubliez pas de tenir compte de ce délai dans toutes les modifications ou les tests que vous effectuez lorsque vous utilisez des groupes dans la configuration du service Azure Rights Management, par exemple, lorsque vous configurez des [modèles personnalisés](../deploy-use/configure-custom-templates.md) ou lorsque vous utilisez un groupe pour la [fonctionnalité de super utilisateur](../deploy-use/configure-super-users.md). 

### <a name="considerations-if-email-addresses-change"></a>Éléments à prendre en considération en cas de modification des adresses de messagerie

Lorsque vous configurez des droits d’utilisation pour les utilisateurs ou les groupes et les sélectionnez par leur nom complet, votre sélection enregistre et utilise l’adresse de messagerie de cet objet. Si l’adresse de messagerie est modifiée ultérieurement, les utilisateurs sélectionnés ne disposeront pas des autorisations.

Si les adresses de messagerie sont modifiées, nous vous recommandons d’ajouter l’ancienne adresse de messagerie en tant qu’adresse de messagerie proxy (également appelée un alias ou une autre adresse de messagerie) à l’utilisateur ou au groupe, afin que les droits d’utilisation qui ont été attribués précédemment soient conservés. Si vous ne pouvez pas le faire, vous devez supprimer l’utilisateur ou le groupe de votre configuration et le sélectionner à nouveau pour enregistrer l’adresse de messagerie mise à jour afin que le contenu nouvellement protégé utilise la nouvelle adresse de messagerie.

Les modèles Custom Rights Management constituent un exemple de l’emplacement à partir duquel vous pouvez sélectionner des utilisateurs ou des groupes en fonction du nom complet pour attribuer des droits d’utilisation. Les utilisateurs peuvent aussi sélectionner des utilisateurs et des groupes en fonction du nom complet lorsqu’ils configurent des autorisations personnalisées avec le client Azure Information Protection.

## <a name="activate-the-rights-management-service-for-data-protection"></a>Activer le service Rights Management pour la protection des données
Lorsque vous êtes prêt à commencer à protéger des documents et des e-mails, activez le service Rights Management pour activer cette technologie. Pour plus d’informations, consultez [Activation d’Azure Rights Management](../deploy-use/activate-service.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


