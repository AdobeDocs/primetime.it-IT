---
description: Il download di video e audio in parallelo, anziché in una serie, riduce i ritardi di avvio.
title: Download paralleli
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Download paralleli {#parallel-downloads}

Il download di video e audio in parallelo, anziché in una serie, riduce i ritardi di avvio.

I download paralleli consentono la riproduzione di file VOD (video on demand), ottimizza l&#39;utilizzo della larghezza di banda disponibile da un server, riduce la probabilità di entrare in situazioni di buffer in fase di esecuzione e riduce al minimo il ritardo tra download e riproduzione.

<!-- 

Removed as part of "no DASH use cases" for 2.5.1, May 31st, 2017 release.
<p>Parallel downloads allows DASH video-on-demand (VOD) files to be played, optimizes the available bandwidth usage from a server, lowers the probability of getting into buffer under-run situations, and minimizes the delay between download and playback. </p>

 -->

Senza download paralleli, TVSDK invia una richiesta per il segmento video e, dopo il caricamento del segmento video, richiede uno o due segmenti audio. Con i download paralleli, i segmenti audio e video vengono scaricati simultaneamente, non sequenzialmente. Inoltre, poiché esistono due connessioni e due richieste HTTP per segmento in parallelo, i dati raggiungono lo schermo più rapidamente.

>[!NOTE]
>
>Questa funzione si applica solo al contenuto in cui audio e video sono codificati in file diversi (contenuto non muxed) e non si applica al contenuto MP4, che è sempre mbox. Il contenuto HLS è spesso privo di mbox, soprattutto con audio alternativo.

<!-- 

See comment above (DASH use case removed).

  This feature applies only to content where the audio and video are encoded into different files (unmuxed content) and does not apply to MP4 content, which is always muxed. Most DASH content is unmuxed, and HLS content is often unmuxed, especially with alternate audio. 
-->

La connessione HTTP potrebbe subire ritardi nelle seguenti fasi:

* Quando si stabilisce la connessione TCP/IP al server

   Sebbene client e server abbiano accettato di comunicare, non si è ancora verificata alcuna comunicazione HTTP. Questo tipo di ritardo dipende dall’infrastruttura tra il client e il server. Questo processo richiede la ricerca di un percorso attraverso Internet tra il client e il server e la verifica che tutti i dispositivi, come i router e i firewall, sulla rotta accettino il trasferimento di dati.
* Quando si invia una richiesta HTTP per un segmento o un manifesto tramite la connessione TCP/IP.

   Il server riceve la richiesta, la elabora e inizia a rimandare i dati al client. Il grado di ritardo dipende dal carico e dalla complessità del software sul server e in qualche modo dalla velocità di connessione di caricamento quando il client invia la richiesta.