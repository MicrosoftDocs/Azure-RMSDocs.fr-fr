---
title: Configurer les étiquettes pour des langues différentes dans Azure Information Protection
description: Vous pouvez ajouter la prise en charge de différentes langues pour les étiquettes que les utilisateurs voient dans la barre Information Protection et pour tous les modèles visibles par l’utilisateur, en spécifiant les langues dans la stratégie Azure Information Protection et en important vos traductions.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 03/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: a0e89fd0-795b-4e7a-aea9-ff6fc9163bde
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: f39ba64ed2702f4f994d5626697fa5185e546f2b
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/19/2020
ms.locfileid: "95568164"
---
# <a name="how-to-configure-labels-and-templates-for-different-languages-in-azure-information-protection"></a>Guide pratique pour configurer des étiquettes et des modèles dans différentes langues dans Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Instructions pour : [Client Azure Information Protection pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Pour fournir une expérience client unifiée et rationalisée, **Azure Information Protection client (Classic)** et **Gestion des étiquettes** dans le Portail Azure sont **dépréciées** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

> [!NOTE]
> Ces instructions s’appliquent au client Azure Information Protection (classique) et pas au client d’étiquetage unifié Azure Information Protection. Vous ne connaissez pas trop la différence entre ces clients ? Consultez ce [FAQ](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients).
> 
> Si vous recherchez des informations pour configurer différentes langues pour les étiquettes de sensibilité, utilisez Office 365 Security & Compliance PowerShell et le paramètre *LocaleSettings* pour [Set-label](/powershell/module/exchange/policy-and-compliance/set-label).

Bien que les étiquettes par défaut pour Azure Information Protection prennent en charge plusieurs langues, vous devez configurer la prise en charge pour les noms et les descriptions d’étiquette que vous spécifiez. Cette configuration nécessite les actions suivantes :

1. Sélectionnez les langues utilisées par vos utilisateurs. 

2. Exportez vos noms et descriptions d’étiquette actuels dans un fichier.

3. Modifiez le fichier pour fournir vos traductions.

4. Réimportez le fichier dans votre stratégie Azure Information Protection.

Vous pouvez aussi configurer des modèles dans différentes langues quand l’une des conditions suivantes s’applique. Cette configuration est appropriée si les utilisateurs ou les administrateurs doivent voir le nom et la description du modèle actuel dans leur langue localisée.

- Le modèle a été créé dans le portail Azure Classic ou à l’aide de PowerShell, et le modèle n’est pas associé à une étiquette à l’aide du paramètre de protection **Sélectionner un modèle prédéfini**.

- Vous n’avez pas d’abonnement qui prend en charge les étiquettes, vous pouvez uniquement créer et gérer des modèles dans le portail Azure.

Sélectionnez les langues qui correspondent à la langue de vos utilisateurs pour Office et Windows. Ces noms et descriptions d’étiquettes s’affichent alors respectivement dans la barre Azure Information Protection des applications Office et dans la boîte de dialogue **Classer et protéger – Azure Information Protection**. Pour plus d’informations sur la langue choisie, consultez la section [Comment le client Azure Information Protection détermine la langue à afficher](#how-the-azure-information-protection-client-determines-the-language-to-display) de cette page. 

## <a name="to-configure-labels-and-templates-for-different-languages"></a>Pour configurer des étiquettes et des modèles dans différentes langues

1. Si ce n’est pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au Portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au volet **Azure Information Protection**.
    
    Par exemple, dans la zone de recherche de ressources, services et documents : Commencez à taper **Information** et sélectionnez **Azure Information Protection**.

2. À partir de l’option de menu **gérer** les  >  **langues** : dans le volet **Azure information protection-langues** , sélectionnez **Ajouter une nouvelle langue pour la traduction**. Sélectionnez les langues à ajouter, puis sélectionnez **OK**. Vous pouvez taper le nom de la langue dans la zone de recherche ou faire défiler la liste des langues disponibles

3. Les langues que vous avez sélectionnées s’affichent désormais dans le volet **Azure information protection-langues** :
    
    - Pour ajouter une autre langue, sélectionnez **Ajouter une langue pour la traduction** et répétez l’étape précédente. 
        
        > [!NOTE]
        > Veillez à sélectionner les langues de vos utilisateurs pour Office et Windows. Dans certains cas, cela peut nécessiter deux sélections différentes par ordinateur.
        
    - Si vous changez d’avis pour une langue que vous avez ajoutée, sélectionnez cette entrée dans la liste, puis cliquez sur **Supprimer**.

4. Lorsque toutes les langues que vous souhaitez prendre en charge sont répertoriées, sélectionnez la case à cocher à côté **NOM DE LA LANGUE** pour sélectionner toutes les entrées (ou vous pouvez également sélectionner des entrées individuelles), puis cliquez sur **Exporter** pour enregistrer une copie locale des noms d’étiquette et descriptions existants dans un fichier. 
    
    Le fichier téléchargé est nommé **exported localization.zip** et est enregistré dans le dossier Téléchargements. Il est également accessible en sélectionnant ce nom de fichier dans la barre d’état du portail Azure.

5. Extrayez les fichiers de **exported localization.zip** afin de disposer des fichiers .xml de chacune des langues que vous avez sélectionnées pour le téléchargement. 

6. Modifier chaque fichier .xml : pour chaque chaîne dans les balises `<LocalizedText>`, fournissez les traductions que vous souhaitez pour chaque langue choisie. 

7. Lorsque vous avez modifié chaque fichier .xml, créez un nouveau dossier compressé qui contient ces fichiers. Le dossier compressé peut avoir n’importe quel nom, mais il doit avoir une extension .zip.
    
    Conseil : vous n’avez pas besoin d’attendre que vous ayez modifié chaque fichier de langue que vous avez téléchargé. Vous pouvez déployer les différentes langues en plusieurs phases, en incluant dans le fichier .zip un sous-ensemble des fichiers téléchargés. Ensuite, répétez les étapes 7 et 8 après avoir effectué les traductions dans d’autres langues.

8. Revenez au volet **Azure information protection-langues** , puis sélectionnez **Importer**. Si cette option n’est pas disponible, désactivez d’abord la case à cocher **NOM DE LA LANGUE** ou les cases à cocher pour les langues sélectionnées individuellement.
    
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