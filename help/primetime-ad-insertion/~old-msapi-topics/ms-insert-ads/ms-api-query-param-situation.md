---
description: Oltre ai parametri di query di base, i parametri di query facoltativi consentono al server manifesto di funzionare con client e situazioni diversi.
title: Parametri di query facoltativi per client e situazione
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 0%

---


# Parametri di query facoltativi per client e situazione {#optional-query-parameters-by-client-and-situation}

Oltre ai parametri di query di base, i parametri di query facoltativi consentono al server manifesto di funzionare con client e situazioni diversi.

## Inserimento di annunci con Akamai Ad Scaler {#section_120FEC75C34D4F4587B77D842166D68A}

Nella rete CDN (Content Delivery Network) di Akamai, il server Akamai Edge funziona come intermediario tra il client e il server manifest. Se utilizzi anche Ad Scaler, il `ptassetid` e `live` I parametri di query forniscono le informazioni richieste ad Akamai Edge.

Il `ptassetid` Il parametro è l&#39;ID dell&#39;editore della relativa risorsa. Akamai utilizza questo URL, anziché l’URL con codifica base64 fornito come parte dell’URL della richiesta, per identificare la playlist da fornire al server del manifesto per l’inserimento degli annunci.

Il `live` Il parametro distingue tra contenuto live e video on-demand (VOD). Il server manifesto necessita di queste informazioni per supportare la sua interfaccia semplificata con Akamai.

Di seguito è riportato un URL di esempio che mostra i parametri relativi ad Akamai:

```
https://. . .master.m3u8?. . .&ptassetid=pubAsset&live=true
```

## Inserimento di annunci da TVSDK su Xbox {#section_5DB405F4647240A0B83E72DE35D5EC80}

Un lettore basato su Primetime TVSDK su Xbox non deve fornire parametri di query aggiuntivi oltre a quelli di base.

## Inserimento di annunci da TVSDK su iOS con Safari {#section_250E493A125E4F82940D19C7DA2AAB2E}

Un lettore basato su Primetime TVSDK su iOS che utilizza il browser Safari deve specificare `ptplayer` e `live` oltre ai parametri di query di base.

Il server manifest riconosce `ptplayer` valore `ios-mobileweb` ed elimina il pre-roll dal manifesto dell’unione di annunci che restituisce.

Il `live` Il parametro indica al server manifesto se restituire contenuto live o VOD.

Di seguito è riportato un URL di esempio che mostra i parametri relativi ad iOS con Safari:

```URL
https://. . .master.m3u8?. . .&ptplayer=ios-mobileweb&live=false
```

## Inserimento di annunci utilizzando un formato di annuncio cue personalizzato {#section_82AF880AAABE4BD4B593D906434D4D89}

In questo Adobe vengono forniti nomi per i formati di cue degli annunci non supportati direttamente nel pacchetto Primetime. Per utilizzare tale formato, fornisci il nome fornito dall’Adobe come valore del `ptcueformat` parametro.

Di seguito è riportato un URL di esempio che specifica un formato di annuncio cue personalizzato:

```URL
https://. . .master.m3u8?. . .&ptcueformat=[custom format name]
```

## Inserimento di annunci tramite suggerimenti di annunci per creare una timeline FreeWheel per VOD {#section_E0D830F5EEE24639819B975B90F6999F}

Per analizzare e includere in una richiesta di annunci FreeWheel il contenuto VOD contenente suggerimenti di annunci, imposta il valore di `ptcueformat` parametro a `DPIsimple`.

Di seguito è riportato un URL di esempio che specifica l’utilizzo di una timeline FreeWheel per VOD:

```URL
https://. . .master.m3u8?. . .&ptcueformat=DPISimple&live=false
```

## Inserimento di annunci utilizzando una timeline personalizzata per VOD {#section_F398F7659164463FA886A4CC787C7B5A}

Per richiedere al server manifest di inserire annunci nel contenuto VOD in base alla timeline fornita, imposta il valore della proprietà `pttimeline` parametro a una stringa che specifica la timeline. Consulta [Formato timeline VOD](/help/primetime-ad-insertion/~old-msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md).

Di seguito è riportato un URL di esempio che utilizza una timeline personalizzata per VOD:

```URL
https://. . .master.m3u8?. . .&live=false&pttimeline=B,60,2,p;C,120,1;B,30,2,m;C,300,1
```

Specifica un’interruzione iniziale di un minuto contenente fino a due annunci, seguita da un segmento di contenuto di due minuti, seguita da un’interruzione di 30 secondi contenente fino a due annunci, seguita da un segmento di contenuto di cinque minuti.

L’unione degli annunci per una timeline di contenuto personalizzato per il contenuto VOD si comporta come segue:

* L’annuncio viene visualizzato al limite di interruzione più vicino dopo il tempo di posizionamento specificato dal server dell’annuncio.

* I segmenti durano almeno due secondi.

## Autorizzazione dei segmenti TS {#section_BF855A4399DC42CB8C0586113A416BBC}

Adobe supporta questa funzione solo per la rete CDN Akamai. HTTP Live Streaming (HLS) distribuisce i segmenti TS (Transport Streaming) utilizzando una playlist M3U8 a livello di flusso. Al client vengono fornite più playlist a livello di flusso in una variante della playlist M3U8. Il client seleziona un flusso di playlist dall’elenco delle varianti, quindi scarica i segmenti TS in tale playlist a livello di flusso uno per uno. In condizioni normali, il contenuto richiesto può richiedere l&#39;autorizzazione dei cookie, che il server del manifesto gestisce in modo invisibile in background. Estrae il cookie dal contenuto non elaborato e aggiunge un token appropriato all’URL da utilizzare nella richiesta del flusso di playlist selezionato.

Quando i parametri di query dell’URL di Bootstrap includono `pttoken=true`, l’editore richiede l’utilizzo di un cookie per richiedere ogni segmento TS, anziché una sola volta per l’intero flusso. Il server di manifesto allega questo cookie come parametro di query a ciascun URL del segmento TS nella playlist di flusso che invia.
