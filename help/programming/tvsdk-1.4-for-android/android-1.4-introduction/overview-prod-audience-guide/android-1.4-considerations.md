---
description: Per utilizzare TVSDK nel modo più efficace, è necessario prendere in considerazione alcuni dettagli del suo funzionamento e seguire alcune best practice.
seo-description: Per utilizzare TVSDK nel modo più efficace, è necessario prendere in considerazione alcuni dettagli del suo funzionamento e seguire alcune best practice.
seo-title: Considerazioni e procedure ottimali
title: Considerazioni e procedure ottimali
uuid: e698ae09-280b-4406-a9b8-4f468b7a6b9c
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---


# Considerazioni e best practice{#considerations-and-best-practices}

Per utilizzare TVSDK nel modo più efficace, è necessario prendere in considerazione alcuni dettagli del suo funzionamento e seguire alcune best practice.

## Considerazioni {#section_tvsdk_considerations}

Ricorda le seguenti informazioni quando utilizzi TVSDK:

*  Adobe Primetime attualmente non funziona sugli emulatori Android.

   Per eseguire il test dovete utilizzare dei dispositivi reali.
* La riproduzione è supportata solo per il contenuto HTTP Live Streaming (HLS).
* Il contenuto video principale può essere multiplexato, dove i flussi video e audio si trovano nella stessa rappresentazione, o non multiplexato, dove i flussi video e audio si trovano in rappresentazioni separate.
* L’API TVSDK è implementata in Java.
* Attualmente, è necessario eseguire la maggior parte delle operazioni API TVSDK sul thread dell&#39;interfaccia utente, che è il thread Android principale.

   Le operazioni eseguite correttamente sul thread principale potrebbero generare un errore e uscire quando eseguite su un thread in background.
* La riproduzione video richiede il motore video  Adobe (AVE). Questo incide su come e quando è possibile accedere alle risorse multimediali:

   * I sottotitoli codificati sono supportati nella misura fornita dall’AVE.
   * A seconda della precisione del codificatore, la durata effettiva del supporto codificato potrebbe essere diversa dalle durate registrate nel manifesto della risorsa di flusso.

      Non esiste un modo affidabile per eseguire nuovamente la sincronizzazione tra la timeline virtuale ideale e la timeline di riproduzione effettiva. Il tracciamento dell’avanzamento della riproduzione del flusso per la gestione degli annunci e per l’analisi video deve utilizzare il tempo di riproduzione effettivo, pertanto il comportamento dei rapporti e dell’interfaccia utente potrebbe non tenere traccia con precisione dei contenuti multimediali e pubblicitari.
   * Al nome dell’agente utente in arrivo per tutte le richieste multimediali da TVSDK su questa piattaforma viene assegnato il seguente pattern di stringa:

      ```
      "Adobe Primetime/ + 
      <varname>
      originalUserAgent
      </varname>" 
      ```

      Tutte le chiamate relative agli annunci utilizzano l’agente utente predefinito Android o l’agente utente personalizzato se lo impostate durante la configurazione dei metadati di inserimento degli annunci.

## Best practice {#section_tvsdk_best_practices}

Seguono alcune pratiche consigliate per TVSDK:

* Utilizzate HLS versione 3.0 o successiva per il contenuto del programma.
* Eseguite la maggior parte delle operazioni TVSDK nel thread principale (interfaccia utente), non sui thread in background.
