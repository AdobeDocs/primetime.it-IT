---
description: TVSDK supporta l’eliminazione e la sostituzione programmatica del contenuto degli annunci nei flussi VOD.
seo-description: TVSDK supporta l’eliminazione e la sostituzione programmatica del contenuto degli annunci nei flussi VOD.
seo-title: Operazioni intervallo di tempo personalizzato
title: Operazioni intervallo di tempo personalizzato
uuid: e04af786-8dac-41a6-8406-f2ca04f612a4
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Operazioni intervallo di tempo personalizzato {#custom-time-range-operations}

TVSDK supporta l’eliminazione e la sostituzione programmatica del contenuto degli annunci nei flussi VOD.

La funzione di eliminazione e sostituzione estende la funzione degli indicatori di annunci personalizzati. I marcatori annunci personalizzati contrassegnano sezioni del contenuto principale come periodi di contenuto correlati agli annunci. Oltre a contrassegnare questi intervalli di tempo, potete anche eliminare e sostituire gli intervalli di tempo.

L&#39;eliminazione e la sostituzione degli annunci è implementata con `TimeRange` elementi che identificano diversi tipi di intervalli di tempo in un flusso VOD: contrassegnare, eliminare e sostituire. Per ciascuno di questi tipi di intervallo di tempo personalizzato, potete eseguire le operazioni corrispondenti, compresa l&#39;eliminazione e la sostituzione del contenuto di un annuncio.

Per l’eliminazione e la sostituzione degli annunci, TVSDK utilizza le seguenti modalità operative *dell’intervallo di tempo* personalizzato:

* **MARK**(questi erano definiti indicatori di annunci personalizzati nelle versioni precedenti di TVSDK). Contrassegna i tempi di inizio e fine per gli annunci già inseriti nel flusso VOD. Quando nel flusso sono presenti indicatori di intervallo di tempo di tipo MARK, il posizionamento iniziale di `Mode.MARK` viene generato e risolto dal `CustomAdMarkersContentResolver`. Non vengono inseriti annunci.

* **DELETE** Per gli intervalli di tempo DELETE, viene creata una prima `placementInformation` di tipo `Mode.DELETE` e risolta dalla `DeleteContentResolver`corrispondente. `ContentRemoval` è una nuova `timelineOperation` che definisce gli intervalli da rimuovere dalla timeline. TVSDK utilizza `removeByLocalTime` l’API Adobe Video Engine (AVE) per facilitare tale operazione. Se sono presenti intervalli DELETE e metadati Adobe Primetime per la decisione degli annunci (precedentemente noti come Auditude), gli intervalli vengono eliminati per primi, quindi gli `AuditudeResolver` annunci vengono risolti utilizzando il normale flusso di lavoro Adobe Primetime e per la decisione degli annunci.

* **SOSTITUISCI** per gli intervalli di tempo SOSTITUISCI, `placementInformations` vengono creati due intervalli iniziali, uno `Mode.DELETE` e uno `Mode.REPLACE`. Vengono `DeleteContentResolver` eliminati prima gli intervalli di tempo, quindi gli `AuditudeResolver` annunci degli annunci degli intervalli di tempo specificati `replaceDuration` vengono inseriti nella timeline. Se non `replaceDuration` viene specificato alcun valore, il server determina cosa inserire.

Per supportare queste operazioni dell’intervallo di tempo personalizzato, TVSDK fornisce quanto segue:

* Più risolutori di contenuti

   Un flusso può avere più risolutori di contenuto basati sulla modalità di segnalazione degli annunci e sui metadati degli annunci. Il comportamento cambia con diverse combinazioni di modalità di segnalazione annunci e metadati annuncio.
* Più iniziali `PlacementInformations` L&#39; `DefaultMediaPlayer` utente crea un elenco delle iniziali `PlacementInformations` in base alla modalità di segnalazione degli annunci e ai metadati degli annunci che devono essere risolti dall&#39; `MediaPlayerClient`.

* Nuova modalità di segnalazione annunci: Intervalli temporali personalizzati

   Gli annunci vengono inseriti in base ai dati Intervallo di tempo provenienti da un&#39;origine esterna (ad esempio un file JSON).