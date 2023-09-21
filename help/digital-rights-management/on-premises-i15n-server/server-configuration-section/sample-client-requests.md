---
title: Richieste client di esempio
description: Richieste client di esempio
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# Richieste client di esempio{#sample-client-requests}

Puoi raccogliere una libreria di richieste client di esempio utilizzando strumenti come Charles Proxy o Wireshark. È necessario acquisire le richieste client dopo la configurazione del server di personalizzazione, utilizzando le credenziali Trasporto di personalizzazione. Puoi quindi inviare queste richieste ai client (tramite *ricciolo* o un altro strumento) al punto finale di Individualization Server per verificare che il server sia in funzione e funzioni correttamente. Ad esempio:

```
curl https://<<yourindivserver:port>>/flashaccess/i15n/v5 -­data-binary  
@sample_client_request.bin > sample_client_response.ber
```

Puoi anche inviare nuovamente queste richieste dopo eventuali modifiche alla configurazione del server o aggiornamenti ECI/CRL.

È inoltre necessario aggiornare la pagina Statistiche di personalizzazione in modo appropriato con le transazioni di personalizzazione riuscite.
