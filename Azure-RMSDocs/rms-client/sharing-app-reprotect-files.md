---
title: "Modifier les autorisations des fichiers qui ont été protégés par Rights Management | Azure Information Protection"
description: "Quand vous protégez un fichier avec Rights Management, vous pouvez modifier les autorisations en le reprotégeant, puis en spécifiant tous les utilisateurs qui doivent y avoir accès et quelles autorisations vous souhaitez leur accorder."
keywords: 
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5ac121b3-d7a0-40e4-8fe7-90bf4cf796f1
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: c0bfd99229e4d93c91fe8f9efafd887aa7562328


---

# <a name="change-permissions-on-files-that-have-been-protected-by-rights-management"></a>Modifier les autorisations des fichiers qui ont été protégés par Rights Management

>*S’applique à : Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 7 avec SP1, Windows 8, Windows 8.1*

Quand vous protégez un fichier avec Rights Management, vous pouvez modifier les autorisations en le reprotégeant, puis en spécifiant tous les utilisateurs qui doivent y avoir accès et quelles autorisations vous souhaitez leur accorder.

> [!IMPORTANT]
> Il ne s’agit pas d’une modification incrémentielle, mais d’un remplacement total. En fait, vous reprotégez le fichier avec l’ensemble complet d’autorisations souhaité.
> 
>  Par exemple, si un fichier est protégé pour que seuls les employés du service Marketing puissent l’ouvrir et que vous souhaitez que les employés du service Ventes puissent également l’ouvrir, vous devez reprotéger le fichier pour que le service Ventes et le service Marketing puissent l’ouvrir.
>
> De même, si vous souhaitez ajouter ou supprimer une autorisation, vous ne pouvez pas simplement spécifier cette autorisation à ajouter ou supprimer. Vous devez spécifier toutes les autorisations que vous voulez accorder aux utilisateurs spécifiés.

Si vous êtes le propriétaire du fichier que vous souhaitez reprotéger (par exemple, vous l’avez initialement protégé à l’aide de l’application de partage), vous êtes automatiquement autorisé à le reprotéger. Si vous n’êtes pas le propriétaire, vous n’êtes pas obligatoirement autorisé à reprotéger le fichier. Cela dépend des autorisations dont le fichier protégé dispose actuellement. Vous devez avoir le [droit d’utilisation Contrôle total](../deploy-use/configure-usage-rights.md#usage-rights-and-descriptions) pour reprotéger un fichier.

Par exemple, si quelqu’un d’autre a protégé le fichier à l’aide de l’application de partage Rights Management et qu’il a spécifié un groupe auquel vous appartenez et **Copropriétaire** comme autorisation personnalisée, vous pouvez reprotéger le fichier. En revanche, s’il n’a pas spécifié votre nom ou un groupe auquel vous appartenez, ou s’il a sélectionné **Réviseur - Consulter et modifier** ou un modèle qui ne vous permet pas de supprimer des autorisations, vous ne pouvez pas reprotéger le fichier. Le moyen le plus simple de le savoir consiste à essayer de reprotéger le fichier.

Si vous souhaitez supprimer complètement toutes les autorisations pour que le fichier ne soit plus protégé, consultez [Supprimer la protection d’un fichier](sharing-app-remove-protection.md).

## <a name="to-re-protect-a-file-in-place"></a>Pour reprotéger un fichier sur place

1.  Dans l'Explorateur de fichiers, sélectionnez un fichier à protéger. Cliquez avec le bouton droit, sélectionnez **Protéger avec RMS**, puis sélectionnez **Protéger sur place**. Exemple :

    ![Option de menu Protéger sur place](../media/ADRMS_MSRMSApp_SP_CompanyDefined.png)

    > [!NOTE]
    > Si vous ne voyez pas l'option **Protéger avec RMS** , il est probable que l'application de partage RMS ne soit pas installée sur votre ordinateur ou que celui-ci nécessite un redémarrage pour terminer l'installation. Pour plus d’informations sur l’installation de l’application de partage RMS, consultez [Télécharger et installer l’application de partage Rights Management](install-sharing-app.md).

2.  Effectuez l'une des opérations suivantes :

    -   Sélectionnez un modèle de stratégie : il s'agit d'une autorisation prédéfinie qui restreint généralement l'accès et l'utilisation à certaines personnes au sein de votre organisation. Par exemple, si le nom de votre organisation est « Contoso, Ltd », voici ce que vous pouvez lire : **Contoso, Ltd - Affichage confidentiel uniquement**. Si vous protégez un fichier sur cet ordinateur pour la première fois, vous devez commencer par sélectionner **Protection définie par la société** pour télécharger les modèles.

        La prochaine fois que vous cliquerez sur l’option **Protéger sur place**, vous aurez jusqu’à 10 modèles affichés, prêts à être sélectionnés. Si le nombre de modèles disponibles est supérieur à 10 et que vous ne voyez pas celui qui vous intéresse, cliquez sur **Protection définie par la société** pour télécharger et afficher tous les modèles.

        Lorsque vous sélectionnez un modèle de stratégie, vous pouvez également protéger plusieurs fichiers et un dossier. Lorsque vous sélectionnez un dossier, tous les fichiers qu'il contient sont automatiquement sélectionnées pour la protection. En revanche, les nouveaux fichiers que vous créez dans ce dossier ne le sont pas.

    -   Sélectionnez **Autorisations personnalisées**: Choisissez cette option si les modèles n'offrent pas le niveau de protection nécessaire, ou si vous souhaitez définir vous-même explicitement les options de protection. Spécifiez les options souhaitées pour ce fichier dans la boîte de dialogue [Ajouter une protection](sharing-app-dialog-box.md), puis cliquez sur **Appliquer**.

3. Si vous n’êtes pas autorisé à reprotéger le fichier, un message **Impossible de protéger le contenu** s’affiche, avec l’e-mail de la personne à contacter (le propriétaire du document) pour que vous puissiez lui demander de modifier les autorisations pour vous.

    Si vous êtes autorisé à reprotéger le fichier, avant que le focus revienne sur l’Explorateur de fichiers, une boîte de dialogue peut s’afficher brièvement pour vous informer que le fichier est protégé. Les fichiers sélectionnés sont désormais protégés avec vos modifications. 

> [!NOTE]
> Pour pouvoir reprotéger le fichier, le service Rights Management doit confirmer que vous êtes autorisé à effectuer cette action sur ce fichier. Pour ce faire, il vérifie vos nom d’utilisateur et mot de passe. Dans certains cas, cette opération peut être mise en cache de sorte que vous ne voyez pas d'invite vous demandant vos informations d'identification. Dans d'autres cas, vous êtes invité à fournir vos informations d'identification.
>
> Si votre organisation n’utilise pas Azure Information Protection ou AD RMS, vous pouvez demander un compte gratuit acceptant vos informations d’identification pour pouvoir utiliser des fichiers protégés à l’aide de RMS :
>
> -   Pour demander ce compte, cliquez sur le lien [RMS for Individuals](http://go.microsoft.com/fwlink/?LinkId=309469).
>
>     Lorsque vous vous inscrivez, utilisez l'adresse de messagerie de votre organisation plutôt qu'une adresse personnelle. Si vous vous inscrivez parce que vous reçu une pièce protégée jointe à un message électronique, utilisez l'adresse de messagerie à laquelle ce message a été envoyé.
> -   Pour plus d’informations, consultez [RMS for individuals et Azure Rights Management](../understand-explore/rms-for-individuals.md).

## <a name="to-re-protect-a-file-that-you-have-emailed"></a>Pour reprotéger un fichier que vous avez envoyé par e-mail

Si vous souhaitez modifier les autorisations pour un fichier que vous avez envoyé par e-mail :

- **Pour permettre à d’autres personnes de lire le fichier** : envoyez-leur le fichier par e-mail en suivant les instructions fournies dans [Protéger un fichier que vous partagez par courrier électronique](sharing-app-protect-by-email.md).

- **Pour modifier les autorisations pour le fichier** : renvoyez le fichier par e-mail en suivant les instructions fournies dans [Protéger un fichier que vous partagez par courrier électronique](sharing-app-protect-by-email.md) et choisissez les nouvelles autorisations souhaitées. 

    Étant donné que vous ne pouvez pas supprimer les autorisations précédentes sur le fichier envoyé initialement par e-mail, mais seulement les remplacer par une nouvelle version, vous pourriez révoquer le fichier précédemment envoyé par e-mail pour que les destinataires ne puissent plus ouvrir cette version du document. La révocation convient si vous devez rendre les autorisations plus restrictives (par exemple supprimer des utilisateurs qui ne doivent pas avoir accès au fichier ou qui ne doivent plus pouvoir le modifier).

    Pour révoquer un fichier que vous avez envoyé par e-mail, consultez [Suivre et révoquer vos documents](sharing-app-track-revoke.md).


## <a name="examples-and-other-instructions"></a>Exemples et autres instructions
Pour obtenir des exemples et des instructions concernant l’utilisation de l’application de partage Rights Management, voir les sections suivantes dans le Guide d’utilisation de l’application de partage Rights Management :

-   [Exemples d’utilisation de l’application de partage RMS](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [Que voulez-vous faire ?](sharing-app-user-guide.md#what-do-you-want-to-do)

## <a name="see-also"></a>Voir aussi
[Guide d’utilisation de l’application de partage Rights Management](sharing-app-user-guide.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO4-->


