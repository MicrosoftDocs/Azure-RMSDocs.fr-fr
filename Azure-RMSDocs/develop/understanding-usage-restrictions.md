---
title: Présentation des restrictions d’utilisation | Azure RMS
description: Toutes les applications prenant en charge RMS doivent appliquer des restrictions d’utilisation.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: E388B16C-ECDA-4696-A040-D457D3C96766
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 2001f779a788e41acbb9319a0c329dfb4705176a
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "60176871"
---
# <a name="understanding-usage-restrictions"></a>Comprendre les restrictions d’utilisation

Toutes les applications prenant en charge RMS doivent appliquer des restrictions d’utilisation. Une restriction d’utilisation est une condition qui se produit quand un utilisateur tente d’effectuer une action (par exemple, imprimer d’un document), alors que la stratégie RMS pour ce document ne lui accorde pas l’autorisation ou le droit nécessaire pour mener à bien cette action (par exemple, le droit PRINT).

Il est possible d’interroger les autorisations dont dispose un utilisateur sur un document à l’aide de la fonction [IpcAccessCheck](https://msdn.microsoft.com/library/hh535253.aspx).

## <a name="designing-with-usage-restrictions"></a>Conception avec des restrictions d’utilisation

-   Se familiariser avec les droits RMS standard

    Pour connaître l’ensemble des droits RMS que peut appliquer votre application, consultez [Informations de référence sur les restrictions d’utilisation](#usage-restriction-reference).

    Notez que vous pouvez créer des droits définis par l’application qui sont propres à votre situation et qui vont au-delà des droits RMS standards.

-   Identifier les points de mise en œuvre de restriction d’utilisation

    Un *point de mise en œuvre de restriction d’utilisation* est un emplacement dans le flux de contrôle de votre application où vous devez mettre en œuvre une restriction d’utilisation. La rubrique [Informations de référence sur les restrictions d’utilisation](#usage-restriction-reference) fournit plusieurs exemples de points de mise en œuvre courants.

    Évaluez votre propre application pour déterminer les points de mise en œuvre de restriction d’utilisation qui s’appliquent.

    Votre application n’a peut-être pas besoin de tous les points de mise en œuvre décrits dans [Informations de référence sur les restrictions d’utilisation](#usage-restriction-reference). Par exemple, si votre application n’autorise pas les utilisateurs à imprimer du contenu, il est inutile de vérifier le droit **IPC\_GENERIC\_PRINT**.

-   Mettre à jour le code pour effectuer une vérification d’accès à chaque point de mise en œuvre

    Pour obtenir des conseils sur la mise en œuvre de droits spécifiques, consultez [Informations de référence sur les restrictions d’utilisation](#usage-restriction-reference).

## <a name="usage-restriction-reference"></a>Informations de référence sur les restrictions d’utilisation

Les restrictions d’utilisation sont définies par les constantes suivantes.

Pour chaque droit utilisateur répertorié dans la colonne Droit AD RMS, vous trouverez une description, un point de mise en œuvre, ainsi que des suggestions de mise en œuvre.

| Droit AD RMS/Description | Procédure de mise en œuvre |
|--------------------------|----------------|
|**IPC_GENERIC_ALL** <br><br> Accorde tous les droits à l’utilisateur. <br><br> **Points de mise en œuvre courants** : Aucune |Utilisé par le système, ce droit ne nécessite généralement pas de vérification directe. <br><br> [IpcAccessCheck](https://msdn.microsoft.com/library/hh535253.aspx) utilise ce droit pour déterminer s’il faut accorder à l’utilisateur d’autres droits, comme dans cet exemple.<br><br> `/* fAccessGranted is set to TRUE if either the IPC_GENERIC_WRITE or the IPC_GENERIC_ALL right is granted */` <br><br> `IpcAccessCheck(hKey, IPC_GENERIC_WRITE, &fAccessGranted);`|
|**IPC_GENERIC_READ** <br><br> Droit de lire le contenu de documents. <br><br> **Points de mise en œuvre courants** : Chargement de documents|Veuillez ne pas charger ni présenter le contenu de documents.|
|**IPC_GENERIC_WRITE** <br><br> Droit de modifier le contenu de documents. <br><br> **Points de mise en œuvre courants** : Modification de documents|Configurez comme non modifiables tous les contrôles d’interface utilisateur pouvant servir à modifier le contenu de documents. <br><br> Désactivez tous les éléments de menu qui déclenchent des modifications de document. Par exemple : **Edition** > **Couper**, **Edition** > **Coller** et **Insérer**. <br><br>Désactivez tous les éléments de menu contextuel qui déclenchent des modifications de document.|
|Aucun droit AD RMS <br><br> Aucune description <br><br> **Points de mise en œuvre courants** : Enregistrer | Désactivez le menu **Fichier** > **Enregistrer**. <br><br> **Remarque** Ce droit ne contrôle pas **Fichier** > **Enregistrer sous**, car il ne représente pas une modification du document d’origine.<br><br> Désactivez tout raccourci clavier pouvant servir à déclencher un enregistrement (par exemple, Ctrl+S).<br><br> **Conseil** Nous vous recommandons de mettre à jour le code de base associé à l’opération **Fichier** > **Enregistrer** pour qu’il échoue si l’utilisateur ne dispose pas de ce droit. Vous bénéficiez ainsi d’un filet de sécurité si vous omettez de désactiver de l’expérience utilisateur des mécanismes pouvant servir à déclencher un enregistrement. |
|**IPC_GENERIC_EXTRACT** <br><br> Droit d’extraire le contenu d’un format protégé et de le placer dans un format non protégé. <br><br> **Points de mise en œuvre courants** : Copier dans le Presse-papiers | Désactivez le menu **Edition** > **Copier**. Désactivez le menu **Edition** > **Couper**. <br><br>Désactivez **Copier** et **Couper** des menus contextuels.<br><br>Désactivez tout raccourci clavier pouvant servir à déclencher une copie (par exemple, Ctrl+C ou Ctrl+X).<br><br>Mettez à jour les gestionnaires de messages de fenêtre pour [**WM_CUT**](https://msdn.microsoft.com/library/ms649023) pour qu’ils rejettent la copie de données si l’utilisateur ne dispose pas de ce droit. Si la fenêtre utilise le gestionnaire de messages fourni par Windows par défaut, créez une sous-classe de cette fenêtre et fournissez vos propres gestionnaires pour **WM_COPY** et **WM_CUT**. |
|Aucun droit AD RMS <br><br> Aucune description <br><br> **Points de mise en œuvre courants** : Enregistrer sous |Dans votre boîte de dialogue **Enregistrer sous**, désactivez tous les formats de fichiers pouvant entraîner l’enregistrement de documents sans protection RMS.|
|Aucun droit AD RMS <br><br> Aucune description <br><br> **Points de mise en œuvre courants** : Alt+Imp. écr.|Appelez [IpcProtectWindow](https://msdn.microsoft.com/library/hh535268.aspx) sur toutes les fenêtres qui affichent le contenu de documents.|
|**IPC_GENERIC_EXPORT** <br><br> Droit d’extraire le contenu d’un format protégé et de le placer dans un autre format protégé par AD RMS. <br><br> **Points de mise en œuvre courants** : Enregistrer sous|Dans votre boîte de dialogue **Enregistrer sous**, désactivez la possibilité d’enregistrer dans d’autres formats de fichiers.<br><br>**Conseil**Nous vous recommandons de mettre à jour le code de base associé à l’opération **Fichier** > **Enregistrer** pour qu’il échoue si l’utilisateur tente d’enregistrer ce fichier dans un format différent et qu’il ne dispose pas de ce droit. Vous bénéficiez ainsi d’un filet de sécurité si vous omettez de désactiver de l’expérience utilisateur des mécanismes pouvant servir à déclencher une opération Enregistrer sous.|
|**IPC_GENERIC_PRINT** <br><br> Droit d’imprimer le contenu de documents. <br><br> **Points de mise en œuvre courants** : Print|Désactivez le menu **Fichier** > **Imprimer**.<br><br>Désactivez tout raccourci clavier pouvant servir à déclencher une impression (par exemple, Ctrl+P).<br><br>Désactivez les éléments de menu contextuel pouvant servir à déclencher une impression.<br><br>**Conseil** Nous vous recommandons de mettre à jour le code de base associé à l’opération **Fichier** > **Imprimer** pour qu’il échoue si l’utilisateur ne dispose pas de ce droit. Vous bénéficiez ainsi d’un filet de sécurité si vous omettez de désactiver de l’expérience utilisateur des mécanismes pouvant servir à déclencher une impression.|
|**IPC_GENERIC_COMMENT** <br><br> Certaines applications prennent en charge l’ajout de commentaires et d’annotations dans le document sans mettre à jour le contenu du document principal.<br><br>Ce droit permet à l’utilisateur d’accéder à cette fonctionnalité. <br><br> **Points de mise en œuvre courants** : <br><br> Révision > Insérer un commentaire <br><br> Révision > Supprimer le commentaire | Désactivez tous les éléments de menu pouvant servir à modifier les commentaires ou annotations d’un document. Par exemple : **Révision** > **Insérer un commentaire** et **Révision** > **Supprimer le commentaire**. <br><br>Désactivez tout raccourci clavier pouvant déclencher la modification de commentaires associés à un document.<br><br>**Remarque** Une implémentation par défaut nécessite **IPC_GENERIC_COMMENT** et **IPC_GENERIC_WRITE** pour conserver les nouveaux commentaires dans un fichier. Les applications peuvent prendre en charge ou non le scénario dans lequel le droit **IPC_GENERIC_COMMENT** est accordé, mais pas le droit **IPC_GENERIC_WRITE**. Dans ce cas, il est permis d’autoriser l’enregistrement, tant que les modifications de documents sont limitées aux commentaires.|
|**IPC_VIEW_RIGHTS** <br><br> Aucune description <br><br> **Points de mise en œuvre courants** : N/A|Appliqué par le système. Le système n’autorise pas le développeur à interroger la [**liste des droits utilisateur**](https://msdn.microsoft.com/library/hh535286.aspx) à partir d’une licence, sauf si ce droit est accordé.
|**IPC_EDIT_RIGHTS** <br><br> Certaines applications autorisent les utilisateurs à modifier l’ensemble des utilisateurs et des droits pour le contenu protégé AD RMS.<br><br>Ce droit permet à l’utilisateur d’accéder à cette fonctionnalité. <br><br> **Points de mise en œuvre courants** : Contrôle d’interface utilisateur de modification des droits de l’application|Désactivez l’accès utilisateur à tout élément d’interface utilisateur pouvant servir à modifier la stratégie RMS pour un document.|


## <a name="related-topics"></a>Rubriques connexes

* [IpcAccessCheck](https://msdn.microsoft.com/library/hh535253.aspx)
