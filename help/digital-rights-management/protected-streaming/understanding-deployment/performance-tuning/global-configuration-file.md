---
description: Questo argomento descrive considerazioni relative alle prestazioni. Qualsiasi impostazione nel file di configurazione globale denominato flashaccess-global.xml influisce sulle prestazioni.
seo-description: Questo argomento descrive considerazioni relative alle prestazioni. Qualsiasi impostazione nel file di configurazione globale denominato flashaccess-global.xml influisce sulle prestazioni.
seo-title: File di configurazione globale
title: File di configurazione globale
uuid: 254925b5-d441-4a35-ad6f-f99db5de7591
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Ottimizzazione delle prestazioni {#performance-tuning}

Questo argomento descrive considerazioni relative alle prestazioni. Qualsiasi impostazione nel file di configurazione globale denominato flashaccess-global.xml influisce sulle prestazioni.

## File di configurazione globale {#global-configuration-file}

Il file di configurazione include i seguenti elementi di configurazione:

* `<Caching>` L&#39; `<Caching>` elemento controlla la memorizzazione nella cache dei file di configurazione. L&#39; `<Caching>` elemento supporta la sintassi seguente:

```
  <Caching refreshDelaySeconds="..." numTenants="..."/>
```

* `refreshDelaySeconds` Controlla la frequenza con cui il server verifica la presenza di aggiornamenti ai file di configurazione. Un valore basso incide `refreshDelaySeconds` negativamente sulle prestazioni, mentre un valore più alto può migliorare le prestazioni.

   Per ulteriori informazioni, consulta *Aggiornamento dei file* di configurazione `refreshDelaySeconds`.

* `numTenants` specifica il numero di tenant. Un valore inferiore al numero di tenant influisce sulle prestazioni perché le richieste ai tenant rimanenti causano errori nella cache. Una perdita della cache per qualsiasi dato di configurazione influisce negativamente sulle prestazioni. Si consiglia pertanto di impostare questo valore superiore al numero di tenant configurati per il server, a meno che non siano presenti limitazioni di memoria da tenere in considerazione.

* `<Logging>` L’ `<Logging>` elemento specifica il livello di registrazione e la frequenza con cui vengono effettuati il rollout dei file di registro. L&#39; `<Logging>` elemento supporta la sintassi seguente:

   ```
   <Logging level="..." rollingFrequency="..."/>
   ```

* `<level>`  specifica `level` i messaggi da inviare a un registro. Un valore di `DEBUG` restituisce molti messaggi di registro, che possono influire negativamente sulle prestazioni. Si consiglia di applicare un&#39;impostazione di `WARN` per ottenere prestazioni ottimali. Tuttavia, questo valore può causare la perdita di informazioni di runtime essenziali, come i controlli delle licenze. Se desiderate salvare le informazioni di registro con un impatto minimo sulle prestazioni, dovete applicare un valore di `INFO`.

* `<rollingFrequency>`  specifica `rollingFrequency` la frequenza di *rollover* dei file di registro. *`Rolling`* è un processo che designa qualsiasi nuovo file di registro come registro attivo. Pertanto, il file di registro attivo in precedenza non può più essere modificato e viene considerato *`rolled`*. È possibile impostare l&#39;intervallo di scorrimento su `MINUTELY`, `HOURLY`, `TWICE-DAILY`, `DAILY`, `WEEKLY`, `MONTHLY`o `NEVER`.

Consultate *Utilizzo di Adobe Primetime DRM SDK per la protezione dei contenuti* per suggerimenti su come ottimizzare le prestazioni.