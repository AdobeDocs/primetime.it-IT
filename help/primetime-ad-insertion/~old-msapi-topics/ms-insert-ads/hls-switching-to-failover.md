---
description: Lo stack Apple HLS supporta il passaggio ai flussi di failover/backup se non è in grado di recuperare flussi del set principale. Per i dispositivi Apple HLS, per facilitare il failover, è possibile segnalare al server manifest il trattamento dei flussi primari e di failover identificati nella playlist principale come set disgiunti (con i propri UUID).
title: Facilitazione del passaggio del lettore HLS ai flussi di failover/backup
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---


# Facilitazione del passaggio del lettore HLS ai flussi di failover/backup {#facilitating-hls-player-switching-to-failover-backup-streams}

Lo stack Apple HLS supporta il passaggio ai flussi di failover/backup se non è in grado di recuperare flussi del set principale. Per i dispositivi Apple HLS, per facilitare il failover, è possibile segnalare al server manifest il trattamento dei flussi primari e di failover identificati nella playlist principale come set disgiunti (con i propri UUID).

Per facilitare il passaggio ai flussi di failover o backup sui dispositivi Apple HLS, è possibile specificare il parametro `ptfailover` nell&#39;URL di Bootstrap. Se si fornisce questo parametro, il server manifest creerà sessioni di riproduzione separate (che determinano gli annunci uniti) per ogni set di failover.

## Dettagli

Come SSAI gestisce il passaggio HLS al failover/backup quando si include `ptfailover=true` nella richiesta di Bootstrap:

* Quando una playlist principale contiene set di backup e principali:

   * Il server manifest identifica gli URL del flusso AV per diversi set di failover utilizzando l&#39;attributo `BANDWIDTH` e l&#39;ordine di analisi degli URL del flusso AV. Crea sessioni di riproduzione interne separate (identificate da UUID separati) e crea URL di flusso che puntano a server manifest con i diversi UID che identificano diverse sessioni di riproduzione.
   * Il server manifest identifica gli URL del flusso I-Frame per diversi set di failover utilizzando l&#39;attributo `RESOLUTION` corrispondente e l&#39;ordine di analisi degli URL del flusso I-Frame. SSAI utilizza gli UUID che identificano i flussi AV associati per gli URL di flussi I-Frame che puntano a SSAI.
   * Per questa funzione, il server manifest supporta solo i gruppi `EXT-X-MEDIA` senza attributi URI nella playlist principale.
   * Il server manifest rileva una risposta di errore 404 da una CDN con un&#39;intestazione `X-Object-Too-Old: true` e conserva il codice di stato e l&#39;intestazione quando invia la risposta al lettore.

* Gli annunci pre-roll vengono aggiunti solo al set principale; sono completamente disabilitati nei set di failover per evitare eventuali annunci di pre-roll errati e/o duplicati quando il lettore passa ai flussi di failover.

