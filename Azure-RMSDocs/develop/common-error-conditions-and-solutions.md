---
# required metadata

title: Conditions d’erreur courantes et solutions | Azure RMS
description: Cette rubrique répertorie les messages d’erreur les plus courants susceptibles de s’afficher quand vous utilisez les outils de développement de RMS SDK 2.1.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: A5B95EB8-3528-4CFF-86FC-166613A5F4A3
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
** Ce contenu de SDK n’est pas à jour. Vous trouverez temporairement la [version actuelle](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx) de la documentation sur MSDN. **
# Conditions d’erreur courantes et solutions
Cette rubrique répertorie les messages d’erreur les plus courants susceptibles de s’afficher quand vous utilisez les outils de développement du Kit Rights Management Services SDK 2.1. Le cas échéant, elle fournit également les actions recommandées pour corriger les erreurs.

**Important** : Pour traiter une condition d’erreur, utilisez toujours un appel à [IpcGetErrorMessageText](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgeterrormessagetext) juste après l’échec d’un appel à l’API du SDK pour obtenir des informations complètes sur la nature de l’erreur.

 

## Erreur et action ##
La liste ci-dessous contient une liste de constantes d’erreur, leur description associée et une suggestion d’action pour résoudre la condition d’erreur.

**ERREUR** - *IPCERROR_DEBUGGER_DETECTED* : Un débogueur a été détecté par RMS SDK 2.1

**ACTION** : la version développeur de RMS SDK 2.1 ne vérifie pas la présence d’un débogueur. Si possible, déboguez votre application à l’aide de cette version de RMS SDK 2.1.
Si vous devez déboguer la version de production de RMS SDK 2.1, utilisez les instructions suivantes.

Certaines fonctions de RMS SDK 2.1 sont conçues pour échouer sous un débogueur :
- [IpcGetKey</strong>](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetkey)
- [IpcGetTemplateList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist)
- [IpcGetTemplateIssuerList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplateissuerlist)

Pour déboguer le code situé après ces appels de fonction, vous devez vous introduire dans le processus et attacher un débogueur une fois les appels de fonction terminés. Une façon de vous introduire dans le débogueur consiste à utiliser une instruction Assert. La macro ASSERTE est incluse dans l’en-tête *Crtdbg.h*.
Pour plus d’informations sur \_ASSERTE, consultez [\_ASSERT, \_ASSERTE, macros](https://msdn.microsoft.com/en-us/library/ezb1wyez.aspx)

**ERREUR** - *IPCERROR_BROKEN_CERT_CHAIN* : La chaîne de certificat ne correspond pas.

**ACTION** : vérifiez que la clé de la hiérarchie contient la valeur correcte en fonction de la clé que vous utilisez pour signer votre manifeste d’application AD RMS.
Il s’agit des clés de signature et de leurs valeurs associées (**DWORD** de la hiérarchie) :
- ISV—1
- Production—0 ou non présent

**ERREUR** - *IPCERROR_MACHINE_CERT_NOT_TRUSTED* : Vous utilisez une application signée avec la clé de signature ISV, mais l’application tente de communiquer avec un serveur AD RMS de production ou vice versa.

- Si vous utilisez la version de développement du serveur AD RMS, veillez à utiliser la clé de signature ISV pour signer votre application.
- Si vous utilisez la version de production du serveur AD RMS, veillez à utiliser la clé de signature de production pour signer votre application.

**ERREUR** - *IPCERROR_APPLICATION_AUTH_ERROR_MANIFEST* : Le manifeste d’application n’est pas valide. Cela peut se produire si le manifeste n’a pas été régénéré quand le binaire (application) a été reconstruit.

**ACTION** : Veillez à régénérer votre manifeste d’application chaque fois que vous régénérez votre application.

## Rubriques connexes ##
* [Notes pour les développeurs](developer-notes.md)
* [IpcGetKey](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetkey)
* [IpcGetTemplateList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist)
* [IpcGetTemplateIssuerList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplateissuerlist)
* [\_ASSERT, \_ASSERTE, macros](https://msdn.microsoft.com/en-us/library/ezb1wyez.aspx)
 

 


<!--HONumber=Jun16_HO1-->


