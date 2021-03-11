---
title: File di configurazione globale
description: File di configurazione globale
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---


# File di configurazione globale{#global-configuration-file}

L&#39;impatto maggiore sulle prestazioni che puoi ottenere è l&#39;utilizzo delle impostazioni nel file di configurazione globale flashaccess-global.xml. Queste impostazioni includono gli elementi `<Caching>` e `<Logging>` .

* `<Caching>` L&#39; `<Caching>` elemento controlla la memorizzazione in cache dei file di configurazione nella memoria. L&#39;elemento `<Caching>` ha la seguente sintassi:

   ```
   <Caching refreshDelaySeconds="..." numTenants="..."/>
   ```

   * `refreshDelaySeconds` controlla la frequenza con cui il server verifica la presenza di aggiornamenti ai file di configurazione. Un valore basso per `refreshDelaySeconds` influisce negativamente sulle prestazioni, mentre un valore più alto può migliorare le prestazioni. Per ulteriori informazioni su `refreshDelaySeconds`, consulta &quot;[Aggiornamento dei file di configurazione](../../aaxs-protected-streaming/updating-configuration-files/updating-configuration-files-overview.md)&quot;.

   * `numTenants` specifica il numero di tenant. Un valore inferiore al numero di tenant probabilmente influisce sulle prestazioni perché le richieste ai tenant rimanenti generano errori di cache. Una perdita della cache per i dati di configurazione influisce negativamente sulle prestazioni. Pertanto, Adobe consiglia di impostare questo valore più alto del numero di tenant configurati per il server, a meno che non vi siano limitazioni di memoria da considerare.

* `<Logging>` L&#39; `<Logging>` elemento specifica il livello di registrazione e la frequenza con cui vengono effettuati i rollup dei file di registro. L&#39;elemento `<Logging>` ha la seguente sintassi:

   ```
   <Logging level="..." rollingFrequency=""/>
   ```

   * `level` specifica i messaggi da registrare. Un valore di &quot;DEBUG&quot; genera molti messaggi di log e può avere un impatto negativo sulle prestazioni. L&#39;Adobe consiglia un&#39;impostazione di &quot;WARN&quot; per prestazioni ottimali. Tuttavia, tale valore rischia di perdere informazioni di runtime essenziali, come i controlli delle licenze. Per preservare informazioni di log preziose con un impatto minimo sulle prestazioni, utilizza un valore di &quot;INFO&quot;.
   * `rollingFrequency` specifica la frequenza con cui vengono  *eseguiti il rollup* dei file di registro. Rolling è il processo in cui un nuovo file di registro diventa il registro attivo, mentre il file di registro precedentemente attivo non viene più scritto in e viene considerato come rollup. L&#39;intervallo di rotolamento può essere impostato su &quot;MINUTELY&quot;, &quot;HOURLY&quot;, &quot;TWICE-DAILY&quot;, &quot;DAILY&quot;, &quot;WEEKLY&quot;, &quot;MONTHLY&quot; o &quot;NEVER&quot;.

Per ulteriori suggerimenti su come ottimizzare le prestazioni, consulta *Utilizzo dell&#39;SDK per l&#39;accesso Adobe per la protezione dei contenuti* .
