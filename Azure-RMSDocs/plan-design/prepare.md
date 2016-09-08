---
title: "Préparation pour Azure Rights Management | Azure RMS"
description: "Une fois que vous avez souscrit un abonnement au cloud et assigné à votre organisation un compte pour Microsoft Office 365 ou Azure Active Directory, vous êtes prêt à activer le service Rights Management."
author: cabailey
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: afbca2d6-32a7-4bda-8aaf-9f93f5da5abc
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 024a29d7c7db2e4c0578a95c93e22f8e7a5b173e
ms.openlocfilehash: 4ebdb8a75b135f4f252d640e4f16da1ea7a1ed04


---

# Préparation pour Azure Rights Management

>*S’applique à : Azure Rights Management, Office 365*

Une fois que vous avez souscrit un abonnement au cloud et assigné à votre organisation un compte pour [!INCLUDE[o365_1](../includes/o365_1_md.md)] ou Azure Active Directory, vous êtes prêt à activer le service [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].

Toutefois, commencez par vous assurer que les éléments suivants sont en place :

-   Les comptes d’utilisateurs et groupes du cloud créés manuellement ou qui sont automatiquement créés et synchronisés par les services de domaine Active Directory (AD DS).

    Lorsque vous synchronisez vos comptes et groupes locaux, certains attributs ne doivent pas être synchronisés. Pour obtenir la liste des attributs qui doivent être synchronisés pour Azure RMS, consultez la [section relative à Azure RMS](/active-directory/active-directory-aadconnectsync-attributes-synchronized#azure-rms) dans la documentation d’Azure Active Directory. Pour faciliter le déploiement, nous vous conseillons d’utiliser [Azure AD Connect](/active-directory/active-directory-aadconnectsync-whatis) pour connecter vos annuaires locaux à Azure Active Directory, mais vous pouvez utiliser toute méthode de synchronisation d’annuaires permettant d’obtenir le même résultat.

-   Les groupes à extension messagerie du cloud que vous utiliserez avec Rights Management. Ceux-ci peuvent être des groupes intégrés ou des groupes créés manuellement contenant les utilisateurs qui utiliseront Rights Management.

    Si vous avez Exchange Online, vous pouvez créer et utiliser des groupes à extension messagerie à l’aide du Centre d’administration Exchange. Si vous disposez d’AD DS et synchronisez sur Azure AD, vous pouvez créer et utiliser des groupes à extension messagerie qui sont des groupes de sécurité ou de distribution.

## Activation de Rights Management
Par défaut, [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] est désactivé quand vous créez votre compte [!INCLUDE[o365_2](../includes/o365_2_md.md)] ou Azure AD. Pour activer [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] pour votre organisation, vous devez activer le service. Pour plus d’informations, consultez [Activation d’Azure Rights Management](../deploy-use/activate-service.md).






<!--HONumber=Aug16_HO4-->


