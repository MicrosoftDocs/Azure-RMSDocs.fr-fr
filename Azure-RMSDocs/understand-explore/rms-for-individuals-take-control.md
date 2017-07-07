---
title: "Contrôler les comptes créés pour RMS for individuals - AIP"
description: "Comment contrôler les comptes d’utilisateur dans Azure Active Directory si vous ne souhaitez pas convertir l’abonnement RMS for Individuals de votre organisation en un abonnement payant."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a83880d0-f0f9-4a32-9e00-2f6635d7cc8d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: ff8cd150ce438a7b9ad5203dfb6d9d01c1a0d85a
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2017
---
# <a name="how-administrators-can-control-the-accounts-created-for-rms-for-individuals"></a>Contrôle administrateur des comptes créés pour RMS for individuals

>*S’applique à : Azure Information Protection*


Même si vous ne souhaitez pas convertir l'abonnement RMS for individuals de votre organisation en un abonnement payant, vous pouvez tout de même contrôler les comptes d'utilisateur associés à l'annuaire Azure de votre organisation de l'une des manières suivantes :

-   Implémentez des solutions d'intégration d'annuaire pour Azure Active Directory et votre infrastructure de services de domaine Active Directory. Vous pouvez synchroniser les comptes et les mots de passe, afin que les utilisateurs n'aient pas à créer de nouveaux comptes pour utiliser Rights Management. Vos stratégies de mot de passe locales s'appliqueront ainsi aux nouveaux comptes utilisateur Azure. Vous pouvez également synchroniser les mots de passe, afin que les utilisateurs n'aient pas à mémoriser un autre mot de passe pour utiliser Rights Management.

-   Vous pouvez empêcher des utilisateurs de s'inscrire pour utiliser Azure Rights Management avec l'abonnement RMS for Individuals. Le plus souvent, cette option est peu avantageuse, car les utilisateurs partagent des fichiers sans protection (ce qui constitue un danger pour l'organisation) ou utilisent un autre mécanisme de protection de fichiers qui empêche le service informatique d'accéder aux données. Toutefois, si vous souhaitez vraiment empêcher des utilisateurs de s'inscrire à RMS for Individuals, procédez de l'une des manières suivantes après avoir acquis la propriété de l'annuaire de votre organisation dans Azure :

    -   Empêchez tout utilisateur de souscrire un abonnement en libre-service, RMS for Individuals inclus.  (Actuellement, ce paramètre s'applique à tous les abonnements Azure qui utilisent le processus en libre-service, et vous ne pouvez pas sélectionner le service concerné). Pour ce faire, définissez le paramètre **AllowAdHocSubscriptions** sur false avec l’applet de commande [Set-MsolCompanySettings](http://technet.microsoft.com/library/dn194127.aspx) du module PowerShell pour Azure Active Directory. Par exemple : **Set-MsolCompanySettings -AllowAdHocSubscriptions $false**

    -   Empêchez les utilisateurs de créer un compte dans Azure, ce qui signifie que seuls les utilisateurs ayant déjà un compte peuvent souscrire des abonnements en libre-service, dont l'abonnement RMS for Individuals.  Pour ce faire, définissez le paramètre **AllowEmailVerifiedUsers** sur false avec l’applet de commande [Set-MsolCompanySettings](http://technet.microsoft.com/library/dn194127.aspx) du module PowerShell pour Azure Active Directory. Par exemple : **Set-MsolCompanySettings -AllowEmailVerifiedUsers $false -AllowAdHocSubscriptions $true**

    -   Synchronisez votre infrastructure de services de domaine Active Directory avec Azure Active Directory. Cela empêche la création de comptes lorsque des utilisateurs souscrivent des abonnements en libre-service tel l'abonnement RMS for Individuals. Vous pouvez par ailleurs supprimer ou désactiver des comptes précédemment créés dans l'annuaire Azure.

Pour contrôler les comptes d'utilisateur dans l'annuaire Azure, ou empêcher des utilisateurs de s'inscrire à RMS for individuals, vous devez disposer d'un abonnement Azure et être propriétaire de l'annuaire. Si vous n'avez pas encore d'abonnement Azure, vous pouvez en obtenir un gratuitement. Si un annuaire a été créé automatiquement pour vous lors du processus d'abonnement en libre-service, acquérez la propriété du domaine utilisé pour le créer. Si vous possédez déjà un annuaire dans Azure, et que les utilisateurs ont spécifié un nouveau domaine que vous utilisez dans votre organisation, fusionnez ce domaine dans votre annuaire existant. Pour plus d'informations, voir les instructions de la rubrique [Qu’est-ce qu'une inscription libre-service à Azure ?](https://azure.microsoft.com/documentation/articles/active-directory-self-service-signup/)


## <a name="next-steps"></a>Étapes suivantes

Comment savoir si des utilisateurs autres que des administrateurs peuvent créer leurs comptes dans Azure Active Directory pour RMS for individuals ?  Consultez [Détermination des utilisateurs inscrits à RMS for Individuals](rms-for-individuals-identify-sign-up.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]