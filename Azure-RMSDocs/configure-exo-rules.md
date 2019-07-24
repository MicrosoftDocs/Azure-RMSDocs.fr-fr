---
title: Règles de workflow du courrier Exchange Online pour les étiquettes Azure Information Protection
description: Instructions et exemples pour configurer des règles de flux de messagerie Exchange Online pour les étiquettes Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ba4e4a4d-5280-4e97-8f5c-303907db1bf5
ms.reviewer: shakella
ms.suite: ems
ms.openlocfilehash: f738f990e6a4c2f79e4eede12431c1afe15803cd
ms.sourcegitcommit: 7992e1dc791d6d919036f7aa98bcdd21a6c32ad0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68428555"
---
# <a name="configuring-exchange-online-mail-flow-rules-for-azure-information-protection-labels"></a>Configuration des règles de flux de messagerie Exchange Online pour les étiquettes Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Les informations suivantes vous permettent de configurer des règles de flux de messagerie dans Exchange Online pour utiliser des étiquettes Azure Information Protection et appliquer une protection supplémentaire dans des scénarios spécifiques. Par exemple :

- Votre étiquette par défaut est **Général**, qui n’applique pas de protection. Pour les e-mails avec cette étiquette qui sont envoyés à l’extérieur, appliquer l’action de protection supplémentaire Ne pas transférer.

- Si une pièce jointe avec une étiquette **Confidentiel\Partenaires** est envoyée par courrier électronique à des personnes extérieures à l’organisation et que l’e-mail n’est pas protégé, appliquez l’action de protection supplémentaire Chiffrer uniquement.

Les règles de flux de messagerie qui appliquent la protection en tant qu’action sont ignorées si l’e-mail est déjà protégé. Par exemple, un message électronique qui a été protégé par Ne pas transférer ne peut pas être modifié par une règle de flux de messagerie Exchange pour utiliser l’option Chiffrement seul.  

Vous pouvez étendre ces exemples ainsi que les modifier. Par exemple, ajoutez plus de conditions. Pour plus d’informations sur la configuration des règles de flux de messagerie, consultez les [règles de flux de messagerie (règles de transport) dans Exchange Online](https://technet.microsoft.com/library/jj919238(v=exchg.150).aspx) dans la documentation d’Exchange Online.

Pour plus d’informations sur la configuration des règles de flux de messagerie afin de chiffrer des messages électroniques, consultez [Définir des règles de flux de messagerie pour chiffrer des messages électroniques dans Office 365](https://support.office.com/article/define-mail-flow-rules-to-encrypt-email-messages-in-office-365-9b7daf19-d5f2-415b-bc43-a0f5f4a585e8) dans la documentation d’Office. 

## <a name="prerequisite-know-your-label-guid"></a>Prérequis : Connaître le GUID de votre étiquette

Étant donné qu’une étiquette Azure Information Protection est stockée dans les métadonnées, les règles de flux de messagerie dans Exchange Online peuvent lire ces informations pour les messages et les pièces jointes des documents Office. Les règles de flux de messagerie ne prennent pas en charge l’inspection des métadonnées pour les documents PDF.

Avant de configurer les règles de flux de messagerie pour identifier les messages et les documents étiquetés, assurez-vous que vous connaissez le GUID de l’étiquette Azure Information Protection que vous souhaitez utiliser. 

Pour plus d’informations sur les métadonnées stockées par une étiquette et sur la façon d’identifier les GUID d’étiquettes, consultez [Étiqueter les informations stockées dans des e-mails et des documents](configure-policy.md#label-information-stored-in-emails-and-documents).

## <a name="example-configurations"></a>Exemples de configurations

Pour les exemples suivants, créez une nouvelle règle de flux de messagerie en procédant comme suit :

1. Dans un navigateur web, à l’aide d’un compte professionnel ou scolaire qui dispose des autorisations d’administrateur général, connectez-vous à Office 365. 

2. Cliquez sur la vignette **Administration**.

3. Dans le Centre d’administration Microsoft 365, choisissez **Centres d’administration** > **Exchange**.

4. Dans le centre d’administration Exchange : **flux de messagerie** > **règles** >  **+**  > **Créer une nouvelle règle**. 

> [!TIP]
> Si vous rencontrez des problèmes avec l’interface utilisateur lorsque vous configurez vos règles, essayez un autre navigateur, tel qu’Internet Explorer.

Les exemples ont une seule condition qui applique une protection quand un e-mail est envoyé à l’extérieur de l’organisation. Pour plus d’informations sur les autres conditions que vous pouvez sélectionner, consultez les [conditions de règle de flux de messagerie et exceptions (prédicats) dans Exchange Online](https://technet.microsoft.com/library/jj919235(v=exchg.150).aspx).


### <a name="example-1-rule-that-applies-the-do-not-forward-option-to-emails-that-are-labeled-general-when-they-are-sent-outside-the-organization"></a>Exemple 1 : Règle qui applique l’option Ne pas transférer à des e-mails étiquetés **Général** quand ils sont envoyés en dehors de l’organisation

Dans cet exemple, l’étiquette **Général** a un GUID de 0e421e6d-ea17-4fdb-8f01-93a3e71333b8. Remplacez par votre propre étiquette ou sous-étiquette GUID que vous souhaitez utiliser avec cette règle. 

Dans la stratégie Azure Information Protection, cette étiquette a été configurée comme l’étiquette par défaut pour classifier des e-mails en tant que **Généraux**, et l’étiquette n’applique pas de protection. 

1. Dans **Nom**, donnez un nom à la règle, par exemple `Apply Do Not Forward for General emails sent externally`.
 
2. Pour **Appliquer cette règle si** : Sélectionnez **Le destinataire se trouve**, **En dehors de l’organisation**, puis **OK**.

3. Sélectionnez **Davantage d’options**, puis **Ajouter une condition**.
 
4. Pour **et** : Sélectionnez **Un en-tête de message**, puis **Inclut au moins un de ces mots** :
     
    a. Sélectionnez **Entrer du texte**, puis entrez `msip_labels`.
     
    b. Sélectionnez **Entrer des mots**, puis entrez `MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled=True;`.
    
    c. Sélectionnez **+** , puis **OK**.

5. Pour **Exécutez les opérations suivantes** : Sélectionnez **Modifier la sécurité des messages** > **Appliquer le chiffrement de messages Office 365 et la protection des droits**  > **Ne pas transférer**, puis sélectionnez **OK**.
    
    Votre règle de configuration doit maintenant se présenter comme suit :  ![Règle de workflow Exchange Online configurée pour un Azure Information Protection étiquette-exemple 1](./media/aip-exo-rule-ex1.png)

7. Sélectionnez **Enregistrer**. 

Pour plus d’informations sur l’option Ne pas transférer, consultez [option Ne pas transférer pour les e-mails](configure-usage-rights.md#do-not-forward-option-for-emails).

### <a name="example-2-rule-that-applies-the-encrypt-only-option-to-emails-when-they-have-attachments-that-are-labeled-confidential--partners-and-these-emails-are-sent-outside-the-organization"></a>Exemple 2 : Règle qui applique l’option Chiffrer uniquement à des e-mails qui ont des pièces jointes étiquetées **Confidentiel\Partenaires** quand ces e-mails sont envoyés en dehors de l’organisation

Dans cet exemple, la sous-étiquette **Confidentiel\Partenaires** a le GUID 0e421e6d-ea17-4fdb-8f01-93a3e71333b8. Remplacez par votre propre étiquette ou sous-étiquette GUID que vous souhaitez utiliser avec cette règle. 

Cette étiquette est utilisée pour classifier et protéger des documents que vous utilisez pour la collaboration avec des partenaires.   

1. Dans **Nom**, donnez un nom à la règle, par exemple `Apply Encrypt to emails sent externally if protected attachments`.
 
2. Pour **Appliquer cette règle si** : Sélectionnez **Le destinataire se trouve**, **En dehors de l’organisation**, puis **OK**.

3. Sélectionnez **Davantage d’options**, puis **Ajouter une condition**.
 
4. Pour **et** : Sélectionnez **Toute pièce jointe**, puis **possède ces propriétés, lesquelles contiennent l’un de ces mots** :
     
    a. Sélectionnez **+**  > **Spécifier une propriété de pièce jointe personnalisée**.
  
    b. Pour **Propriété**, entrez `MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled`.
    
    c. Pour **Valeur**, entrez `True`.
    
    d. Sélectionnez **Enregistrer**, puis **OK**.

5. Pour **Exécutez les opérations suivantes** : Sélectionnez **Modifier la sécurité des messages** > **Appliquer le chiffrement de messages Office 365 et la protection des droits**  > **Chiffrer**, puis sélectionnez **OK**.
    
    Votre règle de configuration doit maintenant se présenter comme suit :  ![Règle de workflow Exchange Online configurée pour un Azure Information Protection étiquette-exemple 2](./media/aip-exo-rule-ex2.png)

6. Sélectionnez **Enregistrer**. 

Pour plus d’informations sur l’option de chiffrement, consultez [option Chiffrement seul pour les e-mails](configure-usage-rights.md#encrypt-only-option-for-emails).


## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la création et la configuration des étiquettes à utiliser avec les règles de flux de messagerie Exchange Online, consultez [Stratégie de configuration d’Azure Information Protection](configure-policy.md).

En outre, pour faciliter la classification des messages e-mail contenant des pièces jointes, envisagez d’utiliser le [paramètre de stratégie](configure-policy-settings.md) d’Azure Information Protection : **Pour les messages électroniques contenant des pièces jointes, appliquez une étiquette correspondant à la classification la plus élevée de ces pièces jointes**.


