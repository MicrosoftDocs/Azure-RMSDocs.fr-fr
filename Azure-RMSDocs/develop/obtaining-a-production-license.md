---
# required metadata

title: Obtention d’une licence de production | Azure RMS
description: La publication d’une application développée avec RMS SDK 2.1 nécessite un contrat de licence de production.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 6749817E-FF34-4384-BF63-39AEA5C372CA
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Obtention d’une licence de production

Avant de pouvoir publier une application développée avec Rights Management Services SDK 2.1, vous devez demander un contrat de licence de production pour obtenir un certificat de production.

> [!IMPORTANT]
> S’il est prévu que vous exécutiez votre application cliente avec Azure RMS, vous devez demander un locataire Azure RMS. Envoyez un e-mail à <rmcstbeta@microsoft.com> avec votre demande de locataire.

Pour plus d’informations sur l’exécution d’Azure RMS, consultez [Permettre à votre application de service de fonctionner avec le service RMS cloud](how-to-use-file-api-with-aadrm-cloud.md).


Le certificat de production et le certificat de préproduction ont une fonction similaire, mais ils sont conçus pour être utilisés dans des environnements différents. Tous deux contiennent une chaîne de certificats avec un certificat d’autorité de certification Microsoft à la racine de confiance, mais le certificat de préproduction est utilisé uniquement pendant le développement d’une application RMS. Le certificat de production est utilisé dans les environnements post-publication. Le certificat de production et la clé privée associée servent à créer et à signer un manifeste qui identifie les fichiers qui peuvent ou doivent être chargés dans l’espace de processus de votre application et ceux qui ne doivent pas être chargés.

Pour plus d’informations sur les clés, consultez [Test de votre application avec gestion des droits](running-your-first-application.md).

Vous pouvez obtenir le certificat en demandant un contrat de licence de production.

## Demander un contrat de licence de production

-   Envoyez un e-mail à [RMLA@microsoft.com](mailto:rmla@microsoft.com) en spécifiant les informations suivantes :

    -   Nom complet de l’entreprise

    -   Adresse physique de l’entreprise (inclure la ville, le département, le pays ou la région et le code postal)
    -   Adresse de correspondance de l’entreprise (inclure la ville, le département, le pays ou la région et le code postal)
    -   Numéros de téléphone et de télécopie de l’entreprise
    -   URL de l’entreprise
    -   Pays ou région où l’entreprise a été créée
    -   Nom de l’application ou du produit
    -   Nom et prénom du demandeur
    -   Titre du demandeur
    -   Adresse de messagerie du demandeur

    Un compte de messagerie n’est pas strictement obligatoire, mais le processus d’application s’appuie généralement sur la messagerie pour la communication. Vous pouvez obtenir un compte de messagerie gratuitement sur Microsoft Outlook.com. Si vous n’avez pas de compte et que vous ne souhaitez pas en créer, vous pouvez envoyer une application à l’adresse suivante :

    `Active Directory Rights Management License Agreements (ADRMLA)`

    `Microsoft Corporation`

    `One Microsoft Way`

    `Redmond, WA 98052-6399`

    Lors de la demande de contrat, procédez comme suit :

    -   Envoyez les informations (en anglais) telles qu’elles doivent apparaître sur le contrat.
    -   Envoyez toutes les informations demandées. Toute information manquante ou incomplète peut retarder le traitement de votre demande.

    L’équipe ADRMLA (Active Directory Rights Management Licensing Agreement) répondra à votre demande dans les trois jours ouvrables suivant la réception de votre e-mail (ou plus si vous avez envoyé la demande par voie postale). La réponse contiendra le formulaire de contrat de licence et d’autres instructions. Lisez, signez et renvoyez toutes les pages du contrat à l’équipe ADRMLA. Veuillez ne pas modifier les polices ou la mise forme des paragraphes du contrat de licence.

    Suivez bien les instructions envoyées par l’équipe ADRMLA. Ces instructions mentionnent les informations numériques nécessaires pour répondre à votre demande de certificat. En suivant les instructions pas à pas, vous réduirez tout risque de retard.

    L’équipe ADRMLA vous transmettra votre certificat de production dès qu’il aura été créé. Le certificat est créé conformément au contrat de licence et aux informations numériques (y compris la clé publique) que vous fournissez. Notez que le délai d’envoi du certificat par e-mail par l’équipe ADRMLA peut aller jusqu’à 15 jours, voire plus en cas de communication par voie postale.

## Rubriques connexes

* [Procédures](how-to-use-msipc.md)
* [Test de votre application avec gestion des droits](running-your-first-application.md)
 

 





<!--HONumber=Apr16_HO4-->


