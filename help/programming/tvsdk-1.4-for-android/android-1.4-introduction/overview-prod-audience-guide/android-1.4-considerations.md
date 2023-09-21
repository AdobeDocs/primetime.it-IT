---
description: Per utilizzare TVSDK nel modo più efficace, è necessario considerare alcuni dettagli del suo funzionamento e seguire alcune best practice.
title: Considerazioni e best practice
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# Considerazioni e best practice{#considerations-and-best-practices}

Per utilizzare TVSDK nel modo più efficace, è necessario considerare alcuni dettagli del suo funzionamento e seguire alcune best practice.

## Considerazioni {#section_tvsdk_considerations}

Quando si utilizza TVSDK, tenere presenti le seguenti informazioni:

* Adobe Primetime al momento non funziona sugli emulatori Android.

  Per il test è necessario utilizzare dispositivi reali.
* La riproduzione è supportata solo per contenuti HTTP Live Streaming (HLS).
* Il contenuto video principale può essere multiplexato, dove i flussi video e audio si trovano nella stessa rappresentazione, o non multiplexato, dove i flussi video e audio si trovano in rappresentazioni separate.
* L’API TVSDK è implementata in Java.
* Attualmente, devi eseguire la maggior parte delle operazioni API TVSDK sul thread dell’interfaccia utente, che è il thread Android principale.

  Le operazioni eseguite correttamente sul thread principale potrebbero generare un errore e uscire se eseguite su un thread in background.
* La riproduzione video richiede l&#39;Adobe del motore video (AVE). Questo influisce su come e quando è possibile accedere alle risorse multimediali:

   * I sottotitoli codificati sono supportati nella misura fornita da AVE.
   * A seconda della precisione del codificatore, la durata effettiva dei file multimediali codificati potrebbe essere diversa dalle durate registrate nel manifesto della risorsa del flusso.

     Non esiste un modo affidabile per sincronizzare nuovamente la timeline virtuale ideale con la timeline effettiva del playout. Il tracciamento dell’avanzamento della riproduzione del flusso per la gestione degli annunci e Video Analytics deve utilizzare il tempo di riproduzione effettivo, pertanto la generazione di rapporti e il comportamento dell’interfaccia utente potrebbero non tenere traccia con precisione del contenuto multimediale e pubblicitario.
   * Al nome dell’agente utente in ingresso per tutte le richieste multimediali provenienti da TVSDK su questa piattaforma viene assegnato il seguente pattern di stringa:

     ```
     "Adobe Primetime/ + 
     <varname>
     originalUserAgent
     </varname>" 
     ```

     Tutte le chiamate relative agli annunci utilizzano l’agente utente predefinito Android o l’agente utente personalizzato, se impostato durante la configurazione dei metadati di inserimento di annunci.

## Best practice {#section_tvsdk_best_practices}

Di seguito sono riportate le procedure consigliate per TVSDK:

* Utilizza la versione 3.0 o successiva di HLS per i contenuti del programma.
* Esegui la maggior parte delle operazioni TVSDK nel thread principale (UI), non nei thread in background.
