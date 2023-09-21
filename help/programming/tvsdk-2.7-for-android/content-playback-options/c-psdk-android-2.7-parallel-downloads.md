---
description: Il download di video e audio in parallelo, anziché in una serie, riduce i ritardi di avvio.
title: Download paralleli
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# Download paralleli {#parallel-downloads}

Il download di video e audio in parallelo, anziché in una serie, riduce i ritardi di avvio.

I download paralleli consentono la riproduzione di file video on-demand (VOD), ottimizzano l&#39;utilizzo della larghezza di banda disponibile da un server, riducono la probabilità di entrare in situazioni di buffer underrun e riducono al minimo il ritardo tra il download e la riproduzione.

<!-- 

Removed as part of "no DASH use cases" for 2.5.1, May 31st, 2017 release.
<p>Parallel downloads allows DASH video-on-demand (VOD) files to be played, optimizes the available bandwidth usage from a server, lowers the probability of getting into buffer under-run situations, and minimizes the delay between download and playback. </p>

 -->

Senza download paralleli, TVSDK invia una richiesta per il segmento video e, una volta caricato, richiede uno o due segmenti audio. Con i download paralleli, i segmenti audio e video vengono scaricati simultaneamente, non in sequenza. Inoltre, poiché esistono due connessioni e due richieste HTTP in parallelo per segmento, i dati raggiungono la schermata più rapidamente.

>[!NOTE]
>
>Questa funzione si applica solo ai contenuti in cui audio e video sono codificati in file diversi (contenuti non misti) e non si applica ai contenuti MP4, che sono sempre misti. Il contenuto HLS è spesso unmuxed, specialmente con l&#39;audio alternativo.

<!-- 

See comment above (DASH use case removed).
  This feature applies only to content where the audio and video are encoded into different files (unmuxed content) and does not apply to MP4 content, which is always muxed. Most DASH content is unmuxed, and HLS content is often unmuxed, especially with alternate audio. 
-->

La connessione HTTP potrebbe subire ritardi nelle seguenti fasi:

* Quando si stabilisce la connessione TCP/IP al server

  Sebbene il client e il server abbiano accettato di comunicare, non si è ancora verificata alcuna comunicazione HTTP. Questo tipo di ritardo dipende dall’infrastruttura tra il client e il server. Questo processo richiede di trovare un percorso attraverso Internet tra il client e il server e di assicurarsi che tutti i dispositivi, come router e firewall, sulla route accettino il trasferimento di dati.
* Quando si invia una richiesta HTTP per un segmento o un manifesto tramite la connessione TCP/IP.

  Il server riceve la richiesta, la elabora e inizia a inviare nuovamente i dati al client. Il grado di ritardo dipende dal carico e dalla complessità del software sul server e in qualche modo dalla velocità di connessione del caricamento quando il client invia la richiesta.
