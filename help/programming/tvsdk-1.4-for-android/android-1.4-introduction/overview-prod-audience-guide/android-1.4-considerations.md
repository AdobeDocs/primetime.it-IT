---
description: Per utilizzare TVSDK nel modo più efficace, è necessario prendere in considerazione alcuni dettagli del suo funzionamento e seguire alcune best practice.
title: Considerazioni e best practice
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# Considerazioni e best practice{#considerations-and-best-practices}

Per utilizzare TVSDK nel modo più efficace, è necessario prendere in considerazione alcuni dettagli del suo funzionamento e seguire alcune best practice.

## Considerazioni {#section_tvsdk_considerations}

Quando utilizzi TVSDK, tieni presente le seguenti informazioni:

* Adobe Primetime al momento non funziona sugli emulatori Android.

   Devi utilizzare dispositivi reali per il test.
* La riproduzione è supportata solo per i contenuti HTTP Live Streaming (HLS).
* Il contenuto video principale può essere multiplexato, dove i flussi video e audio si trovano nella stessa rappresentazione, o non multiplexato, dove i flussi video e audio si trovano in rappresentazioni separate.
* L’API TVSDK è implementata in Java.
* Attualmente, è necessario eseguire la maggior parte delle operazioni API TVSDK sul thread dell&#39;interfaccia utente, che è il thread principale di Android.

   Le operazioni eseguite correttamente sul thread principale potrebbero generare un errore e uscire quando vengono eseguite su un thread in background.
* La riproduzione video richiede l’Adobe del motore video (AVE). Questo influisce su come e quando è possibile accedere alle risorse multimediali:

   * I sottotitoli codificati sono supportati nella misura fornita dall’AVE.
   * A seconda della precisione del codificatore, la durata effettiva del contenuto multimediale codificato potrebbe differire dalle durate registrate nel manifesto della risorsa di flusso.

      Non esiste un modo affidabile per eseguire nuovamente la sincronizzazione tra la timeline virtuale ideale e la timeline effettiva di riproduzione. Il tracciamento dell’avanzamento della riproduzione in streaming per la gestione degli annunci e Video Analytics deve utilizzare il tempo di riproduzione effettivo, pertanto il comportamento di reporting e interfaccia utente potrebbe non tenere traccia con precisione del contenuto multimediale e pubblicitario.
   * Al nome dell’agente utente in arrivo per tutte le richieste di contenuti multimediali da TVSDK su questa piattaforma viene assegnato il seguente pattern di stringa:

      ```
      "Adobe Primetime/ + 
      <varname>
      originalUserAgent
      </varname>" 
      ```

      Tutte le chiamate relative agli annunci utilizzano l&#39;agente utente predefinito Android o l&#39;agente utente personalizzato se lo si imposta durante la configurazione dei metadati di inserimento degli annunci.

## Best practice {#section_tvsdk_best_practices}

Di seguito sono riportate le pratiche consigliate per TVSDK:

* Utilizza HLS versione 3.0 o successiva per il contenuto del programma.
* Esegui la maggior parte delle operazioni TVSDK nel thread principale (interfaccia utente), non nei thread in background.
