---
seo-title: File di configurazione globale
title: File di configurazione globale
uuid: 48c45f56-55c2-4526-b854-5552caf21541
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# File di configurazione globale{#global-configuration-file}

L&#39;impatto maggiore sulle prestazioni che è possibile ottenere è l&#39;utilizzo delle impostazioni nel file di configurazione globale flashaccess-global.xml. Queste impostazioni includono gli `<Caching>` elementi e `<Logging>` gli elementi.

* `<Caching>` L&#39; `<Caching>` elemento controlla la memorizzazione nella cache dei file di configurazione. L&#39; `<Caching>` elemento ha la sintassi seguente:

   ```
   <Caching refreshDelaySeconds="..." numTenants="..."/>
   ```

   * `refreshDelaySeconds` controlla la frequenza con cui il server verifica la presenza di aggiornamenti ai file di configurazione. Un valore basso per le prestazioni influisce `refreshDelaySeconds` negativamente, mentre un valore più elevato può migliorare le prestazioni. Per ulteriori informazioni su `refreshDelaySeconds`, vedere &quot;[Aggiornamento dei file](../../aaxs-protected-streaming/updating-configuration-files/updating-configuration-files-overview.md)di configurazione&quot;.

   * `numTenants` specifica il numero di tenant. Un valore inferiore al numero di tenant che probabilmente influisce sulle prestazioni perché le richieste ai tenant rimanenti causano errori nella cache. Una perdita della cache per i dati di configurazione influisce negativamente sulle prestazioni. Pertanto, Adobe consiglia di impostare questo valore più alto del numero di tenant configurati per il server, a meno che non ci siano limitazioni di memoria da considerare.

* `<Logging>` L’ `<Logging>` elemento specifica il livello di registrazione e la frequenza di scorrimento dei file di registro. L&#39; `<Logging>` elemento ha la sintassi seguente:

   ```
   <Logging level="..." rollingFrequency=""/>
   ```

   * `level` specifica i messaggi da registrare. Il valore &quot;DEBUG&quot; genera molti messaggi di registro e può avere un impatto negativo sulle prestazioni. Adobe consiglia di impostare &quot;WARN&quot; per ottenere prestazioni ottimali. Tuttavia, tale valore rischia di perdere informazioni di runtime essenziali, come i controlli delle licenze. Per conservare informazioni di registro di valore con un impatto minimo sulle prestazioni, utilizzate un valore &quot;INFO&quot;.
   * `rollingFrequency` specifica la frequenza con cui vengono *eseguiti il rollout* dei file di registro. Rolling è il processo in cui un nuovo file di registro diventa il registro attivo, mentre il file di registro precedentemente attivo non viene più scritto e viene considerato come rollout. L&#39;intervallo di rotolamento può essere impostato su &quot;MINUTELY&quot;, &quot;HOURLY&quot;, &quot;DOPPIO GIORNO&quot;, &quot;DAILY&quot;, &quot;WEEKLY&quot;, &quot;MONTHLY&quot; o &quot;NEVER&quot;.

Consulta *Utilizzo di Adobe Access SDK per la protezione dei contenuti* per suggerimenti aggiuntivi sull&#39;ottimizzazione delle prestazioni.
