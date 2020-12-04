---
description: Le seguenti modifiche nel supporto TVSDK e nella sostituzione degli annunci.
seo-description: Le seguenti modifiche nel supporto TVSDK e nella sostituzione degli annunci.
seo-title: Modifiche alle API di eliminazione e sostituzione degli annunci
title: Modifiche alle API di eliminazione e sostituzione degli annunci
uuid: 7cc50e7a-666f-4588-9c16-ad6d7d75cb65
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---


# Modifiche alle API di eliminazione annunci e sostituzione{#ad-deletion-and-replacement-api-changes}

Le seguenti modifiche nel supporto TVSDK e nella sostituzione degli annunci.

**Nuove API**

* `PTTimeRangeCollection` è una classe pubblica che definisce un insieme predefinito di intervalli e un tipo:

   * `property PTTimeRangeCollectionType type` indica il tipo di intervallo di tempo.
   * `property NSArray* ranges` viene utilizzato per impostare gli intervalli di tempo.

      Il tipo previsto di oggetti nell&#39;array è `PTReplacementTimeRange` o `CMTimeRange`.

      >[!TIP]
      >
      >Tutti gli oggetti dell&#39;array devono essere dello stesso tipo.

   * `PTTimeRangeCollectionType` è un enum che definisce il comportamento degli intervalli definiti in  `PTTimeRangeCollection`:

      * `PTTimeRangeCollectionTypeMarkRanges`: Il tipo di intervallo è  *Contrassegno*. Gli intervalli vengono utilizzati per contrassegnare gli intervalli nel contenuto come Annunci.

      * `PTTimeRangeCollectionTypeDeleteRanges`: Il tipo di intervallo è Elimina. Gli intervalli definiti vengono rimossi dal contenuto principale prima dell’inserimento degli annunci.
      * `PTTimeRangeCollectionTypeReplaceRanges`: Il tipo degli intervalli è Replace (Sostituisci). Gli intervalli definiti vengono sostituiti dal principale con Annunci (la modalità Ad Signaling è impostata su `PTAdSignalingModeCustomTimeRanges`).

* `PTReplacementTimeRange` - Nuova classe pubblica che definisce un singolo intervallo di  `PTTimeRangeCollection`:

   * `property CMTimeRange range` - Definisce l&#39;inizio e la durata dell&#39;intervallo.
   * `property long replacementDuration` - Se il tipo di oggetto  `TimeRangeCollection` è  `PTTimeRangeCollectionTypeReplaceRanges`,  `replacementDuration` viene utilizzato per creare un&#39;opportunità di posizionamento (inserimento di annunci) con una durata di  `replacementDuration`. Se `replacementDuration` non è impostato, il server degli annunci determinerà la durata e il numero di annunci per tale opportunità di posizionamento.

* `PTAdSignalingMode`:

   * `PTAdSignalingModeCustomTimeRanges` - Aggiunta di un nuovo tipo di  `PTAdSignalingMode`. Questa modalità viene utilizzata insieme a `PTTimeRangeCollection` con il tipo `PTTimeRangeCollectionReplace` per l&#39;inserimento di annunci in base agli intervalli di sostituzione.

* `PTAdMetadata`:

   * `property PTTimeRangeCollection* timeRangeCollection` - Per impostare gli intervalli di tempo utilizzati negli intervalli di tempo mark/delete/replace nel contenuto di riproduzione.

* Registri di avvisi:

   * `UNDEFINED_TIME_RANGES`

      * Tipo - Avviso
      * Descrizione - La modalità di segnalazione degli annunci è definita come intervalli personalizzati, ma gli intervalli personalizzati non sono definiti.
   * `INVALID_TIME_RANGES`

      * Tipo - Avviso
      * Descrizione: uno o più intervalli di tempo non sono validi e verranno ignorati o modificati.


**API obsolete**

* `PTAdMetadata`:

   * `property NSArray* externalAdRanges` - Questa proprietà è stata utilizzata in precedenza per definire gli intervalli C3 per la marcatura. Ora è obsoleto, in quanto questi intervalli sono impostati tramite `PTTimeRangeCollection`.

