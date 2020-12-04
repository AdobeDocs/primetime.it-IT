---
description: La classe CustomRangeMetadata identifica diversi tipi di intervalli di tempo in un indicatore di flusso VOD, elimina e sostituisce. Per ciascuno di questi tipi di intervallo di tempo personalizzato, potete eseguire le operazioni corrispondenti, compresa l'eliminazione e la sostituzione del contenuto di un annuncio.
seo-description: La classe CustomRangeMetadata identifica diversi tipi di intervalli di tempo in un indicatore di flusso VOD, elimina e sostituisce. Per ciascuno di questi tipi di intervallo di tempo personalizzato, potete eseguire le operazioni corrispondenti, compresa l'eliminazione e la sostituzione del contenuto di un annuncio.
seo-title: Operazioni intervallo di tempo personalizzato
title: Operazioni intervallo di tempo personalizzato
uuid: e9c6a135-124e-44d4-adf2-dc9d671e2483
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---


# Panoramica {#custom-time-range-operations}

La classe CustomRangeMetadata identifica diversi tipi di intervalli di tempo in un flusso VOD: contrassegnare, eliminare e sostituire. Per ciascuno di questi tipi di intervallo di tempo personalizzato, potete eseguire le operazioni corrispondenti, compresa l&#39;eliminazione e la sostituzione del contenuto di un annuncio.

<!--<a id="section_1323C0BAC259424C85A6ACFB48FE77EC"></a>-->

Per l&#39;eliminazione e la sostituzione degli annunci, TVSDK utilizza le seguenti modalità *per l&#39;operazione dell&#39;intervallo di tempo personalizzato*:

* **** MARKTquesta modalità è stata definita come indicatori di annunci personalizzati nelle versioni precedenti di TVSDK. La modalità contrassegna l&#39;ora iniziale e finale per gli annunci già inseriti nel flusso VOD. Quando nel flusso sono presenti indicatori di intervallo di tempo di tipo `MARK`, il posizionamento iniziale di `Mode.MARK` viene generato da `CustomMarkerOpportunityGenerator` e risolto da `CustomRangeResolver`. Non vengono inseriti annunci.

* **** DELETEFo intervalli  `DELETE` di tempo,  `placementInformation` viene creato e risolto un primo  `Mode.DELETE` di tipo  `CustomRangeResolver`. `DeleteRangeTimelineOperation` definisce gli intervalli da rimuovere dalla timeline, e TVSDK utilizza  `removeByLocalTime` dall&#39;API  motore video (AVE) per completare l&#39;operazione. Se sono presenti intervalli di DELETE e  metadati di decisione degli annunci da parte di Adobe Primetime, gli intervalli vengono eliminati per primi, quindi `AuditudeResolver` risolve gli annunci utilizzando il tipico flusso di lavoro di decisione degli annunci da parte di Adobe Primetime .

* **** REPLACEFo intervalli  `REPLACE` di tempo,  `placementInformations` vengono creati due intervalli iniziali, uno  `Mode.DELETE` e uno  `Mode.REPLACE`. `CustomRangeResolver` elimina prima gli intervalli di tempo e quindi  `AuditudeResolver` inserisce  `replaceDuration` nella timeline gli annunci degli annunci specificati. Se non viene specificato `replaceDuration`, il server determina cosa inserire.

Per supportare queste operazioni dell’intervallo di tempo personalizzato, TVSDK fornisce quanto segue:

* Più risolutori di contenuti

   Un flusso può avere più risolutori di contenuto basati sulla modalità di segnalazione degli annunci e sui metadati degli annunci. Il comportamento cambia con diverse combinazioni di modalità di segnalazione annunci e metadati annuncio.
* Più opportunità iniziali utilizzando `CustomMarkerOpportunityGenerator`.
* Una nuova modalità di segnalazione annunci, `CUSTOM_RANGES`.

   Gli annunci vengono inseriti in base ai dati Intervallo di tempo provenienti da un&#39;origine esterna, ad esempio un file JSON.

