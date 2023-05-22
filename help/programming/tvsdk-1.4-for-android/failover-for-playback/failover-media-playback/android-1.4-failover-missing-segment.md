---
description: Quando manca un segmento, ad esempio quando un particolare segmento non viene scaricato, tenta di eseguire il ripristino tramite diversi tentativi di failover. Se non può essere ripristinato, genera un errore.
title: Failover del segmento mancante
exl-id: e941008a-99a5-4fff-ac88-133abcf9380d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# Failover del segmento mancante{#missing-segment-failover}

Quando manca un segmento, ad esempio quando un particolare segmento non viene scaricato, tenta di eseguire il ripristino tramite diversi tentativi di failover. Se non può essere ripristinato, genera un errore.

Se nel server manca un segmento perché, ad esempio, il file manifesto non è presente, il segmento non può essere scaricato e così via, TVSDK tenta di eseguire il failover tentando le seguenti opzioni:

1. Tentare un failover sullo stesso segmento, alla stessa velocità bit, in un file variante.
1. Passare a una velocità bit alternativa (switch ABR) nello stesso file.
1. Scorre ogni bit rate disponibile in ogni variante disponibile.
1. Ignora il segmento e genera un avviso.

Quando TVSDK non è in grado di ottenere un segmento alternativo, attiva un `CONTENT_ERROR` notifica di errore. Questa notifica contiene una notifica interna con il codice `DOWNLOAD_ERROR` codice. Se il flusso con il problema è una traccia audio alternativa, genera il `AUDIO_TRACK_ERROR` notifica di errore.

Se il motore video non è in grado di ottenere segmenti in modo continuo, limita il segmento continuo salta a 5, dopo di che la riproduzione viene interrotta e si verifica un `NATIVE_ERROR` con il codice 5.

>[!NOTE]
>
>I parametri di controllo ABR (Adaptive Bit Rate) non vengono presi in considerazione quando si verifica un failover. Questo perché il meccanismo di failover è progettato per utilizzare come flussi di backup qualsiasi playlist attualmente disponibile, indipendentemente dal suo profilo di bit-rate.
>
>Durante un&#39;operazione di failover può essere presente uno switch di profilo. Se si verifica un errore durante il download di uno dei segmenti della playlist, i parametri di controllo ABR, come la velocità bit minima/massima consentita, vengono ignorati.
