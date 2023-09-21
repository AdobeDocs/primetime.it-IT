---
description: Per visualizzare gli annunci banner, devi creare istanze di banner e consentire a TVSDK di ascoltare eventi relativi agli annunci.
title: Visualizza banner pubblicitari
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# Visualizza banner pubblicitari {#display-banner-ads}

Per visualizzare gli annunci banner, devi creare istanze di banner e consentire a TVSDK di ascoltare eventi relativi agli annunci.

TVSDK fornisce un elenco di banner pubblicitari correlati associati a un annuncio lineare tramite `AdPlaybackEventListener.onAdBreakStart` evento.

I manifesti possono specificare gli annunci banner correlati in base a:

* Un frammento di HTML
* URL di una pagina iFrame
* URL di un&#39;immagine statica o di un file SWF di Flash di Adobe

Per ogni annuncio correlato, TVSDK indica i tipi disponibili per l’applicazione.

1. Aggiungere un listener per `AdPlaybackEventListener.onAdBreakStart` evento che esegue le seguenti operazioni:

   * Cancella gli annunci esistenti nell’istanza del banner.
   * Ottiene l’elenco degli annunci correlati da `Ad.getCompanionAssets`.
   * Se l’elenco degli annunci correlati non è vuoto, scorri l’elenco per le istanze del banner.

     Ogni istanza del banner (un `AdAsset`) contiene informazioni quali larghezza, altezza, tipo di risorsa (html, iframe o statica) e dati necessari per visualizzare il banner correlato.
   * Se un annuncio video non ha annunci correlati prenotati con esso, l’elenco delle risorse correlate non contiene dati per tale annuncio video.
   * Per visualizzare un annuncio di visualizzazione autonomo, aggiungi la logica allo script per eseguire un normale tag annuncio di visualizzazione DFP (DoubleClick for Publishers) nell’istanza del banner appropriata.
   * Invia le informazioni sul banner a una funzione sulla pagina che visualizza i banner in una posizione appropriata.

     Questo è di solito un `div`, e la tua funzione utilizza `div ID` per visualizzare il banner.
