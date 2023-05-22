---
title: Aggiornamento della panoramica dei file di configurazione
description: Aggiornamento della panoramica dei file di configurazione
copied-description: true
exl-id: 51c8a0af-9445-4c9e-93bc-af0af0096705
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# Aggiornamento della panoramica dei file di configurazione {#updating-configuration-files-overview}

Una volta che il server licenze legge uno dei file di configurazione del server licenze (configurazione globale o tenant), le informazioni di configurazione vengono memorizzate nella cache. Pertanto, i file non devono essere letti dal disco per ogni richiesta di licenza. Tuttavia, il server consente anche di modificare la maggior parte dei valori contenuti nei file di configurazione senza richiedere il riavvio del server per rendere effettive le modifiche. (Vedi di seguito per i dettagli sui valori di configurazione che vengono controllati per gli aggiornamenti.)

Per ricaricare la configurazione quando vengono apportate modifiche, il server licenze memorizza l&#39;ora dell&#39;ultima modifica del file. A un intervallo configurabile, il server controlla se il tempo di modifica del file è cambiato e, in tal caso, ricarica il contenuto del file.

Per controllare la frequenza con cui il server verifica la disponibilità di aggiornamenti, impostare `refreshDelaySeconds` nell&#39;elemento Caching del file di configurazione globale. Ad esempio, se `refreshDelaySeconds` è impostato su 3600 secondi, è necessaria al massimo un&#39;ora dal momento in cui il file viene aggiornato per rilevare eventuali aggiornamenti della configurazione da parte del server. Se `refreshDelaySeconds` è impostato su 0, il server controlla la disponibilità di aggiornamenti di configurazione per ogni richiesta. Impostazione `refreshDelaySeconds` Per gli ambienti di produzione non è consigliabile utilizzare la funzione a un valore ridotto, in quanto potrebbe influire sulle prestazioni.

L’elemento Caching controlla anche il numero di configurazioni dei tenant memorizzate nella cache contemporaneamente. Puoi impostare questo valore su un numero inferiore al numero totale di tenant per limitare la quantità di memoria utilizzata per memorizzare nella cache le informazioni di configurazione. Se viene ricevuta una richiesta per un tenant non presente nella cache, la configurazione viene caricata prima dell’elaborazione della richiesta. Se la cache è piena, il tenant utilizzato meno di recente viene rimosso dalla cache.

Se una modifica viene salvata in un file di configurazione o in uno dei file di certificato a cui si fa riferimento in [!DNL flashaccess-tenant.xml] durante il tentativo di lettura del file da parte del server o se il timestamp del file risulta meno di un secondo prima dell&#39;ora corrente o è nel futuro, la versione memorizzata nella cache della configurazione viene utilizzata fino alla successiva verifica degli aggiornamenti da parte del server. Se non è presente alcuna versione memorizzata in cache, il caricamento della configurazione non riesce e viene restituito un errore al client. Il server tenta di caricare di nuovo il file alla successiva richiesta per quel tenant.
