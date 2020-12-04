---
description: Per visualizzare gli annunci per banner, dovete creare istanze di banner e consentire a TVSDK di ascoltare gli eventi relativi agli annunci.
seo-description: Per visualizzare gli annunci per banner, dovete creare istanze di banner e consentire a TVSDK di ascoltare gli eventi relativi agli annunci.
seo-title: Visualizza annunci banner
title: Visualizza annunci banner
uuid: cfd4b26c-9643-4b60-9aff-bc27dec289f1
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---


# Visualizza annunci banner {#display-banner-ads}

Per visualizzare gli annunci per banner, dovete creare istanze di banner e consentire a TVSDK di ascoltare gli eventi relativi agli annunci.

TVSDK fornisce un elenco di banner pubblicitari associati a un annuncio lineare tramite l&#39;evento `AdPlaybackEventListener.onAdBreakStart`.

I manifesti possono specificare annunci banner complementari per:

* Snippet HTML
* URL di una pagina iFrame
* URL di un’immagine statica o di un file SWF di Flash di Adobi 

Per ogni annuncio aggiuntivo complementare, TVSDK indica quali tipi sono disponibili per l’applicazione.

1. Aggiungete un listener per l&#39;evento `AdPlaybackEventListener.onAdBreakStart` che esegue le seguenti operazioni:

   * Cancella gli annunci esistenti nell&#39;istanza del banner.
   * Ottiene l&#39;elenco degli annunci complementari da `Ad.getCompanionAssets`.
   * Se l&#39;elenco degli annunci complementari non è vuoto, ripetete l&#39;operazione sull&#39;elenco per le istanze del banner.

      Ogni istanza del banner (un `AdAsset`) contiene informazioni quali larghezza, altezza, tipo di risorsa (html, iframe o statico) e dati necessari per visualizzare il banner ausiliario.
   * Se un annuncio video non contiene annunci pubblicitari associati, l’elenco delle risorse ausiliarie non contiene dati per tale annuncio video.
   * Per visualizzare un annuncio di visualizzazione indipendente, aggiungete la logica allo script per eseguire un tag di annuncio di visualizzazione normale DFP (DoubleClick for Publishers) nell&#39;istanza di banner appropriata.
   * Invia le informazioni sul banner a una funzione sulla pagina che visualizza i banner in una posizione appropriata.

      In genere si tratta di un `div` e la funzione utilizza il `div ID` per visualizzare il banner.