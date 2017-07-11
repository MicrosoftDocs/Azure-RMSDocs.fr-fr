---
title: "Configurer les étiquettes pour des langues différentes dans Azure Information Protection"
description: "Vous pouvez ajouter la prise en charge de langues différentes pour les étiquettes que les utilisateurs voient dans la barre Information Protection, en spécifiant les langues dans la stratégie Azure Information Protection et en important vos traductions."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/05/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a0e89fd0-795b-4e7a-aea9-ff6fc9163bde
ms.openlocfilehash: ec99bf36e8904a7304a9d33c32d17ba92e2e22d2
ms.sourcegitcommit: 8b768e7e249e124f24acdf630d165eaf743f9c21
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/05/2017
---
<a id="how-to-configure-labels-for-different-languages-in-azure-information-protection" class="xliff"></a>

# Guide de configuration des étiquettes pour des langues différentes dans Azure Information Protection

>*S’applique à : Azure Information Protection*

>[!NOTE]
>Cette fonctionnalité en version préliminaire et peut uniquement être utilisée conjointement avec la **préversion** du client Azure Information Protection que vous pouvez télécharger à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

Par défaut, les noms et descriptions des étiquettes prennent en charge une seule langue affichée pour tous les utilisateurs de votre organisation. Vous pouvez ajouter la prise en charge d’autres langues en sélectionnant celles dont vous avez besoin, exporter les noms d’étiquette actuels et leurs descriptions dans un fichier, modifier le fichier pour fournir vos traductions et réimporter le fichier dans votre stratégie Azure Information Protection.

Sélectionnez les langues qui correspondent à la langue de vos utilisateurs pour Office et Windows. Ces noms d’étiquette et descriptions s’affichent alors dans la barre d’Azure Information Protection dans les applications Office et la boîte de dialogue **Classification et protection - Azure Information Protection**, respectivement. Pour plus d’informations sur la langue choisie, consultez la section [Comment le client Azure Information Protection détermine la langue à afficher](#how-the-azure-information-protection-client-determines-the-language-to- display) de cette page. 

<a id="to-configure-labels-to-display-in-different-languages" class="xliff"></a>

## Pour configurer les étiquettes pour un affichage multilingue

1. Si vous ne l’avez pas déjà fait, dans une nouvelle fenêtre de navigateur, connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur de la sécurité ou administrateur général, puis accédez au panneau **Azure Information Protection**. 
    
    Par exemple, dans le menu du hub, cliquez sur **Autres services** et commencez à taper **Information** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. Dans le premier panneau **Azure Information Protection**, recherchez **GÉRER**, puis sélectionnez **Langues (version préliminaire)**.

3. Dans le panneau **Azure Information Protection - Langues (version préliminaire)**, recherchez la première langue que vous souhaitez ajouter en tapant son nom dans la zone de recherche, ou en faisant défiler la liste des langues disponibles. 

4. Sélectionnez votre langue, puis sélectionnez **OK**.

5. Dans le panneau suivant, vous verrez la langue sélectionnée ajoutée à une liste :
    
    - Pour ajouter une autre langue, sélectionnez **Ajouter une nouvelle langue pour traduction** et répétez les étapes 3 et 4. 
        
        > [!NOTE]
        > Veillez à sélectionner les langues de vos utilisateurs pour Office et Windows. Dans certains cas, cela peut nécessiter deux sélections différentes par ordinateur.
        
    - Si vous changez d’avis pour une langue que vous avez ajoutée, sélectionnez cette entrée dans la liste, puis cliquez sur **Supprimer**.

6. Lorsque toutes les langues que vous souhaitez prendre en charge sont répertoriées, sélectionnez la case à cocher à côté **NOM DE LA LANGUE** pour sélectionner toutes les entrées (ou vous pouvez également sélectionner des entrées individuelles), puis cliquez sur **Exporter** pour enregistrer une copie locale des noms d’étiquette et descriptions existants dans un fichier. 
    
    Le fichier téléchargé est nommé **exported localization.zip** et est enregistré dans le dossier Téléchargements. Il est également accessible en sélectionnant ce nom de fichier dans la barre d’état du portail Azure.

7. Extrayez les fichiers de **exported localization.zip** afin de disposer des fichiers .xml pour chaque langue que vous avez sélectionnée pour le téléchargement. 

8. Modifier chaque fichier .xml : pour chaque chaîne dans les balises `<LocalizedText>`, fournissez les traductions que vous souhaitez pour chaque langue choisie. 

9. Lorsque vous avez modifié chaque fichier .xml, créez un nouveau dossier compressé qui contient ces fichiers. Le dossier compressé peut avoir n’importe quel nom, mais il doit avoir une extension .zip.

10. Revenez au panneau du portail Azure et sélectionnez **Importer**. Si cette option n’est pas disponible, désactivez d’abord la case à cocher **NOM DE LA LANGUE** ou les cases à cocher pour les langues sélectionnées individuellement.
    
    Une fois l’importation terminée, les noms d’étiquettes et descriptions localisés sont téléchargés pour les utilisateurs la prochaine fois que vous publiez la stratégie Azure Information Protection. Vous pouvez cliquer sur **Publier** à partir du panneau **Stratégie globale** ou **Stratégies délimitées**.

<a id="how-the-azure-information-protection-client-determines-the-language-to-display" class="xliff"></a>

## Comment le client Azure Information Protection détermine la langue à afficher

Lorsque les utilisateurs téléchargent une stratégie Azure Information Protection qui prend en charge différentes langues, la langue que les utilisateurs voient pour leurs noms d’étiquette et les info-bulles est déterminée par la logique suivante :

**Pour les étiquettes et les info-bulles que les utilisateurs voient dans la barre Azure Information Protection dans les applications Office :**

- Lorsqu’il existe une correspondance directe avec la langue de leur application Office, les descriptions et les noms d’étiquette s’affichent dans cette langue.

- Lorsqu’il n’existe aucune correspondance directe avec la langue de leur application Office, les descriptions et les noms d’étiquette s’affichent dans la langue spécifiée par défaut pour tous les utilisateurs. Cette langue est généralement l’anglais, qui est la langue utilisée dans la stratégie par défaut.

**Pour les étiquettes et info-bulles que les utilisateurs voient lors qu’ils cliquent avec le bouton droit pour classifier et protéger les fichiers ou dossiers :**

- Lorsqu’il existe une correspondance directe avec la langue de leur système d’exploitation, les descriptions et les noms d’étiquette s’affichent dans cette langue.

- Lorsqu’il n’existe aucune correspondance directe avec la langue de leur système d’exploitation, les descriptions et les noms d’étiquette s’affichent dans la langue spécifiée par défaut pour tous les utilisateurs. Cette langue est généralement l’anglais, qui est la langue utilisée dans la stratégie par défaut.

<a id="when-localized-label-names-are-not-used" class="xliff"></a>

## Si les noms d’étiquettes localisés ne sont pas utilisés

Dans les scénarios suivants, les noms localisés des étiquettes (et sous-étiquettes) ne sont pas utilisés. Par souci de cohérence à travers votre client, la langue par défaut est toujours utilisée pour les éléments suivants :

- Journaux d’utilisation du client

- PowerShell (sortie de Get-AIPFileStatus)

- En-têtes de messagerie et métadonnées de document


<a id="next-steps" class="xliff"></a>

## Étapes suivantes

Pour plus d’informations sur la configuration des options disponibles pour une étiquette et d’autres paramètres de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


