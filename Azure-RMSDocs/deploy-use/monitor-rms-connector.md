---
# required metadata

title: Surveiller le connecteur Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 06/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8a1b3e54-f788-4f84-b9d7-5d5079e50b4e

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Surveiller le connecteur Azure Rights Management

*S’applique à : Azure Rights Management, Windows Server 2012, Windows Server 2012 R2*

Après avoir installé et configuré le connecteur RMS, vous pouvez utiliser les méthodes et les informations suivantes pour surveiller le connecteur ainsi que l’utilisation d’Azure RMS par votre organisation.

## Entrées du journal des événements de l’application

Le connecteur RMS utilise le journal des événements de l’application pour enregistrer des entrées pour le **connecteur Microsoft RMS**. 

Par exemple, les événements d’information comme l’ID 1000 confirment que le service du connecteur a démarré, l’ID 1002 quand un serveur se connecte correctement au connecteur RMS et l’ID 1004 chaque fois que la liste des comptes autorisés (chaque compte est répertorié) est téléchargée sur le connecteur. 

Si vous n’avez pas configuré le connecteur pour utiliser le protocole HTTPS, vous recevez un avertissement avec l’ID 2002 indiquant qu’un client utilise une connexion non sécurisée (HTTP).

Si le connecteur ne parvient pas à se connecter à Azure RMS, vous recevez probablement l’erreur 3001. Il peut s’agir, par exemple, d’un problème DNS ou d’un manque d’accès à Internet pour un ou plusieurs serveurs exécutant le connecteur RMS. 

> [!TIP] Quand les serveurs du connecteur RMS ne peuvent pas se connecter à Azure RMS, les configurations de proxy web sont souvent à l’origine du problème.

Comme avec toutes les entrées de journal des événements, examinez le message pour plus de détails.

Outre la vérification du journal des événements quand vous déployez le connecteur pour la première fois, recherchez régulièrement les avertissements et les erreurs. Par exemple, le connecteur peut fonctionner comme prévu initialement, mais les autres administrateurs peuvent modifier les configurations dépendantes. Par exemple, un autre administrateur modifie la configuration du serveur proxy web et les serveurs du connecteur RMS ne peuvent plus se connecter à Internet (Erreur 3001) ou il supprime un compte d’ordinateur d’un groupe que vous avez autorisé à utiliser le connecteur (Avertissement 2001).

## Compteurs de performances

Quand vous installez le connecteur RMS, il crée automatiquement les compteurs de performances du **connecteur Microsoft Rights Management** qui sont utiles pour surveiller les performances de l’utilisation d’Azure RMS par le biais du connecteur. 

Par exemple, si vous observez régulièrement des retards lors de la protection des documents ou des e-mails, ou lors de l’ouverture de documents ou e-mails protégés, les compteurs de performances peuvent vous aider à déterminer si le retard est dû au temps de traitement sur le connecteur, au temps de traitement dans Azure RMS ou au réseau. Pour vous permettre d’identifier l’origine du retard, recherchez les compteurs qui incluent des valeurs moyennes pour le **Temps de traitement du connecteur**, le **Temps de réponse du service** et le **Temps de réponse du connecteur**. Par exemple : **Temps de réponse moyen du connecteur pour les demandes de licences par lot réussies**.

Si vous avez récemment ajouté des comptes de serveur pour utiliser le connecteur, le compteur à consulter est **Durée depuis la dernière mise à jour de la stratégie d’autorisation** pour vérifier que le connecteur a téléchargé la liste depuis que vous l’avez mise à jour, ou déterminer si vous devez attendre un peu plus longtemps (jusqu’à 15 minutes).

## RMS Analyzer

Vous pouvez utiliser l’outil Rights Management Services Analyzer pour vous aider à surveiller l’intégrité du connecteur et à identifier les problèmes de configuration.

Si vous n’avez pas encore téléchargé cet outil, vous pouvez le faire à partir du [Centre de téléchargement](https://www.microsoft.com/en-us/download/details.aspx?id=46437). Installez-le sur un ordinateur ayant accès à Internet et pouvant se connecter au connecteur RMS. Exécutez l’outil, puis, dans la page **Bienvenue**, sélectionnez l’option **Connecteur Azure RMS**.

Pour des informations et des instructions supplémentaires sur cet outil, consultez les sections **Détails** et **Instructions d’installation** dans la page de téléchargement.

## Journalisation

La journalisation de l’utilisation vous aide à identifier quand les e-mails et les documents sont protégés et consommés. Quand vous utilisez le connecteur RMS, le champ ID d’utilisateur dans les journaux contient le nom principal de service qui est généré automatiquement à l’installation du connecteur RMS.

Pour plus d’informations, consultez [Journalisation et analyse de l’utilisation d’Azure Rights Management](log-analyze-usage.md).

Si vous avez besoin d’une journalisation plus détaillée à des fins de diagnostic, vous pouvez utiliser [Debugview](http://go.microsoft.com/fwlink/?LinkID=309277) dans Windows Sysinternals et activer le suivi pour le connecteur RMS en modifiant le fichier web.config pour le site par défaut dans IIS. Pour effectuer cette opération :

1. Recherchez le fichier web.config dans **%programfiles%\Microsoft Rights Management connector\Web Service**.

2. Recherchez la ligne suivante :

        <trace enabled="false" requestLimit="10" pageOutput="false" traceMode="SortByTime" localOnly="true"/>

3. Remplacez cette ligne par la suivante :

        <trace enabled="true" requestLimit="10" pageOutput="false" traceMode="SortByTime" localOnly="true"/>

4.  Arrêtez et démarrez les services IIS pour activer le suivi. 

5.  Quand vous avez capturé les traces dont vous avez besoin, rétablissez la ligne de l’étape 3, puis arrêtez et redémarrez les services IIS.



<!--HONumber=Jun16_HO2-->


