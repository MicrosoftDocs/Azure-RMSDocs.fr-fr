---
title: Configurer les étiquettes pour des langues différentes dans Azure Information Protection
description: Vous pouvez ajouter la prise en charge de différentes langues pour les étiquettes que les utilisateurs voient dans la barre Information Protection et pour tous les modèles visibles par l’utilisateur, en spécifiant les langues dans la stratégie Azure Information Protection et en important vos traductions.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: a0e89fd0-795b-4e7a-aea9-ff6fc9163bde
ms.openlocfilehash: c89085c7f001cd26ccd0b722196d9678b674163e
ms.sourcegitcommit: f9077101a974459a4252e763b5fafe51ff15a16f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64767948"
---
# <a name="how-to-configure-labels-and-templates-for-different-languages-in-azure-information-protection"></a>Guide pratique pour configurer des étiquettes et des modèles dans différentes langues dans Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Instructions pour : [Client Azure Information Protection pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Bien que les étiquettes par défaut pour Azure Information Protection prennent en charge plusieurs langues, vous devez configurer la prise en charge pour les noms et les descriptions d’étiquette que vous spécifiez. Cette configuration nécessite les actions suivantes :

1. Sélectionnez les langues utilisées par vos utilisateurs. 

2. Exportez vos noms et descriptions d’étiquette actuels dans un fichier.

3. Modifiez le fichier pour fournir vos traductions.

4. Réimportez le fichier dans votre stratégie Azure Information Protection.

Vous pouvez aussi configurer des modèles dans différentes langues quand l’une des conditions suivantes s’applique. Cette configuration est appropriée si les utilisateurs ou les administrateurs doivent voir le nom et la description du modèle actuel dans leur langue localisée.

- Le modèle a été créé dans le portail Azure Classic ou à l’aide de PowerShell, et le modèle n’est pas associé à une étiquette à l’aide du paramètre de protection **Sélectionner un modèle prédéfini**.

- Vous n’avez pas d’abonnement qui prend en charge les étiquettes, vous pouvez uniquement créer et gérer des modèles dans le portail Azure.

Sélectionnez les langues qui correspondent à la langue de vos utilisateurs pour Office et Windows. Ces noms et descriptions d’étiquettes s’affichent alors respectivement dans la barre Azure Information Protection des applications Office et dans la boîte de dialogue **Classer et protéger – Azure Information Protection**. Pour plus d’informations sur la langue choisie, consultez la section [Comment le client Azure Information Protection détermine la langue à afficher](#how-the-azure-information-protection-client-determines-the-language-to- display) de cette page. 

## <a name="to-configure-labels-and-templates-for-different-languages"></a>Pour configurer des étiquettes et des modèles dans différentes langues

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au panneau **Azure Information Protection**.
    
    Par exemple, dans le menu hub, cliquez sur **Tous les services** et tapez **Informations** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. À partir de l’option de menu **Gérer** > **Langues** : Dans le panneau **Azure Information Protection - Langues**, sélectionnez **Ajouter une langue pour la traduction**. Sélectionnez les langues à ajouter, puis sélectionnez **OK**. Vous pouvez taper le nom de la langue dans la zone de recherche ou faire défiler la liste des langues disponibles

3. Les langues sélectionnées s’affichent désormais dans le panneau **Azure Information Protection - Langues** :
    
    - Pour ajouter une autre langue, sélectionnez **Ajouter une langue pour la traduction** et répétez l’étape précédente. 
        
        > [!NOTE]
        > Veillez à sélectionner les langues de vos utilisateurs pour Office et Windows. Dans certains cas, cela peut nécessiter deux sélections différentes par ordinateur.
        
    - Si vous changez d’avis pour une langue que vous avez ajoutée, sélectionnez cette entrée dans la liste, puis cliquez sur **Supprimer**.

4. Lorsque toutes les langues que vous souhaitez prendre en charge sont répertoriées, sélectionnez la case à cocher à côté **NOM DE LA LANGUE** pour sélectionner toutes les entrées (ou vous pouvez également sélectionner des entrées individuelles), puis cliquez sur **Exporter** pour enregistrer une copie locale des noms d’étiquette et descriptions existants dans un fichier. 
    
    Le fichier téléchargé est nommé **exported localization.zip** et est enregistré dans le dossier Téléchargements. Il est également accessible en sélectionnant ce nom de fichier dans la barre d’état du portail Azure.

5. Extrayez les fichiers de **exported localization.zip** afin de disposer des fichiers .xml de chacune des langues que vous avez sélectionnées pour le téléchargement. 

6. Modifiez chaque fichier .xml : pour chaque chaîne dans les balises `<LocalizedText>`, fournissez les traductions souhaitées pour chaque langue choisie. 

7. Lorsque vous avez modifié chaque fichier .xml, créez un nouveau dossier compressé qui contient ces fichiers. Le dossier compressé peut avoir n’importe quel nom, mais il doit avoir une extension .zip.
    
    Conseil : il n’est pas nécessaire d’attendre d’avoir modifié chacun des fichiers de langue téléchargés. Vous pouvez déployer les différentes langues en plusieurs phases, en incluant dans le fichier .zip un sous-ensemble des fichiers téléchargés. Ensuite, répétez les étapes 7 et 8 après avoir effectué les traductions dans d’autres langues.

8. Revenez au panneau **Azure Information Protection - Langues**, puis sélectionnez **Importer**. Si cette option n’est pas disponible, désactivez d’abord la case à cocher **NOM DE LA LANGUE** ou les cases à cocher pour les langues sélectionnées individuellement.
    
    Une fois l’importation terminée, les noms et descriptions localisés sont téléchargés pour les utilisateurs.

Vous devez répéter cette procédure pour prendre en charge une nouvelle langue, créer de nouvelles étiquettes ou modifier le nom ou la description des étiquettes sur le Portail Azure.

## <a name="how-the-azure-information-protection-client-determines-the-language-to-display"></a>Comment le client Azure Information Protection détermine la langue à afficher

Lorsque les utilisateurs téléchargent une stratégie Azure Information Protection qui prend en charge différentes langues, la langue que les utilisateurs voient pour leurs noms d’étiquette et les info-bulles est déterminée par la logique suivante :

**Pour les étiquettes et les info-bulles que les utilisateurs voient dans la barre Azure Information Protection dans les applications Office :**

- Lorsqu’il existe une correspondance directe avec la langue de leur application Office, les descriptions et les noms d’étiquette s’affichent dans cette langue.

- Lorsqu’il n’existe aucune correspondance directe avec la langue de leur application Office, les descriptions et les noms d’étiquette s’affichent dans la langue spécifiée par défaut pour tous les utilisateurs. Cette langue est généralement l’anglais, qui est la langue utilisée dans la stratégie par défaut.

**Pour les étiquettes et info-bulles que les utilisateurs voient lors qu’ils cliquent avec le bouton droit pour classifier et protéger les fichiers ou dossiers :**

- Lorsqu’il existe une correspondance directe avec la langue de leur système d’exploitation, les descriptions et les noms d’étiquette s’affichent dans cette langue.

- Lorsqu’il n’existe aucune correspondance directe avec la langue de leur système d’exploitation, les descriptions et les noms d’étiquette s’affichent dans la langue spécifiée par défaut pour tous les utilisateurs. Cette langue est généralement l’anglais, qui est la langue utilisée dans la stratégie par défaut.

## <a name="when-localized-label-names-are-not-used"></a>Si les noms d’étiquettes localisés ne sont pas utilisés

Dans les scénarios suivants, les noms localisés des étiquettes (et sous-étiquettes) ne sont pas utilisés. Par souci de cohérence à travers votre client, la langue par défaut est toujours utilisée pour les éléments suivants :

- Journaux d’utilisation du client

- PowerShell (sortie de Get-AIPFileStatus)

- En-têtes de messagerie et métadonnées de document


## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration des options disponibles pour une étiquette et d’autres paramètres de vos stratégies Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).



