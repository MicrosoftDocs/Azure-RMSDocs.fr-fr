---
title: Règles de workflow du courrier Exchange Online pour les étiquettes Azure Information Protection
description: Instructions et exemples pour configurer des règles de flux de messagerie Exchange Online pour les étiquettes Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ba4e4a4d-5280-4e97-8f5c-303907db1bf5
ROBOTS: NOINDEX
ms.reviewer: shakella
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 7c76e7e79acb0cd12bfcbe2d71a1fee3ce78b1ba
ms.sourcegitcommit: 78c7ab80be7c292ea4bc62954a4e29c449e97439
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/13/2021
ms.locfileid: "98164281"
---
# <a name="configuring-exchange-online-mail-flow-rules-for-azure-information-protection-labels"></a>Configuration des règles de flux de messagerie Exchange Online pour les étiquettes Azure Information Protection

>***S’applique à** : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Concerne :** [Azure information protection client classique pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Pour le client d’étiquetage unifié, consultez [en savoir plus sur les étiquettes de sensibilité](/microsoft-365/compliance/sensitivity-labels) et les [étiquettes DLP](/microsoft-365/compliance/dlp-sensitivity-label-as-condition) dans la documentation de Microsoft 365. *

> [!NOTE] 
> Pour fournir une expérience client unifiée et homogène, le **client classique Azure Information Protection** et la **gestion des étiquettes** dans le portail Azure seront **dépréciés** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Les informations suivantes vous permettent de configurer des règles de flux de messagerie dans Exchange Online pour utiliser des étiquettes Azure Information Protection et appliquer une protection supplémentaire dans des scénarios spécifiques. Par exemple :

- Votre étiquette par défaut est **Général**, qui n’applique pas de protection. Pour les e-mails avec cette étiquette qui sont envoyés à l’extérieur, appliquer l’action de protection supplémentaire Ne pas transférer.

- Si une pièce jointe avec une étiquette **confidentiel \ Partners** est envoyé par courrier électronique à des personnes extérieures à l’organisation et que le courrier électronique n’est pas protégé, appliquez l’action de protection en chiffre uniquement supplémentaire.

Les règles de flux de messagerie qui appliquent la protection en tant qu’action sont ignorées si l’e-mail est déjà protégé. Par exemple, un message électronique qui a été protégé par ne pas transférer ne peut pas être modifié par une règle de workflow de courrier Exchange pour utiliser l’option de chiffrement uniquement.  

Vous pouvez étendre ces exemples ainsi que les modifier. Par exemple, ajoutez plus de conditions. Pour plus d’informations sur la configuration des règles de flux de messagerie, consultez les [règles de flux de messagerie (règles de transport) dans Exchange Online](/exchange/security-and-compliance/mail-flow-rules/mail-flow-rules) dans la documentation d’Exchange Online.

Pour plus d’informations sur la configuration des règles de courrier électronique pour chiffrer les messages électroniques, consultez [définir des règles de courrier électronique pour chiffrer les messages électroniques dans Microsoft 365](https://support.office.com/article/define-mail-flow-rules-to-encrypt-email-messages-in-office-365-9b7daf19-d5f2-415b-bc43-a0f5f4a585e8) à partir de la documentation Office. 

## <a name="prerequisite-know-your-label-guid"></a>Condition préalable : connaître le GUID de votre étiquette

Étant donné qu’une étiquette Azure Information Protection est stockée dans les métadonnées, les règles de flux de messagerie dans Exchange Online peuvent lire ces informations pour les messages et les pièces jointes des documents Office. Les règles de flux de messagerie ne prennent pas en charge l’inspection des métadonnées pour les documents PDF.

Avant de configurer les règles de flux de messagerie pour identifier les messages et les documents étiquetés, assurez-vous que vous connaissez le GUID de l’étiquette Azure Information Protection que vous souhaitez utiliser. 

Pour plus d’informations sur les métadonnées stockées par une étiquette et sur la façon d’identifier les GUID d’étiquettes, consultez [Étiqueter les informations stockées dans des e-mails et des documents](configure-policy.md#label-information-stored-in-emails-and-documents).

## <a name="example-configurations"></a>Exemples de configurations

Pour les exemples suivants, créez une nouvelle règle de flux de messagerie en procédant comme suit :

1. Dans un navigateur Web, à l’aide d’un compte professionnel ou scolaire disposant des autorisations d’administrateur général, connectez-vous à Microsoft 365. 

2. Choisissez la vignette **admin** .

3. Dans le centre d’administration Microsoft 365, choisissez **administration centres**  >  **Exchange**.

4. Dans le centre d’administration Exchange : règles de **courrier électronique**  >    >  **+**  >  **créez une nouvelle règle**. 

> [!TIP]
> Si vous rencontrez des problèmes avec l’interface utilisateur lorsque vous configurez vos règles, essayez un autre navigateur, tel qu’Internet Explorer.

Les exemples ont une seule condition qui applique une protection quand un e-mail est envoyé à l’extérieur de l’organisation. Pour plus d’informations sur les autres conditions que vous pouvez sélectionner, consultez les [conditions de règle de flux de messagerie et exceptions (prédicats) dans Exchange Online](/exchange/security-and-compliance/mail-flow-rules/conditions-and-exceptions).


### <a name="example-1-rule-that-applies-the-do-not-forward-option-to-emails-that-are-labeled-general-when-they-are-sent-outside-the-organization"></a>Exemple 1 : Règle qui applique l’option Ne pas transférer à des e-mails étiquetés **Général** lorsqu’ils sont envoyés en dehors de l’organisation

Dans cet exemple, l’étiquette **Général** a un GUID de 0e421e6d-ea17-4fdb-8f01-93a3e71333b8. Remplacez par votre propre étiquette ou sous-étiquette GUID que vous souhaitez utiliser avec cette règle. 

Dans la stratégie Azure Information Protection, cette étiquette a été configurée comme l’étiquette par défaut pour classifier des e-mails en tant que **Généraux**, et l’étiquette n’applique pas de protection. 

1. Dans **Nom**, donnez un nom à la règle, par exemple `Apply Do Not Forward for General emails sent externally`.
 
2. Pour **Appliquer cette règle si** : sélectionnez **Le destinataire se trouve**, **En dehors de l’organisation**, puis **OK**.

3. Sélectionnez **Davantage d’options**, puis **Ajouter une condition**.
 
4. Pour **et** : sélectionnez **Un en-tête de message**, puis **Inclut au moins un de ces mots** :
     
    a. Sélectionnez **Entrer du texte**, puis entrez `msip_labels`.
     
    b. Sélectionnez **Entrer des mots**, puis entrez `MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled=True`.
    
    c. Sélectionnez **+** , puis cliquez sur **OK**.

5. Pour **Procédez comme suit** : sélectionnez **Modifier la sécurité des messages** > **Appliquer le chiffrement de messages Office 365 et la protection des droits** > **Ne pas transférer**, puis sélectionnez **OK**.
    
    La configuration de votre règle doit maintenant ressembler à ce qui suit :  ![ règle de workflow de courrier Exchange Online configurée pour un Azure information protection étiquette-exemple 1](./media/aip-exo-rule-ex1.png)

7. Sélectionnez **Enregistrer**. 

Pour plus d’informations sur l’option Ne pas transférer, consultez [option Ne pas transférer pour les e-mails](configure-usage-rights.md#do-not-forward-option-for-emails).

### <a name="example-2-rule-that-applies-the-encrypt-only-option-to-emails-when-they-have-attachments-that-are-labeled-confidential--partners-and-these-emails-are-sent-outside-the-organization"></a>Exemple 2 : règle qui applique l’option de chiffrement uniquement aux e-mails lorsqu’ils ont des pièces jointes étiquetées **confidentiels** et que ces messages électroniques sont envoyés à l’extérieur de l’Organisation

Dans cet exemple, la sous-étiquette **Confidentiel\Partenaires** a le GUID 0e421e6d-ea17-4fdb-8f01-93a3e71333b8. Remplacez par votre propre étiquette ou sous-étiquette GUID que vous souhaitez utiliser avec cette règle. 

Cette étiquette est utilisée pour classifier et protéger des documents que vous utilisez pour la collaboration avec des partenaires.   

1. Dans **Nom**, donnez un nom à la règle, par exemple `Apply Encrypt to emails sent externally if protected attachments`.
 
2. Pour **Appliquer cette règle si** : sélectionnez **Le destinataire se trouve**, **En dehors de l’organisation**, puis **OK**.

3. Sélectionnez **Davantage d’options**, puis **Ajouter une condition**.
 
4. Pour **et** : sélectionnez **Toutes les pièces jointes**, puis **a ces propriétés, y compris tous ces mots** :
     
    a. Sélectionnez **+**  >  **spécifier une propriété de pièce jointe personnalisée**.
  
    b. Pour **Propriété**, entrez `MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled`.
    
    c. Pour **Valeur**, entrez `True`.
    
    d. Sélectionnez **Enregistrer**, puis **OK**.

5. Pour **Procédez comme suit** : sélectionnez **Modifier la sécurité des messages** > **Appliquer le chiffrement de messages Office 365 et la protection des droits** > **Chiffrer**, puis sélectionnez **OK**.
    
    La configuration de votre règle doit maintenant ressembler à ce qui suit :  ![ règle de workflow de courrier Exchange Online configurée pour un Azure information protection étiquette-exemple 2](./media/aip-exo-rule-ex2.png)

6. Sélectionnez **Enregistrer**. 

Pour plus d’informations sur l’option Encrypt, consultez [option encrypt uniquement pour les e-mails](configure-usage-rights.md#encrypt-only-option-for-emails).


## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la création et la configuration des étiquettes à utiliser avec les règles de flux de messagerie Exchange Online, consultez [Stratégie de configuration d’Azure Information Protection](configure-policy.md).

En outre, pour aider à classifier les messages électroniques contenant des pièces jointes, envisagez d’utiliser le [paramètre de stratégie](configure-policy-settings.md) Azure Information Protection suivant : **pour les messages électroniques avec des pièces jointes, appliquez une étiquette qui correspond à la classification la plus élevée de ces pièces jointes**.