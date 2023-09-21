---
description: TVSDK supporta l’eliminazione e la sostituzione programmatica del contenuto di annunci nei flussi VOD.
title: Operazioni per intervalli di tempo personalizzati
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# Operazioni per intervalli di tempo personalizzati {#custom-time-range-operations}

TVSDK supporta l’eliminazione e la sostituzione programmatica del contenuto di annunci nei flussi VOD.

La funzione di eliminazione e sostituzione estende la funzione dei marcatori di annunci personalizzati. I marcatori di annunci personalizzati contrassegnano le sezioni del contenuto principale come periodi di contenuto relativi agli annunci. Oltre a contrassegnare questi intervalli di tempo, puoi anche eliminarli e sostituirli.

L’eliminazione e la sostituzione degli annunci sono implementate con `TimeRange` elementi che identificano diversi tipi di intervalli di tempo in un flusso VOD: contrassegna, elimina e sostituisci. Per ciascuno di questi tipi di intervallo di tempo personalizzati, puoi eseguire le operazioni corrispondenti, inclusa l’eliminazione e la sostituzione del contenuto dell’annuncio.

Per l’eliminazione e la sostituzione degli annunci, TVSDK utilizza quanto segue *operazione intervallo di tempo personalizzato* modalità:

* **CONTRASSEGNA**
Nelle versioni precedenti di TVSDK, questi sono stati denominati marcatori di annunci personalizzati. Segnano l’ora di inizio e di fine per gli annunci già inseriti nel flusso VOD. Quando nel flusso sono presenti marcatori intervallo di tempo di tipo MARK, viene inserito un `Mode.MARK` viene generato e risolto da `CustomAdMarkersContentResolver`. Nessun annuncio inserito.

* **DELETE**
Per gli intervalli di tempo DELETE, un `placementInformation` di tipo `Mode.DELETE` viene creato e risolto dal corrispondente `DeleteContentResolver`. `ContentRemoval` è un nuovo `timelineOperation` che definisce gli intervalli da rimuovere dalla timeline. TVSDK utilizza `removeByLocalTime` dall’API Adobe Video Engine (AVE) per facilitare tale operazione. Se sono presenti intervalli di DELETE e metadati di Adobe Primetime ad decisioning (precedentemente noti come Auditude), questi vengono eliminati prima, quindi `AuditudeResolver` risolve gli annunci utilizzando il normale flusso di lavoro di Adobe Primetime ad decisioning.

* **SOSTITUISCI**
Per gli intervalli di tempo REPLACE, due `placementInformations` vengono creati, uno `Mode.DELETE` e uno `Mode.REPLACE`. Il `DeleteContentResolver` elimina prima gli intervalli di tempo e quindi `AuditudeResolver` inserisce annunci del `replaceDuration` nella timeline. In caso negativo `replaceDuration` è specificato, il server determina l&#39;elemento da inserire.

Per supportare queste operazioni dell&#39;intervallo di tempo personalizzato, TVSDK fornisce quanto segue:

* Più sistemi di risoluzione dei contenuti

  Un flusso può avere più risolutori di contenuto in base alla modalità di segnalazione degli annunci e ai metadati degli annunci. Il comportamento cambia con diverse combinazioni di modalità di segnalazione degli annunci e metadati degli annunci.
* Iniziali multiple `PlacementInformations` Il `DefaultMediaPlayer` crea un elenco di `PlacementInformations` in base alla modalità di segnalazione degli annunci e ai metadati degli annunci che devono essere risolti da `MediaPlayerClient`.

* Nuova modalità di segnalazione degli annunci: intervalli di tempo personalizzati

  Gli annunci vengono inseriti in base ai dati dell’intervallo di tempo provenienti da un’origine esterna (ad esempio un file JSON).
