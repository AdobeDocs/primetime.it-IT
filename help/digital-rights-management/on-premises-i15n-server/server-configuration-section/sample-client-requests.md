---
title: Richieste client di esempio
description: Richieste client di esempio
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 1%

---


# Richieste client di esempio{#sample-client-requests}

È possibile raccogliere una libreria di richieste client di esempio utilizzando strumenti come Charles Proxy o Wireshark. È necessario acquisire le richieste client dopo la configurazione del server Individualization, utilizzando la credenziale Individualization Transport. Puoi quindi inviare queste richieste client (tramite *curl* o un altro strumento) al punto finale di Individualization Server per verificare che il server sia in esecuzione e in esecuzione correttamente. Ad esempio:

```
curl https://<<yourindivserver:port>>/flashaccess/i15n/v5 -­data-binary  
@sample_client_request.bin > sample_client_response.ber
```

Puoi anche inviare nuovamente queste richieste dopo eventuali modifiche alla configurazione del server o aggiornamenti di ECI/CRL.

È inoltre necessario aggiornare opportunamente la pagina Statistiche di Individualizzazione con transazioni di individualizzazione riuscite.
