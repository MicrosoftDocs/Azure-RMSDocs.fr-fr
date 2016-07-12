---
title: Surveiller le connecteur Azure Rights Management | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 07/08/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8a1b3e54-f788-4f84-b9d7-5d5079e50b4e
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f8e23e8bcbfb25092cb31f7af76d17239f3063a7
ms.openlocfilehash: 32c3c93d55bd82f45fa7a081e55ae7ebe8f5956f


---

# Surveiller le connecteur Azure Rights Management

*S’applique à : Azure Rights Management, Windows Server 2012, Windows Server 2012 R2*

Après avoir installé et configuré le connecteur RMS, vous pouvez utiliser les méthodes et les informations suivantes pour surveiller le connecteur ainsi que l’utilisation d’Azure RMS par votre organisation.

## Entrées du journal des événements de l’application

Le connecteur RMS utilise le journal des événements de l’application pour enregistrer des entrées pour le **connecteur Microsoft RMS**. 

Par exemple, les événements d’information comme l’ID 1000 confirment que le service du connecteur a démarré, l’ID 1002 quand un serveur se connecte correctement au connecteur RMS et l’ID 1004 chaque fois que la liste des comptes autorisés (chaque compte est répertorié) est téléchargée sur le connecteur. 

Si vous n’avez pas configuré le connecteur pour utiliser le protocole HTTPS, vous recevez un avertissement avec l’ID 2002 indiquant qu’un client utilise une connexion non sécurisée (HTTP).

Si le connecteur ne parvient pas à se connecter à Azure RMS, vous recevez probablement l’erreur 3001. Il peut s’agir, par exemple, d’un problème DNS ou d’un manque d’accès à Internet pour un ou plusieurs serveurs exécutant le connecteur RMS. 

> [!TIP]
> Quand les serveurs du connecteur RMS ne peuvent pas se connecter à Azure RMS, les configurations de proxy web sont souvent à l’origine du problème.

Comme avec toutes les entrées de journal des événements, examinez le message pour plus de détails.

Outre la vérification du journal des événements quand vous déployez le connecteur pour la première fois, recherchez régulièrement les avertissements et les erreurs. Par exemple, le connecteur peut fonctionner comme prévu initialement, mais les autres administrateurs peuvent modifier les configurations dépendantes. Par exemple, un autre administrateur modifie la configuration du serveur proxy web et les serveurs du connecteur RMS ne peuvent plus se connecter à Internet (Erreur 3001) ou il supprime un compte d’ordinateur d’un groupe que vous avez autorisé à utiliser le connecteur (Avertissement 2001).

### ID du journal des événements et descriptions

Les sections suivantes indiquent les ID d’événement possibles, des descriptions et des informations supplémentaires.

-----

Information **1000**

**Le service web du connecteur Microsoft RMS a démarré.**

Cet événement est consigné à la première tentative de démarrage du connecteur RMS.

----

Information **1001**

**Le service web du connecteur Microsoft RMS s’est arrêté.**

Cet événement est consigné quand le connecteur RMS s’arrête à la suite d’une opération normale. Par exemple, IIS est redémarré ou l’ordinateur est arrêté. 

----

Information **1002**

**Un accès au connecteur Microsoft RMS a été accordé à un serveur autorisé.**

Cet événement est consigné quand un compte à partir d’un serveur local se connecte au connecteur RMS après avoir été autorisé par l’administrateur Azure RMS dans l’outil d’administration du connecteur RMS. Le SID, le nom du compte et le nom de l’ordinateur effectuant la connexion figurent dans le message de l’événement.

----

Information **1003**

**La connexion depuis le client répertorié ci-dessous est passée d’une connexion non sécurisée (HTTP) à une connexion sécurisée (HTTPS).**

Cet événement est consigné quand un serveur local change sa connexion au connecteur RMS de HTTP (moins sécurisé) à HTTPS (plus sécurisé). Le SID, le nom du compte et le nom de l’ordinateur effectuant la connexion figurent dans le message de l’événement.

----

Information **1004**

**La liste des comptes autorisés a été mise à jour.**

Cet événement est consigné quand le connecteur RMS a téléchargé la dernière liste des comptes (comptes existants et toutes les modifications) autorisés à utiliser le connecteur RMS. Cette liste est téléchargée toutes les quinze minutes, à condition que le connecteur RMS puisse communiquer avec Azure RMS.

----

Avertissement **2000**

**Le nom principal de l’utilisateur est absent ou non valide dans le contexte HTTP. Vérifiez, dans le site web du connecteur Microsoft RMS, que l’authentification anonyme est désactivée dans IIS et que seule l’authentification Windows est activée.**

Cet événement est consigné quand le connecteur RMS ne peut pas identifier avec exactitude le compte qui essaie de se connecter au connecteur RMS. Cet événement peut être dû au fait qu’une authentification anonyme est mal configurée pour IIS ou que le compte provient d’une forêt non approuvée.

----

Avertissement **2001**

**Tentative d’accès non autorisée au connecteur Microsoft RMS.**

Cet événement est consigné quand un compte ne parvient pas à se connecter au connecteur RMS. En règle générale, cet événement est dû au fait que le compte qui effectue la connexion ne se trouve pas dans la liste des comptes autorisés téléchargée par le connecteur RMS à partir d’Azure RMS. Par exemple, la liste la plus récente n’est pas encore téléchargée (cette opération se produit toutes les 15 minutes) ou le compte est manquant dans la liste. 

Il est également possible que vous ayez installé le connecteur RMS sur le serveur qui est configuré pour utiliser le connecteur. Par exemple, vous installez le connecteur RMS sur un serveur qui exécute Microsoft Exchange Server et vous autorisez un compte Exchange à utiliser le connecteur. Cette configuration n’est pas prise en charge, car le connecteur RMS ne peut pas identifier correctement le compte quand il tente de se connecter.

Le message d’événement contient des informations sur le compte et l’ordinateur qui essaie de se connecter au connecteur RMS :

- Si le compte qui essaie de se connecter au connecteur RMS est un compte valide, utilisez l’outil d’administration du connecteur RMS pour ajouter le compte à la liste des comptes autorisés. Pour plus d’informations sur les comptes qui doivent être autorisés, consultez [Ajout d’un serveur à la liste des serveurs autorisés](install-configure-rms-connector.md#add-a-server-to-the-list-of-allowed-servers). 

- Si le compte qui essaie de se connecter au connecteur RMS provient du même ordinateur que le serveur de connecteur RMS, installez le connecteur sur un serveur distinct. Pour plus d’informations sur les conditions requises pour le connecteur, consultez [Conditions requises pour l’installation du connecteur RMS]( deploy-rms-connector.md#prerequisites-for-the-rms-connector).

----

Avertissement **2002**

**La connexion depuis le client répertorié ci-dessous utilise une connexion non sécurisée (HTTP).**

Cet événement est consigné quand un serveur local se connecte correctement au connecteur RMS, mais que la connexion utilise le protocole HTTP (moins sécurisé) au lieu du protocole HTTPS (plus sécurisé). Un événement est consigné par compte, plutôt que par connexion. Cet événement est redéclenché si le compte revient à HTTP après avoir basculé vers HTTPS.

Le message d’événement contient le SID du compte, le nom de compte et le nom de l’ordinateur qui établit la connexion au connecteur RMS.

Pour plus d’informations sur la configuration du connecteur RMS pour les connexions HTTPS, consultez [Configuration du connecteur RMS pour le protocole HTTPS](install-configure-rms-connector.md#configuring-the-rms-connector-to-use-https).

----

Avertissement **2003**

**La liste des autorisations est vide. Le service n’est pas utilisable tant que la liste des utilisateurs et groupes autorisés pour le connecteur n’est pas renseignée.**

Cet événement est consigné quand le connecteur RMS n’a pas de liste de comptes autorisés, ce qui empêche tout serveur local de s’y connecter. Le connecteur RMS télécharge la liste toutes les 15 minutes à partir d’Azure RMS. 

Pour spécifier les comptes, utilisez l’outil d’administration du connecteur RMS. Pour plus d’informations, consultez [Définition des serveurs autorisés à utiliser le connecteur RMS]( install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector). 

----

Erreur **3000**

**Une exception non prise en charge s’est produite dans le connecteur Microsoft RMS.**

Cet événement est consigné chaque fois que le connecteur RMS rencontre une erreur inattendue, avec les détails de l’erreur dans le message d’événement.

La présence du texte **Échec de la requête avec une réponse vide** dans le message d’événement peut révéler une cause possible. Si vous voyez ce texte, un appareil réseau effectue peut-être une inspection SSL sur les paquets entre les serveurs locaux et le serveur de connecteur RMS. Cette opération n’étant pas prise en charge, la communication échoue et ce message du journal des événements est généré.

----

Erreur **3001**

**Une exception s’est produite lors du téléchargement des informations d’autorisation.**

Cet événement est consigné si le connecteur RMS ne peut pas télécharger la dernière liste des comptes autorisés à utiliser le connecteur RMS, avec les détails de l’erreur dans le message d’événement.



----

## Compteurs de performances

Quand vous installez le connecteur RMS, il crée automatiquement les compteurs de performances du **connecteur Microsoft Rights Management** qui sont utiles pour surveiller les performances de l’utilisation d’Azure RMS par le biais du connecteur. 

Par exemple, si vous observez régulièrement des retards lors de la protection des documents ou des e-mails, ou lors de l’ouverture de documents ou e-mails protégés, les compteurs de performances peuvent vous aider à déterminer si le retard est dû au temps de traitement sur le connecteur, au temps de traitement dans Azure RMS ou au réseau. Pour vous permettre d’identifier l’origine du retard, recherchez les compteurs qui incluent des valeurs moyennes pour le **Temps de traitement du connecteur**, le **Temps de réponse du service** et le **Temps de réponse du connecteur**. Par exemple : **Temps de réponse moyen du connecteur pour les demandes de licences par lot réussies**.

Si vous avez récemment ajouté des comptes de serveur pour utiliser le connecteur, le compteur à consulter est **Durée depuis la dernière mise à jour de la stratégie d’autorisation** pour vérifier que le connecteur a téléchargé la liste depuis que vous l’avez mise à jour, ou déterminer si vous devez attendre un peu plus longtemps (jusqu’à 15 minutes).

## RMS Analyzer

Vous pouvez utiliser l’outil Rights Management Services Analyzer pour vous aider à surveiller l’intégrité du connecteur et à identifier les problèmes de configuration.

Si vous n’avez pas encore téléchargé cet outil, vous pouvez le faire à partir du [Centre de téléchargement](https://www.microsoft.com/en-us/download/details.aspx?id=46437). Installez-le sur un ordinateur ayant accès à Internet et pouvant se connecter au connecteur RMS. Exécutez l’outil, puis, dans la page **Bienvenue**, sélectionnez l’option **Connecteur Azure RMS**.

Pour des informations et des instructions supplémentaires sur cet outil, consultez les sections **Détails** et **Instructions d’installation** dans la page de téléchargement.

## Journalisation

La journalisation de l’utilisation vous aide à identifier quand les e-mails et les documents sont protégés et consommés. Quand vous utilisez le connecteur RMS, le champ ID d’utilisateur dans les journaux contient le nom principal de service **Aadrm_S-1-7-0** qui est créé automatiquement pour le connecteur RMS.

Pour plus d’informations sur la journalisation de l’utilisation, consultez [Journalisation et analyse de l’utilisation d’Azure Rights Management](log-analyze-usage.md).

Si vous avez besoin d’une journalisation plus détaillée à des fins de diagnostic, vous pouvez utiliser [Debugview](http://go.microsoft.com/fwlink/?LinkID=309277) dans Windows Sysinternals et activer le suivi pour le connecteur RMS en modifiant le fichier web.config pour le site par défaut dans IIS. Pour effectuer cette opération :

1. Recherchez le fichier web.config dans **%programfiles%\Microsoft Rights Management connector\Web Service**.

2. Recherchez la ligne suivante :

        <trace enabled="false" requestLimit="10" pageOutput="false" traceMode="SortByTime" localOnly="true"/>

3. Remplacez cette ligne par la suivante :

        <trace enabled="true" requestLimit="10" pageOutput="false" traceMode="SortByTime" localOnly="true"/>

4.  Arrêtez et démarrez les services IIS pour activer le suivi. 

5.  Quand vous avez capturé les traces dont vous avez besoin, rétablissez la ligne de l’étape 3, puis arrêtez et redémarrez les services IIS.




<!--HONumber=Jul16_HO2-->


