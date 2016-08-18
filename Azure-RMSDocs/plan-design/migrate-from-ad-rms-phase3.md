---
title: "Migration d’AD RMS vers Azure Rights Management - Phase 3 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8b039ad5-95a6-4c73-9c22-78c7b0e12cb7
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f7dd88d90357c99c69fe4fdde67c1544595e02f8
ms.openlocfilehash: 75cce1d0e5a1cff0d4f6609d0f084fda1af62951


---

# Phase de migration 3 : Configuration des services de prise en charge

*S’applique à : Active Directory Rights Management Services, Azure Rights Management*


Utilisez les informations suivantes pour la Phase 3 de la migration d’AD RMS vers Azure Rights Management (Azure RMS). Ces procédures couvrent les étapes 6 à 7 de [Migration d’AD RMS vers Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md).


## Étape 6. Configurer l'intégration de l'IRM pour Exchange Online

Si vous avez précédemment importé votre TDP d'AD RMS dans Exchange Online, vous devez supprimer cette TDP pour éviter des conflits de modèles et de stratégies après la migration vers Azure RMS. Pour ce faire, utilisez l’applet de commande [Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/library/jj200720%28v=exchg.150%29.aspx) d’Exchange Online.

Si vous avez choisi une topologie de clé de locataire Azure RMS **gérée par Microsoft**:

-   Consultez la section [Exchange Online : configuration d’IRM](../deploy-use/configure-office365.md#exchange-online-irm-configuration) de l’article [Office 365 : Configuration pour les clients et les services en ligne](../deploy-use/configure-office365.md). Cette section inclut des commandes spécifiques à exécuter, qui établissent une connexion au service Exchange Online, importent la clé de locataire d’Azure RMS et activent les fonctionnalités de l’IRM pour Exchange Online. Après avoir effectué ces étapes, vous disposez de toutes les fonctionnalités RMS avec Exchange Online.

Si vous avez choisi une topologie de clé de locataire Azure RMS **gérée par le client (BYOK)** :

-   Vous disposez de fonctionnalités RMS réduites avec Exchange Online, comme décrit dans l’article [Tarifs et restrictions BYOK](byok-price-restrictions.md).

## Étape 7. Déployer le connecteur RMS
Si vous avez utilisé la fonctionnalité Information Rights Management (IRM) d'Exchange Server ou de SharePoint Server avec AD RMS, vous devez d'abord désactiver l'IRM sur ces serveurs, puis supprimer la configuration AD RMS. Ensuite, déployez le connecteur Rights Management (RMS), qui agit comme interface de communication (relais) entre les serveurs locaux et Azure RMS.

Enfin, pour cette étape, si vous avez importé plusieurs TPD dans Azure RMS, qui ont été utilisés pour protéger des messages électroniques, vous devez modifier manuellement le Registre sur les ordinateurs Exchange Server afin de rediriger toutes les URL de TPD vers le connecteur RMS.

> [!NOTE]
> Avant de commencer, vérifiez les versions des serveurs locaux prises en charge par Azure RMS, dans [Serveurs locaux prenant en charge Azure RMS](../get-started/requirements-servers.md).

### Désactivation de l'IRM sur les serveurs Exchange et suppression de la configuration AD RMS

1.  Sur chaque serveur Exchange, recherchez le dossier suivant, puis supprimez toutes ses entrées : \ProgramData\Microsoft\DRM\Server\S-1-5-18

2.  Sur l'un des serveurs Exchange, commencez par utiliser l'applet de commande [Set_IRMConfiguration](http://technet.microsoft.com/library/dd979792.aspx) pour désactiver les fonctionnalités de l'IRM pour les messages envoyés à des destinataires internes :

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $false
    ```

3.  Puis, utilisez la même applet de commande pour désactiver les fonctionnalités IRM pour les messages envoyés à des destinataires externes :

    ```
    Set-IRMConfiguration -ExternalLicensingEnabled $false
    ```

4.  Ensuite, utilisez la même applet de commande pour désactiver IRM dans Microsoft Office Outlook Web App et dans Microsoft Exchange ActiveSync :

    ```
    Set-IRMConfiguration -ClientAccessServerEnabled $false
    ```

5.  Enfin, utilisez la même applet de commande pour effacer les certificats mis en cache :

    ```
    Set-IRMConfiguration -RefreshServerCertificates
    ```

6.  Sur chaque serveur Exchange, réinitialisez IIS, par exemple, en exécutant une invite de commandes en tant qu’administrateur et en tapant **iisreset**.

### Désactivation d'IRM sur les serveurs SharePoint et suppression de la configuration AD RMS

1.  Assurez-vous qu'aucun document n'est extrait des bibliothèques protégées par RMS. Les documents extraits deviendront inaccessibles à la fin de cette procédure.

2.  Sur le site web Administration centrale de SharePoint, dans la section **Lancement rapide** , cliquez sur **Sécurité**.

3.  Dans la page **Sécurité** , dans la section **Stratégie d'information** , cliquez sur **Configurer la gestion des droits relatifs à l'information**.

4.  Dans la page **Gestion des droits relatifs à l'information** , dans la section **Gestion des droits relatifs à l'information** , sélectionnez **Ne pas utiliser IRM sur ce serveur**, puis cliquez sur **OK**.

5.  Sur chaque ordinateur SharePoint Server, supprimez le contenu du dossier \ProgramData\Microsoft\MSIPC\Server\*&lt;SID du compte exécutant SharePoint Server&gt;*.

#### Installation et configuration du connecteur RMS

-   Suivez les instructions de l’article [Déploiement du connecteur Azure Rights Management](../deploy-use/deploy-rms-connector.md).

#### Pour Exchange uniquement et plusieurs TPD : modifier le Registre

-   Sur chaque serveur Exchange, ajoutez manuellement les clés de Registre suivantes pour chaque TPD que vous avez importé afin de rediriger les URL de TPD vers le connecteur RMS. Ces entrées de Registre sont spécifiques de la migration et ne sont pas ajoutées par l'outil de configuration de serveur pour le connecteur Microsoft RMS.

    Lorsque vous apportez ces modifications au Registre, suivez les instructions suivantes :

    -   Remplacez *ConnectorFQDN* par le nom défini dans le DNS pour le connecteur. Par exemple, **rmsconnector.contoso.com**.

    -   Utilisez le préfixe HTTP ou HTTPS pour l'URL du connecteur, selon que vous avez configuré le connecteur pour utiliser le protocole HTTP ou HTTPS pour communiquer avec vos serveurs locaux.

Pour Exchange 2013 - Modification du Registre 1 :


**Chemin d’accès au Registre :**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**Tapez :**

Reg_SZ

**Value :**

https://<AD RMS Intranet Licensing URL>/_wmcs/licensing

**Données :**

L'une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur Exchange et votre connecteur RMS :

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorName>/_wmcs/licensing


---

Pour Exchange 2013 - Modification du Registre 2 :

**Chemin d’accès au Registre :**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection 


**Tapez :**

Reg_SZ

**Value :**

https://<AD RMS Extranet Licensing URL>/_wmcs/licensing


**Données :**

L'une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur Exchange et votre connecteur RMS :

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorFQDN>/_wmcs/licensing

---

Pour Exchange 2010 - Modification du Registre 1 :



**Chemin d’accès au Registre :**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**Tapez :**

Reg_SZ

**Value :**

https://<AD RMS Intranet Licensing URL>/_wmcs/licensing

**Données :**

L'une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur Exchange et votre connecteur RMS :

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorName>/_wmcs/licensing


---

Pour Exchange 2010 - Modification du Registre 2 :


**Chemin d’accès au Registre :**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection
 

**Tapez :**

Reg_SZ

**Value :**

https://<AD RMS Extranet Licensing URL>/_wmcs/licensing


**Données :**

L'une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur Exchange et votre connecteur RMS :

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorFQDN>/_wmcs/licensing

---

Une fois ces procédures terminées, vous pouvez lire la section **Étapes suivantes** de l’article [Déploiement du connecteur Azure Rights Management](../deploy-use/deploy-rms-connector.md).

## Étapes suivantes
Pour poursuivre la migration, passez à la [Phase 4 - Tâches de post-migration](migrate-from-ad-rms-phase4.md).


<!--HONumber=Jul16_HO3-->


