---
description: Per visualizzare gli annunci banner, devi creare istanze banner e consentire a TVSDK di ascoltare gli eventi relativi agli annunci.
title: Visualizza annunci banner
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---


# Visualizza annunci banner {#display-banner-ads}

Per visualizzare gli annunci banner, devi creare istanze banner e consentire a TVSDK di ascoltare gli eventi relativi agli annunci.

TVSDK fornisce un elenco di banner pubblicitari associati a un annuncio lineare tramite l&#39;evento `AdPlaybackEventListener.onAdBreakStart` .

I manifesti possono specificare annunci di banner complementari per:

* Frammento HTML
* URL di una pagina iFrame
* URL di un’immagine statica o di un file SWF di Flash di Adobe

Per ogni annuncio correlato, TVSDK indica quali tipi sono disponibili per l’applicazione.

1. Aggiungi un listener per l&#39;evento `AdPlaybackEventListener.onAdBreakStart` che esegue le seguenti operazioni:

   * Cancella gli annunci esistenti nell&#39;istanza del banner.
   * Ottiene l&#39;elenco degli annunci companion da `Ad.getCompanionAssets`.
   * Se l’elenco degli annunci associati non è vuoto, ripeti l’errore sopra l’elenco per le istanze del banner.

      Ogni istanza del banner (un elemento `AdAsset`) contiene informazioni quali larghezza, altezza, tipo di risorsa (html, iframe o statico) e dati necessari per visualizzare il banner correlato.
   * Se un annuncio video non ha annunci correlati prenotati con esso, l’elenco delle risorse correlate non contiene dati per quell’annuncio video.
   * Per mostrare un annuncio di visualizzazione indipendente, aggiungi la logica al tuo script per eseguire un tag di annunci di visualizzazione normale DFP (DoubleClick for Publishers) nell’istanza di banner appropriata.
   * Invia le informazioni sul banner a una funzione nella pagina in cui vengono visualizzati i banner in una posizione appropriata.

      In genere si tratta di una `div` e la funzione utilizza `div ID` per visualizzare il banner.