---
description: Lo stack Apple HLS supporta il passaggio ai flussi di failover/backup se non è in grado di recuperare flussi del set primario. Per i dispositivi Apple HLS, per facilitare il failover, potete segnalare al server manifesto di gestire i flussi primari e di failover identificati nella playlist principale come set disgiunti (con i propri UUID).
seo-description: Lo stack Apple HLS supporta il passaggio ai flussi di failover/backup se non è in grado di recuperare flussi del set primario. Per i dispositivi Apple HLS, per facilitare il failover, potete segnalare al server manifesto di gestire i flussi primari e di failover identificati nella playlist principale come set disgiunti (con i propri UUID).
seo-title: Facilitazione del passaggio del lettore HLS ai flussi di failover/backup
title: Facilitazione del passaggio del lettore HLS ai flussi di failover/backup
uuid: 2fea8a51-e4cb-4fc9-82d5-6305a1d96603
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# Facilitazione del passaggio del lettore HLS ai flussi di failover/backup {#facilitating-hls-player-switching-to-failover-backup-streams}

Lo stack Apple HLS supporta il passaggio ai flussi di failover/backup se non è in grado di recuperare flussi del set primario. Per i dispositivi Apple HLS, per facilitare il failover, potete segnalare al server manifesto di gestire i flussi primari e di failover identificati nella playlist principale come set disgiunti (con i propri UUID).

Per facilitare il passaggio ai flussi di failover o di backup sui dispositivi Apple HLS, è possibile specificare il parametro `ptfailover` nell&#39;URL di Bootstrap. Se fornisci questo parametro, il server manifest creerà sessioni di riproduzione separate (che determinano gli annunci cuciti) per ciascun set di failover.

## Dettagli

In che modo SSAI gestisce il passaggio HLS al failover/backup quando si include `ptfailover=true` nella richiesta di Bootstrap:

* Quando una playlist principale contiene set di riproduzione principali e di backup:

   * Il server manifesto identifica gli URL del flusso AV per diversi set di failover utilizzando l&#39;attributo `BANDWIDTH` e l&#39;ordine di analisi degli URL del flusso AV. Crea sessioni di riproduzione interne separate (identificate da UUID separati) e crea URL di flusso che puntano a server manifest con UUID diversi che identificano le diverse sessioni di riproduzione.
   * Il server manifesto identifica gli URL del flusso I-Frame per diversi set di failover utilizzando l&#39;attributo `RESOLUTION` corrispondente e l&#39;ordine di analisi degli URL del flusso I-Frame. SSAI utilizza gli UUID che identificano i flussi AV associati per gli URL dei flussi I-Frame che puntano a SSAI.
   * Per questa funzione, il server di manifesto supporta solo i gruppi `EXT-X-MEDIA` senza attributi URI nella playlist principale.
   * Il server del manifesto rileva una risposta di errore 404 da un CDN con un&#39;intestazione `X-Object-Too-Old: true` e mantiene il codice di stato e l&#39;intestazione quando invia la risposta al lettore.

* Gli annunci pre-roll vengono aggiunti solo al set principale; sono completamente disattivati nei set di failover per evitare eventuali annunci pre-roll errati e/o duplicati quando il lettore passa ai flussi di failover.
