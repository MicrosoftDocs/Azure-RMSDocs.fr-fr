---
title: Configurations personnalisées-client Azure Information Protection
description: Informations sur la personnalisation du client Azure Information Protection pour Windows.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/06/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.subservice: v1client
ms.reviewer: maayan
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 8f1c4ef83d7e7b34cf0e7c854da203b4e6b1696e
ms.sourcegitcommit: 3b50727cb50a612b12f248a5d18b00175aa775f7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/08/2020
ms.locfileid: "75743735"
---
# <a name="admin-guide-custom-configurations-for-the-azure-information-protection-client"></a>Guide de l’administrateur : Configurations personnalisées pour le client Azure Information Protection

>*S’applique à : services AD RMS (Active Directory Rights Management Services), [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1, windows server 2019, windows server 2016, windows server 2012 R2, windows server 2012, windows Server 2008 R2*
>
> *Instructions pour : [Azure information protection client pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Utilisez les informations suivantes pour les configurations avancées nécessaires dont vous pourrez avoir besoin pour des scénarios spécifiques, ou pour un sous-ensemble d’utilisateurs lorsque vous gérez le client Azure Information Protection.

Certains de ces paramètres nécessitent une modification du Registre, et certains autres utilisent des paramètres avancés que vous devez configurer dans le portail Azure, puis publier pour les clients à télécharger.  

### <a name="how-to-configure-advanced-client-configuration-settings-in-the-portal"></a>Comment configurer les paramètres avancés de configuration du client dans le portail

1. Si vous ne l’avez pas déjà fait, dans une nouvelle fenêtre de navigateur, [Connectez-vous au portail Azure](../configure-policy.md#signing-in-to-the-azure-portal), puis accédez au volet de **Azure information protection** .

2. À partir de l’option de menu **Classifications** > **Étiquettes** : sélectionnez **Stratégies**.

3. Dans le volet **Azure information protection-stratégies** , sélectionnez le menu contextuel ( **...** ) en regard de la stratégie pour contenir les paramètres avancés. Ensuite, sélectionnez **Paramètres avancés**.
    
    Vous pouvez configurer des paramètres avancés pour la stratégie globale et pour les stratégies étendues.

4. Dans le volet **Paramètres avancés** , tapez le nom et la valeur du paramètre avancé, puis sélectionnez **enregistrer et fermer**.

5. Assurez-vous que les utilisateurs de cette stratégie redémarrent toutes les applications Office qu’ils avaient ouvertes.

6. Si vous n’avez plus besoin du paramètre et souhaitez rétablir le comportement par défaut : dans le volet **Paramètres avancés** , sélectionnez le menu contextuel ( **...** ) en regard du paramètre dont vous n’avez plus besoin, puis sélectionnez **supprimer**. Ensuite, cliquez sur **Enregistrer et fermer**.

#### <a name="available-advanced-client-settings"></a>Paramètres client avancés disponibles

|Paramètre|Scénario et instructions|
|----------------|---------------|
|DisableDNF|[Masquer ou afficher le bouton Ne pas transférer dans Outlook](#hide-or-show-the-do-not-forward-button-in-outlook)|
|DisableMandatoryInOutlook|[Exempter les messages Outlook de l’étiquetage obligatoire](#exempt-outlook-messages-from-mandatory-labeling)|
|CompareSubLabelsInAttachmentAction|[Activer la prise en charge de l’ordre des sous-étiquettes](#enable-order-support-for-sublabels-on-attachments) 
|ContentExtractionTimeout|[Modifier les paramètres de délai d’attente pour le scanneur](#change-the-timeout-settings-for-the-scanner)
|EnableBarHiding|[Masquer définitivement la barre Azure Information Protection](#permanently-hide-the-azure-information-protection-bar)|
|EnableCustomPermissions|[Activer ou désactiver les options d’autorisations personnalisées pour les utilisateurs](#make-the-custom-permissions-options-available-or-unavailable-to-users)|
|EnableCustomPermissionsForCustomProtectedFiles|[Pour les fichiers protégés avec des autorisations personnalisées, toujours afficher des autorisations personnalisées pour les utilisateurs dans l’Explorateur de fichiers](#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer) |
|EnablePDFv2Protection|[Ne pas protéger les fichiers PDF suivant la norme ISO pour le chiffrement PDF](#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)|
|FileProcessingTimeout|[Modifier les paramètres de délai d’attente pour le scanneur](#change-the-timeout-settings-for-the-scanner)
|LabelbyCustomProperty|[Migrer des étiquettes de Secure Islands et autres solutions d’étiquetage](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|LabelToSMIME|[Configurer une étiquette pour appliquer la protection S/MIME dans Outlook](#configure-a-label-to-apply-smime-protection-in-outlook)|
|LogLevel|[Modifier le niveau de journalisation local](#change-the-local-logging-level)
|LogMatchedContent|[Désactiver l’envoi de correspondances de types d’informations pour un sous-ensemble d’utilisateurs](#disable-sending-information-type-matches-for-a-subset-of-users)|
|OutlookBlockTrustedDomains|[Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookBlockUntrustedCollaborationLabel|[Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookDefaultLabel|[Définir une autre étiquette par défaut pour Outlook](#set-a-different-default-label-for-outlook)|
|OutlookJustifyTrustedDomains|[Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookJustifyUntrustedCollaborationLabel|[Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookRecommendationEnabled|[Activer la classification recommandée dans Outlook](#enable-recommended-classification-in-outlook)|
|OutlookOverrideUnlabeledCollaborationExtensions|[Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior|[Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookWarnTrustedDomains|[Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookWarnUntrustedCollaborationLabel|[Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|PostponeMandatoryBeforeSave|[Supprimer « Pas maintenant » pour les documents quand l’étiquetage obligatoire est utilisé](#remove-not-now-for-documents-when-you-use-mandatory-labeling)|
|ProcessUsingLowIntegrity|[Désactiver le niveau d’intégrité faible pour le scanneur](#disable-the-low-integrity-level-for-the-scanner)|
|PullPolicy|[Prendre en charge les ordinateurs déconnectés](#support-for-disconnected-computers)
|RemoveExternalContentMarkingInApp|[Supprimer les en-têtes et les pieds de page d’autres solutions d’étiquetage](#remove-headers-and-footers-from-other-labeling-solutions)|
|ReportAnIssueLink|[Ajouter « Signaler un problème » pour les utilisateurs](#add-report-an-issue-for-users)|
|RunAuditInformationTypesDiscovery|[Désactiver l’envoi d’informations sensibles découvertes dans des documents à Azure Information Protection Analytics](#disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics)|
|RunPolicyInBackground|[Activer la classification pour qu’elle s’exécute en continu en arrière-plan](#turn-on-classification-to-run-continuously-in-the-background)|
|ScannerConcurrencyLevel|[Limiter le nombre de threads utilisés par le scanneur](#limit-the-number-of-threads-used-by-the-scanner)|
|SyncPropertyName|[Étiqueter un document Office en utilisant une propriété personnalisée existante](#label-an-office-document-by-using-an-existing-custom-property)|
|SyncPropertyState|[Étiqueter un document Office en utilisant une propriété personnalisée existante](#label-an-office-document-by-using-an-existing-custom-property)|

## <a name="prevent-sign-in-prompts-for-ad-rms-only-computers"></a>Empêcher l’affichage des invites de connexion sur les ordinateurs AD RMS uniquement

Par défaut, le client Azure Information Protection tente automatiquement de se connecter au service Azure Information Protection. Pour les ordinateurs qui communiquent uniquement avec AD RMS, cette configuration peut entraîner inutilement l’affichage d’une invite de connexion pour les utilisateurs. Vous pouvez empêcher l’affichage de cette invite de connexion en modifiant le Registre.

 - Recherchez le nom de valeur suivant et définissez la valeur à **0** :
    
    **HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

Indépendamment de ce paramètre, le client Azure Information Protection se conforme au [processus de découverte du service RMS](client-deployment-notes.md#rms-service-discovery) pour trouver son cluster AD RMS.

## <a name="sign-in-as-a-different-user"></a>Se connecter avec l’identité d’un autre utilisateur

Dans un environnement de production, les utilisateurs ne doivent généralement pas se connecter sous un autre nom lorsqu’ils utilisent le client Azure Information Protection. Toutefois, en tant qu’administrateur, vous devrez peut-être vous connecter sous un autre nom d’utilisateur pendant une phase de test. 

Vous pouvez vérifier le compte auquel vous êtes actuellement connecté à l’aide de la boîte de dialogue **Microsoft Azure Information Protection** : ouvrez une application Office et, dans l’onglet **Accueil**, dans le groupe **Protection**, cliquez sur **Protéger**, puis sur **Aide et commentaires**. Votre nom de votre compte s’affiche dans la section **État du client**.

Pensez à vérifier le nom de domaine du compte connecté. En effet, vous pouvez accidentellement vous connecter avec le bon nom de compte, mais avec le mauvais domaine. Vous pouvez vous apercevoir que vous utilisez le mauvais compte en cas d’échec du téléchargement de la stratégie Azure Information Protection ou si vous ne voyez pas les étiquettes ou le comportement auxquels vous vous attendez.

Pour se connecter avec l’identité d’un autre utilisateur :

1. Accédez à **%localappdata%\Microsoft\MSIP** et supprimez le fichier **TokenCache**.

2. Redémarrez les applications Office ouvertes et connectez-vous avec votre autre compte d’utilisateur. Si l’invite de connexion au service Azure Information Protection n’apparaît pas dans votre application Office, revenez à la boîte de dialogue **Microsoft Azure Information Protection** et cliquez sur **Connexion** depuis la section mise à jour **État du Client**.

En outre :

- Si le client Azure Information Protection est toujours connecté avec l’ancien compte après avoir effectué ces étapes, supprimez tous les cookies à partir d’Internet Explorer et répétez les étapes 1 et 2.

- Si vous utilisez l’authentification unique, vous devrez vous déconnecter de Windows et vous reconnecter avec votre autre compte d’utilisateur après avoir supprimé le fichier de jeton. Le client Azure Information Protection peut alors vous authentifier automatiquement à l’aide du compte d’utilisateur connecté à ce moment-là.

- Cette solution prend en charge la connexion sous un nom d’utilisateur différent à partir du même locataire. Elle ne prend en pas charge la connexion sous un nom d’utilisateur différent à partir d’un autre locataire. Pour tester Azure Information Protection avec plusieurs locataires, utilisez des ordinateurs différents.

- Vous pouvez utiliser l’option **Réinitialiser les paramètres** dans **Aide et commentaires** pour vous déconnecter et supprimer la stratégie Azure Information Protection téléchargée.


## <a name="enforce-protection-only-mode-when-your-organization-has-a-mix-of-licenses"></a>Appliquer le mode Protection uniquement si votre organisation possède différents types de licences

Si votre organisation n’a pas de licences pour Azure Information Protection, mais a des licences pour Office 365 qui incluent le service Azure Rights Management pour la protection des données, le client Azure Information Protection pour Windows s’exécute automatiquement en mode [Protection uniquement](client-protection-only-mode.md).

Toutefois, si votre organisation a un abonnement à Azure Information Protection, tous les ordinateurs Windows peuvent, par défaut, télécharger la stratégie Azure Information Protection. Le client Azure Information Protection ne procède pas à la vérification et l’application de la licence. 

Si certains utilisateurs n’ont pas de licence pour Azure Information Protection, mais une licence pour Office 365 qui inclut le service Azure Rights Management, modifiez le Registre sur les ordinateurs de ces utilisateurs pour les empêcher d’exécuter les fonctionnalités de classification et d’étiquetage non autorisées par leur licence depuis Azure Information Protection.

Recherchez le nom de la valeur suivant et définissez les données de la valeur sur **0** :

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

Vérifiez par ailleurs que ces ordinateurs n’ont pas de fichier nommé **Policy.msip** dans le dossier **%LocalAppData%\Microsoft\MSIP**. S’il existe, supprimez-le. Ce fichier contient la stratégie Azure Information Protection et peut avoir été téléchargé avant que vous n’ayez modifié le Registre ou si le client Azure Information Protection a été installé avec l’option de démonstration.

## <a name="add-report-an-issue-for-users"></a>Ajouter « Signaler un problème » pour les utilisateurs

Cette configuration utilise un [paramètre client avancé](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que vous devez configurer dans le portail Azure. 

Quand vous spécifiez le paramètre client avancé suivant, les utilisateurs voient une option **Signaler un problème** qu’ils peuvent sélectionner dans la boîte de dialogue **Aide et commentaires** du client. Spécifiez une chaîne HTTP pour le lien. (par exemple, une page web personnalisée permettant aux utilisateurs de signaler des problèmes, ou une adresse e-mail qui pointe vers votre support technique). 

Pour configurer ce paramètre avancé, entrez les chaînes suivantes :

- Clé : **ReportAnIssueLink**

- Valeur : **\<chaîne HTTP >**

Exemple de valeur pour un site web : `https://support.contoso.com`

Exemple de valeur pour une adresse e-mail : `mailto:helpdesk@contoso.com`

## <a name="hide-the-classify-and-protect-menu-option-in-windows-file-explorer"></a>Masquer l’option de menu Classifier et protéger dans l’Explorateur de fichiers Windows

Créez le nom de la valeur DWORD suivant (avec toutes données de la valeur) :

**HKEY_CLASSES_ROOT\AllFilesystemObjects\shell\Microsoft.Azip.RightClick\LegacyDisable**

## <a name="support-for-disconnected-computers"></a>Prise en charge des ordinateurs déconnectés

Par défaut, le client Azure Information Protection tente automatiquement de se connecter au service Azure Information Protection pour télécharger la dernière stratégie Azure Information Protection. Si vous avez des ordinateurs dont vous savez qu’ils ne seront pas en mesure de se connecter à Internet pendant un certain temps, vous pouvez empêcher le client d’essayer de se connecter au service en modifiant le registre. 

Notez que sans connexion Internet, le client ne peut pas appliquer la protection (ou supprimer la protection) à l’aide de la clé basée sur le Cloud de votre organisation. Il ne peut qu’utiliser les étiquettes qui appliquent seulement la classification, ou la protection qui utilise [HYOK](../configure-adrms-restrictions.md).

Vous pouvez empêcher l’affichage d’une invite de connexion au service Azure Information Protection soit en utilisant un [paramètre client avancé](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que vous devez configurer sur le Portail Azure, puis en téléchargeant la stratégie pour les ordinateurs, soit en modifiant le Registre.

- Pour configurer le paramètre client avancé :
    
    1. Entrez les chaînes suivantes :
    
        - Clé : **PullPolicy**
        
        - Valeur : **False**
    
    2. Téléchargez la stratégie avec ce paramètre et installez-la sur les ordinateurs en suivant les instructions ci-dessous.

- Autre possibilité, modifiez le Registre :
    
    - Recherchez le nom de valeur suivant et définissez la valeur à **0** :
    
        **HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 


Le client doit avoir un fichier de stratégie valide nommé **Policy.msip**, dans le dossier **%LocalAppData%\Microsoft\MSIP**.

Vous pouvez exporter la stratégie globale ou une stratégie délimitée à partir du Portail Azure, puis copier le fichier exporté sur l’ordinateur client. Vous pouvez également suivre cette méthode pour remplacer un fichier de stratégie obsolète par la dernière stratégie. Toutefois, l’exportation de la stratégie ne prend pas en charge le scénario où un utilisateur appartient à plusieurs stratégies délimitées. Sachez également que si les utilisateurs sélectionnent l’option **Réinitialiser les paramètres** dans [Aide et commentaires](client-admin-guide.md#help-and-feedback-section), cette action supprime le fichier de stratégie et empêche le client de fonctionner jusqu’à ce que vous remplaciez manuellement le fichier de stratégie ou que le client se connecte au service pour télécharger la stratégie.

Lorsque vous exportez la stratégie à partir du portail Azure, un fichier compressé est téléchargé qui contient plusieurs versions de la stratégie. Ces versions de la stratégie correspondent à différentes versions du client Azure Information Protection :

1. Décompressez le fichier et utilisez le tableau suivant pour identifier le fichier de stratégie dont vous avez besoin. 
    
    |Nom du fichier|Version du client correspondante|
    |--------------------------|---------------------------------------------|
    |Policy1.1.msip |version 1.2|
    |Policy1.2.msip |version 1.3 - 1.7|
    |Policy1.3.msip |version 1.8 - 1.29|
    |Policy1.4.msip |version 1.32 et ultérieure|
    
2. Renommez le fichier identifié en **Policy.msip** et copiez-le dans le dossier **%LocalAppData%\Microsoft\MSIP** sur les ordinateurs où le client Azure Information Protection est installé. 

Si votre ordinateur déconnecté exécute la version GA actuelle du scanneur Azure Information Protection, vous devez effectuer des étapes de configuration supplémentaires. Pour plus d’informations, voir [restriction : le serveur du scanneur ne peut pas disposer d’une connexion Internet](../deploy-aip-scanner.md#restriction-the-scanner-server-cannot-have-internet-connectivity) à partir des instructions de déploiement de l’analyseur.

## <a name="hide-or-show-the-do-not-forward-button-in-outlook"></a>Masquer ou afficher le bouton Ne pas transférer dans Outlook

La méthode recommandée pour configurer cette option consiste à utiliser le [paramètre de stratégie](../configure-policy-settings.md) **Ajouter le bouton ne pas transférer au ruban Outlook**. Cela dit, vous pouvez également configurer cette option en utilisant un [paramètre client avancé](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que vous configurez dans le portail Azure.

Lorsque vous configurez ce paramètre, celui-ci masque ou affiche le bouton **Ne pas transférer** dans le ruban Outlook. Ce paramètre n’a aucun effet sur l’option Ne pas transférer à partir des menus Office.

Pour configurer ce paramètre avancé, entrez les chaînes suivantes :

- Clé : **DisableDNF**

- Valeur : **True** pour masquer le bouton, ou **False** pour afficher le bouton

## <a name="make-the-custom-permissions-options-available-or-unavailable-to-users"></a>Activer ou désactiver les options d’autorisations personnalisées pour les utilisateurs

La méthode recommandée pour configurer cette option consiste à utiliser le [paramètre de stratégie](../configure-policy-settings.md) **rendre l’option des autorisations personnalisées disponible pour les utilisateurs**. Cela dit, vous pouvez également configurer cette option en utilisant un [paramètre client avancé](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que vous configurez dans le portail Azure. 

Lorsque vous configurez ce paramètre et que vous publiez la stratégie pour les utilisateurs, les options des autorisations personnalisées deviennent visibles pour les utilisateurs qui peuvent ainsi sélectionner leurs propres paramètres de protection, ou sont masquées pour ne pas que les utilisateurs puissent sélectionner leurs propres paramètres de protection à moins d’y être invités.

Pour configurer ce paramètre avancé, entrez les chaînes suivantes :

- Clé : **EnableCustomPermissions**

- Valeur : **True** pour rendre l’option des autorisations personnalisées visible, ou **False** pour masquer cette option

## <a name="for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer"></a>Pour les fichiers protégés avec des autorisations personnalisées, toujours afficher des autorisations personnalisées aux utilisateurs dans l’Explorateur de fichiers

Cette configuration utilise un [paramètre client avancé](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que vous devez configurer dans le portail Azure. Ce paramètre est en préversion et est susceptible de changer.

Quand vous configurez le [paramètre de stratégie](../configure-policy-settings.md) **rendre l’option des autorisations personnalisées disponible pour les utilisateurs** ou le paramètre client avancé équivalent dans la section précédente, les utilisateurs ne peuvent pas afficher ou modifier les autorisations personnalisées qui sont déjà définies dans un document protégé. 

Quand vous créez et que vous configurez ce paramètre client avancé, les utilisateurs peuvent voir et changer les autorisations personnalisées pour un document protégé quand ils utilisent l’Explorateur de fichiers, en cliquant avec le bouton droit sur le fichier. L’option **Autorisations personnalisées** du bouton **Protéger** sur le ruban Office reste masquée.

Pour configurer ce paramètre avancé, entrez les chaînes suivantes :

- Clé : **EnableCustomPermissionsForCustomProtectedFiles**

- Valeur : **True**

## <a name="permanently-hide-the-azure-information-protection-bar"></a>Masquer définitivement la barre Azure Information Protection

Cette configuration utilise un [paramètre client avancé](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que vous devez configurer dans le portail Azure. Utilisez-le uniquement lorsque le [paramètre de stratégie](../configure-policy-settings.md) **afficher la barre d’information protection dans applications Office** est défini **sur activé**.

Par défaut, si un utilisateur efface l’option **Afficher la barre** de l’onglet **Accueil**, le groupe **Protection** et le bouton **Protéger**, la barre Information Protection ne s’affiche plus dans cette application Office. Toutefois, la barre réapparaît automatiquement la prochaine fois qu’une application Office s’ouvre.

Pour empêcher la barre de réapparaître automatiquement une fois que l’utilisateur a choisi de la masquer, utilisez ce paramètre client. Ce paramètre n’a aucun effet si l’utilisateur ferme la barre à l’aide de l’icône **Fermer cette barre**.

Même si la barre Azure Information Protection reste masquée, les utilisateurs peuvent encore sélectionner une étiquette dans une barre qui s’affiche temporairement si vous avez configuré la classification recommandée ou si un document ou un e-mail doit avoir une étiquette. 

Pour configurer ce paramètre avancé, entrez les chaînes suivantes :

- Clé : **EnableBarHiding**

- Valeur : **True**

## <a name="enable-order-support-for-sublabels-on-attachments"></a>Activer la prise en charge de l’ordre des sous-étiquettes sur les pièces jointes

Cette configuration utilise un [paramètre client avancé](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que vous devez configurer dans le portail Azure.

Utilisez ce paramètre lorsque vous avez sous-étiquettes et que vous avez configuré le [paramètre de stratégie](../configure-policy-settings.md) suivant :

- **Pour les e-mails avec pièces jointes, appliquez une étiquette correspondant à la classification la plus élevée de ces pièces jointes**

Configurez les chaînes suivantes :

- Clé : **CompareSubLabelsInAttachmentAction**

- Valeur : **True**

Sans ce paramètre, la première étiquette trouvée dans l’étiquette parente avec la classification la plus élevée est appliquée à l’e-mail. 

Avec ce paramètre, la sous-étiquette classée en dernier à partir de l’étiquette parente avec la classification la plus élevée est appliquée à l’e-mail. Si vous avez besoin réorganiser vos étiquettes pour appliquer l’étiquette que vous souhaitez pour ce scénario, consultez [Comment supprimer ou réorganiser une étiquette pour Azure Information Protection](../configure-policy-delete-reorder.md).

## <a name="exempt-outlook-messages-from-mandatory-labeling"></a>Exempter les messages Outlook de l’étiquetage obligatoire

Cette configuration utilise un [paramètre client avancé](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que vous devez configurer dans le portail Azure.

Par défaut, lorsque vous activez le [paramètre de stratégie](../configure-policy-settings.md) , **tous les documents et e-mails doivent avoir une étiquette**, tous les documents enregistrés et les e-mails envoyés doivent avoir une étiquette appliquée. Quand vous configurez le paramètre avancé suivant, le paramètre de stratégie s’applique uniquement aux documents Office et non aux messages Outlook.

Pour configurer ce paramètre avancé, entrez les chaînes suivantes :

- Clé : **DisableMandatoryInOutlook**

- Valeur : **True**

## <a name="enable-recommended-classification-in-outlook"></a>Activer la classification recommandée dans Outlook

Cette configuration utilise un [paramètre client avancé](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que vous devez configurer dans le portail Azure. Ce paramètre est en préversion et est susceptible de changer.

Quand vous configurez une étiquette pour la classification recommandée, les utilisateurs sont invités à accepter ou ignorer l’étiquette recommandée dans Word, Excel et PowerPoint. Ce paramètre affiche également cette recommandation d’étiquette dans Outlook.

Pour configurer ce paramètre avancé, entrez les chaînes suivantes :

- Clé : **OutlookRecommendationEnabled**

- Valeur : **True**


## <a name="implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent"></a>Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails

Cette configuration utilise plusieurs [paramètres clients avancés](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que vous devez configurer dans le portail Azure.

Quand vous créez et que vous configurez les paramètres client avancés suivants, les utilisateurs voient des messages contextuels dans Outlook qui peuvent les avertir avant d’envoyer un e-mail, leur demander de justifier la raison pour laquelle ils envoient un e-mail ou les empêcher d’envoyer un e-mail pour un des scénarios suivants :

- **Leur e-mail ou la pièce jointe à leur e-mail a une étiquette spécifique** :
    - La pièce jointe peut être n’importe quel type de fichier

- **Leur e-mail ou leur pièce jointe à l’e-mail n’a pas d’étiquette** :
    - La pièce jointe peut être un document Office ou un document PDF

Lorsque ces conditions sont remplies, l’utilisateur voit un message contextuel avec l’une des actions suivantes :

- **WARN**: l’utilisateur peut confirmer et envoyer, ou annuler.

- **Justify**: l’utilisateur est invité à fournir une justification (options prédéfinies ou forme libre).  L’utilisateur peut ensuite envoyer ou annuler l’e-mail. Le texte de la justification est écrit dans l’en-tête X de l’e-mail afin qu’il puisse être lu par d’autres systèmes, par exemple des services de protection contre la perte de données.

- **Bloquer**: l’utilisateur ne peut pas envoyer l’e-mail tant que la condition est conservée. Le message contient la raison du blocage de l’e-mail pour que l’utilisateur puisse résoudre le problème, par exemple supprimer des destinataires spécifiques ou appliquer une étiquette à l’e-mail. 

Quand les messages contextuels concernent une étiquette spécifique, vous pouvez configurer des exceptions pour les destinataires par nom de domaine.

Les actions résultantes des messages contextuels sont consignées dans le journal des événements Windows local **journaux des applications et des Services** > **Azure information protection**:

- Messages d’avertissement : ID d’informations 301

- Justification des messages : ID d’informations 302

- Bloquer les messages : ID d’informations 303

Exemple d’entrée événement d’un message de justification :

```
Client Version: 1.53.10.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Price list.msg
Item Name: Price list
Process Name: OUTLOOK
Action: Justify
User Justification: My manager approved sharing of this content
Action Source: 
User Response: Confirmed
```
Les sections suivantes contiennent des instructions de configuration pour chaque paramètre de client avancé. vous pouvez les voir en action pour vous-même avec [le didacticiel : configurer Azure information protection pour contrôler le surPartage des informations à l’aide d’Outlook](../infoprotect-oversharing-tutorial.md).

### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-specific-labels"></a>Pour implémenter des messages d’avertissement, de justification ou de blocage pour des étiquettes spécifiques :

Pour implémenter les messages contextuels pour des étiquettes spécifiques, vous devez connaître l’ID d’étiquette pour ces étiquettes. La valeur ID de l’étiquette s’affiche dans le volet **étiquette** , lorsque vous affichez ou configurez la stratégie de Azure information protection dans le portail Azure. Pour les fichiers auxquels des étiquettes sont appliquées, vous pouvez également exécuter l’applet de commande PowerShell [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) pour identifier l’ID de l’étiquette (MainLabelId ou SubLabelId). Si une étiquette a des sous-étiquettes, spécifiez toujours l’ID de la sous-étiquette et non celui de l’étiquette parente.

Créez un ou plusieurs des paramètres client avancés avec les clés suivantes. Pour les valeurs, spécifiez une ou plusieurs étiquettes en utilisant leur ID, chacun d’eux séparé par une virgule.

Exemple de valeur pour plusieurs ID d’étiquette sous forme de chaîne séparée par des virgules : `dcf781ba-727f-4860-b3c1-73479e31912b,1ace2cc3-14bc-4142-9125-bf946a70542c,3e9df74d-3168-48af-8b11-037e3021813f`


- Messages d’avertissement :
    
    - Clé : **OutlookWarnUntrustedCollaborationLabel**
    
    - Valeur : \<**ID d’étiquette séparés par des virgules**>

- Messages de justification :
    
    - Clé : **OutlookJustifyUntrustedCollaborationLabel**
    
    - Valeur : \<**ID d’étiquette séparés par des virgules**>

- Messages de blocage :
    
    - Clé : **OutlookBlockUntrustedCollaborationLabel**
    
    - Valeur : \<**ID d’étiquette séparés par des virgules**>

#### <a name="to-exempt-domain-names-for-pop-up-messages-configured-for-specific-labels"></a>Pour exempter les noms de domaine pour les messages contextuels configurés pour des étiquettes spécifiques

Pour les étiquettes que vous avez spécifiées avec ces messages contextuels, vous pouvez exempter des noms de domaine spécifiques afin que les utilisateurs ne voient pas les messages pour les destinataires qui ont ce nom de domaine inclus dans leur adresse de messagerie. Dans ce cas, les e-mails sont envoyés sans qu’un message interrompe le processus. Pour spécifier plusieurs domaines, ajoutez-les sous la forme d’une seule chaîne, en les séparant par des virgules.

Une configuration typique consiste à afficher les messages contextuels seulement pour les destinataires qui sont externes à votre organisation ou qui ne sont pas des partenaires autorisés de votre organisation. Dans ce cas, vous spécifiez tous les domaines de messagerie utilisés par votre organisation et par vos partenaires.

Créez les paramètres client avancés suivants et, pour la valeur, spécifiez un ou plusieurs domaines, chacun séparé par une virgule.

Exemple de valeur pour plusieurs domaines sous forme de chaîne séparée par des virgules : `contoso.com,fabrikam.com,litware.com`

- Messages d’avertissement :
    
    - Clé : **OutlookWarnTrustedDomains**
    
    - Valeur : **\<** noms de domaine, séparés par des virgules **>**

- Messages de justification :
    
    - Clé : **OutlookJustifyTrustedDomains**
    
    - Valeur : **\<** noms de domaine, séparés par des virgules **>**

- Messages de blocage :
    
    - Clé : **OutlookBlockTrustedDomains**
    
    - Valeur : **\<** noms de domaine, séparés par des virgules **>**

Par exemple, vous avez spécifié le paramètre client avancé **OutlookBlockUntrustedCollaborationLabel** pour l’étiquette **confidentiel \ tous les employés** . Vous spécifiez maintenant le paramètre de client avancé supplémentaire **OutlookBlockTrustedDomains** et **contoso.com**. Par conséquent, un utilisateur peut envoyer un e-mail à john@sales.contoso.com lorsqu’il est étiqueté **confidentiel \ tous les employés** , mais qu’il ne peut pas envoyer un e-mail avec la même étiquette à un compte gmail.

### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-emails-or-attachments-that-dont-have-a-label"></a>Pour implémenter des messages contextuels d’avertissement, de justification ou de blocage pour des e-mails ou des pièces jointes qui n’ont pas d’étiquette :

Créez le paramètre client avancé suivant avec une des valeurs suivantes :

- Messages d’avertissement :
    
    - Clé : **OutlookUnlabeledCollaborationAction**
    
    - Valeur : **avertir**

- Messages de justification :
    
    - Clé : **OutlookUnlabeledCollaborationAction**
    
    - Valeur : **justifier**

- Messages de blocage :
    
    - Clé : **OutlookUnlabeledCollaborationAction**
    
    - Valeur : **bloquer**

- Désactiver ces messages :
    
    - Clé : **OutlookUnlabeledCollaborationAction**
    
    - Valeur : **désactivé**

#### <a name="to-define-specific-file-name-extensions-for-the-warn-justify-or-block-pop-up-messages-for-email-attachments-that-dont-have-a-label"></a>Pour définir des extensions de nom de fichier spécifiques pour les messages contextuels avertir, justifier ou bloquer pour les pièces jointes qui n’ont pas d’étiquette

Par défaut, les messages contextuels avertir, justifier ou bloquer s’appliquent à tous les documents Office et documents PDF. Vous pouvez affiner cette liste en spécifiant les extensions de nom de fichier qui doivent afficher les messages d’avertissement, de justification ou de blocage avec une propriété de client avancée supplémentaire et une liste séparée par des virgules d’extensions de noms de fichiers.

Exemple de valeur pour plusieurs extensions de nom de fichier à définir en tant que chaîne séparée par des virgules : `.XLSX,.XLSM,.XLS,.XLTX,.XLTM,.DOCX,.DOCM,.DOC,.DOCX,.DOCM,.PPTX,.PPTM,.PPT,.PPTX,.PPTM`

Dans cet exemple, un document PDF sans étiquette n’a pas pour effet d’avertir, de justifier ou de bloquer les messages contextuels.


- Clé : **OutlookOverrideUnlabeledCollaborationExtensions**

- Valeur : **\<** des extensions de nom de fichier pour afficher des messages, séparés par des virgules **>**

#### <a name="to-specify-a-different-action-for-email-messages-without-attachments"></a>Pour spécifier une action différente pour les messages électroniques sans pièces jointes

Par défaut, la valeur que vous spécifiez pour OutlookUnlabeledCollaborationAction pour avertir, justifier ou bloquer les messages contextuels s’applique aux e-mails ou pièces jointes qui n’ont pas d’étiquette. Vous pouvez affiner cette configuration en spécifiant un autre paramètre de client avancé pour les messages électroniques qui n’ont pas de pièces jointes.

Créez le paramètre client avancé suivant avec une des valeurs suivantes :

- Messages d’avertissement :
    
    - Clé : **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - Valeur : **avertir**

- Messages de justification :
    
    - Clé : **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - Valeur : **justifier**

- Messages de blocage :
    
    - Clé : **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - Valeur : **bloquer**

- Désactiver ces messages :
    
    - Clé : **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - Valeur : **désactivé**

Si vous ne spécifiez pas ce paramètre client, la valeur que vous spécifiez pour OutlookUnlabeledCollaborationAction est utilisée pour les messages électroniques sans étiquette, et les messages électroniques sans étiquette avec pièces jointes.


## <a name="set-a-different-default-label-for-outlook"></a>Définir une autre étiquette par défaut pour Outlook

Cette configuration utilise un [paramètre client avancé](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que vous devez configurer dans le portail Azure. 

Quand vous configurez ce paramètre, Outlook n’applique pas l’étiquette par défaut qui est configurée dans la stratégie Azure Information Protection pour le paramètre **Sélectionner l’étiquette par défaut**. Au lieu de cela, Outlook peut appliquer une autre étiquette par défaut ou ne rien appliquer.

Pour appliquer une autre étiquette, vous devez spécifier son ID. La valeur ID de l’étiquette s’affiche dans le volet **étiquette** , lorsque vous affichez ou configurez la stratégie de Azure information protection dans le portail Azure. Pour les fichiers auxquels des étiquettes sont appliquées, vous pouvez également exécuter l’applet de commande PowerShell [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) pour identifier l’ID de l’étiquette (MainLabelId ou SubLabelId). Si une étiquette a des sous-étiquettes, spécifiez toujours l’ID de la sous-étiquette et non celui de l’étiquette parente.

Pour qu’Outlook n’applique pas l’étiquette par défaut, spécifiez **None**.

Pour configurer ce paramètre avancé, entrez les chaînes suivantes :

- Clé : **OutlookDefaultLabel**

- Valeur : \<**ID d’étiquette**> ou **None**

## <a name="configure-a-label-to-apply-smime-protection-in-outlook"></a>Configurer une étiquette pour appliquer la protection S/MIME dans Outlook

Cette configuration utilise un [paramètre client avancé](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que vous devez configurer dans le portail Azure.

N’utilisez ce paramètre que si vous avez un [déploiement S/MIME](https://docs.microsoft.com/exchange/s-mime-for-message-signing-and-encryption) fonctionnel et que vous souhaitez qu’une étiquette applique automatiquement cette méthode de protection aux e-mails, plutôt que la protection Rights Management d’Azure Information Protection. La protection qui en résulte est la même que lorsque l’utilisateur sélectionne manuellement les options S/MIME dans Outlook.

Cette configuration implique de spécifier un paramètre client avancé nommé **LabelToSMIME** pour chacune des étiquettes Azure Information Protection qui devront appliquer la protection S/MIME. Ensuite, définissez la valeur à utiliserpour chaque entrée avec la syntaxe suivante :

`[Azure Information Protection label ID];[S/MIME action]`

La valeur ID de l’étiquette s’affiche dans le volet **étiquette** , lorsque vous affichez ou configurez la stratégie de Azure information protection dans le portail Azure. Pour utiliser S/MIME avec une sous-étiquette, spécifiez toujours l’ID de la sous-étiquette et non celui de l’étiquette parente. L’étiquette parente doit être dans la même étendue que la sous-étiquette, ou dans la stratégie globale.

L’action S/MIME peut être :

- `Sign;Encrypt` : pour appliquer une signature numérique et le chiffrement S/MIME ;

- `Encrypt` : pour appliquer uniquement le chiffrement S/MIME ;

- `Sign` : pour appliquer uniquement une signature numérique.

Exemples de valeurs pour l’ID d’étiquette **dcf781ba-727f-4860-b3c1-73479e31912b** :

- Pour appliquer une signature numérique et le chiffrement S/MIME :
    
    **dcf781ba-727f-4860-b3c1-73479e31912b;Sign;Encrypt**

- Pour appliquer uniquement le chiffrement S/MIME :
    
    **dcf781ba-727f-4860-b3c1-73479e31912b;Encrypt**
    
- Pour appliquer uniquement une signature numérique :
    
    **dcf781ba-727f-4860-b3c1-73479e31912b;Sign**

Dans cette configuration, lorsque l’étiquette est associée à un e-mail, la protection S/MIME est appliquée à l’e-mail en plus de la classification de l’étiquette.

Si l’étiquette spécifiée est configurée avec la protection Rights sur le Portail Azure, la protection S/MIME ne remplace la protection Rights Management que dans Outlook. Dans tous les autres scénarios qui gèrent l’étiquetage, la protection Rights Management s’applique.

Si vous souhaitez que l’étiquette ne soit visible que dans Outlook, configurez-la de façon à ce qu’elle applique l’action unique définie par l’utilisateur **Ne pas transférer**, conformément au [Démarrage rapide : Configurer une étiquette permettant aux utilisateurs de protéger facilement les e-mails qui contiennent des informations sensibles](../quickstart-label-dnf-protectedemail.md).

## <a name="remove-not-now-for-documents-when-you-use-mandatory-labeling"></a>Supprimer « Pas maintenant » pour les documents quand vous utilisez l’étiquetage obligatoire

Cette configuration utilise un [paramètre client avancé](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que vous devez configurer dans le portail Azure. 

Quand vous utilisez le [paramètre de stratégie](../configure-policy-settings.md)**All documents and emails must have a label** (Tous les documents et e-mails doivent avoir une étiquette), les utilisateurs sont invités à sélectionner une étiquette au moment du premier enregistrement d’un document Office et de l’envoi d’un e-mail. Pour les documents, les utilisateurs peuvent sélectionner **Pas maintenant** pour ignorer temporairement l’invite à sélectionner une étiquette et revenir au document. En revanche, ils ne peuvent pas fermer le document enregistré sans l’étiqueter. 

Quand vous configurez ce paramètre, l’option **Pas maintenant** n’est pas proposée, et les utilisateurs sont obligés de sélectionner une étiquette au premier enregistrement du document.

Pour configurer ce paramètre avancé, entrez les chaînes suivantes :

- Clé : **PostponeMandatoryBeforeSave**

- Valeur : **False**

## <a name="turn-on-classification-to-run-continuously-in-the-background"></a>Activer la classification pour qu’elle s’exécute en continu en arrière-plan

Cette configuration utilise un [paramètre client avancé](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que vous devez configurer dans le portail Azure. Ce paramètre est en préversion et est susceptible de changer.

Quand vous configurez ce paramètre, le [comportement par défaut](../configure-policy-classification.md#how-automatic-or-recommended-labels-are-applied) du client Azure Information Protection pour appliquer les étiquettes automatiques et recommandées aux documents : 

- Pour Word, Excel et PowerPoint, la classification automatique s’exécute en continu en arrière-plan.  

Le comportement ne change pas pour Outlook.

Quand le client Azure Information Protection vérifie à intervalles réguliers si les règles de condition que vous spécifiez sont exécutées pour les documents, ce comportement permet la classification et la protection automatiques et recommandées des documents stockés dans SharePoint Online. Les fichiers volumineux s’enregistrent également plus rapidement car les règles des conditions se sont déjà exécutées. 

Les règles des conditions ne s’exécutent pas en temps réel pendant la saisie de l’utilisateur. Elles s’exécutent plutôt à intervalles réguliers sous la forme d’une tâche en arrière-plan si le document est modifié.

Pour configurer ce paramètre avancé, entrez les chaînes suivantes :

- Clé : **RunPolicyInBackground**

- Valeur : **True**

## <a name="dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption"></a>Ne pas protéger les fichiers PDF suivant la norme ISO pour le chiffrement PDF

Cette configuration utilise un [paramètre client avancé](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que vous devez configurer dans le portail Azure. 

Quand la dernière version du client Azure Information Protection protège un fichier PDF, l’extension de nom de fichier résultante reste .pdf et adhère à la norme ISO pour le chiffrement PDF. Pour plus d’informations sur cette norme, consultez la section **7.6 Chiffrement** dans le [document qui est dérivé d’ISO 32000-1](https://www.adobe.com/content/dam/acom/en/devnet/pdf/pdfs/PDF32000_2008.pdf) et publié par Adobe Systems Incorporated.

Si vous voulez que le client rétablisse le comportement des versions antérieures du client qui protégeait les fichiers PDF à l’aide d’une extension de nom de fichier .ppdf, utilisez le paramètre avancé suivant en entrant la chaîne suivante :

- Clé : **EnablePDFv2Protection**

- Valeur : **False**

Par exemple, vous pouvez avoir besoin de ce paramètre pour tous les utilisateurs si vous utilisez un lecteur PDF qui ne prend pas en charge la norme ISO pour le chiffrement des PDF, ou vous avez besoin de le configurer pour certains utilisateurs dans le cadre d’un changement progressif pour un lecteur PDF qui prend en charge le nouveau format. Une autre raison potentielle pour utiliser ce paramètre est le cas où vous avez besoin d’ajouter une protection à des documents PDF signés. Les documents PDF signés peuvent bénéficier d’une protection supplémentaire avec le format .ppdf, car cette protection est implémentée comme wrapper pour le fichier. 

Pour que le scanneur Azure Information Protection utilise le nouveau paramètre, le service du scanneur doit être redémarré. De plus, le scanneur ne protègera plus par défaut les documents PDF. Si vous voulez que les documents PDF soient protégés par le scanneur quand EnablePDFv2Protection est défini sur False, vous devez [modifier le Registre](../deploy-aip-scanner.md#scanner-from-the-classic-client-use-the-registry-to-change-which-file-types-are-protected).

Pour plus d’informations sur le nouveau chiffrement PDF, consultez le billet de blog [New support for PDF encryption with Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/New-support-for-PDF-encryption-with-Microsoft-Information/ba-p/262757).

Pour obtenir la liste des lecteurs PDF qui prennent en charge la norme ISO pour le chiffrement des PDF, et des lecteurs qui prennent en charge des formats plus anciens, consultez [Lecteurs PDF pris en charge pour Microsoft Information Protection](protected-pdf-readers.md).

### <a name="to-convert-existing-ppdf-files-to-protected-pdf-files"></a>Pour convertir des fichiers .ppdf existants en fichiers .pdf protégés

Quand le client Azure Information Protection a téléchargé la stratégie client avec le nouveau paramètre, vous pouvez utiliser des commandes PowerShell pour convertir des fichiers .ppdf existants en fichiers .pdf protégés qui utilisent la norme ISO pour le chiffrement PDF. 

Pour utiliser les instructions suivantes pour les fichiers que vous n’avez pas vous-même protégés, vous devez disposer d’un [droit d’utilisation Rights Management](../configure-usage-rights.md) pour supprimer la protection de fichiers, ou être un super utilisateur. Pour activer la fonctionnalité de super utilisateur et configurer votre compte pour être un super utilisateur, consultez [Configuration de super utilisateurs pour Azure Rights Management et les services de découverte ou la récupération de données](../configure-super-users.md).

De plus, quand vous utilisez ces instructions pour des fichiers que vous n’avez pas vous-même protégés, vous devenez [l’émetteur RMS](../configure-usage-rights.md#rights-management-issuer-and-rights-management-owner). Dans ce scénario, l’utilisateur qui a initialement protégé le document ne peut plus le suivre et le révoquer. Si les utilisateurs doivent suivre et révoquer leurs documents PDF protégés, demandez-leur de les supprimer manuellement, puis de réappliquer l’étiquette à l’aide de l’Explorateur de fichiers.

Pour utiliser des commandes PowerShell pour convertir des fichiers .ppdf existants en fichiers .pdf protégés qui utilisent la norme ISO pour le chiffrement PDF :

1. Utilisez [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) avec le fichier .ppdf. Exemple :
    
        Get-AIPFileStatus -Path \\Finance\Projectx\sales.ppdf

2. Dans la sortie, notez les valeurs de paramètre suivantes :
    
   - La valeur (GUID) pour **SubLabelId**, le cas échéant. Si cette valeur est vide, cela signifie qu’aucune sous-étiquette n’a été utilisée. Par conséquent, notez la valeur de **MainLabelId** à la place.
    
     Remarque : S’il n’y a aucune valeur pour **MainLabelId**, le fichier n’est pas étiqueté. Dans ce cas, vous pouvez utiliser la commande [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) et la commande [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) au lieu des commandes mentionnées à l’étape 3 et 4.
    
   - La valeur pour **RMSTemplateId**. Si cette valeur est **Accès restreint**, un utilisateur a protégé le fichier à l’aide d’autorisations personnalisées au lieu d’utiliser des paramètres de protection configurés pour l’étiquette. Si vous continuez, ces autorisations personnalisées sont remplacées par les paramètres de protection de l’étiquette. Décidez s’il faut continuer ou demander à l’utilisateur (valeur affichée pour **RMSIssuer**) de supprimer l’étiquette et de la réappliquer, avec leurs autorisations personnalisées d’origine.

3. Supprimez l’étiquette à l’aide de [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) avec le paramètre *RemoveLabel*. Si vous utilisez le [paramètre de stratégie](../configure-policy-settings.md)**Les utilisateurs doivent fournir une justification pour définir une étiquette de classification moins élevée, supprimer une étiquette ou supprimer la protection**, vous devez également spécifier le paramètre  *Justification* avec la raison. Exemple : 
    
        Set-AIPFileLabel \\Finance\Projectx\sales.ppdf -RemoveLabel -JustificationMessage 'Removing .ppdf protection to replace with .pdf ISO standard'

4. Réappliquez l’étiquette d’origine, en spécifiant la valeur de l’étiquette que vous avez identifiée à l’étape 1. Exemple :
    
        Set-AIPFileLabel \\Finance\Projectx\sales.pdf -LabelId d9f23ae3-1234-1234-1234-f515f824c57b

Le fichier conserve l’extension de nom de fichier .pdf, mais il est classé comme auparavant et il est protégé à l’aide de la norme ISO pour le chiffrement PDF.

## <a name="support-for-files-protected-by-secure-islands"></a>Prise en charge des fichiers protégés par Secure Islands

Cette option de configuration est en version préliminaire et peut changer.

Si vous avez utilisé Secure Islands pour protéger des documents, vous avez certainement protégé les fichiers texte et image, ainsi que les fichiers protégés de manière générique à la suite de cette protection. Par exemple, les fichiers avec une extension de nom de fichier .ptxt, .pjpeg ou .pfile. Quand vous modifiez le Registre comme suit, Azure Information Protection peut déchiffrer ces fichiers :


Ajoutez la valeur DWORD suivante de **EnableIQPFormats** au chemin suivant du Registre et définissez les données de valeur sur **1** :

- Pour une version 64 bits de Windows : HKEY_LOCAL_MACHINE\\SOFTWARE\\WOW6432Node\\Microsoft\\MSIP

- Pour une version 32 bits de Windows : HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\MSIP

Suite à cette modification du Registre, les scénarios suivants sont pris en charge :

- La visionneuse Azure Information Protection peut ouvrir ces fichiers protégés.

- Le scanneur Azure Information Protection peut inspecter ces fichiers à la recherche d’informations sensibles.

- L’Explorateur de fichiers, PowerShell et le scanneur Azure Information Protection peuvent étiqueter ces fichiers. Par conséquent, vous pouvez appliquer une étiquette Azure Information Protection qui applique le nouveau groupe de protection d’Azure Information Protection, ou qui supprime la protection existante de Secure Islands.

- Vous pouvez utiliser la [personnalisation du client de migration d’étiquetage](#migrate-labels-from-secure-islands-and-other-labeling-solutions) pour convertir automatiquement l’étiquette Secure Islands de ces fichiers protégés en étiquette Azure Information Protection.

## <a name="migrate-labels-from-secure-islands-and-other-labeling-solutions"></a>Migrer des étiquettes de Secure Islands et d’autres solutions d’étiquetage

Cette configuration utilise un [paramètre client avancé](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que vous devez configurer dans le portail Azure.

Cette configuration n’est actuellement pas compatible avec le nouveau comportement par défaut qui protège les fichiers PDF en utilisant la norme ISO pour le chiffrement des PDF. Dans ce scénario, les fichiers .ppdf ne peuvent pas être ouverts par l’Explorateur de fichiers, PowerShell ou le scanneur. Pour résoudre ce problème, utilisez le paramètre client avancé [Ne pas utiliser la norme ISO pour le chiffrement des PDF](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption).

Vous pouvez ré-étiqueter les documents Office et PDF étiquetés par Secure Islands avec une étiquette Azure Information Protection à l’aide d’un mappage défini par vos soins. Cette méthode permet également de réutiliser les étiquettes d’autres solutions qui se trouvent sur des documents Office. 

> [!NOTE]
> Si vous avez des fichiers autres que des documents Office et PDF protégés par Secure Islands, vous pouvez les réétiqueter après avoir modifié le Registre comme décrit dans la [section précédente](#support-for-files-protected-by-secure-islands). 

Cette option de configuration permet au client Azure Information Protection d’appliquer la nouvelle étiquette Azure Information Protection comme suit :

- Pour les documents Office : lorsque le document est ouvert dans l’application de Bureau, la nouvelle étiquette Azure Information Protection est affichée comme définie et appliquée lorsque le document est enregistré.

- Pour l’Explorateur de fichiers : dans la boîte de dialogue Azure Information Protection, la nouvelle étiquette Azure Information Protection est affichée comme définie et appliquée lorsque l’utilisateur sélectionne **Appliquer**. Si l’utilisateur sélectionne **Annuler**, la nouvelle étiquette n’est pas appliquée.

- Pour PowerShell : [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) applique la nouvelle étiquette Azure Information Protection. [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) n’affiche pas la nouvelle étiquette Azure Information Protection tant qu’elle n’est pas définie par une autre méthode.

- Pour le scanneur Azure Information Protection : rapport de détection lorsque la nouvelle étiquette Azure Information Protection est définie et qu’elle peut être appliquée avec le mode d’application.

Cette configuration nécessite que vous spécifiiez un paramètre client avancé nommé **LabelbyCustomProperty** pour chaque étiquette Azure Information Protection que vous souhaitez associer à l’ancienne étiquette. Ensuite, définissez la valeur à utiliserpour chaque entrée avec la syntaxe suivante :

`[Azure Information Protection label ID],[migration rule name],[Secure Islands custom property name],[Secure Islands metadata Regex value]`

La valeur ID de l’étiquette s’affiche dans le volet **étiquette** , lorsque vous affichez ou configurez la stratégie de Azure information protection dans le portail Azure. Pour spécifier une sous-étiquette, l’étiquette parente doit être dans la même étendue, ou dans la stratégie globale.

Spécifiez votre choix d’un nom de règle de migration. Utilisez un nom descriptif qui vous aide à identifier la manière dont une ou plusieurs étiquettes de votre solution d’étiquetage précédente doivent être mappées à une étiquette Azure Information Protection. Le nom s’affiche dans les rapports d’analyse et dans l’observateur d’événements. Notez que ce paramètre ne supprime pas l’étiquette d’origine du document ni les marquages visuels du document que l’étiquette d’origine a éventuellement appliqués. Pour supprimer des en-têtes et des pieds de page, consultez la section suivante, [Supprimer les en-têtes et les pieds de page d’autres solutions d’étiquetage](#remove-headers-and-footers-from-other-labeling-solutions).

### <a name="example-1-one-to-one-mapping-of-the-same-label-name"></a>Exemple 1 : mappage du même nom d’étiquette

Exigence : les documents qui ont une étiquette des îlots sécurisés « confidentiel » doivent être réétiquetés comme « confidentiels » par Azure Information Protection.

Exemple :

- L’étiquette Azure Information Protection que vous voulez utiliser s’appelle **Confidentiel** et a l’ID d’étiquette **1ace2cc3-14bc-4142-9125-bf946a70542c**. 

- L’étiquette Secure Islands s’appelle **Confidentiel** et est stockée dans la propriété personnalisée nommée **Classification**.

Le paramètre client avancé :

    
|Nom|valeur|
|---------------------|---------|
|LabelbyCustomProperty|1ace2cc3-14bc-4142-9125-bf946a70542c, « L’étiquette Secure Islands est confidentiel », Classification, Confidentiel|

### <a name="example-2-one-to-one-mapping-for-a-different-label-name"></a>Exemple 2 : un mappage pour un autre nom d’étiquette

Exigence : les documents intitulés « sensibles » par les îles sécurisées doivent être renommés comme « hautement confidentiels » par Azure Information Protection.

Exemple :

- L’étiquette Azure Information Protection que vous voulez utiliser s’appelle **Hautement confidentiel** et a l’ID d’étiquette **3e9df74d-3168-48af-8b11-037e3021813f**.

- L’étiquette Secure Islands s’appelle **Sensible** et est stockée dans la propriété personnalisée nommée **Classification**.

Le paramètre client avancé :

    
|Nom|valeur|
|---------------------|---------|
|LabelbyCustomProperty|3e9df74d-3168-48af-8b11-037e3021813f, «L’étiquette Secure Islands est sensible », Classification, Sensible|


### <a name="example-3-many-to-one-mapping-of-label-names"></a>Exemple 3 : mappage de plusieurs noms d’étiquettes en un

Exigence : vous avez deux étiquettes de îles sécurisées qui incluent le mot « Internal » et vous souhaitez que les documents qui ont l’une de ces étiquettes des îlots sécurisés soient réétiquetés comme « général » par Azure Information Protection.

Exemple :

- L’étiquette Azure Information Protection que vous voulez utiliser s’appelle **Général** et a l’ID d’étiquette **2beb8fe7-8293-444c-9768-7fdc6f75014d**.

- L’étiquette Secure Islands inclut le mot **Interne** et est stockée dans la propriété personnalisée nommée **Classification**.

Le paramètre client avancé :

    
|Nom|valeur|
|---------------------|---------|
|LabelbyCustomProperty|2beb8fe7-8293-444c-9768-7fdc6f75014d, «L’étiquette Secure Islands contient Interne », Classification,. \*Interne.\*|


## <a name="remove-headers-and-footers-from-other-labeling-solutions"></a>Supprimer les en-têtes et les pieds de page d’autres solutions d’étiquetage

Cette configuration utilise plusieurs [paramètres clients avancés](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que vous devez configurer dans le portail Azure. Ces paramètres sont en préversion et sont susceptibles de changer.

Les paramètres permettent de supprimer ou de remplacer des en-têtes ou des pieds de page textuels de documents quand ces marquages visuels ont été appliqués par une autre solution d’étiquetage. Par exemple, l’ancien pied de page contient le nom d’une ancienne étiquette que vous avez migrée vers Azure Information Protection avec un nouveau nom d’étiquette et son propre pied de page.

Lorsque le client obtient cette configuration dans sa stratégie, les anciens en-têtes et pieds de page sont supprimés ou remplacés lorsque le document est ouvert dans l’application Office et une étiquette Azure Information Protection est appliquée au document.

Cette configuration n’est pas prise en charge pour Outlook. Sachez également que quand vous l’utilisez avec Word, Excel et PowerPoint, elle peut affecter négativement les performances de ces applications pour les utilisateurs. La configuration vous permet de définir des paramètres par application, par exemple, rechercher du texte dans les en-têtes et les pieds de page des documents Word, mais pas dans les feuilles de calcul Excel ni dans les présentations PowerPoint.

Étant donné que les critères spéciaux affectent les performances pour les utilisateurs, nous vous recommandons de limiter les types d’applications Office (**W**ORD, E**X**cel, **P**owerPoint) à ceux qui doivent être recherchés :

- Clé : **RemoveExternalContentMarkingInApp**

- Valeur : \<**Types d’application Office WXP**> 

Exemples :

- Pour rechercher dans des documents Word uniquement, spécifiez **W**.

- Pour rechercher dans des documents Word et des présentations PowerPoint, spécifiez **WP**.

Ensuite, vous avez besoin d’au moins un paramètre client avancé de plus, **ExternalContentMarkingToRemove**, pour spécifier le contenu de l’en-tête ou du pied de page et comment les supprimer ou les remplacer.

### <a name="how-to-configure-externalcontentmarkingtoremove"></a>Comment configurer ExternalContentMarkingToRemove

Lorsque vous spécifiez la valeur de chaîne pour la clé **ExternalContentMarkingToRemove**, vous disposez de trois options qui utilisent des expressions régulières :

- Correspondance partielle pour tout supprimer dans l’en-tête ou le pied de page.
    
    Exemple : Les en-têtes ou les pieds de page contiennent la chaîne **TEXTE À SUPPRIMER**. Vous souhaitez entièrement supprimer ces en-têtes ou pieds de page. Spécifiez la valeur : `*TEXT*`.

- Correspondance totale pour juste supprimer des mots spécifiques dans l’en-tête ou le pied de page.
    
    Exemple : Les en-têtes ou les pieds de page contiennent la chaîne **TEXTE À SUPPRIMER**. Vous souhaitez supprimer le mot **TEXTE** uniquement, ce qui laisse la chaîne d’en-tête ou de pied de page avec **À SUPPRIMER**. Spécifiez la valeur : `TEXT `.

- Correspondance totale pour tout supprimer dans l’en-tête ou le pied de page.
    
    Exemple : Les en-têtes ou les pieds de page ont la chaîne **TEXTE À SUPPRIMER**. Vous voulez supprimer les en-têtes ou les pieds de page qui ont exactement cette chaîne. Spécifiez la valeur : `^TEXT TO REMOVE$`.
    

Les caractères génériques de la chaîne que vous spécifiez sont sensibles à la casse. La longueur maximale de la chaîne est de 255 caractères.

Étant donné que des documents peuvent contenir des caractères invisibles ou différents types d’espaces ou des tabulations, la chaîne que vous spécifiez pour une expression ou une phrase peut ne pas être détectée. Si possible, spécifiez un seul mot distinctif pour la valeur et veillez à tester les résultats avant de procéder au déploiement en production.

- Clé : **ExternalContentMarkingToRemove**

- Valeur : \<**chaîne à trouver, définie comme expression régulière**> 

#### <a name="multiline-headers-or-footers"></a>En-têtes ou pieds de page multilignes

Si un texte d’en-tête ou de pied de page prend plus d’une ligne, créez une clé et une valeur pour chaque ligne. Par exemple, vous avez le pied de page suivant sur deux lignes :

**Le fichier est classé confidentiel**

**Étiquette appliquée manuellement**

Pour supprimer ce pied de page multiligne, créez les deux entrées suivantes :

- Clé 1 : **ExternalContentMarkingToRemove**

- Valeur de la clé 1 : **\*Confidentiel***

- Clé 2 : **ExternalContentMarkingToRemove**

- Valeur de la clé 2 : **\*Étiquette appliquée*** 

#### <a name="optimization-for-powerpoint"></a>Optimisation pour PowerPoint

Les pieds de page dans PowerPoint sont implémentés en tant que formes. Pour éviter de supprimer les formes qui contiennent le texte que vous avez spécifié, mais qui ne sont ni des en-têtes ni des pieds de page, utilisez un paramètre client avancé supplémentaire nommé **PowerPointShapeNameToRemove**. Nous recommandons également d’utiliser ce paramètre pour éviter de vérifier le texte dans toutes les formes, qui est un processus gourmand en ressources.

Si vous ne spécifiez pas ce paramètre client avancé supplémentaire et si PowerPoint est inclus dans la valeur de la clé **RemoveExternalContentMarkingInApp**, toutes les formes sont vérifiées à la recherche du texte que vous spécifiez dans la valeur  **ExternalContentMarkingToRemove**. 

Pour rechercher le nom de la forme que vous utilisez comme en-tête ou pied de page :

1. Dans PowerPoint, affichez le volet **Sélection** : onglet **Mise en forme** > groupe **Organiser** > **volet sélection**.

2. Sélectionnez la forme sur la diapositive qui contient votre en-tête ou votre pied de page. Le nom de la forme sélectionnée est maintenant en surbrillance dans le volet **Sélection**.

Utilisez le nom de la forme afin de spécifier une valeur de chaîne pour la clé **PowerPointShapeNameToRemove**. 

Exemple : Le nom de la forme est **fc**. Pour supprimer la forme portant ce nom, spécifiez la valeur : `fc`.

- Clé : **PowerPointShapeNameToRemove**

- Valeur : \<**Nom de la forme PowerPoint**> 

Lorsque vous avez plusieurs formes PowerPoint à supprimer, créez autant de clés **PowerPointShapeNameToRemove** que vous avez de formes à supprimer. Pour chaque entrée, spécifiez le nom de la forme à supprimer.

Par défaut, seuls les en-têtes et les pieds de page qui se trouvent dans les diapositives principales sont recherchés. Pour étendre cette recherche à toutes les diapositives, processus beaucoup plus gourmand en ressources, utilisez un paramètre client avancé supplémentaire nommé **RemoveExternalContentMarkingInAllSlides**:

- Clé : **RemoveExternalContentMarkingInAllSlides**

- Valeur : **True**

## <a name="label-an-office-document-by-using-an-existing-custom-property"></a>Étiquette d’un document Office en utilisant une propriété personnalisée existante

> [!NOTE]
> Si vous utilisez cette configuration et la configuration pour [migrer les étiquettes à partir de Secure Islands et autres solutions d’étiquetage](#migrate-labels-from-secure-islands-and-other-labeling-solutions), le paramètre de migration de l’étiquetage est prioritaire. 

Cette configuration utilise un [paramètre client avancé](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que vous devez configurer dans le portail Azure. 

Lorsque vous configurez ce paramètre, vous pouvez classer (et éventuellement protéger) un document Office quand celui-ci a une propriété personnalisée existante avec une valeur qui correspond à l’un de vos noms d’étiquette. Cette propriété personnalisée peut être définie à partir d’une autre solution de classification, ou définie comme propriété par SharePoint.

Suite à cette configuration, lorsqu’un document sans étiquette Azure Information Protection est ouvert et enregistré par un utilisateur dans une application Office, il est étiqueté pour correspondre à la valeur de propriété. 

Pour cette configuration, vous devez spécifier deux paramètres avancés qui fonctionnent ensemble. Le premier s’appelle **SyncPropertyName**, qui est le nom de la propriété personnalisée qui a été définie à partir de l’autre solution de classification ou une propriété qui est définie par SharePoint. Le second s’appelle **SyncPropertyState** et doit être défini sur OneWay.

Pour configurer ce paramètre avancé, entrez les chaînes suivantes :

- Clé 1 : **SyncPropertyName**

- Valeur de la clé 1 : \<**nom de la propriété**> 

- Clé 2 : **SyncPropertyState**

- Valeur de la clé 2 : **OneWay**

Utilisez ces clés et les valeurs correspondantes pour une seule propriété personnalisée.

Par exemple, vous avez une colonne SharePoint nommée **Classification** qui a les valeurs possibles **Public**, **Général** et **Hautement confidentiel Tous les employés**. Les documents sont stockés dans SharePoint et ont des valeurs définies **Public**, **Général** ou **Hautement confidentiel Tous les employés** pour la propriété Classification.

Pour étiqueter un document Office avec l’une de ces valeurs de classification, définissez **SyncPropertyName** sur **Classification** et **SyncPropertyState** sur **OneWay**. 

À partir de maintenant, quand un utilisateur ouvre et enregistre un de ces documents Office, le document est étiqueté **Public**, **Général** ou **Hautement confidentiel\Tous les employés** si vous avez des étiquettes avec ces noms dans votre stratégie Azure Information Protection. Si vous n’avez pas d’étiquettes avec ces noms, le document reste sans étiquette.

## <a name="disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics"></a>Désactiver l’envoi d’informations sensibles découvertes dans des documents à Azure Information Protection Analytics

Cette configuration utilise un [paramètre client avancé](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que vous devez configurer dans le portail Azure.

Lorsque le client Azure Information Protection est utilisé dans les applications Office, il recherche des informations sensibles dans les documents lorsqu’ils sont enregistrés pour la première fois. Si le client n’est pas configuré pour ne pas envoyer d’informations d’audit, tous les types d’informations sensibles détectés (prédéfinis ou personnalisés) sont ensuite envoyés à [Azure information protection Analytics](../reports-aip.md). 

La configuration qui contrôle si le client envoie des informations d’audit est le [paramètre de stratégie](../configure-policy-settings.md) **Envoyer des données d’audit à Azure information protection log Analytics**. Lorsque ce paramètre de stratégie est activé parce que vous souhaitez envoyer **des** informations d’audit incluant des actions d’étiquetage mais que vous ne souhaitez pas envoyer de types d’informations sensibles détectés par le client, entrez les chaînes suivantes :

- Clé : **RunAuditInformationTypesDiscovery**

- Valeur : **False**

Si vous définissez ce paramètre de client avancé, les informations d’audit peuvent toujours être envoyées à partir du client, mais les informations sont limitées à l’étiquetage de l’activité.

Exemple :

- Avec ce paramètre, vous pouvez voir qu’un utilisateur a accédé à Financial. docx qui est étiqueté **confidentiel \ Sales**.

- Sans ce paramètre, vous pouvez voir que Financial. docx contient 6 numéros de carte de crédit.
    
    - Si vous activez également des [analyses plus approfondies dans vos données sensibles](../reports-aip.md#content-matches-for-deeper-analysis), vous serez en outre en mesure de voir ce que sont ces numéros de carte de crédit.

## <a name="disable-sending-information-type-matches-for-a-subset-of-users"></a>Désactiver l’envoi de correspondances de types d’informations pour un sous-ensemble d’utilisateurs

Cette configuration utilise un [paramètre client avancé](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que vous devez configurer dans le portail Azure.

Lorsque vous activez la case à cocher [Azure information protection Analytics](../reports-aip.md) qui permet des analyses plus approfondies dans vos données sensibles, collecte les correspondances de contenu pour vos types d’informations sensibles ou vos conditions personnalisées, par défaut, ces informations sont envoyées par tous les utilisateurs, y compris les comptes de service qui exécutent le scanneur Azure information protection. Pour éviter que certains utilisateurs n’envoient ces données, créez les paramètres clients avancés suivants dans une [stratégie délimitée](../configure-policy-scope.md) autour de ces utilisateurs : 

- Clé : **LogMatchedContent**

- Valeur : **Désactiver**


## <a name="limit-the-number-of-threads-used-by-the-scanner"></a>Limiter le nombre de threads utilisés par le scanneur

Cette configuration utilise un [paramètre client avancé](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que vous devez configurer dans le portail Azure.

Par défaut, le scanneur utilise toutes les ressources du processeur disponibles sur l’ordinateur exécutant le service du scanneur. Si vous devez limiter la consommation de l’UC pendant l’exécution de ce service, créez le paramètre avancé suivant. 

Pour la valeur, spécifiez le nombre de threads simultanés que le scanneur peut exécuter en parallèle. Comme le scanneur utilise un thread distinct pour chaque fichier qu’il analyse, cette configuration de limitation définit donc le nombre de fichiers pouvant être analysés en parallèle. 

Lorsque vous configurez tout d’abord la valeur pour le test, nous vous recommandons de spécifier 2 par cœur, puis de surveiller les résultats. Par exemple, si vous exécutez le scanneur sur un ordinateur disposant de 4 cœurs, définissez tout d’abord la valeur 8. Si nécessaire, augmentez ou diminuez ce nombre, selon les performances qui vous sont nécessaires pour l’ordinateur du scanneur et votre fréquence d’analyse. 

- Clé : **ScannerConcurrencyLevel**

- Valeur : **\<nombre maximal de threads simultanés**

## <a name="disable-the-low-integrity-level-for-the-scanner"></a>Désactiver le niveau d’intégrité faible pour le scanneur

Cette configuration utilise un [paramètre client avancé](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que vous devez configurer dans le portail Azure.

Par défaut, le scanneur Azure Information Protection s’exécute avec un niveau d’intégrité faible. Ce paramètre offre une isolation de sécurité plus élevée, mais au détriment des performances. Un niveau d’intégrité faible est adapté si vous exécutez le scanneur avec un compte qui dispose de droits privilégiés (comme un compte d’administrateur local), car ce paramètre permet de protéger l’ordinateur exécutant le scanneur.

Toutefois, lorsque le compte de service qui exécute le scanneur dispose seulement des droits documentés dans les [prérequis du scanneur](../deploy-aip-scanner.md#prerequisites-for-the-azure-information-protection-scanner), le niveau d’intégrité faible n’est pas nécessaire et n’est pas recommandé, car il a un impact négatif sur les performances. 

Pour plus d’informations sur les niveaux d’intégrité de Windows, consultez [Qu’est-ce que le mécanisme d’intégrité de Windows ?](https://msdn.microsoft.com/library/bb625957.aspx)

Pour configurer ce paramètre avancé afin que le scanneur s’exécute avec un niveau d’intégrité attribué automatiquement par Windows (un compte d’utilisateur standard s’exécute avec un niveau d’intégrité moyen), entrez les chaînes suivantes :

- Clé : **ProcessUsingLowIntegrity**

- Valeur : **False**

## <a name="change-the-timeout-settings-for-the-scanner"></a>Modifier les paramètres de délai d’attente pour le scanneur

Cette configuration utilise des [Paramètres client avancés](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que vous devez configurer dans la portail Azure.

Par défaut, le Azure Information Protection scanneur a un délai d’expiration de 00:15:00 (15 minutes) pour inspecter chaque fichier à la fin des types d’informations sensibles ou des expressions Regex que vous avez configurées pour des conditions personnalisées. Lorsque le délai d’attente est atteint pour ce processus d’extraction de contenu, tous les résultats avant le délai d’expiration sont retournés et l’inspection supplémentaire du fichier s’arrête. Dans ce scénario, le message d’erreur suivant est consigné dans%*LocalAppData*% \ Microsoft\MSIP\Logs\MSIPScanner.Iplog (zippé s’il y a plusieurs journaux) : **GetContentParts a échoué** avec **l’opération a été annulée** dans les détails.

Si vous rencontrez ce problème de délai d’expiration en raison de fichiers volumineux, vous pouvez augmenter ce délai d’attente pour l’extraction de contenu complète :

- Clé : **ContentExtractionTimeout**

- Valeur : **\<hh : min : sec >**

Le type de fichier peut influencer le temps nécessaire à l’analyse d’un fichier. Exemples de temps d’analyse :

- Fichier Word 100 Mo standard : 0,5 à 5 minutes

- Fichier PDF 100 Mo standard : 5-20 minutes

- Fichier Excel 100 Mo standard : 12-30 minutes

Pour certains types de fichiers très volumineux, tels que les fichiers vidéo, pensez à les exclure de l’analyse en ajoutant l’extension de nom de fichier à l’option **types de fichiers à analyser** dans le profil du scanneur.

En outre, le Azure Information Protection scanneur a un délai d’expiration de 00:30:00 (30 minutes) pour chaque fichier qu’il traite. Cette valeur prend en compte le temps qu’elle peut prendre pour récupérer un fichier à partir d’un référentiel et l’enregistrer temporairement localement pour les actions qui peuvent inclure le déchiffrement, l’extraction de contenu pour l’inspection, l’étiquetage et le chiffrement.

Bien que le scanneur Azure Information Protection puisse analyser des dizaines de centaines de fichiers par minute, si vous disposez d’un référentiel de données qui contient un grand nombre de fichiers très volumineux, le scanneur peut dépasser ce délai d’expiration par défaut et dans le Portail Azure semble s’arrêter après 30 maximum. Dans ce scénario, le message d’erreur suivant est consigné dans%*LocalAppData*% \ Microsoft\MSIP\Logs\MSIPScanner.Iplog (zippé s’il y a plusieurs journaux) et le fichier journal scanner. csv : **l’opération a été annulée**.

Un scanneur avec 4 processeurs de base par défaut a 16 threads pour l’analyse et la probabilité de rencontrer 16 fichiers volumineux dans un laps de temps de 30 minutes dépend du rapport des fichiers volumineux. Par exemple, si la vitesse d’analyse est de 200 fichiers par minute et que 1% des fichiers dépassent le délai d’expiration de 30 minutes, il existe une probabilité de plus de 85% que le moteur d’analyse rencontrera la situation du délai d’expiration de 30 minutes. Ces délais d’expiration peuvent entraîner des temps d’analyse plus longs et une plus grande consommation de mémoire.

Dans ce cas, si vous ne pouvez pas ajouter d’autres processeurs de base à l’ordinateur du scanneur, envisagez de réduire le délai d’expiration pour obtenir de meilleurs taux d’analyse et une consommation de mémoire inférieure, mais avec l’accusé de réception que certains fichiers seront exclus. Vous pouvez également envisager d’augmenter le délai d’expiration pour obtenir des résultats d’analyse plus précis, mais avec l’accusé de réception que cette configuration entraînera probablement des taux d’analyse inférieurs et une consommation de mémoire plus élevée.

Pour modifier le délai d’attente pour le traitement des fichiers, configurez le paramètre de client avancé suivant :

- Clé : **FileProcessingTimeout**

- Valeur : **\<hh : min : sec >**

## <a name="change-the-local-logging-level"></a>Modifier le niveau de journalisation local

Cette configuration utilise un [paramètre client avancé](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que vous devez configurer dans le portail Azure.

Par défaut, le client Azure Information Protection écrit les fichiers journaux clients dans le dossier **%localappdata%\Microsoft\MSIP**. Ces fichiers servent à la résolution des problèmes par le Support Microsoft.
 
Pour modifier le niveau de journalisation de ces fichiers, configurez le paramètre client avancé suivant :

- Clé : **LogLevel**

- Valeur : **\<niveau de journalisation>**

Définissez le niveau de journalisation sur l'une des valeurs suivantes :

- **Off**: aucune journalisation locale.

- **Erreur**: erreurs uniquement.

- **Info**: journalisation minimale, qui n’indique aucun ID d’événement (paramètre par défaut pour le scanneur).

- **Débogage**: informations complètes.

- **Trace**: journalisation détaillée (paramètre par défaut pour les clients). Pour le scanneur, ce paramètre a un impact significatif sur les performances et doit être activé pour le scanneur uniquement si cela est demandé par le Support Microsoft. S’il vous est demandé de définir ce niveau de journalisation pour le scanneur, pensez à fixer une valeur différente lorsque les journaux souhaités ont été collectés.

Ce paramètre client avancé ne modifie ni les informations envoyées à Azure Information Protection pour le [reporting central](../reports-aip.md), ni les informations écrites dans le [journal des événements](client-admin-guide-files-and-logging.md#usage-logging-for-the-azure-information-protection-client) local.

## <a name="integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution"></a>Intégration avec la classification des messages Exchange pour une solution d’étiquetage des appareils mobiles

Outlook sur le Web prend désormais en charge l’étiquetage intégré pour Exchange Online, qui est la méthode recommandée pour étiqueter les messages électroniques dans Outlook sur le Web. Toutefois, si vous n’utilisez pas encore les étiquettes de sensibilité publiées à partir du Centre de sécurité et de conformité Office 365, Microsoft 365 Security Center ou Microsoft Compliance Center, vous pouvez utiliser la classification des messages Exchange pour étendre les informations Azure Des étiquettes de protection à vos utilisateurs mobiles lorsqu’ils utilisent Outlook sur le Web. Vous pouvez également utiliser cette méthode pour Exchange Server. 

Outlook Mobile ne prend pas en charge la classification des messages Exchange.

Pour obtenir cette solution : 

1. Utilisez l’applet de commande PowerShell Exchange [New-MessageClassification](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/New-MessageClassification?view=exchange-ps) pour créer des classifications des messages avec la propriété Name qui correspond à vos noms d’étiquette dans votre stratégie Azure Information Protection. 

2. Créez une règle de flux de messagerie Exchange pour chaque étiquette : appliquez la règle quand les propriétés de message incluent la classification que vous avez configurée, puis modifiez les propriétés de message pour définir un en-tête de message. 

     Pour l’en-tête de message, vous trouvez les informations à spécifier en examinant les en-têtes Internet d’un e-mail que vous avez envoyé et classifié à l’aide de votre étiquette Azure Information Protection. Recherchez l’en-tête **msip_labels** et la chaîne qui suit immédiatement, jusqu’au point-virgule et sans le point-virgule. Exemple :
    
    **msip_labels : MSIP_Label_0e421e6d-EA17-4FDB-8F01-93a3e71333b8_Enabled = true**
    
    Ensuite, pour l’en-tête du message dans la règle, spécifiez **msip_labels** pour l’en-tête, et le reste de cette chaîne pour la valeur de l’en-tête. Exemple :
    
    ![Exemple de règles de flux de messagerie Exchange Online qui définit l’en-tête de message pour une étiquette Azure Information Protection spécifique](../media/exchange-rule-for-message-header.png)
    
    Remarque : Quand l’étiquette est une sous-étiquette, vous devez également spécifier l’étiquette parent avant la sous-étiquette dans la valeur de l’en-tête, en utilisant le même format. Par exemple, si votre sous-étiquette a le GUID 27efdf94-80a0-4d02-b88c-b615c12d69a9, votre valeur doit ressembler à ceci : `MSIP_Label_ab70158b-bdcc-42a3-8493-2a80736e9cbd_Enabled=True;MSIP_Label_27efdf94-80a0-4d02-b88c-b615c12d69a9_Enabled=True`

Avant de tester cette configuration, n’oubliez pas qu’il y a souvent un délai quand vous créez ou modifiez des règles de flux de messagerie (attendez par exemple une heure). Lorsque la règle est appliquée, les événements suivants se produisent quand les utilisateurs utilisent Outlook sur le web : 

- Les utilisateurs sélectionnent la classification des messages Exchange et envoient l’e-mail.

- La règle Exchange détecte la classification Exchange et modifie en conséquence l’en-tête de message pour ajouter la classification Azure Information Protection.

- Quand les destinataires internes qui disposent du client Azure Information Protection affichent l’e-mail dans Outlook, ils voient l’étiquette Azure Information Protection attribuée. 

Si vos étiquettes d’Azure Information Protection appliquent la protection, ajoutez cette protection à la configuration de la règle : sélectionnez l’option permettant de modifier la sécurité des messages, appliquez la protection des droits, puis sélectionnez le modèle de protection ou l’option ne pas transférer.

Vous pouvez également configurer des règles de flux de messagerie pour effectuer le mappage inverse. Quand une étiquette Azure Information Protection est détectée, définissez la classification de messages Exchange correspondante :

- Pour chaque étiquette Azure Information Protection : créez une règle de flux de messagerie appliquée quand l’en-tête **msip_labels** inclut le nom de votre étiquette (par exemple **Général**), puis appliquez une classification de messages qui correspond à cette étiquette.


## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez personnalisé le client Azure Information Protection, consultez les ressources suivantes pour obtenir des informations supplémentaires sur la prise en charge de ce client :

- [Fichiers du client et journalisation de l’utilisation](client-admin-guide-files-and-logging.md)

- [Suivi des documents](client-admin-guide-document-tracking.md)

- [Types de fichier pris en charge](client-admin-guide-file-types.md)

- [Commandes PowerShell](client-admin-guide-powershell.md)


