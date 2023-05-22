---
description: In questo argomento vengono descritte le considerazioni relative alle prestazioni. Qualsiasi impostazione nel file di configurazione globale denominato flashaccess-global.xml influisce sulle prestazioni.
title: File di configurazione globale
exl-id: 52d41476-d352-4c02-8af6-25c0fe6bcaa7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Ottimizzazione delle prestazioni {#performance-tuning}

In questo argomento vengono descritte le considerazioni relative alle prestazioni. Qualsiasi impostazione nel file di configurazione globale denominato flashaccess-global.xml influisce sulle prestazioni.

## File di configurazione globale {#global-configuration-file}

Il file di configurazione include i seguenti elementi delle impostazioni:

* `<Caching>` Il `<Caching>` l&#39;elemento controlla la memorizzazione nella cache dei file di configurazione in memoria. Il `<Caching>` supporta la seguente sintassi:

```
  <Caching refreshDelaySeconds="..." numTenants="..."/>
```

* `refreshDelaySeconds` Controlla la frequenza con cui il server verifica la disponibilità di aggiornamenti per i file di configurazione. Un valore basso per `refreshDelaySeconds` influisce negativamente sulle prestazioni, mentre un valore più elevato può migliorarle.

   Consulta *Aggiornamento dei file di configurazione* per ulteriori informazioni su `refreshDelaySeconds`.

* `numTenants` specifica il numero di tenant. Un valore inferiore al numero di tenant influisce sulle prestazioni perché le richieste ai tenant rimanenti causano errori nella cache. Un mancato riscontro nella cache per qualsiasi dato di configurazione influisce negativamente sulle prestazioni. Pertanto, si consiglia di impostare questo valore su un valore maggiore del numero di tenant configurati per il server, a meno che non vi siano limitazioni di memoria da considerare.

* `<Logging>` Il `<Logging>` specifica il livello di registrazione e la frequenza con cui vengono eseguiti i rollback dei file di registro. Il `<Logging>` supporta la seguente sintassi:

   ```
   <Logging level="..." rollingFrequency="..."/>
   ```

* `<level>`  `level` specifica i messaggi in un registro. Un valore di `DEBUG` genera molti messaggi di registro, che possono influire negativamente sulle prestazioni. Si consiglia di applicare un&#39;impostazione `WARN` per prestazioni ottimali. Tuttavia, questo valore può comportare la perdita di informazioni di runtime essenziali, ad esempio i controlli delle licenze. Se desideri salvare le informazioni di registro con un impatto minimo sulle prestazioni, devi applicare un valore di `INFO`.

* `<rollingFrequency>`  `rollingFrequency` specifica la frequenza dei file di registro *laminato*. *`Rolling`* è un processo che designa qualsiasi nuovo file di registro come registro attivo. Pertanto, il file di registro precedentemente attivo non può più essere modificato e viene considerato *`rolled`*. È possibile impostare l&#39;intervallo continuo su `MINUTELY`, `HOURLY`, `TWICE-DAILY`, `DAILY`, `WEEKLY`, `MONTHLY`, o `NEVER`.

Consulta *Utilizzo dell’SDK Adobe Primetime DRM per la protezione dei contenuti* per suggerimenti su come ottimizzare le prestazioni.
