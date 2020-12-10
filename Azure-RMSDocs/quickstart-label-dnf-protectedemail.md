---
title: Démarrage rapide – Configuration d’une étiquette pour permettre aux utilisateurs de protéger facilement les e-mails avec Azure Information Protection (AIP)
description: Configurez une étiquette qui protège l’e-mail d’un utilisateur en appliquant automatiquement la protection Ne pas transférer.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/04/2020
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: e21a19d44c287de326c7bcd2425b94bba9b984ef
ms.sourcegitcommit: 13dac930fabafeb05d71d7ae8acf5c0a78c12397
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/08/2020
ms.locfileid: "96849808"
---
# <a name="quickstart-configure-a-label-for-users-to-easily-protect-emails-that-contain-sensitive-information"></a>Démarrage rapide : Configurer une étiquette pour permettre aux utilisateurs de protéger facilement les e-mails qui contiennent des informations sensibles

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Instructions pour : [Client classique Azure Information Protection pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE]
> Pour fournir une expérience client unifiée et rationalisée, **Azure Information Protection client (Classic)** et **Gestion des étiquettes** dans le Portail Azure sont **dépréciées** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Dans ce guide de démarrage rapide, vous allez configurer une étiquette Azure Information Protection déjà créée pour appliquer automatiquement le paramètre de protection **Ne pas transférer**.

La stratégie Azure Information Protection actuelle contient déjà des deux étiquettes avec cette configuration :

- **Confidentiel \ Destinataires uniquement**

- **Hautement confidentiel \ Destinataires uniquement**

Toutefois, si votre stratégie est antérieure, ou si la protection n’a pas été activée lors de la création de la stratégie de votre organisation, ces étiquettes ne seront pas disponibles.

**Temps nécessaire :** Cette configuration prend moins de 5 minutes.

## <a name="prerequisites"></a>Prérequis

Pour pouvoir suivre ce guide de démarrage rapide, il vous faut :

|Condition requise  |Description  |
|---------|---------|
|**Un abonnement avec prise en charge**     |  Il vous faut un abonnement comportant [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection/). <br><br>Si vous n’avez aucun de ces abonnements, vous pouvez créer un compte [gratuit](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) pour votre organisation.       |
|**AIP ajouté au Portail Azure**    |  Vous avez ajouté le volet Azure Information Protection au Portail Azure et vérifié que le service de protection est activé. <br><br>Pour plus d’informations, consultez [Démarrage rapide : Bien démarrer avec le portail Azure](quickstart-viewpolicy.md).       |
|**Une étiquette Azure Information Protection à configurer**     | Utilisez une des étiquettes par défaut ou une étiquette que vous avez créée. Pour plus d’informations, consultez [Démarrage rapide : Créer une étiquette Azure Information Protection pour des utilisateurs spécifiques](quickstart-label-specificusers.md). |
|**Client classique installé**    |   Pour que vous puissiez tester la nouvelle étiquette, le client classique doit être installé sur votre ordinateur. <br><br>Le client classique Azure Information Protection est en cours de dépréciation pour mars 2021. Pour le déployer, ouvrez un ticket de support afin d’obtenir l’accès au téléchargement.  |
|**Un ordinateur Windows, connecté à des applications Office** |Pour tester la nouvelle étiquette, il vous faut un ordinateur Windows (au minimum Windows 7 avec Service Pack 1). <br><br>Sur cet ordinateur, connectez-vous à l’une des versions suivantes des applications Office : <br><br>- **Applications Office,** pour les versions listées dans le [tableau des versions prises en charge pour Microsoft 365 Apps par le canal de mise à jour](/officeupdates/update-history-microsoft365-apps-by-date), depuis Microsoft 365 Apps for Business ou Microsoft 365 Business Premium, lorsqu’une licence Azure Rights Management (également appelé Azure Information Protection pour Office 365) est attribuée à l’utilisateur. <br>- **Microsoft 365 Apps for Enterprise**. <br>- **Office Professionnel Plus 2019**. <br>- **Office Professionnel Plus 2016**.<br>- **Office Professionnel Plus 2013 avec Service Pack 1**. <br>- **Office Professional Plus 2010 avec Service Pack 2**.|
| | |

Pour obtenir la liste complète des prérequis d’Azure Information Protection, voir [Prérequis d’Azure Information Protection](requirements.md).

## <a name="configure-an-existing-label-to-apply-the-do-not-forward-protection"></a>Configurer une étiquette existante pour appliquer la protection Ne pas transférer

1. Ouvrez une nouvelle fenêtre de navigateur et connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur général. Accédez ensuite à **Azure Information Protection**.

    Par exemple, dans la zone de recherche de ressources, services et documents : Commencez à taper **Information** et sélectionnez **Azure Information Protection**.

    Si vous n’êtes pas l’administrateur général, utilisez le lien suivant pour les autres rôles : [Connexion au portail Azure](configure-policy.md#signing-in-to-the-azure-portal)

1. À partir de l’option de menu **Classifications** > **Étiquettes** : dans le volet **Azure Information Protection - Étiquettes**, sélectionnez l’étiquette que vous souhaitez configurer pour appliquer la protection.

1. Dans le volet **Étiquette**, recherchez **Définir les autorisations pour les documents et les e-mails contenant cette étiquette**. Sélectionnez **Protéger**, le volet **Protection** s’ouvre alors automatiquement si l’option **Non configuré** ou **Supprimer la protection** a été sélectionnée précédemment.

    Si le volet **Protection** ne s’ouvre pas automatiquement, sélectionnez **Protection** :

    :::image type="content" source="media/info-protect-protection-bar-configured.png" alt-text="Configuration de la protection d’une étiquette Azure Information Protection":::

1. Dans le volet **Protection**, vérifiez que l’option **Azure (clé cloud)** est sélectionnée.

1. Sélectionnez **Configurer les autorisations définies par l’utilisateur (préversion)** .

1. Vérifiez que l’option suivante est sélectionnée : **Dans Outlook appliquer Ne pas transférer**.

1. Si l’option suivante est cochée, décochez-la : **Dans Word, Excel, PowerPoint et l’Explorateur de fichiers, demander à l’utilisateur des autorisations personnalisées**.

1. Cliquez sur **OK** dans le volet **Protection**, puis sur **Enregistrer** dans le volet **Étiquette**.

Votre étiquette est maintenant configurée pour s’afficher uniquement dans Outlook et appliquer la protection **Ne pas transférer** aux e-mails.

## <a name="test-your-new-label"></a>Tester votre nouvelle étiquette

Votre étiquette configurée apparaît uniquement dans Outlook et s’applique aux e-mails envoyés à des destinataires en dehors de votre organisation si Exchange Online est configuré pour les [nouvelles fonctionnalités dans Chiffrement de messages Office 365](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e).

1. Sur votre ordinateur, ouvrez Outlook et créez un nouvel e-mail. Si Outlook est déjà ouvert, redémarrez-le pour forcer l’actualisation de la stratégie.

2. Spécifiez les destinataires, saisissez le texte de l’e-mail, puis appliquez l’étiquette que vous venez de créer.

    L’e-mail est classé en fonction du nom de l’étiquette et protégé par la restriction Ne pas transférer.

3. Envoyez l’e-mail.

De cette manière, les destinataires ne peuvent pas transférer l’e-mail, l’imprimer, effectuer une copie, enregistrer les pièces jointes ni enregistrer l’e-mail sous un autre nom. L’e-mail protégé peut être lu par n’importe quel utilisateur, sur n’importe quel appareil.

## <a name="clean-up-resources"></a>Nettoyer les ressources

Procédez comme suit si vous souhaitez ignorer cette configuration et retourner votre étiquette de façon à ne pas appliquer la protection :

1. À partir de l’option de menu **Classifications** > **Étiquettes** : dans le volet **Azure Information Protection - Étiquettes**, sélectionnez l’étiquette que vous avez configurée.

1. Dans le volet **Étiquette**, recherchez la zone **Définir les autorisations pour les documents et les e-mails contenant cette étiquette**, sélectionnez **Non configuré**, puis cliquez sur **Enregistrer**.

## <a name="next-steps"></a>Étapes suivantes

Ce démarrage rapide inclut les options minimales pour rapidement configurer une étiquette qui aide les utilisateurs à protéger leurs e-mails. Mais si la configuration est trop ou pas assez restrictive, consultez les autres exemples de configuration :

- [Étiquette pour des e-mails protégés qui prend en charge des autorisations moins restrictives que l’option Ne pas transférer](configure-policy-protection.md#example-4-label-for-protected-email-that-supports-less-restrictive-permissions-than-do-not-forward)

- [Étiquette qui chiffre le contenu, mais n’en restreint pas l’accès](configure-policy-protection.md#example-5-label-that-encrypts-content-but-doesnt-restrict-who-can-access-it)

Pour obtenir des instructions complètes sur la configuration d’une étiquette qui applique une protection, voir [Comment configurer une étiquette pour la protection offerte par Rights Management](configure-policy-protection.md).
