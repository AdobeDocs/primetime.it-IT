---
description: TVSDK supporta l’eliminazione e la sostituzione programmatica del contenuto di annunci nei flussi VOD.
title: Modifiche all’API di eliminazione e sostituzione dell’annuncio
exl-id: 4093af3c-41fd-4486-9e1c-26f68d3fbeb4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---

# Modifiche all’API di eliminazione e sostituzione dell’annuncio {#ad-deletion-and-replacement-api-changes}

TVSDK supporta l’eliminazione e la sostituzione programmatica del contenuto di annunci nei flussi VOD.

La funzione di eliminazione e sostituzione estende la funzione dei marcatori di annunci personalizzati. I marcatori di annunci personalizzati contrassegnano le sezioni del contenuto principale come periodi di contenuto relativi agli annunci. Oltre a contrassegnare questi intervalli di tempo, puoi anche eliminarli e sostituirli.

<!--<a id="section_7A90BFE99F1A4D908D6DDB0B49FA1199"></a>-->

Le seguenti modifiche in TVSDK supportano l’eliminazione e la sostituzione degli annunci.

**Nuove API**

* `PTTimeRangeCollection` è una classe pubblica che definisce un set predefinito di intervalli e un tipo:

   * `property PTTimeRangeCollectionType type` indica il tipo di intervallo di tempo.
   * `property NSArray* ranges` viene utilizzato per impostare gli intervalli di tempo.

      Il tipo di oggetti previsto nell’array è `PTReplacementTimeRange` o `CMTimeRange`.

      >[!TIP]
      >
      >Tutti gli oggetti dell&#39;array devono essere dello stesso tipo.

   * `PTTimeRangeCollectionType` è un&#39;enumerazione che definisce il comportamento degli intervalli definiti nel `PTTimeRangeCollection`:

      * `PTTimeRangeCollectionTypeMarkRanges`: il tipo di intervalli è *Contrassegna*. Gli intervalli vengono utilizzati per contrassegnare gli intervalli nel contenuto come Annunci.

      * `PTTimeRangeCollectionTypeDeleteRanges`: il tipo di intervalli è Elimina. Gli intervalli definiti vengono rimossi dal contenuto principale prima dell’inserimento dell’annuncio.
      * `PTTimeRangeCollectionTypeReplaceRanges`: il tipo di intervalli è Sostituisci. Gli intervalli definiti vengono sostituiti dal principale con Annunci (la modalità di segnalazione dell’annuncio è impostata su `PTAdSignalingModeCustomTimeRanges`).

* `PTReplacementTimeRange` - Nuova classe pubblica che definisce una singola gamma di `PTTimeRangeCollection`:

   * `property CMTimeRange range` - Definisce l’inizio e la durata dell’intervallo.
   * `property long replacementDuration` - Se il tipo di `TimeRangeCollection` è `PTTimeRangeCollectionTypeReplaceRanges`, il `replacementDuration` viene utilizzato per creare un’opportunità di posizionamento (inserimento di annunci) con una durata di `replacementDuration`. Se il `replacementDuration` non è impostato, il server di annunci determinerà la durata e il numero di annunci per tale opportunità di posizionamento.

* `PTAdSignalingMode`:

   * `PTAdSignalingModeCustomTimeRanges` - È stato aggiunto un nuovo tipo di `PTAdSignalingMode`. Questa modalità viene utilizzata insieme al `PTTimeRangeCollection` con tipo `PTTimeRangeCollectionReplace` per l’inserimento di annunci in base agli intervalli di sostituzione.

* `PTAdMetadata`:

   * `property PTTimeRangeCollection* timeRangeCollection` : per impostare gli intervalli di tempo utilizzati negli intervalli di contrassegno, eliminazione e sostituzione nel contenuto della riproduzione.

* Registri di avviso:

   * `UNDEFINED_TIME_RANGES`

      * Tipo - Avvertenza
      * Descrizione: la modalità di segnalazione degli annunci è definita come intervallo personalizzato, ma non sono definiti intervalli personalizzati.
   * `INVALID_TIME_RANGES`

      * Tipo - Avvertenza
      * Descrizione: uno o più intervalli di tempo non sono validi e verranno ignorati o modificati.


**API obsolete**

* `PTAdMetadata`:

   * `property NSArray* externalAdRanges` - Questa proprietà è stata utilizzata in precedenza per definire gli intervalli C3 per la marcatura. Ora è diventato obsoleto, poiché questi intervalli sono impostati tramite `PTTimeRangeCollection`.
