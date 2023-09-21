---
title: Facilitare il passaggio del lettore HLS ai flussi di failover/backup
description: Lo stack HLS di Apple supporta il passaggio a flussi di failover/backup se non è in grado di recuperare alcun flusso del set principale. Per i dispositivi Apple HLS, per facilitare il failover, è possibile segnalare al server di manifesto di trattare i flussi primari e di failover identificati nella playlist principale come set disgiunti (con i propri UUID).
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# Facilitare il passaggio del lettore HLS ai flussi di failover/backup {#facilitating-hls-player-switching-to-failover-backup-streams}

Lo stack HLS di Apple supporta il passaggio a flussi di failover/backup se non è in grado di recuperare alcun flusso del set principale. Per i dispositivi Apple HLS, per facilitare il failover, è possibile segnalare al server di manifesto di trattare i flussi primari e di failover identificati nella playlist principale come set disgiunti (con i propri UUID).

Per facilitare il passaggio ai flussi di failover o backup sui dispositivi Apple HLS, è possibile specificare `ptfailover` parametro nell&#39;URL di Bootstrap. Se si specifica questo parametro, il server manifest creerà sessioni di riproduzione separate (che determinano gli annunci uniti) per ogni set di failover.

## Dettagli

Come SSAI gestisce il passaggio da HLS a failover/backup quando si includono `ptfailover=true` nella richiesta Bootstrap:

* Quando una playlist principale contiene set principali e di backup:

   * Il server manifesto identifica gli URL del flusso AV per diversi set di failover utilizzando `BANDWIDTH` e l&#39;ordine di analisi degli URL di flusso AV. Crea sessioni di riproduzione interne separate (identificate da UUID separati) e URL di flusso che puntano ai server manifest con UUID diversi che identificano sessioni di riproduzione diverse.
   * Il server manifesto identifica gli URL di flusso I-Frame per set di failover diversi utilizzando il corrispondente `RESOLUTION` e l’ordine di analisi degli URL di flusso I-Frame. SSAI utilizza gli UUID che identificano i flussi AV associati per gli URL di flusso I-Frame che puntano a SSAI.
   * Per questa funzionalità, il server manifesto supporta solo `EXT-X-MEDIA` gruppi senza attributi URI nella playlist principale.
   * Il server manifesto rileva una risposta di errore 404 da una rete CDN con un `X-Object-Too-Old: true` e conserva il codice di stato e l’intestazione quando invii tale risposta al lettore.

* Gli annunci pre-roll vengono aggiunti solo al set principale; vengono completamente disabilitati nei set di failover per evitare annunci pre-roll errati e/o duplicati quando il lettore passa ai flussi di failover.
