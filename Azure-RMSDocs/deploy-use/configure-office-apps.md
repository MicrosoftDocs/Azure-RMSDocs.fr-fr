---
title: Configuration pour les clients utilisant des applications Office avec Azure RMS d’Azure Information Protection
description: Informations et instructions permettant aux administrateurs de configurer des applications Office pour qu’elles fonctionnent avec le service Azure Rights Management d’Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ec269afe-4e87-4cc1-9144-5fbb594b412e
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 79c3da1d2fcf9405389f5ceba25b81f4808713b8
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
ms.locfileid: "30204688"
---
# <a name="office-apps-configuration-for-clients-to-use-the-azure-rights-management-service"></a>Applications Office : configuration pour les clients utilisant le service Azure Rights Management

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Utilisez ces informations pour déterminer ce que vous devez faire pour que les applications Office fonctionnent avec le service Azure Rights Management d’Azure Information Protection.

## <a name="office-2016-and-office-2013"></a>Office 2016 et Office 2013
Ces versions d’Office prenant en charge le service Azure Rights Management en mode natif, aucune configuration de l’ordinateur client n’est nécessaire pour la prise en charge des fonctionnalités de gestion des droits relatifs à l’information (IRM) pour des applications comme Word, Excel, PowerPoint, Outlook et Outlook sur le web. Tout ce que les utilisateurs doivent faire est de se connecter à leurs applications Office avec leurs informations d’identification [!INCLUDE[o365_1](../includes/o365_1_md.md)]. Ils peuvent alors protéger des fichiers et des e-mails, et utiliser des fichiers et des e-mails qui ont été protégés par d’autres.

Cependant, nous vous recommandons de compléter ces applications par le client Azure Information Protection, afin que les utilisateurs puissent bénéficier du complément Office et de la prise en charge de types de fichiers supplémentaires. Pour plus d’informations, consultez [Client Azure Information Protection : installation et configuration pour les clients](configure-client.md).

## <a name="office-2010"></a>Office 2010
Pour pouvoir utiliser le service Azure Rights Management avec Office 2010, les ordinateurs client doivent disposer du client Azure Information Protection ou de l’application de partage Rights Management pour Windows. Aucune autre configuration n’est requise. Les utilisateurs doivent simplement se connecter avec leurs informations d’identification [!INCLUDE[o365_1](../includes/o365_1_md.md)] pour pouvoir protéger des fichiers et accéder à des fichiers protégés par d’autres.

Pour plus d’informations sur le client Azure Information Protection, consultez [Azure Information Protection : installation et configuration pour les clients](configure-client.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
