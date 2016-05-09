![](../media/AzRMS_QuickStartSteps3.PNG)

Pour cette étape, commencez par créer et enregistrer un document Word qui représente le document que vous souhaitez protéger, puis nommez-le **Confidential.docx**. Dans le cadre de ce didacticiel, faites en sorte que le document contienne du texte, quel qu’il soit, afin de pouvoir confirmer plus facilement que le destinataire autorisé a pu le lire. Par exemple, vous pouvez saisir le texte suivant : **Si vous pouvez lire ce texte à partir de la pièce jointe de votre courrier électronique, l’expéditeur a réussi à partager un fichier protégé par Azure RMS.**

Ensuite, vous pouvez partager en toute sécurité ce document par courrier électronique.

![Captures d’écran de partage par courrier électronique Azure RMS](../media/AzRMS_Tutorial_3_Screenshots.png)

#### Partage en toute sécurité d’un document par courrier électronique

1.  Dans Outlook, créez un message et joignez le fichier que vous venez de créer.

2.  Dans la zone **À** , saisissez au moins une adresse de messagerie professionnelle. Veillez à indiquer une adresse de messagerie professionnelle, comme **janetm@contoso.com** ou **p.dover@fabrikam.com**, car Azure Rights Management ne prend actuellement pas en charge les adresses e-mail personnelles de votre fournisseur Internet que vous utilisez chez vous. Le fait de savoir si le destinataire possède également Azure Rights Management n’est pas important.

3.  Indiquez un objet, tel que  **Document confidentiel** , puis saisissez un bref message, tel que **Merci de lire ce document et de ne pas le partager.**

4.  Puis, sous l’onglet **Message** du groupe **RMS**, cliquez sur **Partage protégé**, puis à nouveau sur **Partage protégé** :

5.  Dans la boîte de dialogue **Partage protégé** :

    1.  Sélectionnez **Visionneuse – Affichage uniquement**.

        Cela signifie que les destinataires seront en mesure d’afficher le document, mais pas de le modifier ou de l’imprimer.

    2.  Sélectionnez **M’avertir par message électronique lorsque quelqu’un essaie d’ouvrir ces documents**.

        Vous recevrez une notification par courrier électronique chaque fois que les destinataires ou d’autres personnes tenteront d’ouvrir la pièce jointe, par exemple, si votre destinataire transfère le courrier à un collègue. Dans ce dernier scénario, vous verrez que l’accès a été refusé, et dans les détails de l’utilisateur, vous pouvez décider d’envoyer à cette personne une copie du document qu’elle peut ouvrir.

    3.  Sélectionnez **M’autoriser à révoquer de suite l’accès à ces documents**.

        Cette option nécessite que les destinataires disposent d’une connexion Internet chaque fois qu’ils ouvrent la pièce jointe, mais le point positif réside dans le fait que si vous révoquez ultérieurement le document, ils ne seront pas en mesure de l’ouvrir lors de leur prochaine tentative d’ouverture. Si vous ne sélectionnez pas cette option, il est possible que les destinataires puissent ouvrir le document, même sans connexion Internet. Toutefois, si vous révoquez ultérieurement le document, sa prise d’effet peut survenir après un certain délai.

    4.  Cliquez sur **Envoyer maintenant**.

        Le courrier électronique avec une pièce jointe est envoyé aux adresses de messagerie que vous avez indiquées. En plus de votre message électronique, les destinataires reçoivent des instructions sur la façon de lire le document joint protégé par Azure Rights Management.

Maintenant que vous avez envoyé votre document protégé, vous pouvez demander à vos destinataires de l’ouvrir dès qu’ils le reçoivent. Ne fermez pas Outlook, car nous allons l’utiliser à nouveau lors de la dernière étape pour suivre la pièce jointe.

|Pour en savoir plus|Informations supplémentaires|
|--------------------------------|--------------------------|
|Instructions détaillées et méthodes alternatives pour protéger des fichiers que vous partagez par courrier électronique   →|[Protéger un fichier partagé par courrier électronique à l’aide de l’application de partage Rights Management](../rms-client/sharing-app-protect-by-email.md)|
|Options de la boîte de dialogue **partage protégé** →|[Options de boîte de dialogue pour l'application de partage Rights Management](../rms-client/sharing-app-dialog-box.md)|


<!--HONumber=Apr16_HO3-->


