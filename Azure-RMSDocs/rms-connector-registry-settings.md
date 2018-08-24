---
title: Paramètres de Registre pour le connecteur Rights Management - AIP
description: Informations relatives aux paramètres du Registre sur les serveurs utilisant le connecteur RMS. La méthode recommandée pour configurer ces paramètres consiste à utiliser l’outil de configuration de serveur pour le connecteur Microsoft RMS.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/16/2018
ms.topic: article
ms.service: information-protection
ms.assetid: ed3e9a3d-0f7c-4abc-9d0b-aa3b18403d39
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 9b99f914e78adafbcfd0f01f0937c6d636f43159
ms.sourcegitcommit: 7ba9850e5bb07b14741bb90ebbe98f1ebe057b10
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42808694"
---
# <a name="registry-setting-for-the-rights-management-connector"></a>Paramètres de Registre pour le connecteur Rights Management

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*


Utilisez les tableaux fournis dans les sections suivantes seulement si vous voulez ajouter ou vérifier manuellement les paramètres de Registre sur les serveurs qui exécutent Exchange, SharePoint ou Windows Server. Ces paramètres de Registre configurent les serveurs pour qu’ils utilisent le [connecteur RMS](deploy-rms-connector.md). La méthode recommandée pour configurer ces serveurs consiste à utiliser l’outil de configuration de serveur pour le connecteur Microsoft RMS.

Voici quelques indications pour savoir quand utiliser ces paramètres :

-   *\<URL_votre_locataire>* est l’URL de votre service Azure Rights Management pour votre locataire Azure Information Protection. Pour obtenir cette valeur :

    1.  Exécutez l’applet de commande [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) pour le service Azure Rights Management. Si vous n’avez pas encore installé le module Windows PowerShell pour Azure RMS, consultez [Installation du module PowerShell AADRM](install-powershell.md).

    2.  Dans le résultat de l'applet de commande, identifiez la valeur **LicensingIntranetDistributionPointUrl**.

        Par exemple : **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

    3.  À partir de la valeur, supprimez la section **_wmcs/licensing** de cette chaîne. La chaîne restante est l’URL de votre service Azure Rights Management. Dans notre exemple, l’URL du service Azure Rights Management aurait la valeur suivante :

        **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**
        
        Vous pouvez vérifier que vous avez la valeur correcte en exécutant la commande PowerShell suivante :
        
            (Get-AadrmConfiguration).LicensingIntranetDistributionPointUrl -match "https:\/\/[0-9A-Za-z\.-]*" | Out-Null; $matches[0]

-   *\<FQDN_connecteur>* est le nom de l’équilibrage de charge que vous avez défini dans le système DNS pour le connecteur. Par exemple, **rmsconnector.contoso.com**.

-   Utilisez le préfixe HTTPS pour l'URL du connecteur si vous avez configuré le connecteur pour utiliser le protocole HTTPS pour communiquer avec vos serveurs locaux. Pour plus d’informations, consultez la section [Configuration du connecteur RMS pour le protocole HTTPS](install-configure-rms-connector.md#configuring-the-rms-connector-to-use-https) dans les instructions principales. L’URL du service Azure Rights Management utilise toujours HTTPS.


## <a name="exchange-2016-or-exchange-2013-registry-settings"></a>Paramètres de Registre Exchange 2013 ou Exchange 2016

**Chemin du Registre :** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\Activation

**Type :** Reg_SZ

**Valeur :** Par défaut

**Données :** https://*\<URL_votre_locataire>*/_wmcs/certification

---

**Chemin du Registre :** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**Type :** Reg_SZ

**Valeur :** Par défaut

**Données :** https://*\<URL_votre_locataire>*/_wmcs/Licensing

---

**Chemin du Registre :** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\CertificationServerRedirection

**Type :** Reg_SZ

**Valeur :** https://*\<URL_votre_locataire>*


**Données :** L’une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur Exchange et votre connecteur RMS :

- http://*<\FQDN_connecteur>*

- https://*<\FQDN_connecteur>*

---

**Chemin du Registre :** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**Type :** Reg_SZ

**Valeur :** https://*<\URL_votre_locataire>*


**Données :** L’une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur Exchange et votre connecteur RMS :

- http://*<\FQDN_connecteur>*

- https://*<\FQDN_connecteur>*


## <a name="exchange-2010-registry-settings"></a>Paramètres de Registre Exchange 2010

**Chemin du Registre :** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\Activation

**Type :** Reg_SZ

**Valeur :** Par défaut

**Données :** https://*<\URL_votre_locataire>*/_wmcs/certification

---

**Chemin du Registre :** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**Type :** Reg_SZ

**Valeur :** Par défaut

**Données :** https://*<\URL_votre_locataire>*/_wmcs/Licensing

---

**Chemin du Registre :** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\CertificationServerRedirection

**Type :** Reg_SZ

**Valeur :** https://*<\URL_votre_locataire>*

**Données :** L’une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur Exchange et votre connecteur RMS :

- http://*<\FQDN_connecteur>*

- https://*<\FQDN_connecteur>*

---

**Chemin du Registre :** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**Type :** Reg_SZ

**Valeur :** https://*<\URL_votre_locataire>*

**Données :** L’une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur Exchange et votre connecteur RMS :

- http://*<\FQDN_connecteur>*

- https://*<\FQDN_connecteur>*


## <a name="sharepoint-2016-or-sharepoint-2013-registry-settings"></a>Paramètres de Registre SharePoint 2016 ou SharePoint 2013

**Chemin du Registre :** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\LicensingRedirection

**Type :** Reg_SZ

**Valeur :** https://*<\URL_votre_locataire>*/_wmcs/licensing


**Données :** L’une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur SharePoint et le connecteur RMS :

- http://*<\FQDN_connecteur>*/_wmcs/licensing

- https://*<\FQDN_connecteur>*/_wmcs/licensing

---

**Chemin du Registre :** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterpriseCertification

**Type :** Reg_SZ

**Valeur :** Par défaut

**Données :** L’une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur SharePoint et le connecteur RMS :

- http://*<\FQDN_connecteur>*/_wmcs/certification

- https://*<\FQDN_connecteur>*/_wmcs/certification

---

**Chemin du Registre :** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterprisePublishing

**Type :** Reg_SZ

**Valeur :** Par défaut


**Données :** L’une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur SharePoint et le connecteur RMS :

- http://*<\FQDN_connecteur>*/_wmcs/licensing

- https://*<\FQDN_connecteur>*/_wmcs/licensing




## <a name="file-server-and-file-classification-infrastructure-registry-settings"></a>Paramètres de Registre du serveur de fichiers et de l’Infrastructure de classification des fichiers

**Chemin du Registre :** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**Type :** Reg_SZ

**Valeur :** Par défaut

**Données :** http://*</FQDN_connecteur*/_wmcs/licensing

---

**Chemin du Registre :** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation

**Type :** Reg_SZ

**Valeur :** Par défaut

**Données :** http://*</FQDN_connecteur>*/_wmcs/certification


Retour à [Déploiement du connecteur Azure Rights Management](deploy-rms-connector.md)
