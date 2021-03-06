---
title: Problèmes connus - Azure Information Protection
description: Recherchez et parcourez les problèmes connus et les limitations de Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 03/16/2021
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 220b1e7ffec1f1bd4332058c9320241106de2e1d
ms.sourcegitcommit: 99f1a1ab40eea7802e6c4f98724958409ee779ba
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/16/2021
ms.locfileid: "103558148"
---
# <a name="known-issues---azure-information-protection"></a>Problèmes connus - Azure Information Protection

>***S’applique à** : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***Concerne** : [Client d’étiquetage unifié AIP et client classique](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Pour fournir une expérience client unifiée et homogène, le **client classique Azure Information Protection** et la **gestion des étiquettes** dans le portail Azure seront **dépréciés** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Utilisez les listes et les tableaux ci-dessous pour trouver des informations sur les problèmes connus et les limitations liées aux fonctionnalités de Azure Information Protection.

## <a name="third-party-digital-signing-apps"></a>Applications tierces de signature numérique

Azure Information Protection ne peut pas protéger ou déchiffrer des fichiers signés numériquement.

## <a name="client-support-for-container-files-such-as-zip-files"></a>Prise en charge des fichiers de conteneur par les clients, tels que les fichiers. zip

Les fichiers conteneurs sont des fichiers qui incluent d’autres fichiers, comme l’exemple classique des fichiers .zip qui contiennent des fichiers compressés. D’autres exemples incluent les fichiers .rar, .7z, .msg et les documents PDF qui incluent des pièces jointes.

Vous pouvez classifier et protéger ces fichiers conteneurs, mais la classification et la protection ne sont pas appliquées à chaque fichier situé à l’intérieur du conteneur.

Si vous avez un fichier conteneur qui inclut des fichiers classifiés et protégés, vous devez d’abord extraire ces fichiers pour modifier leurs paramètres de classification ou de protection. Toutefois, vous pouvez supprimer la protection pour tous les fichiers inclus dans des fichiers conteneurs pris en charge à l’aide de l’applet de commande [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile).

La visionneuse Azure Information Protection ne peut pas ouvrir les pièces jointes dans un document PDF protégé. Dans ce scénario, lorsque le document est ouvert dans la visionneuse, les pièces jointes ne sont pas visibles.

Pour plus d’informations, consultez [le Guide de l’administrateur : types de fichiers pris en charge par le client Azure information protection](rms-client/client-admin-guide-file-types.md).

## <a name="known-issues-for-aip-and-exploit-protection"></a>Problèmes connus liés à AIP et à la protection contre les attaques

Le client Azure Information Protection n’est pas pris en charge sur les ordinateurs disposant de .NET 2 ou 3, où la [protection contre l’exploitation](/windows/security/threat-protection/microsoft-defender-atp/enable-exploit-protection) est activée et entraîne un comportement inattendu des applications Office.

Dans ce cas, nous vous recommandons de mettre à niveau votre version .NET. Pour plus d’informations, consultez [Microsoft .NET Framework Requirements](rms-client/reqs-ul-client.md#microsoft-net-framework-requirements).

Si vous devez conserver votre .NET version 2 ou 3, veillez à désactiver la protection contre l’exploitation avant d’installer AIP. 

Pour désactiver la protection contre les attaques par le biais de PowerShell, exécutez la commande suivante :

```PowerShell
Set-ProcessMitigation -Name "OUTLOOK.EXE" -Disable EnableExportAddressFilterPlus, EnableExportAddressFilter, EnableImportAddressFilter
```

## <a name="powershell-support-for-the-azure-information-protection-client"></a>Prise en charge de PowerShell pour le client Azure Information Protection

La version actuelle du module PowerShell **AzureInformationProtection** qui est installée avec le client Azure information protection présente les problèmes connus suivants :

- **Dossiers personnels Outlook (* fichiers. pst *) * *. La protection native des fichiers *. pst* n’est pas prise en charge à l’aide du module **AzureInformationProtection** .

- **Messages électroniques protégés par Outlook *(fichiers. rpmsg* )**. La déprotection des messages électroniques protégés par Outlook est prise en charge par le module **AzureInformationProtection** uniquement s’ils se trouvent dans un dossier personnel Outlook *(fichier. pst* ).

    La déprotection des messages électroniques en dehors d’un fichier *. pst* n’est pas prise en charge.

Pour plus d’informations, consultez [le Guide de l’administrateur : utilisation de PowerShell avec le client Azure information protection](rms-client/client-admin-guide-powershell.md).

## <a name="aip-known-issues-in-office-applications"></a>Problèmes connus liés à AIP dans les applications Office

|Fonctionnalité  |Problèmes connus  |
|---------|---------|
|**Plusieurs versions d’Office <br> <br> comptes multiples Office**    | Les clients Azure Information Protection, y compris les étiquettes classiques et unifiées, ne prennent pas en charge :  <br><br>-Plusieurs versions d’Office sur le même ordinateur <br>-Plusieurs comptes Office ou basculer des comptes d’utilisateur dans Office <br>-Boîtes aux lettres partagées     |
|**Affichages multiples** |Si vous utilisez plusieurs affichages et que vous avez une application Office ouverte : <br><br>-Vous pouvez rencontrer des problèmes de performances dans vos applications Office.<br>-La barre de Azure Information Protection peut sembler flotter au milieu de l’écran du bureau, sur l’un ou l’autre des écrans <br><br>Pour garantir des performances cohérentes et que la barre reste à l’emplacement approprié, ouvrez la boîte de dialogue **options** de votre application Office et, sous **général**, sélectionnez **optimiser pour la compatibilité** plutôt que **optimiser pour une meilleure apparence**.    |
|**Prise en charge d’IRM dans Office 2016**| Le paramètre de Registre [DRMEncryptProperty](/deployoffice/security/protect-sensitive-messages-and-documents-by-using-irm-in-office#office-2016-irm-registry-key-options) , qui contrôle le chiffrement des métadonnées dans Office 2016, n’est pas pris en charge pour les étiquettes de Azure information protection.|
|**Accès au modèle objet Outlook** | -Le paramètre de Registre [PromptOOMAddressBookAccess](/outlook/troubleshoot/security/information-about-email-security-settings#configure-a-prompt-when-a-program-accesses-an-address-book-by-using-the-outlook-object-model) , qui contrôle les invites qui s’affichent lorsque les carnets d’adresses sont accessibles via le modèle objet Outlook, n’est pas pris en charge avec les étiquettes Azure information protection. <br><br>-Le paramètre de Registre [PromptOOMAddressInformationAccess](/outlook/troubleshoot/security/information-about-email-security-settings#configure-a-prompt-when-a-program-reads-address-information-by-using-the-outlook-object-model) , qui contrôle les invites qui s’affichent lorsqu’un programme lit les informations d’adresse, n’est pas pris en charge pour les étiquettes de Azure information protection.|
|**Marquages de contenu dans Word**    | Les [marquages de contenu](configure-policy-markings.md) AIP dans les en-têtes ou pieds de page de Microsoft Word peuvent être décalés ou placés de manière incorrecte, ou peuvent être masqués entièrement, lorsque ce même en-tête ou pied de page contient également un tableau.<br><br>Pour plus d’informations, consultez la page [quand des marquages visuels sont appliqués](configure-policy-markings.md#when-visual-markings-are-applied). |
|**Fichiers joints aux courriers électroniques** |En raison d’une limitation dans les mises à jour Windows récentes, lorsque [Microsoft Outlook est protégé par Azure Rights Management](office-apps-services-support.md), les fichiers joints aux courriers électroniques peuvent être verrouillés après l’ouverture du fichier. |
|**Fusion et publipostage**    |  La fonctionnalité [Publipostage](https://support.office.com/article/use-mail-merge-for-bulk-email-letters-labels-and-envelopes-f488ed5b-b849-4c11-9cff-932c49474705) n’est pas prise en charge avec les fonctionnalités Azure Information Protection.       |
| **Courriers électroniques S/MIME** | L’ouverture des e-mails S/MIME dans le volet de lecture d’Outlook peut entraîner des problèmes de performances. <br><br>Pour éviter les problèmes de performances avec les e-mails S/MIME, activez la propriété avancée [**OutlookSkipSmimeOnReadingPaneEnabled**](rms-client/clientv2-admin-guide-customizations.md#prevent-outlook-performance-issues-with-smime-emails) . <br><br>**Remarque**: l’activation de cette propriété empêche l’affichage de la barre AIP ou de la classification des messages dans le volet de lecture d’Outlook. |
|**Option Envoyer vers l’Explorateur de fichiers** |Si vous choisissez de cliquer avec le bouton droit sur un fichier dans l’Explorateur de fichiers et que vous sélectionnez **Envoyer à > destinataire du courrier**, le message Outlook qui s’ouvre avec le fichier joint peut ne pas afficher la barre d’outils AIP. <br><br>Si cela se produit et que vous devez utiliser les options de la barre d’outils AIP, commencez votre adresse de messagerie à partir d’Outlook, puis accédez au fichier que vous souhaitez envoyer et joignez-le.|
|**Co-création** |La prise en charge de la co-création est assurée par une [installation dédiée](rms-client/unifiedlabelingclient-version-release-history.md#version-210460-for-co-authoring-public-preview) du client Azure information protection et est actuellement en version préliminaire publique. <br><br>Pour plus d’informations, consultez [problèmes connus pour la co-création (](#known-issues-for-co-authoring-public-preview)préversion publique). |
| | |

### <a name="known-issues-for-co-authoring-public-preview"></a>Problèmes connus de la co-création (version préliminaire publique)

- [Utiliser dans les environnements de test uniquement](#use-in-testing-environments-only)
- [Versions prises en charge pour les étiquettes de co-création et de sensibilité](#supported-versions-for-co-authoring-and-sensitivity-labels)
- [Mises à jour de stratégie](#policy-updates)
- [Journaux d’analyse et d’audit AIP](#aip-analytics-and-audit-logs)
- [Étiquettes avec des autorisations définies par l’utilisateur](#labels-with-user-defined-permissions)
- [Fonctionnalités non prises en charge pour la co-création](#unsupported-features-for-co-authoring)

> [!IMPORTANT]
> Les étiquettes de co-création et de sensibilité ne peuvent pas être déployées sur certains utilisateurs uniquement, car les nouvelles étiquettes ne sont pas visibles par les utilisateurs ayant une version antérieure du client Office.
> 
Pour plus d’informations sur la prise en charge de la co-création, y compris les limitations et les problèmes connus de la version préliminaire publique, consultez la [documentation Microsoft 365](/microsoft-365/compliance/sensitivity-labels-coauthoring).

#### <a name="use-in-testing-environments-only"></a>Utiliser dans les environnements de test uniquement

Pour éviter les conflits entre vos fichiers étiquetés, la co-création ne peut pas être désactivée sans l’assistance du support client pendant la période de la version préliminaire publique.

Pour cette raison, nous vous recommandons d’activer la co-création pour votre système dans les environnements de test uniquement.

#### <a name="supported-versions-for-co-authoring-and-sensitivity-labels"></a>Versions prises en charge pour les étiquettes de co-création et de sensibilité

L’ensemble des applications, services et outils opérationnels de votre locataire doivent prendre en charge la co-création.

Avant de commencer, assurez-vous que votre système est conforme à la configuration requise indiquée dans la [Microsoft 365 conditions préalables pour la co-création](/microsoft-365/compliance/sensitivity-labels-coauthoring#prerequisites).

> [!NOTE]
> Alors que les étiquettes de sensibilité peuvent être appliquées aux fichiers dans les formats Office 97-2003, tels que  **. doc**, **. ppt** et **. xls**, la co-création de ces types de fichiers n’est pas prise en charge. Une fois qu’une étiquette est appliquée à un fichier nouvellement créé, ou à un fichier au format de fichier avancé, tel que **. docx**, **. pptx** et **. xlsx**, l’enregistrement du fichier au format Office 97-2003 entraîne la suppression de l’étiquette.
> 

#### <a name="policy-updates"></a>Mises à jour de stratégie

Si votre stratégie d’étiquetage a été mise à jour lors de l’ouverture d’une application Office avec Azure Information Protection, toute nouvelle étiquette s’affiche, mais l’application de ces étiquettes génère une erreur. 

Si cela se produit, fermez et rouvrez votre application Office pour pouvoir appliquer vos étiquettes.

#### <a name="aip-analytics-and-audit-logs"></a>Journaux d’analyse et d’audit AIP

Lorsque la co-création est activée, le client Azure Information Protection n’envoie aucun [Journal d’audit](audit-logs.md).

#### <a name="labels-with-user-defined-permissions"></a>Étiquettes avec des autorisations définies par l’utilisateur

Dans Microsoft Word, Excel et PowerPoint, les étiquettes avec des autorisations définies par l’utilisateur sont toujours disponibles et peuvent être appliquées aux documents, mais ne sont pas prises en charge pour les fonctionnalités de co-création. 

Cela signifie que l’application d’une étiquette avec des autorisations définies par l’utilisateur vous empêchera de travailler sur le document avec d’autres utilisateurs en même temps.

#### <a name="unsupported-features-for-co-authoring"></a>Fonctionnalités non prises en charge pour la co-création

Les fonctionnalités suivantes ne sont pas prises en charge lors de l’utilisation de la co-création et des étiquettes de sensibilité :

- **Les modèles DKE et les propriétés définies par l’utilisateur DKE**. Pour plus d’informations, consultez [chiffrement à clé double (DKE)](plan-implement-tenant-key.md#double-key-encryption-dke).

- **Suppression du marquage de contenu externe dans les applications**. Pour plus d’informations, consultez [Côté client d’Azure Information Protection](rms-client/use-client.md).

- Les paramètres avancés suivants :

    - **customPropertiesByLabel**. Pour plus d’informations, consultez [application d’une propriété personnalisée lorsqu’une étiquette est appliquée](rms-client/clientv2-admin-guide-customizations.md#apply-a-custom-property-when-a-label-is-applied).

    - **labelByCustomProperties** et **EnableLabelBySharePointProperties**. Pour plus d’informations, consultez [migrer des étiquettes à partir d’îlots sécurisés et d’autres solutions d’étiquetage](rms-client/clientv2-admin-guide-customizations.md#migrate-labels-from-secure-islands-and-other-labeling-solutions).

## <a name="known-issues-in-policies"></a>Problèmes connus dans les stratégies

La publication des stratégies peut prendre jusqu’à 24 heures.

## <a name="maximum-file-sizes"></a>Tailles maximales de fichiers

Les fichiers de plus de 2 Go sont pris en charge pour la protection, mais pas pour le déchiffrement.

## <a name="known-issues-for-the-aip-viewer"></a>Problèmes connus de la visionneuse AIP

- [Modes paysage](#landscape-views-in-the-aip-viewer)
- [Utilisateurs externes](#external-users-and-the-aip-viewer)

Pour plus d’informations, consultez [ **client d’étiquetage unifié**: afficher les fichiers protégés avec la visionneuse de Azure information protection](rms-client/clientv2-view-use-files.md).
### <a name="landscape-views-in-the-aip-viewer"></a>Affichages en mode paysage dans la visionneuse AIP

La visionneuse AIP affiche des images en mode portrait, et certaines images larges et de vue paysage peuvent sembler étirées.

Par exemple, une image d’origine est représentée ci-dessous à gauche, avec une version en mode portrait étirée dans la visionneuse AIP à droite. 

:::image type="content" source="media/client-viewer-stretched-images.PNG" alt-text="Image étirée dans la visionneuse cliente":::

### <a name="external-users-and-the-aip-viewer"></a>Utilisateurs externes et visionneuse AIP 

Si un utilisateur externe a déjà un compte invité dans Azure AD, la visionneuse AIP peut afficher une erreur quand l’utilisateur ouvre un document protégé, lui indiquant qu’il ne peut pas se connecter avec un compte personnel.

Si une telle erreur s’affiche, l’utilisateur doit installer [Adobe Acrobat DC avec l’extension MIP](https://helpx.adobe.com/il_en/acrobat/kb/mip-plugin-download.html) afin d’ouvrir le document protégé.

Lors de l’ouverture du document protégé après l’installation d’Adobe Acrobat DC avec l’extension MIP, l’utilisateur peut toujours voir une erreur indiquant que le compte d’utilisateur sélectionné n’existe pas dans le locataire et lui demander de sélectionner un compte. 

Il s’agit d’une erreur attendue. Dans la fenêtre d’invite, sélectionnez **précédent** pour continuer à ouvrir le document protégé.

## <a name="known-issues-for-track-and-revoke-features-public-preview"></a>Problèmes connus pour les fonctionnalités de suivi et de révocation (version préliminaire publique)

Le suivi et la révocation de l’accès aux documents à l’aide du client d’étiquetage unifié présente les problèmes connus suivants :

- [Documents protégés par mot de passe](#password-protected-documents)
- [Plusieurs pièces jointes dans un e-mail protégé](#multiple-attachments-in-a-protected-email)
- [Documents accessibles via SharePoint ou OneDrive](#documents-accessed-via-sharepoint-or-onedrive)

Pour plus d’informations, consultez le Guide de l' [administrateur](rms-client/track-and-revoke-admin.md) et les procédures du Guide de l' [utilisateur](rms-client/revoke-access-user.md) .

#### <a name="password-protected-documents"></a>Documents protégés par mot de passe

Les documents protégés par mot de passe ne sont pas pris en charge par les fonctionnalités suivre et révoquer.
#### <a name="multiple-attachments-in-a-protected-email"></a>Plusieurs pièces jointes dans un e-mail protégé

Si vous joignez plusieurs documents à un message électronique, puis Protégez l’e-mail et l’envoyez, chacune des pièces jointes obtient la même valeur ContentID.

Cette valeur ContentID est retournée uniquement avec le premier fichier qui avait été ouvert. La recherche des autres pièces jointes ne retourne pas la valeur ContentID requise pour obtenir les données de suivi.

En outre, la révocation de l’accès pour l’une des pièces jointes révoque également l’accès aux autres pièces jointes dans le même e-mail protégé.

#### <a name="documents-accessed-via-sharepoint-or-onedrive"></a>Documents accessibles via SharePoint ou OneDrive

- Les documents protégés qui sont téléchargés sur SharePoint ou OneDrive perdent leur valeur **contentid** , et l’accès ne peut pas être suivi ou révoqué.

- Si un utilisateur télécharge le fichier à partir de SharePoint ou OneDrive et y accède à partir de son ordinateur local, une nouvelle **contentid** est appliquée au document lorsqu’il l’ouvre localement.

    L’utilisation de la valeur **contentid** d’origine pour le suivi des données n’inclut pas les accès effectués pour le fichier téléchargé de l’utilisateur. En outre, la révocation de l’accès basé sur la valeur **contentid** d’origine ne révoque pas l’accès pour les fichiers téléchargés.

    Dans ce cas, les administrateurs peuvent être en mesure de localiser les fichiers téléchargés à l’aide de PowerShell pour rechercher les nouvelles valeurs **contentid** pour suivre ou révoquer l’accès.

### <a name="known-issues-for-the-aip-client-and-onedrive"></a>Problèmes connus liés au client AIP et à OneDrive

Si vous avez des documents stockés dans OneDrive avec une étiquette de sensibilité appliquée et qu’un administrateur modifie l’étiquette dans la stratégie d’étiquetage pour ajouter une protection, la protection récemment appliquée n’est pas appliquée automatiquement au document étiqueté. 

Dans ce cas, renommez le document manuellement pour appliquer la protection en fonction des besoins.
## <a name="aip-and-legacy-windows-and-office-versions"></a>AIP et versions héritées de Windows et d’Office

- La [**prise en charge étendue de Windows 7 a pris fin le 14 janvier 2020**](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).

    Nous vous encourageons vivement à effectuer une mise à niveau vers une version plus récente de Windows 10.

    Toutefois, si vous avez étendu des mises à jour de sécurité (UDE) et un contrat de support, le support AIP est disponible pour maintenir la sécurité de vos systèmes Windows 7.

    Pour plus d’informations, consultez votre contact de support technique.

- [**Le support étendu Office 2010 a pris fin le 13 octobre 2020**](https://support.microsoft.com/lifecycle/search?alpha=office%202010).

    Cette prise en charge n’est pas étendue et l’UDE n’est pas proposée pour Office 2010.

    Nous vous encourageons vivement à effectuer une mise à niveau vers une version plus récente d’Office 365.

    Pour plus d’informations, consultez votre contact de support technique.

## <a name="aip-based-conditional-access-policies"></a>Stratégies d’accès conditionnel basées sur AIP

Les utilisateurs externes qui reçoivent du contenu protégé par des [stratégies d’accès conditionnel](/azure/active-directory/conditional-access/concept-conditional-access-policy-common) doivent disposer d’un compte d’utilisateur invité de collaboration Business-to-Business (B2B) Azure Active Directory (Azure AD) pour pouvoir afficher le contenu.

Bien que vous puissiez inviter des utilisateurs externes à activer un compte d’utilisateur invité, ce qui leur permet de s’authentifier et de répondre aux exigences en matière d’accès conditionnel, il peut être difficile de s’assurer que cela se produit pour tous les utilisateurs externes requis.

Nous vous recommandons d’activer les stratégies d’accès conditionnel basé sur AIP pour vos utilisateurs internes uniquement.

**Activez les stratégies d’accès conditionnel pour AIP pour les utilisateurs internes uniquement**:

1.  Dans le Portail Azure, accédez au panneau **accès conditionnel** , puis sélectionnez la stratégie d’accès conditionnel que vous souhaitez modifier.
2.  Sous **affectations**, sélectionnez **utilisateurs et groupes**, puis sélectionnez **tous les utilisateurs**. Assurez-vous que l’option **tous les utilisateurs invités et externes** n’est *pas* sélectionnée.
3.  Enregistrez vos modifications.

Vous pouvez également désactiver entièrement l’autorité de certification dans Azure Information Protection si cette fonctionnalité n’est pas requise pour votre organisation, afin d’éviter ce problème potentiel.

Pour plus d’informations, consultez la [documentation relative à l’accès conditionnel](/azure/active-directory/conditional-access/concept-conditional-access-users-groups).

## <a name="more-information"></a>Plus d’informations

Les articles supplémentaires suivants peuvent être utiles pour répondre à des questions sur les problèmes connus dans Azure Information Protection :

- [Forum aux questions sur Azure Information Protection](faqs.md)
- [Forum aux questions sur la protection des données dans Azure Information Protection](faqs-rms.md)
- [Forum aux questions sur la classification et l’étiquetage dans Azure Information Protection](faqs-infoprotect.md)
- [FAQ pour l’application Microsoft Azure Information Protection pour iOS et Android](rms-client/mobile-app-faq.md)