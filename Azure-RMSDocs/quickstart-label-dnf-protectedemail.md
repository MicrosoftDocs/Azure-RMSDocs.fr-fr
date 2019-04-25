---
title: 'Démarrage rapide : Configurer une étiquette pour permettre aux utilisateurs de protéger facilement les e-mails qui contiennent des informations sensibles – AIP'
description: Configurez une étiquette qui protège l’e-mail d’un utilisateur en appliquant automatiquement la protection Ne pas transférer.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.openlocfilehash: 052dc5d4bbbd0a74bb92f87351ece62eb37e565b
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "60181682"
---
# <a name="quickstart-configure-a-label-for-users-to-easily-protect-emails-that-contain-sensitive-information"></a>Démarrage rapide : Configurer une étiquette pour permettre aux utilisateurs de protéger facilement les e-mails qui contiennent des informations sensibles

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Instructions pour : [Client Azure Information Protection pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Dans ce démarrage rapide, vous allez configurer une étiquette existante pour appliquer automatiquement le paramètre de protection Ne pas transférer.

La stratégie Azure Information Protection actuelle contient déjà des deux étiquettes avec cette configuration :

- **Confidentiel \ Destinataires uniquement**

- **Hautement confidentiel \ Destinataires uniquement**

Toutefois, si votre stratégie est antérieure, ou si la protection n’a pas été activée lors de la création de la stratégie de votre organisation, ces étiquettes ne seront pas disponibles. 

Cette configuration prend moins de 5 minutes.

## <a name="prerequisites"></a>Prérequis

Pour pouvoir suivre ce guide de démarrage rapide, il vous faut :

1. Un abonnement comportant le plan Azure Information Protection 1 ou 2.
    
    Si vous n’avez aucun de ces abonnements, vous pouvez créer un compte [gratuit](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) pour votre organisation.

2. Vous avez ajouté le panneau Azure Information Protection au Portail Azure et vérifié que le service de protection est activé.

    Si vous avez besoin d’aide avec ces actions, consultez [Démarrage rapide : Bien démarrer avec le portail Azure](quickstart-viewpolicy.md).

3. Une étiquette Azure Information Protection à configurer. 
    
    Vous pouvez utiliser une des étiquettes par défaut, ou une étiquette que vous avez créée. Si vous avez besoin d’aide pour créer une étiquette, consultez [Démarrage rapide : Créer une étiquette Azure Information Protection pour des utilisateurs spécifiques](quickstart-label-specificusers.md).

4. Pour tester la nouvelle étiquette : le client Azure Information Protection doit être installé sur les ordinateurs des utilisateurs. 
    
    Pour tester l’étiquette par vous-même, vous pouvez installer le client en accédant au [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018) et en téléchargeant **AzInfoProtection.exe** sur la page Azure Information Protection.

5. Pour tester la nouvelle étiquette : Un ordinateur exécutant Windows (au minimum Windows 7 avec Service Pack 1). Sur cet ordinateur, vous êtes connecté aux applications Office de l’une des catégories suivantes :
    
    - Applications Office version minimale 1805, build 9330.2078 d’Office 365 Business ou de Microsoft 365 Business quand une licence Azure Rights Management (également appelé Azure Information Protection pour Office 365) vous est affectée.
    
    - Office 365 ProPlus.
    
    - Office Professionnel Plus 2019.
    
    - Office Professionnel Plus 2016.
    
    - Office Professionnel Plus 2013 avec Service Pack 1.
    
    - Office Professionnel Plus 2010 avec Service Pack 2.

Pour obtenir la liste complète des prérequis d’Azure Information Protection, voir [Prérequis d’Azure Information Protection](requirements.md).

## <a name="configure-an-existing-label-to-apply-the-do-not-forward-protection"></a>Configurer une étiquette existante pour appliquer la protection Ne pas transférer

1. Ouvrez une nouvelle fenêtre de navigateur et connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur général. Accédez ensuite à **Azure Information Protection**. 
    
    Par exemple, dans le menu hub, cliquez sur **Tous les services** et tapez **Informations** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.
    
    Si vous n’êtes pas l’administrateur général, utilisez le lien suivant pour les autres rôles : [Connexion au portail Azure](configure-policy.md#signing-in-to-the-azure-portal)

2. À partir de l’option de menu **Classifications** > **Étiquettes** : dans le panneau **Azure Information Protection - Étiquettes**, sélectionnez l’étiquette que vous souhaitez configurer pour appliquer la protection. 

3. Dans le panneau **Étiquette**, recherchez **Définir des autorisations pour les documents et les e-mails contenant cette étiquette**. Sélectionnez **Protéger** ; le panneau **Protection** s’ouvre alors automatiquement si l’une des autres options a été sélectionnée précédemment. 
    
    Si le panneau **Protection** ne s’ouvre pas automatiquement, sélectionnez **Protection** :
    
    ![Configurer la protection d’une étiquette Azure Information Protection](./media/info-protect-protection-bar-configured.png).

4. Dans le panneau **Protection**, vérifiez que l’option **Azure (clé du cloud)** est sélectionnée.
    
5. Sélectionnez **Configurer les autorisations définies par l’utilisateur (préversion)**.

6. Vérifiez que l’option suivante est sélectionnée : **Dans Outlook appliquer Ne pas transférer**.

7. Si l’option suivante est cochée, décochez-la : **Dans Word, Excel, PowerPoint et l’Explorateur de fichiers, demander à l’utilisateur des autorisations personnalisées**.

8. Cliquez sur **OK** dans le panneau **Protection**, puis sur **Enregistrer** dans le panneau **Étiquette**.

Votre étiquette est maintenant configurée pour s’afficher uniquement dans Outlook et pour appliquer la protection Ne pas transférer aux e-mails.

## <a name="test-your-new-label"></a>Tester votre nouvelle étiquette

Votre étiquette configurée apparaît uniquement dans Outlook et s’applique aux e-mails envoyés à des destinataires en dehors de votre organisation si Exchange Online est configuré pour les [nouvelles fonctionnalités dans Chiffrement de messages Office 365](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e).

1. Sur votre ordinateur, ouvrez Outlook et créez un nouvel e-mail. Si Outlook est déjà ouvert, redémarrez-le pour forcer l’actualisation de la stratégie.

2. Spécifiez les destinataires, saisissez le texte de l’e-mail, puis appliquez l’étiquette que vous venez de créer. 
    
    L’e-mail est classé en fonction du nom de l’étiquette et protégé par la restriction Ne pas transférer.

3. Envoyez l’e-mail. 

Par conséquent, les destinataires ne peuvent pas transférer l’e-mail, ni l’imprimer, le copier, enregistrer des pièces jointes ou enregistrer l’e-mail sous un autre nom. L’e-mail protégé peut être lu par n’importe quel utilisateur, sur n’importe quel appareil.

## <a name="clean-up-resources"></a>Nettoyer les ressources

Procédez comme suit si vous souhaitez ignorer cette configuration et retourner votre étiquette de façon à ne pas appliquer la protection :

1. À partir de l’option de menu **Classifications** > **Étiquettes** : dans le panneau **Azure Information Protection - Étiquettes**, sélectionnez l’étiquette que vous avez configurée. 

3. Dans le panneau **Étiquette**, recherchez la zone **Définir des autorisations pour les documents et les e-mails contenant cette étiquette**, sélectionnez **Non configuré**, puis cliquez sur **Enregistrer**.

## <a name="next-steps"></a>Étapes suivantes

Ce démarrage rapide inclut les options minimales pour rapidement configurer une étiquette qui aide les utilisateurs à protéger leurs e-mails. Mais si la configuration est trop ou pas assez restrictive, consultez les autres exemples de configuration :

- [Étiquette pour des e-mails protégés qui prend en charge des autorisations moins restrictives que l’option Ne pas transférer](configure-policy-protection.md#example-4-label-for-protected-email-that-supports-less-restrictive-permissions-than-do-not-forward)

- [Étiquette qui chiffre le contenu, mais n’en restreint pas l’accès](configure-policy-protection.md#example-5-label-that-encrypts-content-but-doesnt-restrict-who-can-access-it)

Pour obtenir des instructions complètes sur la configuration d’une étiquette qui applique une protection, voir [Comment configurer une étiquette pour la protection offerte par Rights Management](configure-policy-protection.md). 
