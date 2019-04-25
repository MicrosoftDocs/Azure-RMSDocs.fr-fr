---
title: Azure Information Protection unifiée étiquetage guide de l’administrateur client
description: Instructions et informations destinées aux administrateurs sur un réseau d’entreprise qui sont responsables du déploiement d’Azure Information Protection unifiée étiquetage client pour Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: 7caa35896e0dcfd3cd6dc1cf407da87e41e71ef5
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "60183171"
---
# <a name="azure-information-protection-unified-labeling-client-administrator-guide"></a>Azure Information Protection unifiée étiquetage guide de l’administrateur client

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*
>
> *Instructions pour : [Azure Information Protection unifiée étiquetage client pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Utilisez les informations de ce guide si vous êtes responsable pour Azure Information Protection unifiée étiquetage client sur un réseau d’entreprise, ou si vous souhaitez des informations plus techniques que celles se trouve dans le [Azure Information Protection unifiée de l’étiquetage guide de l’utilisateur client](clientv2-user-guide.md). 

Exemple :

- Comprendre les différents composants de ce client et si vous devez les installer ou non

- Comment installer le client pour les utilisateurs, avec des informations sur les conditions préalables, des options et paramètres d’installation et des contrôles de vérification

- Localiser les fichiers du client et les journaux d’utilisation

- Identifier les types de fichiers pris en charge par le client

- Utiliser le client avec PowerShell pour le contrôle de ligne de commande

**Vous avez une question qui n’est pas traitée dans cette documentation ?** Visitez notre [site Yammer Azure Information Protection](https://www.yammer.com/AskIPTeam). 

## <a name="technical-overview-of-the-azure-information-protection-unified-labeling-client"></a>Vue d’ensemble technique du client Azure Information Protection unifié étiquetage

Le client d’étiquetage unifié Azure Information Protection inclut les éléments suivants :

- Un complément Office, qui installe un **sensibilité** bouton sur le ruban pour les utilisateurs à sélectionner des étiquettes de sensibilité et une option pour afficher la barre Azure Information Protection pour une meilleure visibilité de l’étiquette.

- L’Explorateur de fichiers Windows, avec des options contextuelles permettant aux utilisateurs d’appliquer des étiquettes de classification et la protection aux fichiers.

- Une visionneuse pour afficher les fichiers protégés lorsqu’une application native ne peut pas les ouvrir.

- Un module PowerShell pour appliquer et supprimer des étiquettes de classification et la protection de fichiers. 

- Le client Rights Management qui communique avec le service Azure Rights Management (Azure RMS) pour chiffrer et protéger des fichiers.

À l’exception de la visionneuse, le client d’étiquetage unifié Azure Information Protection ne peut pas être utilisé avec les applications et services qui communiquent directement avec le service Azure Rights Management ou Active Directory Rights Management Services.

Si vous avez AD RMS et que vous souhaitez migrer AD RMS vers Azure Information Protection, consultez [Migration d’AD RMS vers Azure Information Protection](../migrate-from-ad-rms-to-azure-rms.md).


## <a name="should-you-deploy-the-azure-information-protection-unified-labeling-client"></a>Si vous déployez le client d’étiquetage unifié Azure Information Protection ?

Déployer le client d’étiquetage unifié Azure Information Protection si vous utilisez [des étiquettes de sensibilité dans le centre de la conformité et de sécurité Office 365](https://docs.microsoft.com/Office365/SecurityCompliance/sensitivity-labels), et une des options suivantes s’applique :

- Vous souhaitez classifier (et éventuellement protéger) des documents et messages électroniques en sélectionnant des étiquettes à partir de vos applications Office (Word, Excel, PowerPoint, Outlook) sur les ordinateurs Windows.

- Vous souhaitez classifier (et éventuellement protéger) des fichiers à l’aide de l’Explorateur de fichiers, qui prend en charge des types de fichiers supplémentaires que ceux pris en charge par Office, des sélections multiples et des dossiers.

- Vous souhaitez exécuter des scripts qui classifient (et éventuellement protègent) des documents à l’aide de commandes PowerShell.

- Vous souhaitez afficher des documents protégés lorsqu’une application native permettant d’afficher le fichier n’est pas installée ou ne parvient pas à ouvrir ces documents.

Exemple illustrant le bureau de complément pour Azure Information Protection unifiée client étiquetage, affichage de la nouvelle **sensibilité** bouton du ruban et la barre Azure Information Protection facultative :

![Barre Azure Information Protection avec la stratégie par défaut](../media/v2word2016-calloutsv2.png)

## <a name="installing-and-supporting-the-azure-information-protection-unified-labeling-client"></a>L’installation et la prise en charge le client d’étiquetage unifié Azure Information Protection

Vous pouvez installer le client d’étiquetage unifié Azure Information Protection à l’aide d’un fichier exécutable ou un fichier de programme d’installation de Windows. Pour plus d’informations sur chaque option et pour obtenir des instructions, consultez [installer le client étiquetage Azure Information Protection unifié pour les utilisateurs](clientv2-admin-guide-install.md).  

Utilisez les sections suivantes pour plus d’informations sur l’installation du client. 

### <a name="installation-checks-and-troubleshooting"></a>Vérifications et résolution des problèmes liés à l’installation

Quand le client est installé, utilisez l’option **Aide et commentaires** pour ouvrir la boîte de dialogue **Microsoft Azure Information Protection** :

- À partir d’une application Office : Sur le **accueil** sous l’onglet le **sensibilité** groupe, sélectionnez **sensibilité**, puis sélectionnez **aide et commentaires**.

- Depuis l’Explorateur de fichiers : Cliquez avec le bouton droit sur un ou plusieurs fichiers ou sur un dossier, sélectionnez **Classifier et protéger**, puis **Aide et commentaires**. 

#### <a name="help-and-feedback-section"></a>Section **Aide et commentaires**

Le **me dire plus lien** par défaut, va à la [Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection) site Web. Vous pouvez configurer votre propre lien URL qui pointe vers une page d’aide personnalisé comme l’un des paramètres de stratégie dans le centre de la conformité et de sécurité Office 365.

Le **exporter les journaux** automatiquement de collecter et de joindre des fichiers journaux pour Azure Information Protection unifiée étiquetage client si vous avez été invité à envoyer au Support Microsoft. Cette option peut également être utilisée par les utilisateurs finaux pour envoyer ces fichiers journaux à votre support technique.

Le **réinitialiser les paramètres** déconnecte l’utilisateur, supprime les stratégies et les étiquettes de sensibilité actuellement téléchargée et réinitialise les paramètres utilisateur pour le service Azure Rights Management.

##### <a name="more-information-about-the-reset-settings-option"></a>Informations supplémentaires sur l’option Réinitialiser les paramètres

- Il n’est pas obligatoire d’être un administrateur local pour utiliser cette option, et cette action n’est pas enregistrée dans l’Observateur d’événements. 

- Sauf si des fichiers sont verrouillés, cette action supprime tous les fichiers dans les emplacements suivants. Ces fichiers incluent des certificats clients, les modèles Rights Management, les étiquettes de sensibilité et stratégies à partir de la sécurité et Office 365 & centre de conformité, les informations d’identification utilisateur mis en cache. Les fichiers journaux clients ne sont pas supprimés.
    
    - %LocalAppData%\Microsoft\DRM
    
    - %LocalAppData%\Microsoft\MSIPC
    
    - %LocalAppData%\Microsoft\MSIP\Policy.msip
    
    - %LocalAppData%\Microsoft\MSIP\TokenCache

- Les clés de Registre et les paramètres suivants sont supprimés. Si les paramètres d’une de ces clés de Registre ont des valeurs personnalisées, ils doivent être reconfigurés après la réinitialisation du client. 
    
    En général, pour les réseaux d’entreprise, ces paramètres sont configurés à l’aide de la stratégie de groupe, auquel cas ils sont automatiquement réappliqués lorsque la stratégie de groupe est actualisée sur l’ordinateur. Par contre, certains paramètres peuvent avoir été configurés ponctuellement, par le biais d’un script ou manuellement. Dans ce cas, vous devez prendre des mesures supplémentaires pour reconfigurer ces paramètres. Par exemple, les ordinateurs peuvent exécuter un script ponctuellement afin de configurer des paramètres pour une redirection vers Azure Information Protection, car vous procédez à la migration depuis AD RMS et vous disposez toujours d’un point de connexion de service sur votre réseau. Après la réinitialisation du client, l’ordinateur doit réexécuter ce script.
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\15.0\Common\Identity
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\14.0\Common\DRM
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\15.0\Common\DRM
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\16.0\Common\DRM
    
    - HKEY_CURRENT-USER\SOFTWARE\Classes\Local Settings\Software\Microsoft\MSIPC    

- L’utilisateur actuellement connecté est déconnecté.

#### <a name="client-status-section"></a>Section **État du client**

Utilisez la valeur **Connecté en tant que** pour confirmer que le nom d’utilisateur affiché identifie le compte à utiliser pour l’authentification avec Azure Information Protection. Ce nom d’utilisateur doit correspondre à un compte que vous utilisez pour Office 365 ou Azure Active Directory. Le compte doit également appartenir à un client Office 365 qui est configuré pour les étiquettes de sensibilité dans le centre de la conformité et de sécurité Office 365.

Si vous devez vous connecter avec un utilisateur différent de celui qui est affiché, consultez le [connectez-vous en tant qu’autre utilisateur](clientv2-admin-guide-customizations.md#sign-in-as-a-different-user) obtenir des instructions.

Utilisez l’information **Version** pour vérifier la version installée sur le client. Vous pouvez vérifier s’il s’agit de la dernière version et les correctifs correspondants et les nouvelles fonctionnalités de la version en lisant le [informations sur la Version release](unifiedlabelingclient-version-release-history.md) pour le client.

## <a name="support-for-multiple-languages"></a>Prise en charge de plusieurs langues

Le client d’étiquetage unifié Azure Information Protection prend en charge les mêmes langues que Office 365 prend en charge. Pour obtenir la liste de ces langues, consultez la section **Office 365, Exchange Online Protection et Power BI** dans la page [Disponibilité internationale](https://products.office.com/business/international-availability) des produits Office.

Pour ces langues, les options de menu, les boîtes de dialogue et les messages à partir d’Azure Information Protection client étiquetage unifié afficher dans la langue de l’utilisateur. Il existe un programme d’installation unique qui détecte la langue, par conséquent, aucune configuration supplémentaire n’est requise pour installer le client étiquetage unifié d’Azure Information Protection pour des langues différentes. 

Toutefois, client Azure Information Protection unifié étiquetage ne prend pas en charge différentes langues pour les étiquettes. En outre, les marquages visuels ne sont pas traduits et ne prennent pas en charge plusieurs langues.

## <a name="post-installation-tasks"></a>Tâches post-installation

Une fois que vous avez installé le client d’étiquetage unifié Azure Information Protection, assurez-vous que vous donnez des instructions aux utilisateurs pour savoir comment étiqueter leurs e-mails et documents et des conseils pour les étiquettes à choisir pour des scénarios spécifiques. Exemple :

- Instructions en ligne pour l’utilisateur : [Azure Information Protection - Guide de l’utilisateur](client-user-guide.md)

- Téléchargez un guide d’utilisation personnalisable : [Azure Information Protection End User Adoption Guide](https://download.microsoft.com/download/7/1/2/712A280C-1C66-4EF9-8DC3-88EE43BEA3D4/Azure_Information_Protection_End_User_Adoption_Guide_EN_US.pdf)

## <a name="upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client"></a>La mise à niveau et la gestion de client Azure Information Protection unifié étiquetage

> [!NOTE]
> Azure Information Protection unifiée étiquetage client prend en charge la mise à niveau le client Azure Information Protection, ainsi que la mise à niveau à partir de versions précédentes du client Azure Information Protection unifiée étiquetage.

L’équipe Azure Information Protection met régulièrement à jour le client étiquetage Azure Information Protection unifié pour les nouvelles fonctionnalités et les correctifs. Les annonces sont postées sur le [site Yammer](https://www.yammer.com/AskIPTeam) de l’équipe.

Si vous utilisez Windows Update, le client d’étiquetage unifié Azure Information Protection pour Azure Information Protection met automatiquement à niveau la version disponibilité générale de ce client, quel que soit la façon dont le client a été installé. Les nouvelles versions de client sont publiées dans le catalogue quelques semaines après le lancement.

Vous pouvez également mettre à niveau manuellement le client en téléchargeant la nouvelle version à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). Installez ensuite la nouvelle version pour mettre à niveau le client. Vous devez utiliser cette méthode pour mettre à niveau les versions préliminaires et si vous mettez à niveau le client Azure Information Protection.

Lorsque vous mettez à niveau manuellement, ne désinstallez la version précédente que si vous changez de méthode d’installation. Par exemple, si vous passez de la version du fichier exécutable (.exe) du client à la version du programme d’installation (.msi) Windows du client. Ou si vous devez installer une version antérieure du client. Par exemple, vous avez installé la préversion actuelle pour la tester et vous devez maintenant revenir à la version actuelle en disponibilité générale.

Utilisez le [Version release historique et politique du support](unifiedlabelingclient-version-release-history.md) pour comprendre la politique de support pour Azure Information Protection unifiée étiquetage client, les versions sont actuellement pris en charge, et ce qui est nouvelles et modifiées pour la prise en charge versions. 

## <a name="uninstalling-the-azure-information-protection-unified-labeling-client"></a>Désinstallation d’Azure Information Protection unifiée étiquetage client

Vous pouvez utiliser l’une des options suivantes pour désinstaller le client :

- Utiliser le Panneau de configuration pour désinstaller un programme : Cliquez sur **Microsoft Azure Information Protection** > **Désinstaller**

- Réexécutez le fichier exécutable (par exemple, **AzInfoProtection_UL.exe**) et à partir de la **modifier l’installation** , cliquez sur **désinstallation**. 

- Exécutez le fichier exécutable avec **/uninstall**. Par exemple : `AzInfoProtection.exe /uninstall`

## <a name="next-steps"></a>Étapes suivantes
Pour installer le client, consultez [installer le client étiquetage Azure Information Protection unifié pour les utilisateurs](clientv2-admin-guide-install.md).

Si vous avez déjà installé le client, consultez les informations supplémentaires suivantes sur la prise en charge de ce client :

- [Customizations](clientv2-admin-guide-customizations.md)

- [Fichiers du client et journalisation de l’utilisation](client-admin-guide-files-and-logging.md)

- [Types de fichier pris en charge](client-admin-guide-file-types.md)

- [Commandes PowerShell](client-admin-guide-powershell.md)


