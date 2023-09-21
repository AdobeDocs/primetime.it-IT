---
title: File di configurazione globale
description: File di configurazione globale
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# File di configurazione globale{#global-configuration-file}

L&#39;impatto maggiore sulle prestazioni che è possibile ottenere è l&#39;utilizzo delle impostazioni del file di configurazione globale flashaccess-global.xml. Queste impostazioni includono `<Caching>` e `<Logging>` elementi.

* `<Caching>` Il `<Caching>` l&#39;elemento controlla la memorizzazione nella cache dei file di configurazione in memoria. Il `<Caching>` l&#39;elemento ha la seguente sintassi:

  ```
  <Caching refreshDelaySeconds="..." numTenants="..."/>
  ```

   * `refreshDelaySeconds` controlla la frequenza con cui il server verifica la disponibilità di aggiornamenti per i file di configurazione. Un valore basso per `refreshDelaySeconds` influisce negativamente sulle prestazioni, mentre un valore più elevato può migliorarle. Per ulteriori informazioni su `refreshDelaySeconds`, vedere &quot;[Aggiornamento dei file di configurazione](../../aaxs-protected-streaming/updating-configuration-files/updating-configuration-files-overview.md)&quot;.

   * `numTenants` specifica il numero di tenant. Un valore inferiore al numero di tenant influisce probabilmente sulle prestazioni perché le richieste ai tenant rimanenti si traducono in mancati riscontri nella cache. Un mancato riscontro della cache per i dati di configurazione influisce negativamente sulle prestazioni. Pertanto, Adobe consiglia di impostare questo valore su un valore maggiore del numero di tenant configurati per il server, a meno che non vi siano limitazioni di memoria da considerare.

* `<Logging>` Il `<Logging>` specifica il livello di log e la frequenza con cui viene eseguito il rollback dei file di log. Il `<Logging>` l&#39;elemento ha la seguente sintassi:

  ```
  <Logging level="..." rollingFrequency=""/>
  ```

   * `level` specifica i messaggi da registrare. Il valore &quot;DEBUG&quot; genera molti messaggi di registro e può avere un impatto negativo sulle prestazioni. L’Adobe consiglia di impostare &quot;WARN&quot; per ottenere prestazioni ottimali. Tuttavia, tale valore rischia di perdere informazioni di runtime essenziali, come i controlli delle licenze. Per conservare informazioni di registro preziose con un impatto minimo sulle prestazioni, utilizza il valore &quot;INFO&quot;.
   * `rollingFrequency` specifica la frequenza dei file di registro *laminato*. Il rollover è il processo in cui un nuovo file di log diventa il log attivo, mentre il file di log precedentemente attivo non viene più scritto in e viene considerato rollover. L&#39;intervallo continuo può essere impostato su &quot;MINUTELY&quot;, &quot;HOURLY&quot;, &quot;TWICE-DAILY&quot;, &quot;DAILY&quot;, &quot;WEEKLY&quot;, &quot;MONTHLY&quot; o &quot;NEVER&quot;.

Consulta *Utilizzo dell’SDK per l’accesso agli Adobi per la protezione dei contenuti* per ulteriori suggerimenti sull’ottimizzazione delle prestazioni.
