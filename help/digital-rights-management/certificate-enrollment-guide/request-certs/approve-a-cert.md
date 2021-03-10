---
title: Approvare un certificato (account o amministratore secondario)
description: Approvare un certificato (account o amministratore secondario)
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---


# Approvare un certificato (Account o Amministratore secondario){#approve-a-certificate-account-or-secondary-administrator}

1. Accedere al sito di registrazione certificati.
1. Seleziona la scheda **[!UICONTROL Certificates]** .
1. Rivedi la richiesta per verificare che la richiesta sia valida.
1. Se la richiesta è valida, fare clic su **[!UICONTROL Approve]**.

   È inoltre possibile aggiungere un commento. Viene inviata al richiedente un&#39;e-mail in cui si attesta che la richiesta è stata approvata da uno degli amministratori aziendali. Una copia di questa e-mail viene inviata all&#39;azienda e agli amministratori di Adobe.

1. Se la richiesta non è valida, fare clic su **[!UICONTROL Reject]** e inserire un commento nella finestra di dialogo di conferma.

   Viene inviata al richiedente un&#39;e-mail in cui si attesta che la richiesta è stata rifiutata da uno degli amministratori dell&#39;azienda. Una copia di questa e-mail viene inviata agli amministratori aziendali.

Quando un amministratore approva una richiesta di certificato, Adobe verifica l’identità del richiedente. L&#39;Adobe contatta il Richiedente al numero di telefono indicato nel suo profilo.

L’amministratore di Adobe tenta di contattare il richiedente due volte entro un periodo di tre giorni. Se l’amministratore di Adobe non è in grado di contattare il Richiedente, lascia un messaggio che richiede una chiamata di ritorno o specifica l’ora in cui effettuerà una nuova chiamata. Se l’amministratore di Adobe non è in grado di contattare il Richiedente, viene inviata un’e-mail agli amministratori.

>[!NOTE]
>
>Solo gli amministratori Account e Secondari possono cambiare il numero di telefono dell&#39;azienda e la frase di sfida del Richiedente.

Se l&#39;identità del richiedente viene verificata, il richiedente riceve un messaggio di posta elettronica contenente il file PKCS#7 ( [!DNL p7b]).

Il richiedente può copiare il contenuto PKCS#7 dal corpo della posta elettronica e salvarlo in un file o utilizzare il file allegato alla posta elettronica. Adobe consiglia di utilizzare il nome base utilizzato per generare la chiave privata e il file CSR quando si salva il file PKSC#7.

>[!NOTE]
>
>Il file inviato al richiedente contiene solo il certificato. Il file non contiene informazioni di chiave privata.

