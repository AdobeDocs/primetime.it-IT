---
description: Quando un segmento non è presente, ad esempio quando un particolare segmento non riesce a scaricarsi, tenta di recuperare attraverso una serie di tentativi di failover. Se non riesce a recuperare, genera un errore.
seo-description: Quando un segmento non è presente, ad esempio quando un particolare segmento non riesce a scaricarsi, tenta di recuperare attraverso una serie di tentativi di failover. Se non riesce a recuperare, genera un errore.
seo-title: Failover del segmento mancante
title: Failover del segmento mancante
uuid: 17ee1221-e1eb-4f64-a406-4d7eff1d7555
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Failover del segmento mancante{#missing-segment-failover}

Quando un segmento non è presente, ad esempio quando un particolare segmento non riesce a scaricarsi, tenta di recuperare attraverso una serie di tentativi di failover. Se non riesce a recuperare, genera un errore.

Se sul server manca un segmento perché, ad esempio, il file manifesto non è presente, il segmento non può essere scaricato e così via, TVSDK tenta di eseguire il failover provando le seguenti opzioni:

1. Tentate un failover sullo stesso segmento, allo stesso bitrate, in un file di variante.
1. Passa a un bitrate alternativo (switch ABR) nello stesso file.
1. Scorri ogni bitrate disponibile in ogni variante disponibile.
1. Salta il segmento ed emette un avviso.

Quando TVSDK non è in grado di ottenere un segmento alternativo, attiva una notifica `CONTENT_ERROR` di errore. Questa notifica contiene una notifica interna con il `DOWNLOAD_ERROR` codice. Se il flusso con il problema è una traccia audio alternativa, genera la notifica di `AUDIO_TRACK_ERROR` errore.

Se il motore video non è in grado di ottenere i segmenti in modo continuo, limita l’opzione di salta continua a 5, dopo di che la riproduzione viene interrotta ed emette un `NATIVE_ERROR` messaggio con il codice 5.

>[!NOTE]
>
>I parametri di controllo ABR (Adaptive Bit Rate) non vengono presi in considerazione quando si verifica un failover. Ciò è dovuto al fatto che il meccanismo di failover è progettato per utilizzare come flussi di backup uno qualsiasi degli elenchi di riproduzione attualmente disponibili, indipendentemente dal profilo del bit rate.
>
>Durante un&#39;operazione di failover, può verificarsi uno switch di profilo. Se si verifica un errore durante il download di uno dei segmenti di playlist, i parametri di controllo ABR come il bit rate minimo/massimo consentito vengono ignorati.

