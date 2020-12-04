---
description: TVSDK supporta l’eliminazione e la sostituzione programmatica del contenuto degli annunci nei flussi VOD.
seo-description: TVSDK supporta l’eliminazione e la sostituzione programmatica del contenuto degli annunci nei flussi VOD.
seo-title: Operazioni intervallo di tempo personalizzato
title: Operazioni intervallo di tempo personalizzato
uuid: e04af786-8dac-41a6-8406-f2ca04f612a4
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---


# Operazioni intervallo di tempo personalizzato {#custom-time-range-operations}

TVSDK supporta l’eliminazione e la sostituzione programmatica del contenuto degli annunci nei flussi VOD.

La funzione di eliminazione e sostituzione estende la funzione degli indicatori di annunci personalizzati. I marcatori annunci personalizzati contrassegnano sezioni del contenuto principale come periodi di contenuto correlati agli annunci. Oltre a contrassegnare questi intervalli di tempo, potete anche eliminare e sostituire gli intervalli di tempo.

L&#39;eliminazione e la sostituzione degli annunci è implementata con elementi `TimeRange` che identificano diversi tipi di intervalli di tempo in un flusso VOD: contrassegnare, eliminare e sostituire. Per ciascuno di questi tipi di intervallo di tempo personalizzato, potete eseguire le operazioni corrispondenti, compresa l&#39;eliminazione e la sostituzione del contenuto di un annuncio.

Per l&#39;eliminazione e la sostituzione degli annunci, TVSDK utilizza le seguenti modalità *per l&#39;operazione dell&#39;intervallo di tempo personalizzato*:

* **MARK**
(questi erano definiti indicatori di annunci personalizzati nelle versioni precedenti di TVSDK). Contrassegna i tempi di inizio e fine per gli annunci già inseriti nel flusso VOD. Quando nel flusso sono presenti indicatori di intervallo di tempo di tipo MARK, una posizione iniziale di 
`Mode.MARK` viene generato e risolto dal  `CustomAdMarkersContentResolver`. Non vengono inseriti annunci.

* **intervalli di tempo**
DELETEF o DELETE, una 
`placementInformation` di tipo  `Mode.DELETE` viene creato e risolto dal corrispondente  `DeleteContentResolver`. `ContentRemoval` è una nuova  `timelineOperation` che definisce gli intervalli da rimuovere dalla timeline. TVSDK utilizza `removeByLocalTime` dall&#39;API  motore video (AVE) per facilitare tale operazione. Se sono presenti intervalli di DELETE e  metadati Adobe Primetime ad Decision (precedentemente noti come Auditude), gli intervalli vengono eliminati per primi, quindi `AuditudeResolver` risolve gli annunci utilizzando il normale flusso di lavoro di Adobe Primetime ad Decioning .

* **Intervalli di tempo**
SOSTITUISCI o SOSTITUISCI, due intervalli iniziali 
`placementInformations` vengono creati, uno  `Mode.DELETE` e uno  `Mode.REPLACE`. `DeleteContentResolver` elimina prima gli intervalli di tempo, quindi `AuditudeResolver` inserisce nella timeline gli annunci della `replaceDuration` specificata. Se non viene specificato `replaceDuration`, il server determina cosa inserire.

Per supportare queste operazioni dell’intervallo di tempo personalizzato, TVSDK fornisce quanto segue:

* Più risolutori di contenuti

   Un flusso può avere più risolutori di contenuto basati sulla modalità di segnalazione degli annunci e sui metadati degli annunci. Il comportamento cambia con diverse combinazioni di modalità di segnalazione annunci e metadati annuncio.
* Più iniziali `PlacementInformations` Il `DefaultMediaPlayer` crea un elenco di `PlacementInformations` iniziali in base alla modalità di segnalazione degli annunci e ai metadati degli annunci che devono essere risolti dal `MediaPlayerClient`.

* Nuova modalità di segnalazione annunci: Intervalli temporali personalizzati

   Gli annunci vengono inseriti in base ai dati Intervallo di tempo provenienti da un&#39;origine esterna (ad esempio un file JSON).