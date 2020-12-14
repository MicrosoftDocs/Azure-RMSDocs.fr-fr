---
title: Configuration pour les clients utilisant des applications Office avec Azure RMS d’Azure Information Protection
description: Informations et instructions permettant aux administrateurs de configurer des applications Office pour qu’elles fonctionnent avec le service Azure Rights Management d’Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/30/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ec269afe-4e87-4cc1-9144-5fbb594b412e
ms.subservice: azurerms
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: ea6b8afa02b9555924bcd1df5dfae1b7b37a217a
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97383531"
---
# <a name="office-apps-configuration-for-clients-to-use-the-azure-rights-management-service"></a>Applications Office : configuration pour les clients utilisant le service Azure Rights Management

>***S’applique à**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>*Concerne : client **d'** [étiquetage unifié AIP et client Classic](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*


Utilisez ces informations pour déterminer ce que vous devez faire pour que les applications Office fonctionnent avec le service Azure Rights Management d’Azure Information Protection.

## <a name="office-365-apps-office-2019-office-2016-and-office-2013"></a>Applications Office 365, Office 2019, Office 2016 et Office 2013

Étant donné que ces versions ultérieures d’Office fournissent une prise en charge intégrée du service Azure Rights Management, aucune configuration d’ordinateur client n’est requise pour prendre en charge les fonctionnalités de gestion des droits relatifs à l’information (IRM) pour les applications telles que Word, Excel, PowerPoint, Outlook et Outlook sur le Web. 

Pour ces applications sur Windows, tous les utilisateurs doivent se connecter à leurs applications Office avec leurs informations d’identification de Microsoft 365. Ils peuvent alors protéger des fichiers et des e-mails, et utiliser des fichiers et des e-mails qui ont été protégés par d’autres.

### <a name="user-instructions-for-office-for-mac"></a>Instructions de l’utilisateur pour Office pour Mac

Les utilisateurs qui disposent d’Office pour Mac doivent tout d’abord vérifier leurs informations d’identification pour pouvoir protéger du contenu. Par exemple :

1. Ouvrez Outlook et créez un profil à l’aide de votre compte professionnel ou scolaire Microsoft 365. 

2. Créez un nouveau message et, sous l’onglet **options** , sélectionnez **autorisations**, puis sélectionnez **vérifier les informations d’identification**. Lorsque vous y êtes invité, spécifiez à nouveau les détails de votre compte Microsoft 365 professionnel ou scolaire, puis sélectionnez **se connecter**.
    
    Cette action télécharge les modèles Azure Rights Management et **vérifie que les informations d’identification** sont désormais remplacées par des options qui incluent **aucune restriction**, **ne pas transférer** et tous les modèles de Rights Management Azure publiés pour votre locataire. 

3. Vous pouvez désormais annuler ce nouveau message.

4. Pour protéger un message électronique ou un document : sous l’onglet **options** , sélectionnez **autorisations** et choisissez une option ou un modèle qui protège votre courrier électronique ou document.

## <a name="office-2010"></a>Office 2010

Pour pouvoir utiliser le service Azure Rights Management avec Office 2010, les ordinateurs clients doivent disposer du client Azure Information Protection. Aucune autre configuration n’est requise, car les utilisateurs doivent se connecter avec leurs informations d’identification de Microsoft 365 et peuvent ensuite protéger des fichiers et utiliser des fichiers qui ont été protégés par d’autres.

Pour plus d’informations, consultez [Client Azure Information Protection : installation et configuration pour les clients](configure-client.md).

