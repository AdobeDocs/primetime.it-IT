---
description: Il download di video e audio in parallelo, anziché in serie, riduce i ritardi di avvio.
seo-description: Il download di video e audio in parallelo, anziché in serie, riduce i ritardi di avvio.
seo-title: Download paralleli
title: Download paralleli
uuid: fa3edb50-7c24-433c-bc50-72d6cf73d834
translation-type: tm+mt
source-git-commit: 51b3713e04fcb4adeaa7a8d1b700372b1dba7cf6
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---


# Download paralleli {#parallel-downloads}

Il download di video e audio in parallelo, anziché in serie, riduce i ritardi di avvio.

I download paralleli consentono la riproduzione di file video su richiesta (VOD), ottimizza l&#39;utilizzo della larghezza di banda disponibile da un server, riduce la probabilità di trovarsi in situazioni di sovraccarico del buffer e riduce al minimo il ritardo tra il download e la riproduzione.

<!-- 

Removed as part of "no DASH use cases" for 2.5.1, May 31st, 2017 release.
<p>Parallel downloads allows DASH video-on-demand (VOD) files to be played, optimizes the available bandwidth usage from a server, lowers the probability of getting into buffer under-run situations, and minimizes the delay between download and playback. </p>

 -->

Senza download paralleli, TVSDK invia una richiesta per il segmento video, e dopo il caricamento del segmento video, richiede uno o due segmenti audio. Con i download paralleli, i segmenti audio e video vengono scaricati simultaneamente, non in sequenza. Inoltre, poiché esistono due connessioni e due richieste HTTP per segmento in parallelo, i dati raggiungono lo schermo più rapidamente.

>[!NOTE]
>
>Questa funzione è valida solo per i contenuti in cui audio e video sono codificati in file diversi (contenuto non muxed) e non si applica al contenuto MP4, che viene sempre muxed. I contenuti HLS spesso non vengono combinati, specialmente con audio alternativo.

<!-- 

See comment above (DASH use case removed).
  This feature applies only to content where the audio and video are encoded into different files (unmuxed content) and does not apply to MP4 content, which is always muxed. Most DASH content is unmuxed, and HLS content is often unmuxed, especially with alternate audio. 
-->

La connessione HTTP potrebbe presentare dei ritardi nelle seguenti fasi:

* Quando si stabilisce la connessione TCP/IP al server

   Sebbene client e server abbiano accettato di comunicare, non è ancora stata effettuata alcuna comunicazione HTTP. Questo tipo di ritardo dipende dall&#39;infrastruttura tra client e server. Questo processo richiede la ricerca di un percorso attraverso Internet tra il client e il server e la verifica che tutti i dispositivi, come router e firewall, sulla rotta accettino il trasferimento dei dati.
* Quando si invia una richiesta HTTP per un segmento o un manifesto attraverso la connessione TCP/IP.

   Il server riceve la richiesta, la elabora e inizia a restituire i dati al client. Il livello di ritardo dipende dal carico e dalla complessità del software sul server e in qualche modo dalla velocità della connessione di caricamento quando il client invia la richiesta.

