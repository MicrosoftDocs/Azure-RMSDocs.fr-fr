---
title: "Préparer la protection des données Azure Rights Management - AIP"
description: "Vérifiez que tout est en place pour utiliser le service Azure Rights Management afin de permettre à votre organisation de protéger les documents et les e-mails."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: afbca2d6-32a7-4bda-8aaf-9f93f5da5abc
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: 909becbdf902d552a967506b80f173e59cf756c7
ms.lasthandoff: 02/24/2017


---

# <a name="preparing-for-azure-information-protection"></a>Préparation d’Azure Information Protection

>*S’applique à : Azure Information Protection, Office 365*

Avant de déployer Azure Information Protection dans votre organisation, vérifiez que les éléments suivants sont en place :

-   Les comptes d’utilisateurs et groupes du cloud créés manuellement ou qui sont automatiquement créés et synchronisés par les services de domaine Active Directory (AD DS).

    Lorsque vous synchronisez vos comptes et groupes locaux, certains attributs ne doivent pas être synchronisés. Pour obtenir la liste des attributs qui doivent être synchronisés pour le service Azure Rights Management utilisé par Azure Information Protection, consultez la [section relative à Azure RMS](/active-directory/active-directory-aadconnectsync-attributes-synchronized#azure-rms) dans la documentation Azure Active Directory. Pour faciliter le déploiement, nous vous conseillons d’utiliser [Azure AD Connect](/active-directory/active-directory-aadconnectsync-whatis) pour connecter vos annuaires locaux à Azure Active Directory, mais vous pouvez utiliser toute méthode de synchronisation d’annuaires permettant d’obtenir le même résultat.

-   Les groupes à extension messagerie du cloud que vous utiliserez avec Azure Information Protection. Ceux-ci peuvent être des groupes intégrés ou des groupes créés manuellement contenant les utilisateurs qui utiliseront des documents et e-mails protégés.

    Si vous avez Exchange Online, vous pouvez créer et utiliser des groupes à extension messagerie à l’aide du Centre d’administration Exchange. Si vous disposez d’AD DS et synchronisez sur Azure AD, vous pouvez créer et utiliser des groupes à extension messagerie qui sont des groupes de sécurité ou de distribution.

## <a name="activate-the-rights-management-service-for-data-protection"></a>Activer le service Rights Management pour la protection des données
Lorsque vous êtes prêt à commencer à protéger des documents et des e-mails, activez le service Rights Management pour activer cette technologie. Pour plus d’informations, consultez [Activation d’Azure Rights Management](../deploy-use/activate-service.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]



