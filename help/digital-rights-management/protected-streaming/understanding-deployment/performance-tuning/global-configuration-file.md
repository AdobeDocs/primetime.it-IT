---
description: Questo argomento descrive considerazioni relative alle prestazioni. Qualsiasi impostazione nel file di configurazione globale denominato flashaccess-global.xml influisce sulle prestazioni.
title: File di configurazione globale
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# Ottimizzazione delle prestazioni {#performance-tuning}

Questo argomento descrive considerazioni relative alle prestazioni. Qualsiasi impostazione nel file di configurazione globale denominato flashaccess-global.xml influisce sulle prestazioni.

## File di configurazione globale {#global-configuration-file}

Il file di configurazione include i seguenti elementi di impostazione:

* `<Caching>` L&#39; `<Caching>` elemento controlla la memorizzazione in cache dei file di configurazione nella memoria. L&#39;elemento `<Caching>` supporta la seguente sintassi:

```
  <Caching refreshDelaySeconds="..." numTenants="..."/>
```

* `refreshDelaySeconds` Controlla la frequenza con cui il server verifica la presenza di aggiornamenti ai file di configurazione. Un valore basso per `refreshDelaySeconds` influisce negativamente sulle prestazioni, mentre un valore più alto può migliorare le prestazioni.

   Consulta *Aggiornamento dei file di configurazione* per ulteriori informazioni su `refreshDelaySeconds`.

* `numTenants` specifica il numero di tenant. Un valore inferiore al numero di tenant influisce sulle prestazioni perché le richieste ai tenant rimanenti generano errori di cache. Una perdita di cache per qualsiasi dato di configurazione influisce negativamente sulle prestazioni. Pertanto, si consiglia di impostare questo valore superiore al numero di tenant configurati per il server, a meno che non siano presenti limitazioni di memoria da considerare.

* `<Logging>` L&#39; `<Logging>` elemento specifica il livello di registrazione e la frequenza con cui vengono effettuati i rollup dei file di registro. L&#39;elemento `<Logging>` supporta la seguente sintassi:

   ```
   <Logging level="..." rollingFrequency="..."/>
   ```

* `<level>`  `level` specifica i messaggi in un registro. Il valore `DEBUG` genera molti messaggi di log che possono influire negativamente sulle prestazioni. Si consiglia di applicare un&#39;impostazione di `WARN` per ottenere prestazioni ottimali. Tuttavia, questo valore può causare la perdita di informazioni di runtime essenziali, come i controlli di licenza. Se desideri salvare le informazioni di registro con un impatto minimo sulle prestazioni, devi applicare un valore di `INFO`.

* `<rollingFrequency>`  `rollingFrequency` specifica la frequenza con cui vengono  *eseguiti il rollup* dei file di registro. *`Rolling`* è un processo che designa qualsiasi nuovo file di registro come registro attivo. Pertanto il file di registro precedentemente attivo non può più essere modificato e viene considerato *`rolled`*. È possibile impostare l’intervallo di scorrimento su `MINUTELY`, `HOURLY`, `TWICE-DAILY`, `DAILY`, `WEEKLY`, `MONTHLY` o `NEVER`.

Per suggerimenti su come ottimizzare le prestazioni, consulta *Utilizzo dell&#39;SDK DRM di Adobe Primetime per la protezione dei contenuti* .