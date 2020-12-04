---
seo-title: Richieste client di esempio
title: Richieste client di esempio
uuid: 330d5e3c-1711-4375-bd11-e7702f0cde31
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 1%

---


# Richieste client di esempio{#sample-client-requests}

Potete raccogliere una libreria di richieste client di esempio utilizzando strumenti quali Charles Proxy o Wireshark. È necessario acquisire le richieste del client dopo che il server di individuazione è stato configurato, utilizzando la credenziale Trasporto di individualizzazione. Potete quindi inviare queste richieste client (tramite *curl* o un altro strumento) al punto finale del server di individuazione per verificare che il server sia in esecuzione e funzionante correttamente. Ad esempio:

```
curl https://<<yourindivserver:port>>/flashaccess/i15n/v5 -­data-binary  
@sample_client_request.bin > sample_client_response.ber
```

È inoltre possibile inviare nuovamente tali richieste dopo eventuali modifiche alla configurazione del server o aggiornamenti ECI / CRL.

È inoltre necessario aggiornare la pagina Statistiche di individualizzazione in modo appropriato con transazioni di individualizzazione riuscite.
