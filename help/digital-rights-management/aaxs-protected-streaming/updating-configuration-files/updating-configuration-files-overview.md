---
title: Panoramica sull'aggiornamento dei file di configurazione
description: Panoramica sull'aggiornamento dei file di configurazione
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---


# Aggiornamento della panoramica dei file di configurazione {#updating-configuration-files-overview}

Una volta che il server licenze legge uno dei file di configurazione del server licenze (configurazione globale o tenant), le informazioni di configurazione vengono memorizzate nella cache. Pertanto, i file non devono essere letti dal disco per ogni richiesta di licenza. Tuttavia, il server consente anche di modificare la maggior parte dei valori nei file di configurazione senza richiedere il riavvio del server per rendere effettive le modifiche. (Vedi di seguito per i dettagli sui valori di configurazione controllati per verificare la disponibilità di aggiornamenti.)

Per ricaricare la configurazione quando vengono apportate modifiche, il server licenze memorizza l&#39;ora dell&#39;ultima modifica del file. A un intervallo configurabile, il server controlla se l&#39;ora di modifica del file è cambiata e, in tal caso, ricarica il contenuto del file.

Per controllare la frequenza con cui il server controlla gli aggiornamenti, imposta l&#39;attributo `refreshDelaySeconds` nell&#39;elemento Cache del file di configurazione globale. Ad esempio, se `refreshDelaySeconds` è impostato su 3600 secondi, ci vuole al massimo un&#39;ora dal momento in cui il file viene aggiornato per rilevare eventuali aggiornamenti di configurazione da parte del server. Se `refreshDelaySeconds` è impostato su 0, il server verifica la disponibilità di aggiornamenti di configurazione per ogni richiesta. L’impostazione di `refreshDelaySeconds` su un valore basso non è consigliata per gli ambienti di produzione, in quanto potrebbe influire sulle prestazioni.

L’elemento Caching controlla anche quante configurazioni dei tenant sono memorizzate nella cache contemporaneamente. Puoi impostare questo valore su un numero inferiore al numero totale di tenant per limitare la quantità di memoria utilizzata per memorizzare nella cache le informazioni di configurazione. Se viene ricevuta una richiesta per un tenant non presente nella cache, la configurazione viene caricata prima che la richiesta possa essere elaborata. Se la cache è piena, il tenant utilizzato meno di recente viene rimosso dalla cache.

Se una modifica viene salvata in un file di configurazione o in uno qualsiasi dei file di certificato a cui si fa riferimento all&#39;interno di [!DNL flashaccess-tenant.xml] mentre il server sta tentando di leggere il file, o se la marca temporale del file si trova meno di un secondo prima dell&#39;ora corrente o in futuro, la versione cache della configurazione viene utilizzata fino alla successiva verifica degli aggiornamenti da parte del server. Se non è presente una versione cache, il caricamento della configurazione non riesce e viene restituito un errore al client. Il server tenta di caricare nuovamente il file alla successiva ricezione di una richiesta per quel tenant.
