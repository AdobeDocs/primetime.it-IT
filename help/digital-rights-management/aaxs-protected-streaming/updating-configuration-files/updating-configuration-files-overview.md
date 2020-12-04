---
seo-title: Aggiornamento della panoramica dei file di configurazione
title: Aggiornamento della panoramica dei file di configurazione
uuid: e9be21cf-ad23-4ed6-8bef-f194bc1fd749
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---


# Aggiornamento della panoramica dei file di configurazione {#updating-configuration-files-overview}

Una volta che il server licenze legge uno dei file di configurazione del server licenze (configurazione globale o tenant), le informazioni di configurazione vengono memorizzate nella cache. Pertanto, i file non devono essere letti da disco per ogni richiesta di licenza. Tuttavia, il server consente anche di modificare la maggior parte dei valori nei file di configurazione senza che sia necessario riavviare il server per rendere attive le modifiche. (Per informazioni dettagliate su quali valori di configurazione vengono verificati per verificare la disponibilità di aggiornamenti, vedere di seguito.)

Per ricaricare la configurazione quando vengono apportate modifiche, il server licenze memorizza l’ora dell’ultima modifica del file. A un intervallo configurabile, il server verifica se l&#39;ora di modifica del file è cambiata e, in tal caso, ricarica il contenuto del file.

Per controllare la frequenza con cui il server verifica la presenza di aggiornamenti, impostate l&#39;attributo `refreshDelaySeconds` nell&#39;elemento Cache del file di configurazione globale. Ad esempio, se `refreshDelaySeconds` è impostato su 3600 secondi, è necessario un&#39;ora al massimo dal momento in cui il file viene aggiornato per rilevare eventuali aggiornamenti di configurazione da parte del server. Se `refreshDelaySeconds` è impostato su 0, il server verifica la disponibilità di aggiornamenti di configurazione per ogni richiesta. L&#39;impostazione di `refreshDelaySeconds` su un valore basso non è consigliata per gli ambienti di produzione, in quanto potrebbe influire sulle prestazioni.

L&#39;elemento Caching controlla anche quante configurazioni di tenant vengono memorizzate nella cache contemporaneamente. È possibile impostare questo valore su un numero inferiore al numero totale di tenant per limitare la quantità di memoria utilizzata per memorizzare nella cache le informazioni di configurazione. Se viene ricevuta una richiesta per un tenant non presente nella cache, la configurazione viene caricata prima che sia possibile elaborare la richiesta. Se la cache è piena, il tenant utilizzato meno di recente viene rimosso dalla cache.

Se una modifica viene salvata in un file di configurazione o in uno dei file di certificato a cui si fa riferimento in [!DNL flashaccess-tenant.xml] mentre il server sta tentando di leggere il file, oppure se la marca temporale del file viene trovata meno di un secondo prima dell&#39;ora corrente o in futuro, la versione memorizzata nella cache della configurazione viene utilizzata fino alla successiva verifica da parte del server della disponibilità di aggiornamenti. In assenza di una versione memorizzata nella cache, il caricamento della configurazione non riesce e viene restituito un errore al client. Il server tenta di caricare di nuovo il file alla successiva ricezione di una richiesta per quel tenant.
