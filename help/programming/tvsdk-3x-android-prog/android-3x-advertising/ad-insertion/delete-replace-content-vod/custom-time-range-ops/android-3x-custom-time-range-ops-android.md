---
description: La classe CustomRangeMetadata identifica diversi tipi di intervalli di tempo in un indicatore di flusso VOD, elimina e sostituisce. Per ciascuno di questi tipi di intervallo di tempo personalizzato, puoi eseguire le operazioni corrispondenti, tra cui eliminare e sostituire il contenuto dell’annuncio.
title: Operazioni con intervalli di tempo personalizzati
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# Operazioni con intervallo di tempo personalizzato {#custom-time-range-operations}

La classe CustomRangeMetadata identifica diversi tipi di intervalli di tempo in un flusso VOD: contrassegna, elimina e sostituisci. Per ciascuno di questi tipi di intervallo di tempo personalizzato, puoi eseguire le operazioni corrispondenti, tra cui eliminare e sostituire il contenuto dell’annuncio.

<!--<a id="section_1323C0BAC259424C85A6ACFB48FE77EC"></a>-->

Per l&#39;eliminazione e la sostituzione degli annunci, TVSDK utilizza le seguenti modalità *funzionamento dell&#39;intervallo di tempo personalizzato*:

* **** MARKTquesta modalità è stata definita come ad markers personalizzati nelle versioni precedenti di TVSDK. La modalità contrassegna i tempi di inizio e fine per gli annunci che sono già inseriti nel flusso VOD. Quando nel flusso sono presenti marcatori di intervallo di tempo di tipo `MARK`, un posizionamento iniziale di `Mode.MARK` viene generato da `CustomMarkerOpportunityGenerator` e risolto da `CustomRangeResolver`. Non vengono inseriti annunci.

* **** DELETEFo intervalli di  `DELETE` tempo,  `placementInformation` viene creato e risolto un iniziale  `Mode.DELETE` di tipo  `CustomRangeResolver`. `DeleteRangeTimelineOperation` definisce gli intervalli da rimuovere dalla timeline e per completare l’operazione TVSDK utilizza  `removeByLocalTime` l’API del motore video di Adobe (AVE). Se sono presenti intervalli di DELETE e metadati Adobe Primetime ad decisioning, gli intervalli vengono eliminati per primi, quindi il `AuditudeResolver` risolve gli annunci utilizzando il flusso di lavoro tipico di Adobe Primetime ad decision ioning.

* **** SOSTITUISCIo intervalli di  `REPLACE` tempo,  `placementInformations` vengono creati due intervalli iniziali, uno  `Mode.DELETE` e uno  `Mode.REPLACE`. `CustomRangeResolver` elimina prima gli intervalli di tempo e quindi  `AuditudeResolver` inserisce gli annunci degli annunci specificati  `replaceDuration` nella timeline. Se non viene specificato alcun valore `replaceDuration`, il server determina cosa inserire.

Per supportare queste operazioni dell’intervallo di tempo personalizzato, TVSDK fornisce quanto segue:

* Più risolutori di contenuti

   Un flusso può avere più risolutori di contenuti in base alla modalità di segnalazione degli annunci e ai metadati degli annunci. Il comportamento cambia con diverse combinazioni di modalità di segnalazione degli annunci e metadati degli annunci.
* Molteplici opportunità iniziali tramite `CustomMarkerOpportunityGenerator`.
* Una nuova modalità di segnalazione degli annunci, `CUSTOM_RANGES`.

   Gli annunci vengono inseriti in base ai dati dell’intervallo di tempo provenienti da un’origine esterna, ad esempio un file JSON.