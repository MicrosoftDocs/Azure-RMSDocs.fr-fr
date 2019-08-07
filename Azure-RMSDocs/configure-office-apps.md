---
title: Configuration pour les clients utilisant des applications Office avec Azure RMS d’Azure Information Protection
description: Informations et instructions permettant aux administrateurs de configurer des applications Office pour qu’elles fonctionnent avec le service Azure Rights Management d’Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ec269afe-4e87-4cc1-9144-5fbb594b412e
ms.subservice: azurerms
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 32461a7d3edb53003ea12a7dc26e8b78966e1a4f
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/05/2019
ms.locfileid: "68789256"
---
# <a name="office-apps-configuration-for-clients-to-use-the-azure-rights-management-service"></a>Applications Office : Configuration pour que les clients utilisent le service Azure Rights Management

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Utilisez ces informations pour déterminer ce que vous devez faire pour que les applications Office fonctionnent avec le service Azure Rights Management d’Azure Information Protection.

## <a name="office365-apps-office-2019-office-2016-and-office-2013"></a>Office 365 Apps, Office 2019, Office 2016 et Office 2013
Ces versions d’Office prenant en charge le service Azure Rights Management en mode natif, aucune configuration de l’ordinateur client n’est nécessaire pour la prise en charge des fonctionnalités de gestion des droits relatifs à l’information (IRM) pour des applications comme Word, Excel, PowerPoint, Outlook et Outlook sur le web. Tous les utilisateurs doivent faire pour ces applications sur Windows, se connectent à leurs applications Office avec leurs informations d’identification Office 365. Ils peuvent alors protéger des fichiers et des e-mails, et utiliser des fichiers et des e-mails qui ont été protégés par d’autres.

### <a name="user-instructions-for-office-for-mac"></a>Instructions de l’utilisateur pour Office pour Mac

Les utilisateurs qui disposent d’Office pour Mac doivent tout d’abord vérifier leurs informations d’identification pour pouvoir protéger du contenu. Par exemple :

1. Ouvrez Outlook et créez un profil à l’aide de compte de travail ou scolaire Office 365. 

2. Créez un nouveau message et, sous l’onglet **options** , sélectionnez **autorisations**, puis sélectionnez **vérifier les informations d’identification**. Lorsque vous y êtes invité, spécifiez à nouveau les détails votre compte de travail ou scolaire Office 365, puis sélectionnez **Connexion**.
    
    Cette action télécharge les modèles Azure Rights Management et **vérifie que les informations d’identification** sont désormais remplacées par des options qui incluent **aucune restriction**, **ne pas transférer**et tous les modèles de Rights Management Azure publiés pour votre priorité. 

3. Vous pouvez désormais annuler ce nouveau message.

4. Pour protéger un message ou un document : Dans l’onglet **options** , sélectionnez **autorisations** et choisissez une option ou un modèle qui protège votre courrier électronique ou document.

## <a name="office2010"></a>Office 2010
Pour que les ordinateurs clients utilisent le service Azure Rights Management avec Office 2010, ils doivent disposer du client Azure Information Protection (Classic). Aucune autre configuration n’est requise. Les utilisateurs doivent juste se connecter avec leurs informations d’identification Office 365 pour pouvoir protéger des fichiers et utiliser des fichiers protégés par d’autres.

Pour plus d’informations sur le client Azure information protection (Classic), [consultez Azure information protection client: Installation et configuration pour les clients](configure-client.md).

