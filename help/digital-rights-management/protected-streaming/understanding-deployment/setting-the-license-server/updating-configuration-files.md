---
description: Non appena il server licenze legge uno dei file di configurazione del server licenze (configurazione globale o tenant), le informazioni di configurazione vengono memorizzate nella cache. Pertanto i file non devono essere letti da disco per ogni richiesta di licenza. Tuttavia, il server consente anche di modificare la maggior parte dei valori nei file di configurazione senza che sia necessario riavviare il server per rendere attive le modifiche.
seo-description: Non appena il server licenze legge uno dei file di configurazione del server licenze (configurazione globale o tenant), le informazioni di configurazione vengono memorizzate nella cache. Pertanto i file non devono essere letti da disco per ogni richiesta di licenza. Tuttavia, il server consente anche di modificare la maggior parte dei valori nei file di configurazione senza che sia necessario riavviare il server per rendere attive le modifiche.
seo-title: Aggiornamento dei file di configurazione
title: Aggiornamento dei file di configurazione
uuid: 34b3247c-3458-49de-b1b0-dc0ebbf61c88
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Aggiornamento dei file di configurazione{#updating-configuration-files}

Non appena il server licenze legge uno dei file di configurazione del server licenze (configurazione globale o tenant), le informazioni di configurazione vengono memorizzate nella cache. Pertanto i file non devono essere letti da disco per ogni richiesta di licenza. Tuttavia, il server consente anche di modificare la maggior parte dei valori nei file di configurazione senza che sia necessario riavviare il server per rendere attive le modifiche.

Ogni volta che modificate il file di configurazione, il server licenze memorizza l&#39;ora dell&#39;ultima modifica del file. A un intervallo configurabile, il server verifica se l&#39;ora di modifica del file è cambiata. Se è stato modificato, il server ricarica automaticamente il contenuto del file di configurazione.

Per controllare la frequenza con cui il server verifica la presenza di aggiornamenti, è necessario impostare l&#39; `refreshDelaySeconds` attributo nell&#39; `Caching` elemento del file di configurazione globale. Ad esempio, se `refreshDelaySeconds` è impostato su 3600 secondi, il server aggiorna la configurazione entro al massimo un&#39;ora dal momento in cui il file di configurazione viene modificato. Se `refreshDelaySeconds` è impostato su 0, il server verifica la disponibilità di aggiornamenti di configurazione a ogni richiesta. Non è consigliabile impostare `refreshDelaySeconds` un valore basso in qualsiasi ambiente di produzione, in quanto questo può influire sulle prestazioni.

L&#39; `Caching` elemento controlla anche quante configurazioni di tenant vengono memorizzate nella cache contemporaneamente. È possibile impostare questo valore su un numero inferiore al numero totale di tenant per limitare la quantità di memoria utilizzata per memorizzare nella cache le informazioni di configurazione. Se viene ricevuta una richiesta per un tenant che non si trova nella cache, la configurazione viene caricata prima che sia possibile elaborare la richiesta. Se la cache è piena, il tenant utilizzato meno di recente viene rimosso dalla cache.

La versione memorizzata nella cache della configurazione continua a essere utilizzata nelle seguenti situazioni (fino alla successiva verifica degli aggiornamenti da parte del server):

* Se una modifica viene salvata in un file di configurazione o in uno dei file di certificato a cui si fa riferimento nel [!DNL flashaccess-tenant.xml] file mentre il server tenta di leggere il file
* Se la marca temporale del file è inferiore a un secondo prima dell&#39;ora corrente
* Se la marca temporale del file è futura

In assenza di una versione memorizzata nella cache, il caricamento della configurazione non riesce e viene restituito un errore al client. Il server quindi tenta di caricare di nuovo il file alla successiva ricezione di una richiesta per quel tenant.

## Aggiornamento del file di configurazione globale {#section_AA546C72442646CFB8906AEEBDF50587}

È possibile modificare la password HSM in [!DNL flashaccess-global.xml] qualsiasi momento. Le modifiche avranno effetto alla successiva ricarica del file di configurazione da parte del server. Tuttavia, le modifiche apportate agli elementi Logging e Caching non vengono ricaricate. È necessario riavviare il server prima che eventuali modifiche per questi elementi diventino effettive.

## Aggiornamento del file di configurazione del tenant {#section_71624DB8DF28480F84F34F0FF7FD4365}

È possibile modificare tutti i valori specificati nel [!DNL flashaccess-tenant.xml] file in qualsiasi momento. Le modifiche avranno effetto alla successiva ricarica del file di configurazione da parte del server. Inoltre, il server verifica la presenza di eventuali modifiche in tutti i file di credenziali ( [!DNL .pfx]) e i file di certificati whitelist del packager a cui viene fatto riferimento nel file di configurazione del tenant.
