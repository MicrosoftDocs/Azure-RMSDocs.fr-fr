---
title: "Paramètres de Registre pour le connecteur RMS | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ed3e9a3d-0f7c-4abc-9d0b-aa3b18403d39
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 0f355da35dff62ecee111737eb1793ae286dc93e
ms.openlocfilehash: ff90f009f9fda90171bbeeb2a7bb421376d4695c


---


# Paramètres de Registre pour le connecteur Rights Management

*S’applique à : Azure Rights Management, Office 365*


Reportez-vous aux tableaux des sections suivantes uniquement si vous voulez ajouter ou vérifier manuellement les paramètres de Registre des serveurs exécutant Exchange, SharePoint ou Windows Server, qui configure les serveurs pour utiliser le [connecteur RMS](deploy-rms-connector.md). La méthode recommandée pour configurer ces serveurs consiste à utiliser l’outil de configuration de serveur pour le connecteur Microsoft RMS.

Voici quelques indications pour savoir quand utiliser ces paramètres :

-   *MicrosoftRMSURL* est l'URL de service Microsoft RMS de votre organisation. Pour obtenir cette valeur :

    1.  Exécutez l’applet de commande [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) pour Azure RMS. Si vous n’avez pas déjà installé le module Windows PowerShell pour Azure RMS, consultez [Installation de Windows PowerShell pour Azure Rights Management](install-powershell.md).

    2.  Dans le résultat de l'applet de commande, identifiez la valeur **LicensingIntranetDistributionPointUrl** .

        Par exemple : **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

    3.  À partir de la valeur, supprimez la section **_wmcs/licensing** de cette chaîne. La chaîne restante correspond à votre URL Microsoft RMS. Dans notre exemple, l'URL Microsoft RMS correspond à la valeur suivante :

        **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

-   *ConnectorFQDN* est le nom d’équilibrage de charge que vous avez défini dans le système DNS pour le connecteur. Par exemple, **rmsconnector.contoso.com**.

-   Utilisez le préfixe HTTPS pour l'URL du connecteur si vous avez configuré le connecteur pour utiliser le protocole HTTPS pour communiquer avec vos serveurs locaux. Pour plus d’informations, consultez la section [Configuration du connecteur RMS pour le protocole HTTPS](deploy-rms-connector.md#BKMK_ConfiguringHTTPS) dans cette rubrique. Notez que les URL Microsoft RMS utilisent toujours le protocole HTTPS.


## Paramètres de Registre Exchange 2013 ou Exchange 2016

**Chemin du Registre :** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\Activation

**Type :** Reg_SZ

**Valeur :** Par défaut

**Données :** https://*MicrosoftRMSURL*/_wmcs/certification

---

**Chemin du Registre :** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**Type :** Reg_SZ

**Valeur :** Par défaut

**Données :** https://*MicrosoftRMSURL*/_wmcs/Licensing

---

**Chemin du Registre :**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\CertificationServerRedirection

**Type :** Reg_SZ

**Valeur :** https://*MicrosoftRMSURL*


**Données :** L’une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur Exchange et votre connecteur RMS :

- http://*ConnectorFQDN*

- https://*ConnectorFQDN*

---

**Chemin du Registre :** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**Type :** Reg_SZ

**Valeur :** https://*MicrosoftRMSURL*


**Données :** L’une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur Exchange et votre connecteur RMS :

- http://*ConnectorFQDN*

- https://*ConnectorFQDN*


## Paramètres de Registre Exchange 2010

**Chemin du Registre :** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\Activation

**Type :** Reg_SZ

**Valeur :** Par défaut

**Données :** https://*MicrosoftRMSURL*/_wmcs/certification

---

**Chemin du Registre :** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**Type :** Reg_SZ

**Valeur :** Par défaut

**Données :** https://*MicrosoftRMSURL*/_wmcs/Licensing

---

**Chemin du Registre :**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\CertificationServerRedirection

**Type :** Reg_SZ

**Valeur :** https://*MicrosoftRMSURL*

**Données :** L’une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur Exchange et votre connecteur RMS :

- http://*ConnectorFQDN*

- https://*ConnectorFQDN*

---

**Chemin du Registre :** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**Type :** Reg_SZ

**Valeur :** https://*MicrosoftRMSURL*

**Données :** L’une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur Exchange et votre connecteur RMS :

- http://*ConnectorFQDN*

- https://*ConnectorFQDN*


## Paramètres de Registre SharePoint 2016 ou SharePoint 2013

**Chemin du Registre :** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\LicensingRedirection

**Type :** Reg_SZ

**Valeur :** https://*MicrosoftRMSURL*/_wmcs/licensing


**Données :** L’une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur SharePoint et le connecteur RMS :

- http://*ConnectorFQDN*/_wmcs/licensing

- https://*ConnectorFQDN*/_wmcs/licensing

---

**Chemin du Registre :**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterpriseCertification

**Type :** Reg_SZ

**Valeur :** Par défaut

**Données :** L’une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur SharePoint et le connecteur RMS :

- http://*ConnectorFQDN*/_wmcs/certification

- https://*ConnectorFQDN*/_wmcs/certification

---

**Chemin du Registre :** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterprisePublishing

**Type :** Reg_SZ

**Valeur :** Par défaut


**Données :** L’une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur SharePoint et le connecteur RMS :

- http://*ConnectorFQDN*/_wmcs/licensing

- https://*ConnectorFQDN*/_wmcs/licensing




## Paramètres de Registre du serveur de fichiers et de l’Infrastructure de classification des fichiers

**Chemin du Registre :** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**Type :** Reg_SZ

**Valeur :** Par défaut

**Données :** http://*ConnectorFQDN*/_wmcs/licensing

---

**Chemin du Registre :** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation

**Type :** Reg_SZ

**Valeur :** Par défaut

**Données :** http://*ConnectorFQDN*/_wmcs/certification


Retour à [Déploiement du connecteur Azure Rights Management](deploy-rms-connector.md)


<!--HONumber=Jun16_HO4-->


