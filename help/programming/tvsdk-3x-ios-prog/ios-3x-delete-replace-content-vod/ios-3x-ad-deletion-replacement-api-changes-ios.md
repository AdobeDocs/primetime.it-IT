---
description: TVSDK supporta l’eliminazione programmatica e la sostituzione del contenuto degli annunci nei flussi VOD.
title: Modifiche all’API di cancellazione e sostituzione degli annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# Modifiche API di cancellazione e sostituzione degli annunci {#ad-deletion-and-replacement-api-changes}

TVSDK supporta l’eliminazione programmatica e la sostituzione del contenuto degli annunci nei flussi VOD.

La funzione di eliminazione e sostituzione estende la funzione degli ad markers personalizzati. Gli ad markers personalizzati contrassegnano sezioni del contenuto principale come periodi di contenuto relativi agli annunci. Oltre a contrassegnare questi intervalli di tempo, puoi anche eliminare e sostituire gli intervalli di tempo.

<!--<a id="section_7A90BFE99F1A4D908D6DDB0B49FA1199"></a>-->

Le seguenti modifiche in TVSDK supportano e cancellano e sostituiscono gli annunci.

**Nuove API**

* `PTTimeRangeCollection` è una classe pubblica che definisce un set predefinito di intervalli e un tipo:

   * `property PTTimeRangeCollectionType type` indica il tipo di intervallo di tempo.
   * `property NSArray* ranges` viene utilizzato per impostare gli intervalli di tempo.

      Il tipo previsto di oggetti nell&#39;array è `PTReplacementTimeRange` o `CMTimeRange`.

      >[!TIP]
      >
      >Tutti gli oggetti della matrice devono essere dello stesso tipo.

   * `PTTimeRangeCollectionType` è un enum che definisce il comportamento degli intervalli definiti in  `PTTimeRangeCollection`:

      * `PTTimeRangeCollectionTypeMarkRanges`: Il tipo degli intervalli è  *Mark*. Gli intervalli vengono utilizzati per contrassegnare gli intervalli nel contenuto come Annunci.

      * `PTTimeRangeCollectionTypeDeleteRanges`: Il tipo di intervallo è Elimina. Gli intervalli definiti vengono rimossi dal contenuto principale prima dell’inserimento dell’annuncio.
      * `PTTimeRangeCollectionTypeReplaceRanges`: Il tipo degli intervalli è Replace. Gli intervalli definiti vengono sostituiti dal principale con Annunci (la modalità di segnalazione degli annunci è impostata su `PTAdSignalingModeCustomTimeRanges`).

* `PTReplacementTimeRange` - Nuova classe pubblica che definisce un singolo intervallo di  `PTTimeRangeCollection`:

   * `property CMTimeRange range` - Definisce l&#39;inizio e la durata dell&#39;intervallo.
   * `property long replacementDuration` - Se il tipo di  `TimeRangeCollection` è  `PTTimeRangeCollectionTypeReplaceRanges`,  `replacementDuration` viene utilizzato per creare un’opportunità di posizionamento (inserimento di annunci) con una durata di  `replacementDuration`. Se `replacementDuration` non è impostato, il server di annunci determinerà la durata e il numero di annunci per l’opportunità di posizionamento.

* `PTAdSignalingMode`:

   * `PTAdSignalingModeCustomTimeRanges` - È stato aggiunto un nuovo tipo di  `PTAdSignalingMode`. Questa modalità viene utilizzata insieme al `PTTimeRangeCollection` con il tipo `PTTimeRangeCollectionReplace` per l’inserimento di annunci in base agli intervalli di sostituzione.

* `PTAdMetadata`:

   * `property PTTimeRangeCollection* timeRangeCollection` - Per impostare gli intervalli di tempo utilizzati negli intervalli di tempo di mark/delete/replace nel contenuto di riproduzione.

* Log di avviso:

   * `UNDEFINED_TIME_RANGES`

      * Tipo - Avviso
      * Descrizione : la modalità di segnalazione degli annunci è definita come intervalli personalizzati, ma gli intervalli personalizzati non sono definiti.
   * `INVALID_TIME_RANGES`

      * Tipo - Avviso
      * Descrizione: uno o più intervalli di tempo non sono validi e verranno ignorati o modificati.


**API obsolete**

* `PTAdMetadata`:

   * `property NSArray* externalAdRanges` - Questa proprietà è stata utilizzata in precedenza per definire intervalli C3 per la marcatura. È ora obsoleto, in quanto questi intervalli vengono impostati tramite `PTTimeRangeCollection`.