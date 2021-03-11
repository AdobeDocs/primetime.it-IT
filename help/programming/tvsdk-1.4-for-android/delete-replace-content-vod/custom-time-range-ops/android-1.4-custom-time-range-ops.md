---
description: TVSDK supporta l’eliminazione programmatica e la sostituzione del contenuto degli annunci nei flussi VOD.
title: Operazioni con intervalli di tempo personalizzati
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---


# Operazioni con intervallo di tempo personalizzato {#custom-time-range-operations}

TVSDK supporta l’eliminazione programmatica e la sostituzione del contenuto degli annunci nei flussi VOD.

La funzione di eliminazione e sostituzione estende la funzione degli ad markers personalizzati. Gli ad markers personalizzati contrassegnano sezioni del contenuto principale come periodi di contenuto relativi agli annunci. Oltre a contrassegnare questi intervalli di tempo, puoi anche eliminare e sostituire gli intervalli di tempo.

L’eliminazione e la sostituzione degli annunci viene implementata con elementi `TimeRange` che identificano diversi tipi di intervalli di tempo in un flusso VOD: contrassegna, elimina e sostituisci. Per ciascuno di questi tipi di intervallo di tempo personalizzato, puoi eseguire le operazioni corrispondenti, tra cui eliminare e sostituire il contenuto dell’annuncio.

Per l&#39;eliminazione e la sostituzione degli annunci, TVSDK utilizza le seguenti modalità *funzionamento dell&#39;intervallo di tempo personalizzato*:

* **MARK**
 (Questi sono stati definiti indicatori di annunci personalizzati nelle versioni precedenti di TVSDK). Contrassegnano i tempi di inizio e fine per gli annunci che sono già inseriti nel flusso VOD. Quando nel flusso sono presenti marcatori di intervallo di tempo di tipo MARK, un posizionamento iniziale di 
`Mode.MARK` viene generato e risolto da  `CustomAdMarkersContentResolver`. Non vengono inseriti annunci.

* ****
DELETEFo intervalli di tempo di DELETE, un iniziale 
`placementInformation` di tipo  `Mode.DELETE` viene creato e risolto dal corrispondente  `DeleteContentResolver`. `ContentRemoval` è una nuova  `timelineOperation` che definisce gli intervalli da rimuovere dalla timeline. TVSDK utilizza `removeByLocalTime` dall’API Adobe Video Engine (AVE) per facilitare tale operazione. Se esistono intervalli di DELETE e metadati di Adobe Primetime ad decisioning (precedentemente noti come Auditude), gli intervalli vengono eliminati per primi, quindi `AuditudeResolver` risolve gli annunci utilizzando il normale flusso di lavoro Adobe Primetime ad decision ioning.

* ****
SOSTITUISCI o SOSTITUISCI intervalli di tempo, due intervalli iniziali 
`placementInformations` vengono creati uno  `Mode.DELETE` e uno  `Mode.REPLACE`. Il `DeleteContentResolver` elimina prima gli intervalli di tempo e quindi il `AuditudeResolver` inserisce gli annunci del `replaceDuration` specificato nella timeline. Se non viene specificato alcun valore `replaceDuration`, il server determina cosa inserire.

Per supportare queste operazioni dell’intervallo di tempo personalizzato, TVSDK fornisce quanto segue:

* Più risolutori di contenuti

   Un flusso può avere più risolutori di contenuti in base alla modalità di segnalazione degli annunci e ai metadati degli annunci. Il comportamento cambia con diverse combinazioni di modalità di segnalazione degli annunci e metadati degli annunci.
* Più iniziali `PlacementInformations` Il `DefaultMediaPlayer` crea un elenco di iniziali `PlacementInformations` in base alla modalità di segnalazione degli annunci e ai metadati degli annunci che devono essere risolti dal `MediaPlayerClient`.

* Nuova modalità di segnalazione annunci: Intervalli di tempo personalizzati

   Gli annunci vengono inseriti in base ai dati dell’intervallo di tempo provenienti da un’origine esterna (ad esempio un file JSON).