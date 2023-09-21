---
description: La classe CustomRangeMetadata identifica diversi tipi di intervalli di tempo in un flusso VOD, contrassegnandoli, eliminandoli e sostituendoli. Per ciascuno di questi tipi di intervallo di tempo personalizzati, puoi eseguire le operazioni corrispondenti, inclusa l’eliminazione e la sostituzione del contenuto dell’annuncio.
title: Operazioni per intervalli di tempo personalizzati
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# Operazioni per intervalli di tempo personalizzati {#custom-time-range-operations}

La classe CustomRangeMetadata identifica diversi tipi di intervalli di tempo in un flusso VOD: mark, delete e replace. Per ciascuno di questi tipi di intervallo di tempo personalizzati, puoi eseguire le operazioni corrispondenti, inclusa l’eliminazione e la sostituzione del contenuto dell’annuncio.

<!--<a id="section_1323C0BAC259424C85A6ACFB48FE77EC"></a>-->

Per l’eliminazione e la sostituzione degli annunci, TVSDK utilizza quanto segue *operazione intervallo di tempo personalizzato* modalità:

* **CONTRASSEGNA** Questa modalità era nota come marcatori di annunci personalizzati nelle versioni precedenti di TVSDK. La modalità contrassegna l’ora di inizio e di fine per gli annunci già inseriti nel flusso VOD. Quando sono presenti marcatori intervallo di tempo di tipo `MARK` nel flusso, un posizionamento iniziale di `Mode.MARK` è generato da `CustomMarkerOpportunityGenerator` e risolti da `CustomRangeResolver`. Nessun annuncio inserito.

* **DELETE** Per `DELETE` intervalli di tempo, un `placementInformation` di tipo `Mode.DELETE` viene creato e risolto da `CustomRangeResolver`. `DeleteRangeTimelineOperation` definisce gli intervalli da rimuovere dalla timeline e TVSDK utilizza `removeByLocalTime` dall’API Adobe Video Engine (AVE) per completare questa operazione. Se sono presenti intervalli di DELETE e metadati di Adobe Primetime ad Decisioning, questi vengono eliminati per primi, quindi viene `AuditudeResolver` risolve gli annunci utilizzando il flusso di lavoro tipico di Adobe Primetime ad decisioning.

* **SOSTITUISCI** Per `REPLACE` intervalli di tempo, due `placementInformations` vengono creati, uno `Mode.DELETE` e uno `Mode.REPLACE`. `CustomRangeResolver` elimina prima gli intervalli di tempo e quindi `AuditudeResolver` inserisce annunci del `replaceDuration` nella timeline. In caso negativo `replaceDuration` è specificato, il server determina l&#39;elemento da inserire.

Per supportare queste operazioni dell&#39;intervallo di tempo personalizzato, TVSDK fornisce quanto segue:

* Più sistemi di risoluzione dei contenuti

  Un flusso può avere più risolutori di contenuto in base alla modalità di segnalazione degli annunci e ai metadati degli annunci. Il comportamento cambia con diverse combinazioni di modalità di segnalazione degli annunci e metadati degli annunci.
* Più opportunità iniziali utilizzando `CustomMarkerOpportunityGenerator`.
* Una nuova modalità di segnalazione pubblicitaria, `CUSTOM_RANGES`.

  Gli annunci vengono inseriti in base ai dati dell’intervallo di tempo provenienti da un’origine esterna, ad esempio un file JSON.
