---
title: Configurer des règles de flux de messagerie Exchange Online pour les étiquettes Azure Information Protection
description: Instructions et exemples pour configurer des règles de flux de messagerie Exchange Online pour les étiquettes Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/27/2018
ms.topic: article
ms.service: information-protection
ms.assetid: ba4e4a4d-5280-4e97-8f5c-303907db1bf5
ms.reviewer: shakella
ms.suite: ems
ms.openlocfilehash: 322972000ff68194f0df94949b919aef5b2a1c3c
ms.sourcegitcommit: 7ba9850e5bb07b14741bb90ebbe98f1ebe057b10
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42804407"
---
# <a name="configuring-exchange-online-mail-flow-rules-for-azure-information-protection-labels"></a>Configuration des règles de flux de messagerie Exchange Online pour les étiquettes Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Les informations suivantes vous permettent de configurer des règles de flux de messagerie dans Exchange Online pour utiliser des étiquettes Azure Information Protection et appliquer une protection supplémentaire dans des scénarios spécifiques. Par exemple :

- Votre étiquette par défaut est **Général**, qui n’applique pas de protection. Pour les e-mails avec cette étiquette qui sont envoyés à l’extérieur, appliquer l’action de protection supplémentaire Ne pas transférer.

- Si une pièce jointe avec une étiquette **Confidentiel\Partenaires** est envoyée par courrier électronique à des personnes extérieures à l’organisation et que l’e-mail n’est pas protégé, appliquez l’action de protection supplémentaire Chiffrer uniquement.

Les règles de flux de messagerie qui appliquent la protection en tant qu’action sont ignorées si l’e-mail est déjà protégé. Par exemple, un message électronique qui a été protégé par Ne pas transférer ne peut pas être modifié par une règle de flux de messagerie Exchange pour utiliser l’option Chiffrement seul.  

Vous pouvez étendre ces exemples ainsi que les modifier. Par exemple, ajoutez plus de conditions. Pour plus d’informations sur la configuration des règles de flux de messagerie, consultez [messagerie règles de flux (règles de transport) dans Exchange Online] (https://technet.microsoft.com/library/jj919238(v=exchg.150\).aspx) dans la documentation d’Exchange Online.

Pour plus d’informations sur la configuration des règles de flux de messagerie afin de chiffrer des messages électroniques, consultez [Définir des règles de flux de messagerie pour chiffrer des messages électroniques dans Office 365](https://support.office.com/article/define-mail-flow-rules-to-encrypt-email-messages-in-office-365-9b7daf19-d5f2-415b-bc43-a0f5f4a585e8) dans la documentation d’Office. 

## <a name="where-labels-are-stored-in-emails-and-documents"></a>Où les étiquettes sont stockées dans des e-mails et des documents

Étant donné qu’une étiquette Azure Information Protection est stockée dans les métadonnées, les règles de flux de messagerie dans Exchange Online peuvent lire ces informations pour les messages et les pièces jointes des documents :

- Dans les e-mails, ces informations sont stockées dans l’en-tête x- : **msip_labels: MSIP_Label_\<GUID>_Enabled=True;** 

- Pour les documents Word (.doc et .docx), les feuilles de calcul Excel (.xls et .xlsx), les présentations PowerPoint (.ppt et .pptx) et les documents PDF (.pdf), ces métadonnées sont stockées dans la propriété personnalisée suivante : **MSIP_Label_\<GUID>_Enabled=True**  

Pour identifier le GUID d’une étiquette, recherchez la valeur de l’ID de l’étiquette dans le panneau **Étiquette** quand vous affichez ou configurez la stratégie Azure Information Protection dans le portail Azure. Pour les fichiers auxquels des étiquettes sont appliquées, vous pouvez également exécuter l’applet de commande PowerShell [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) pour identifier le GUID (MainLabelId ou SubLabelId). Si une étiquette a des sous-étiquettes, spécifiez toujours le GUID de la sous-étiquette et non celui de l’étiquette parente.

Avant de configurer vos règles de flux de messagerie, assurez-vous que vous connaissez le GUID de l’étiquette Azure Information Protection que vous souhaitez utiliser.

## <a name="example-configurations"></a>Exemples de configurations

Pour les exemples suivants, créez une nouvelle règle de flux de messagerie en procédant comme suit :

1. Dans un navigateur web, à l’aide d’un compte professionnel ou scolaire qui dispose des autorisations d’administrateur général, connectez-vous à Office 365. 

2. Cliquez sur la vignette **Administration**.

3. Dans le centre d'administration Office 365, choisissez **Centres d’administration** > **Exchange**.

4. Dans le centre d’administration Exchange : **flux de messagerie** > **règles** > **+** > **Créer une nouvelle règle**. 

> [!TIP]
> Si vous rencontrez des problèmes avec l’interface utilisateur lorsque vous configurez vos règles, essayez un autre navigateur, tel qu’Internet Explorer.

Les exemples ont une seule condition qui applique une protection quand un e-mail est envoyé à l’extérieur de l’organisation. Pour plus d’informations sur les autres conditions que vous pouvez sélectionner, consultez [conditions de règle de flux de messagerie et exceptions (prédicats) dans Exchange Online] (https://technet.microsoft.com/library/jj919235(v=exchg.150\).aspx).


### <a name="example-1-rule-that-applies-the-do-not-forward-option-to-emails-that-are-labeled-general-when-they-are-sent-outside-the-organization"></a>Exemple 1 : Règle qui applique l’option Ne pas transférer à des e-mails étiquetés **Général** lorsqu’ils sont envoyés en dehors de l’organisation

Dans cet exemple, l’étiquette **Général** a un GUID de 0e421e6d-ea17-4fdb-8f01-93a3e71333b8. Remplacez par votre propre étiquette ou sous-étiquette GUID que vous souhaitez utiliser avec cette règle. 

Dans la stratégie Azure Information Protection, cette étiquette a été configurée comme l’étiquette par défaut pour classifier des e-mails en tant que **Généraux**, et l’étiquette n’applique pas de protection. 

1. Dans **Nom**, donnez un nom à la règle, par exemple `Apply Do Not Forward for General emails sent externally`.
 
2. Pour **Appliquer cette règle si** : sélectionnez **Le destinataire se trouve**, **En dehors de l’organisation**, puis **OK**.

3. Sélectionnez **Davantage d’options**, puis **Ajouter une condition**.
 
4. Pour **et** : sélectionnez **Un en-tête de message**, puis **Inclut au moins un de ces mots** :
     
    a. Sélectionnez **Entrer du texte**, puis entrez `msip_labels`.
     
    b. Sélectionnez **Entrer des mots**, puis entrez `MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled=True;`.
    
    c. Sélectionnez **+**, puis **OK**.

5. Pour **Procédez comme suit** : sélectionnez **Modifier la sécurité des messages** > **Appliquer le chiffrement de messages Office 365 et la protection des droits**  >  **Ne pas transférer**, puis sélectionnez **OK**.
    
    La configuration de votre règle doit maintenant ressembler à ce qui suit : ![Règle de flux de messagerie Exchange Online configurée pour une étiquette Azure Information Protection – exemple1](./media/aip-exo-rule-ex1.png)

7. Sélectionnez **Enregistrer**. 

Pour plus d’informations sur l’option Ne pas transférer, consultez [option Ne pas transférer pour les e-mails](configure-usage-rights.md#do-not-forward-option-for-emails).

### <a name="example-2-rule-that-applies-the-encrypt-only-option-to-emails-when-they-have-attachments-that-are-labeled-confidential--partners-and-these-emails-are-sent-outside-the-organization"></a>Exemple 2 : Règle qui applique l’option Chiffrement seul à des e-mails qui ont des pièces jointes étiquetées **Confidentiel\Partenaires** et ces e-mails sont envoyés en dehors de l’organisation

Dans cet exemple, la sous-étiquette **Confidentiel\Partenaires** possède un GUID de 5ab1c8a1-8241-72bc-3f22-304a0558362a. Remplacez par votre propre étiquette ou sous-étiquette GUID que vous souhaitez utiliser avec cette règle. 

Cette étiquette est utilisée pour classifier et protéger des documents que vous utilisez pour la collaboration avec des partenaires.   

1. Dans **Nom**, donnez un nom à la règle, par exemple `Apply Encrypt to emails sent externally if protected attachments`.
 
2. Pour **Appliquer cette règle si** : sélectionnez **Le destinataire se trouve**, **En dehors de l’organisation**, puis **OK**.

3. Sélectionnez **Davantage d’options**, puis **Ajouter une condition**.
 
4. Pour **et** : sélectionnez **Toutes les pièces jointes**, puis **a ces propriétés, y compris tous ces mots** :
     
    a. Sélectionnez **+** > **Spécifier une propriété de pièce jointe personnalisée**.
  
    b. Pour **Propriété**, entrez `MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled`.
    
    c. Pour **Valeur**, entrez `True`.
    
    d. Sélectionnez **Enregistrer**, puis **OK**.

5. Pour **Procédez comme suit** : sélectionnez **Modifier la sécurité des messages** > **Appliquer le chiffrement de messages Office 365 et la protection des droits**  >  **Chiffrer**, puis sélectionnez **OK**.
    
    La configuration de votre règle doit maintenant ressembler à ce qui suit : ![Règle de flux de messagerie Exchange Online configurée pour une étiquette Azure Information Protection – exemple1](./media/aip-exo-rule-ex2.png)

6. Sélectionnez **Enregistrer**. 

Pour plus d’informations sur l’option de chiffrement, consultez [option Chiffrement seul pour les e-mails](configure-usage-rights.md#encrypt-only-option-for-emails).


## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la création et la configuration des étiquettes à utiliser avec les règles de flux de messagerie Exchange Online, consultez [Stratégie de configuration d’Azure Information Protection](configure-policy.md).

En outre, pour aider à classifier les messages électroniques contenant des pièces jointes, envisagez d’utiliser le [paramètre de stratégie](configure-policy-settings.md) Azure Information Protection suivant : **pour les messages électroniques avec des pièces jointes, appliquez une étiquette qui correspond à la classification la plus élevée de ces pièces jointes**.


