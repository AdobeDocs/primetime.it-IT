---
description: 'null'
seo-description: 'null'
seo-title: Approvare un certificato (account o amministratore secondario)
title: Approvare un certificato (account o amministratore secondario)
uuid: 5b95e2e8-abe9-4aef-bcb4-9b98ba6604d1
translation-type: tm+mt
source-git-commit: b4b50471ab0ba98329862322a61bf73aa9e471d5
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---


# Approvare un certificato (account o amministratore secondario){#approve-a-certificate-account-or-secondary-administrator}

1. Accedete al sito di registrazione certificati.
1. Selezionare la scheda **[!UICONTROL Certificates]**.
1. Rivedete la richiesta per verificare che la richiesta sia valida.
1. Se la richiesta è valida, fare clic su **[!UICONTROL Approve]**.

   È inoltre possibile aggiungere un commento. Viene inviato un messaggio e-mail al richiedente in cui si attesta che la richiesta è stata approvata da uno degli amministratori della società. Una copia di questo messaggio e-mail viene inviata agli amministratori della società e  Adobe.

1. Se la richiesta non è valida, fare clic su **[!UICONTROL Reject]** e inserire un commento nella finestra di dialogo di conferma.

   Viene inviato un messaggio e-mail al richiedente in cui si attesta che la richiesta è stata rifiutata da uno degli amministratori della società. Una copia di questo messaggio e-mail viene inviata agli amministratori della società.

Quando un amministratore approva una richiesta di certificato,  Adobe verifica l&#39;identità del richiedente.  Adobe contatta il richiedente al numero di telefono indicato nel suo profilo.

L&#39;amministratore di Adobe  tenta di contattare il richiedente due volte entro un periodo di tre giorni. Se l&#39;amministratore di Adobe  non riesce a contattare il richiedente, questi deve lasciare un messaggio che richiede una chiamata o specificare l&#39;ora in cui effettuerà di nuovo la chiamata. Se l&#39;amministratore del Adobe  non è in grado di contattare il richiedente, viene inviato un messaggio e-mail agli amministratori.

>[!NOTE]
>
>Solo gli amministratori di account e secondari possono cambiare il numero di telefono della società e la frase di sfida del richiedente.

Se l&#39;identità del richiedente viene verificata, il richiedente riceve un messaggio e-mail contenente il file PKCS#7 ( [!DNL p7b]).

Il richiedente può copiare il contenuto PKCS#7 dal corpo del messaggio e-mail e salvarlo in un file o utilizzare il file allegato al messaggio e-mail.  Adobe consiglia di utilizzare il nome base utilizzato per generare la chiave privata e il file CSR quando si salva il file PKSC#7.

>[!NOTE]
>
>Il file inviato al richiedente contiene solo il certificato. Il file non contiene informazioni sulla chiave privata.

