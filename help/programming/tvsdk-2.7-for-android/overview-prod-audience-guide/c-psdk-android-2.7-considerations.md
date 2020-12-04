---
description: Per utilizzare TVSDK nel modo più efficace, è necessario prendere in considerazione alcuni dettagli del suo funzionamento e seguire alcune best practice.
seo-description: Per utilizzare TVSDK nel modo più efficace, è necessario prendere in considerazione alcuni dettagli del suo funzionamento e seguire alcune best practice.
seo-title: Considerazioni e procedure ottimali
title: Considerazioni e procedure ottimali
uuid: 049da1f4-028b-49d2-9ebd-e5d9edcbaf8a
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# Considerazioni e best practice{#considerations-and-best-practices}

Per utilizzare TVSDK nel modo più efficace, è necessario prendere in considerazione alcuni dettagli del suo funzionamento e seguire alcune best practice.

## Considerazioni {#section_tvsdk_considerations}

Ricorda le seguenti informazioni quando utilizzi TVSDK:

* L’API TVSDK è implementata in Java.
*  Adobe Primetime attualmente non funziona sugli emulatori Android.

   Per eseguire il test dovete utilizzare dei dispositivi reali.
* La riproduzione è supportata solo per il contenuto HTTP Live Streaming (HLS).
* Il contenuto video principale può essere multiplexato (flussi video e audio nella stessa rappresentazione) o non multiplexato (flussi video e audio in rappresentazioni separate).
* Attualmente, è necessario eseguire la maggior parte delle operazioni API TVSDK sul thread dell&#39;interfaccia utente, che è il thread Android principale.

   Le operazioni eseguite correttamente sul thread principale possono generare un errore e uscire quando vengono eseguite su un thread in background.
* La riproduzione video richiede il motore video  Adobe (AVE). Questo incide su come e quando è possibile accedere alle risorse multimediali:

   * I sottotitoli codificati sono supportati nella misura fornita dall’AVE.
   * A seconda della precisione del codificatore, la durata effettiva del supporto codificato potrebbe essere diversa dalle durate registrate nel manifesto della risorsa di flusso.

      Non esiste un modo affidabile per risincronizzare tra la timeline virtuale ideale e la timeline di riproduzione effettiva. Il tracciamento dell’avanzamento della riproduzione del flusso per la gestione degli annunci e per l’analisi video deve utilizzare il tempo di riproduzione effettivo, pertanto il comportamento dei rapporti e dell’interfaccia utente potrebbe non tenere traccia con precisione dei contenuti multimediali e pubblicitari.
   * Al nome dell’agente utente in arrivo per tutte le richieste multimediali da TVSDK su questa piattaforma viene assegnato il seguente pattern di stringa:

   ```
   "Adobe Primetime/" + 
   <varname>
   originalUserAgent
   </varname> 
   ```

   Tutte le chiamate relative agli annunci utilizzano l’agente utente predefinito Android o l’agente utente personalizzato se lo impostate durante la configurazione dei metadati di inserimento degli annunci.

## Best practice {#section_tvsdk_best_practices}

Seguono alcune pratiche consigliate per TVSDK:

* Utilizzate HLS versione 3.0 o successiva per il contenuto del programma.
* Eseguite la maggior parte delle operazioni TVSDK sul thread principale (interfaccia utente), non sui thread in background.
* Per TVSDK 2.5 per Android, la risoluzione degli annunci pigri è attivata per impostazione predefinita.

   Per i contenuti senza pre-roll o mid-roll, potete utilizzare `AdvertisingMetadata.setPreroll(false)` per accelerare il caricamento del contenuto.
