---
title: Approvare un certificato (account o amministratore secondario)
description: Approvare un certificato (account o amministratore secondario)
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# Approvare un certificato (account o amministratore secondario){#approve-a-certificate-account-or-secondary-administrator}

1. Accedi al sito di registrazione certificati.
1. Seleziona la **[!UICONTROL Certificates]** scheda.
1. Rivedi la richiesta per verificare che sia valida.
1. Se la richiesta è valida, fai clic su **[!UICONTROL Approve]**.

   È inoltre possibile aggiungere un commento. Al richiedente viene inviato un messaggio di posta elettronica in cui si dichiara che la richiesta è stata approvata da uno degli amministratori della società. Una copia di questa e-mail viene inviata all&#39;azienda e agli amministratori di Adobi.

1. Se la richiesta non è valida, fai clic su **[!UICONTROL Reject]** e inserisci un commento nella finestra di dialogo di conferma.

   Al richiedente viene inviato un messaggio di posta elettronica in cui si informa che la richiesta è stata rifiutata da uno degli amministratori della società. Una copia di questa e-mail viene inviata agli amministratori della società.

Quando un amministratore approva una richiesta di certificato, Adobe verifica l’identità del richiedente. L’Adobe contatta il richiedente al numero di telefono indicato nel suo profilo.

L’amministratore Adobe tenta di contattare il richiedente due volte entro un periodo di tre giorni. Se l’amministratore Adobe non è in grado di contattare il richiedente, lascia un messaggio di richiesta di richiamata oppure indica un’ora in cui richiamerà. Se l’amministratore dell’Adobe non è in grado di raggiungere il richiedente, viene inviata un’e-mail agli amministratori.

>[!NOTE]
>
>Solo gli amministratori Account e Secondario possono modificare il numero di telefono della società e la frase di richiesta di verifica del richiedente.

Se l&#39;identità del richiedente viene verificata, il richiedente riceve un messaggio di posta elettronica contenente il file PKCS#7 ( [!DNL p7b]).

Il richiedente può copiare il contenuto di PKCS#7 dal corpo del messaggio di posta elettronica e salvarlo in un file oppure utilizzare il file allegato al messaggio. L&#39;Adobe consiglia di utilizzare, quando si salva il file PKSC#7, il nome di base utilizzato per generare la chiave privata e il file CSR.

>[!NOTE]
>
>Il file inviato al richiedente contiene solo il certificato. Il file non contiene informazioni sulla chiave privata.
