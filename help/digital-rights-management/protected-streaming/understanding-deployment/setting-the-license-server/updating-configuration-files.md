---
description: Non appena il server licenze legge uno dei file di configurazione del server licenze (configurazione globale o tenant), le informazioni di configurazione vengono memorizzate nella cache. Pertanto, i file non devono essere letti dal disco per ogni richiesta di licenza. Tuttavia, il server consente anche di modificare la maggior parte dei valori contenuti nei file di configurazione senza richiedere il riavvio del server per rendere effettive le modifiche.
title: Aggiornamento dei file di configurazione
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---


# Aggiornamento dei file di configurazione{#updating-configuration-files}

Non appena il server licenze legge uno dei file di configurazione del server licenze (configurazione globale o tenant), le informazioni di configurazione vengono memorizzate nella cache. Pertanto, i file non devono essere letti dal disco per ogni richiesta di licenza. Tuttavia, il server consente anche di modificare la maggior parte dei valori contenuti nei file di configurazione senza richiedere il riavvio del server per rendere effettive le modifiche.

Ogni volta che si modifica il file di configurazione, il server licenze memorizza l&#39;ora dell&#39;ultima modifica apportata al file. A un intervallo configurabile, il server controlla se il tempo di modifica del file è cambiato. Se è stato modificato, il server ricarica automaticamente il contenuto del file di configurazione.

Per controllare la frequenza con cui il server verifica la disponibilità di aggiornamenti, è necessario impostare `refreshDelaySeconds` attributo in `Caching` del file di configurazione globale. Ad esempio, se `refreshDelaySeconds` è impostato su 3600 secondi, il server aggiornerà la configurazione entro al massimo un&#39;ora dalla modifica del file di configurazione. Se `refreshDelaySeconds` è impostato su 0, il server controlla la disponibilità di aggiornamenti della configurazione a ogni richiesta. Non è consigliabile impostare `refreshDelaySeconds` a un valore ridotto in qualsiasi ambiente di produzione, in quanto ciò può influire sulle prestazioni.

Il `Caching` L&#39;elemento controlla anche il numero di configurazioni dei tenant memorizzate nella cache contemporaneamente. Puoi impostare questo valore su un numero inferiore al numero totale di tenant, in modo da limitare la quantità di memoria utilizzata per memorizzare nella cache le informazioni di configurazione. Se viene ricevuta una richiesta per un tenant non presente nella cache, la configurazione viene caricata prima che la richiesta possa essere elaborata. Se la cache è piena, il tenant utilizzato meno di recente viene rimosso dalla cache.

La versione cache della configurazione continua a essere utilizzata nelle seguenti situazioni (fino alla successiva verifica della disponibilità di aggiornamenti da parte del server):

* Se una modifica viene salvata in un file di configurazione o in uno dei file di certificato a cui si fa riferimento nel [!DNL flashaccess-tenant.xml] mentre il server tenta di leggere il file
* Se il timestamp del file risulta essere inferiore a un secondo prima dell’ora corrente
* Se la marca temporale del file è nel futuro

Se non è presente alcuna versione memorizzata nella cache, il caricamento della configurazione non riesce e viene restituito un errore al client. Il server tenta quindi di caricare di nuovo il file alla successiva richiesta per quel tenant.

## Aggiornamento del file di configurazione globale {#section_AA546C72442646CFB8906AEEBDF50587}

È possibile modificare la password HSM in [!DNL flashaccess-global.xml] in qualsiasi momento. Le modifiche diventano effettive al successivo ricaricamento del file di configurazione da parte del server. Tuttavia, le modifiche apportate agli elementi Logging e Caching non vengono ricaricate. È necessario riavviare il server prima che qualsiasi modifica apportata a questi elementi diventi effettiva.

## Aggiornamento del file di configurazione tenant {#section_71624DB8DF28480F84F34F0FF7FD4365}

È possibile modificare tutti i valori specificati in [!DNL flashaccess-tenant.xml] in qualsiasi momento. Le modifiche diventano effettive al successivo ricaricamento del file di configurazione da parte del server. Inoltre, il server verifica la presenza di eventuali modifiche in tutte le credenziali ( [!DNL .pfx]) file e file di certificato di elenco consentiti packager a cui viene fatto riferimento nel file di configurazione tenant.
