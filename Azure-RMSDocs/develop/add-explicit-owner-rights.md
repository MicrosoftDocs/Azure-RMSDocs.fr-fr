---
title: "Procédure d’ajout des droits de propriétaire explicites | Azure RMS"
description: Your application should explicitly add "Owner" rights when creating a license from scratch.
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: EF43FAC4-ABB4-459D-B173-972B5716F816
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8be965d76578c28457eee207b56e5da83f7eb468
ms.openlocfilehash: 36c0bece4fb99e4d92fcda0c57da1b3cee11e37a


---

# Comment : ajouter des droits de propriétaire explicites

Votre application doit ajouter explicitement les droits « Owner » lors de la création d’une licence à partir de rien (à l’aide de [IpcCreateLicenseFromScratch](https://msdn.microsoft.com/library/hh535256.aspx)).

## Conditions préalables

Quand votre application crée un handle de licence en utilisant [IpcCreateLicenseFromScratch](https://msdn.microsoft.com/library/hh535256.aspx), elle doit également accorder explicitement les droits (autorisations) complets de propriétaire.

>[!NOTE] 
> La définition d’un utilisateur comme « Owner » en utilisant [IpcSetLicenseProperty](https://msdn.microsoft.com/library/hh535271.aspx) avec la propriété **IPC\_LI\_OWNER** n’accorde pas toutes les autorisations de propriétaire.

L’exemple de code suivant représente uniquement les étapes de création et d’ajout des droits spécifiques à une licence donnée.

## Instructions
 
## Étape 1 : Exemple de scénario

Dans cet exemple, les droits nécessaires sont ajoutés à une licence créée avec [IpcCreateLicenseFromScratch](https://msdn.microsoft.com/library/hh535256.aspx). L’exemple montre la création et l’attribution des droits à la licence via une liste de droits.

Les deux droits suivants sont ajoutés à ces utilisateurs :

-   Autorisations *Read* attribuées à joe@contoso.com
-   Autorisations *Full* attribuées à mary\_kay@contoso.com

        // Create User Rights structure
        IPC_USER_RIGHTS ownerRightForOwner = {0};

        // Create rights
        LPCWSTR rgwszOwnerRights[1] = {IPC_GENERIC_ALL};

        // Assign values to members of Rights structure
        ownerRightForOwner.User.dwType = IPC_USER_TYPE_IPC;
        ownerRightForOwner.User.wszID = IPC_USER_ID_OWNER;
        ownerRightForOwner.rgwszRights = rgwszOwnerRights;
        ownerRightForOwner.cRights = 1;

        // Create User Rights structure for Joe with Read permissions
        IPC_USER_RIGHTS joeReadRight = {0};
        LPCWSTR rgwszReadRights[1] = {IPC_GENERIC_READ};

        // Assign values to members of Rights structure for Joe
        joeReadRight.User.dwType = IPC_USER_TYPE_EMAIL;
        joeReadRight.User.wszID = "joe@contoso.com";
        joeReadRight.rgwszRights = rgwszReadRights;
        joeReadRight.cRights = 1;

        // Create User Rights structure for Mary Kay with Full permissions
        IPC_USER_RIGHTS mary_kayFullRight = {0};
        LPCWSTR rgwszFullRights[1] = {IPC_GENERIC_ALL};

        // Assign values to members of Rights structure for Mary Kay
        mary_kayFullRight.User.dwType = IPC_USER_TYPE_EMAIL;
        mary_kayFullRight.User.wszID = L"mary_kay@contoso.com";
        mary_kayFullRight.rgwszRights = rgwszFullRights;
        mary_kayFullRight.cRights = 1;

        // Create User Rights List and assign the above rights
        size_t uNoOfUserRights = 3;
        PIPC_USER_RIGHTS_LIST pUserRightsList = NULL;
        pUserRightsList = reinterpret_cast<PIPC_USER_RIGHTS_LIST>
        (new BYTE[ sizeof(IPC_USER_RIGHTS_LIST) + uNoOfUserRights * sizeof(IPC_USER_RIGHTS)]);

        if(pUserRightsList == NULL)
        {
          // Handle error
        }

        // Assign values to members of Rights List structure for Joe and Mary Kay
        (*pUserRightsList).cbSize = sizeof(IPC_USER_RIGHTS_LIST);
        (*pUserRightsList).cUserRights = uNoOfUserRights;
        (*pUserRightsList).rgUserRights[0] = ownerRightForOwner;
        (*pUserRightsList).rgUserRights[1] = joeReadRight;
        (*pUserRightsList).rgUserRights[2] = mary_kayFullRight;

        // Set the Rights List property on the license via its handle
        // hLicense is a license handle created with IpcCreateLicenseFromScratch
        hr = IpcSetLicenseProperty(hLicense, FALSE, IPC_LI_USER_RIGHTS_LIST, pUserRightsList);

        if(FAILED(hr))
        {
          // Handle the error
        }



## Rubriques connexes

- [Notes pour le développeur](developer-notes.md)
- [IpcSetLicenseProperty](https://msdn.microsoft.com/library/hh535271.aspx)
- [IpcCreateLicenseFromScratch](https://msdn.microsoft.com/library/hh535256.aspx)
 

 



<!--HONumber=Oct16_HO3-->


