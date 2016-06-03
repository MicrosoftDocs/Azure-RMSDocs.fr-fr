---
# required metadata

title: Informations de référence sur les restrictions d’utilisation | Azure RMS
description: Les restrictions d’utilisation sont définies par les constantes répertoriées dans cette rubrique.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 16E36039-0FD6-4A0A-82C8-2C9DB19D27DD
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Informations de référence sur les restrictions d’utilisation

Les restrictions d’utilisation sont définies par les constantes répertoriées dans cette rubrique.



Pour chaque droit utilisateur répertorié dans la colonne Droit AD RMS, vous trouverez une description, un point de mise en œuvre, ainsi que des suggestions de mise en œuvre.

| Droit AD RMS | Description | Points de mise en œuvre courants | Procédure de mise en œuvre |
|--------------|-------------|---------------------------|----------------|
|IPC_GENERIC_ALL |Accorde tous les droits à l’utilisateur.| Aucun |Utilisé par le système, ce droit ne nécessite généralement pas de vérification directe. <br><br> [**IpcAccessCheck**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcaccesscheck) utilise ce droit pour déterminer s’il faut accorder à l’utilisateur d’autres droits, comme dans cet exemple.<br><br> `/* fAccessGranted is set to TRUE if either the IPC_GENERIC_WRITE or the IPC_GENERIC_ALL right is granted */` <br><br> `IpcAccessCheck(hKey, IPC_GENERIC_WRITE, &fAccessGranted);`
|IPC_GENERIC_READ |Droit de lire le contenu de documents.|Chargement de documents|Veuillez ne pas charger ni présenter le contenu de documents.|
|IPC_GENERIC_WRITE|Droit de modifier le contenu de documents.|Modification de documents|Configurez comme non modifiables tous les contrôles d’interface utilisateur pouvant servir à modifier le contenu de documents. <br><br> Désactivez tous les éléments de menu qui déclenchent des modifications de document. Par exemple : **Edition** > **Couper**, **Edition** > **Coller** et **Insérer**. <br><br>Désactivez tous les éléments de menu contextuel qui déclenchent des modifications de document.|
|Aucun droit AD RMS|L’appelant ne bénéficie d’aucun droit AD RMS.|Enregistrer|Désactivez le menu **Fichier** > **Enregistrer**. <br><br> **Remarque** Ce droit ne contrôle pas **Fichier** > **Enregistrer sous**, car il ne représente pas une modification du document d’origine.<br><br> Désactivez tout raccourci clavier pouvant servir à déclencher un enregistrement (par exemple, Ctrl+S).<br><br> **Conseil** Nous vous recommandons de mettre à jour le code de base associé à l’opération **Fichier** > **Enregistrer** pour qu’il échoue si l’utilisateur ne dispose pas de ce droit. Vous bénéficiez ainsi d’un filet de sécurité si vous omettez de désactiver de l’expérience utilisateur des mécanismes pouvant servir à déclencher un enregistrement.
|IPC_GENERIC_EXTRACT|Droit d’extraire le contenu d’un format protégé et de le placer dans un format non protégé.|Copier dans le Presse-papiers|Désactivez le menu **Edition** > **Copier**. Désactivez le menu **Edition** > **Couper**. <br><br>Désactivez **Copier** et **Couper** des menus contextuels.<br><br>Désactivez tout raccourci clavier pouvant servir à déclencher une copie (par exemple, Ctrl+C ou Ctrl+X).<br><br>Mettez à jour les gestionnaires de messages de fenêtre pour [**WM_CUT**](https://msdn.microsoft.com/library/windows/desktop/ms649023) pour qu’ils rejettent la copie de données si l’utilisateur ne dispose pas de ce droit. Si la fenêtre utilise le gestionnaire de messages fourni par Windows par défaut, créez une sous-classe de cette fenêtre et fournissez vos propres gestionnaires pour **WM_COPY** et **WM_CUT**.
|Aucun droit AD RMS|L’appelant ne bénéficie d’aucun droit AD RMS.|Enregistrer sous...|Dans votre boîte de dialogue **Enregistrer sous**, désactivez tous les formats de fichiers pouvant entraîner l’enregistrement de documents sans protection RMS.|
|Aucun droit AD RMS|L’appelant ne bénéficie d’aucun droit AD RMS.|Alt+Imp. écr.|Appelez [**IpcProtectWindow**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcprotectwindow) sur toutes les fenêtres qui affichent le contenu de documents.|
|IPC_GENERIC_EXPORT|Droit d’extraire le contenu d’un format protégé et de le placer dans un autre format protégé par AD RMS.|Enregistrer sous|Dans votre boîte de dialogue **Enregistrer sous**, désactivez la possibilité d’enregistrer dans d’autres formats de fichiers.<br><br>**Conseil**Nous vous recommandons de mettre à jour le code de base associé à l’opération **Fichier** > **Enregistrer** pour qu’il échoue si l’utilisateur tente d’enregistrer ce fichier dans un format différent et qu’il ne dispose pas de ce droit. Vous bénéficiez ainsi d’un filet de sécurité si vous omettez de désactiver de l’expérience utilisateur des mécanismes pouvant servir à déclencher une opération Enregistrer sous.|
|IPC_GENERIC_PRINT|Droit d’imprimer le contenu de documents.|Imprimer|Désactivez le menu **Fichier** > **Imprimer**.<br><br>Désactivez tout raccourci clavier pouvant servir à déclencher une impression (par exemple, Ctrl+P).<br><br>Désactivez les éléments de menu contextuel pouvant servir à déclencher une impression.<br><br>**Conseil** Nous vous recommandons de mettre à jour le code de base associé à l’opération **Fichier** > **Imprimer** pour qu’il échoue si l’utilisateur ne dispose pas de ce droit. Vous bénéficiez ainsi d’un filet de sécurité si vous omettez de désactiver de l’expérience utilisateur des mécanismes pouvant servir à déclencher une impression.|
|IPC_GENERIC_COMMENT|Certaines applications prennent en charge l’ajout de commentaires et d’annotations dans le document sans mettre à jour le contenu du document principal.<br><br>Ce droit permet à l’utilisateur d’accéder à cette fonctionnalité.|Révision > Insérer un commentaire <br><br> Révision > Supprimer le commentaire | Désactivez tous les éléments de menu pouvant servir à modifier les commentaires ou annotations d’un document. Par exemple : **Révision** > **Insérer un commentaire** et **Révision** > **Supprimer le commentaire**. <br><br>Désactivez tout raccourci clavier pouvant déclencher la modification de commentaires associés à un document.<br><br>**Remarque** Une implémentation par défaut nécessite **IPC_GENERIC_COMMENT** et **IPC_GENERIC_WRITE** pour conserver les nouveaux commentaires dans un fichier. Les applications peuvent prendre en charge ou non le scénario dans lequel le droit **IPC_GENERIC_COMMENT** est accordé, mais pas le droit **IPC_GENERIC_WRITE**. Dans ce cas, il est permis d’autoriser l’enregistrement, tant que les modifications de documents sont limitées aux commentaires.|
|IPC_VIEW_RIGHTS||N/A|Appliqué par le système. Le système n’autorise pas le développeur à interroger la [**liste des droits utilisateur**](/rights-management/sdk/2.1/api/win/structures#msipc_ipc_user_rights_list) à partir d’une licence, sauf si ce droit est accordé.
|IPC_EDIT_RIGHTS|Certaines applications autorisent les utilisateurs à modifier l’ensemble des utilisateurs et des droits pour le contenu protégé AD RMS.<br><br>Ce droit permet à l’utilisateur d’accéder à cette fonctionnalité.|Contrôle d’interface utilisateur de modification des droits de l’application|Désactivez l’accès utilisateur à tout élément d’interface utilisateur pouvant servir à modifier la stratégie RMS pour un document.|

 

 

 


<!--HONumber=May16_HO2-->


