---
title: Télécharger & installer le client classique Azure Information Protection
description: Instructions permettant aux utilisateurs d’installer le client Azure Information Protection Classic pour Windows, afin que vous puissiez classer et protéger vos documents et e-mails.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/17/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 2bf09690-9dba-43b7-9e0a-0110915d4081
ROBOTS: NOINDEX
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: user
ms.openlocfilehash: df5328b94112342276028e2a74da02de14170418
ms.sourcegitcommit: af7ac2eeb8f103402c0036dd461c77911fbc9877
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/18/2021
ms.locfileid: "98560236"
---
# <a name="user-guide-download-and-install-the-azure-information-protection-classic-client"></a>Guide de l’utilisateur : Télécharger et installer le client Azure Information Protection Classic

>***S’applique à**: services AD RMS (Active Directory Rights Management Services), [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8 *
>
>***Concerne :** [Azure information protection client classique pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Pour le client d’étiquetage unifié, reportez-vous au Guide de l' [utilisateur d’étiquetage unifié](install-unifiedlabelingclient-app.md). *

> [!NOTE] 
> Pour fournir une expérience client unifiée et homogène, le **client classique Azure Information Protection** et la **gestion des étiquettes** dans le portail Azure seront **dépréciés** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Si votre administrateur n’installe pas le client Azure Information Protection pour vous, vous pouvez le faire vous-même. Vous devez être un administrateur local de votre PC pour installer ce client, de sorte qu’il puisse étiqueter et protéger vos documents et vos e-mails.

De plus :

- Le client Azure Information Protection requiert une version minimale de Microsoft .NET Framework 4.6.2. Si cette version est manquante, le programme d’installation tente de télécharger et d’installer ce composant requis. Lorsque ce composant requis est installé dans le cadre de l’installation du client, votre ordinateur doit être redémarré.


## <a name="to-download-and-install-the-azure-information-protection-client"></a>Pour télécharger et installer le client Azure Information Protection

Le client Azure Information Protection Classic est déconseillé en mars 2021. 

Pour le déployer, ouvrez un ticket de support afin d’obtenir l’accès au téléchargement.

1. Exécutez le fichier **AzInfoProtection.exe** pour démarrer l’installation. Si vous êtes invité à continuer, cliquez sur **Oui**.    

1. Dans la page **Installer le client Azure Information Protection** :     
    - Sélectionnez l’option d’installation d’une stratégie de démonstration si vous ne pouvez pas vous connecter au cloud mais souhaitez évaluer l’expérience avec le côté client d’Azure Information Protection à l’aide d’une stratégie locale à des fins de démonstration. Lorsque votre client se connecte à un service Azure Information Protection, cette stratégie de démonstration est remplacée par la stratégie Azure Information Protection de votre organisation.    

    - Cliquez sur **J’accepte** quand vous avez lu les termes du contrat de licence.    

1. Si vous êtes invité à continuer, cliquez sur **Oui** et attendez que l’installation se termine.    

1. Cliquez sur **Fermer**. 

    Avant de commencer à utiliser le client Azure Information Protection, redémarrez toutes les applications Office et toutes les instances de l’Explorateur de fichiers. L’installation est à présent terminée. Vous pouvez désormais utiliser le client pour étiqueter et protéger vos documents et vos e-mails.

    > [!NOTE]
    > Si votre ordinateur exécute Office 2010, redémarrez votre ordinateur, puis passez à la [section suivante](#installing-the-azure-information-protection-client-with-office-2010) pour la dernière étape.  

### <a name="installing-the-azure-information-protection-client-with-office-2010"></a>Installation du client Azure Information Protection avec Office 2010

> [!IMPORTANT]
> Le support étendu Office 2010 a pris fin le 13 octobre 2020. Pour plus d’informations, consultez [AIP et versions héritées de Windows et d’Office](../known-issues.md#aip-and-legacy-windows-and-office-versions).
> 

Une fois le client Azure Information Protection installé à l’aide des instructions précédentes :    

1. Ouvrez Microsoft Word. Lorsque vous exécutez une application Office 2010 pour la première fois après avoir installé le client Azure Information Protection, une boîte de dialogue **Microsoft Azure Information Protection** s’affiche. Cette boîte de dialogue vous indique que des informations d’identification administrateur sont requises pour terminer la connexion.

2. Dans la boîte de dialogue **Microsoft Azure Information Protection**, cliquez sur **OK**.

3. Si une boîte de dialogue **Contrôle d’accès utilisateur** s’affiche, cliquez sur **Oui**, afin que le client Azure Information Protection puisse mettre à jour le registre.

L’installation est à présent terminée. Vous pouvez désormais utiliser Azure Information Protection pour étiqueter et protéger vos documents et vos e-mails.

## <a name="other-instructions"></a>Autres instructions    
Plus d’instructions pratiques dans le guide de l’utilisateur Azure Information Protection :

- [Que voulez-vous faire ?](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Informations supplémentaires pour les administrateurs    
Consultez [Installer le client Azure Information Protection pour les utilisateurs](client-admin-guide-install.md) dans le [guide de l’administrateur](client-admin-guide.md).
 
  
