---
title: Configurations personnalisées pour le client d’étiquetage unifiée Azure Information Protection
description: Informations sur la personnalisation du client d’étiquetage unifié d’Azure Information Protection pour Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: c565c025b6ae3001984141a691ed37a057203f38
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "60181087"
---
# <a name="admin-guide-custom-configurations-for-the-azure-information-protection-unified-labeling-client"></a>Guide de l’administrateur : Configurations personnalisées pour le client d’étiquetage unifiée Azure Information Protection

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*
>
> *Instructions pour : [Azure Information Protection unifiée étiquetage client pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Utilisez les informations suivantes pour les configurations avancées que vous devrez peut-être pour des scénarios spécifiques ou un sous-ensemble d’utilisateurs lorsque vous gérez le client d’étiquetage unifié Azure Information Protection.

Ces paramètres nécessitent une modification du Registre.  

## <a name="sign-in-as-a-different-user"></a>Se connecter avec l’identité d’un autre utilisateur

Dans un environnement de production, les utilisateurs n’aurait pas généralement obligé de vous connecter comme un autre utilisateur lorsqu’ils utilisent Azure Information Protection unifiée étiquetage client. Toutefois, en tant qu’administrateur, vous devrez peut-être vous connecter sous un autre nom d’utilisateur pendant une phase de test. 

Vous pouvez vérifier sous quel compte vous êtes actuellement connecté en utilisant la boîte de dialogue **Microsoft Azure Information Protection** : Ouvrez une application Office et sur le **accueil** onglet, sélectionnez le **sensibilité** bouton, puis sélectionnez **aide et commentaires**. Votre nom de votre compte s’affiche dans la section **État du client**.

Pensez à vérifier le nom de domaine du compte connecté. En effet, vous pouvez accidentellement vous connecter avec le bon nom de compte, mais avec le mauvais domaine. Un symptôme d’à l’aide de compte incorrect inclut ne parvient pas à télécharger les étiquettes, ou vous ne voyez ne pas les étiquettes ou le comportement que vous attendez.

Pour se connecter avec l’identité d’un autre utilisateur :

1. Accédez à **%localappdata%\Microsoft\MSIP** et supprimez le fichier **TokenCache**.

2. Redémarrez les applications Office ouvertes et connectez-vous avec votre autre compte d’utilisateur. Si vous ne voyez pas une invite de commandes dans votre application Office pour vous connecter au service Azure Information Protection, revenez à la **Microsoft Azure Information Protection** boîte de dialogue et sélectionnez **connectez-vous** à partir de la mise à jour **d’état du Client** section.

En outre :

- Si le client d’étiquetage unifié Azure Information Protection est toujours connecté avec l’ancien compte après avoir effectué ces étapes, supprimer tous les cookies à partir d’Internet Explorer et répétez les étapes 1 et 2.

- Si vous utilisez l’authentification unique, vous devrez vous déconnecter de Windows et vous reconnecter avec votre autre compte d’utilisateur après avoir supprimé le fichier de jeton. Client Azure Information Protection unifié étiquetage alors vous authentifier automatiquement à l’aide de votre actuellement connecté dans le compte d’utilisateur.

- Cette solution prend en charge la connexion sous un nom d’utilisateur différent à partir du même locataire. Elle ne prend en pas charge la connexion sous un nom d’utilisateur différent à partir d’un autre locataire. Pour tester Azure Information Protection avec plusieurs locataires, utilisez des ordinateurs différents.

- Vous pouvez utiliser la **réinitialiser les paramètres** option à partir de **aide et commentaires** pour vous déconnecter et supprimer les étiquettes actuellement téléchargés et les paramètres de stratégie à partir de la sécurité et Office 365 centre de conformité, le Microsoft 365 Security center, ou le centre de conformité de Microsoft 365.


## <a name="change-the-local-logging-level"></a>Modifier le niveau de journalisation local

Par défaut, Azure Information Protection unifiée étiquetage écritures client fichiers journaux du client pour le **%localappdata%\Microsoft\MSIP** dossier. Ces fichiers servent à la résolution des problèmes par le Support Microsoft.
 
Pour modifier le niveau de journalisation pour ces fichiers, recherchez le nom de valeur suivant dans le Registre et définir les données de valeur pour le niveau de journalisation requis :

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\LogLevel**

Définissez le niveau de journalisation sur l'une des valeurs suivantes :

- **Désactivé** : aucune journalisation locale.

- **Erreur** : erreurs uniquement.

- **Info** : journalisation minimale, qui n’inclut aucun ID d’événement.

- **Debug** : Informations complètes.

- **Trace** : Journalisation détaillée (paramètre par défaut pour les clients).

Ce paramètre de Registre ne modifie pas les informations qui sont envoyées vers Azure Information Protection pour [centrale reporting](../reports-aip.md).


## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez personnalisé le client étiquetage d’Azure Information Protection unifié, consultez les ressources suivantes pour plus d’informations que vous devrez peut-être prendre en charge de ce client :

- [Fichiers du client et journalisation de l’utilisation](client-admin-guide-files-and-logging.md)

- [Types de fichier pris en charge](client-admin-guide-file-types.md)

- [Commandes PowerShell](client-admin-guide-powershell.md)
