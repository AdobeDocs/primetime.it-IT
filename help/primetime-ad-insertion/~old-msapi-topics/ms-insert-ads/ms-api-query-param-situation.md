---
description: Oltre ai parametri di query di base, i parametri di query facoltativi consentono al server manifest di lavorare con client e situazioni diverse.
title: Parametri di query opzionali per client e situazione
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 0%

---


# Parametri di query opzionali per client e situazione {#optional-query-parameters-by-client-and-situation}

Oltre ai parametri di query di base, i parametri di query facoltativi consentono al server manifest di lavorare con client e situazioni diverse.

## Inserimento di annunci con Akamai Ad Scaler {#section_120FEC75C34D4F4587B77D842166D68A}

Sulla rete CDN (Content Delivery Network) di Akamai, il server Akamai Edge funziona come intermediario tra il client e il server manifest. Se utilizzi anche Ad Scaler, i parametri di query `ptassetid` e `live` forniscono informazioni necessarie ad Akamai Edge.

Il parametro `ptassetid` è l’ID dell’editore per la relativa risorsa. Akamai utilizza questo URL invece dell&#39;URL con codifica base64 fornito come parte dell&#39;URL della richiesta, per identificare la playlist da fornire al server manifesto per l&#39;inserimento di annunci.

Il parametro `live` distingue tra contenuto live e video on demand (VOD). Il server manifest ha bisogno di queste informazioni per supportare la sua interfaccia semplificata con Akamai.

Ecco un URL di esempio che mostra i parametri relativi ad Akamai:

```
https://. . .master.m3u8?. . .&ptassetid=pubAsset&live=true
```

## Inserimento di annunci da TVSDK su Xbox {#section_5DB405F4647240A0B83E72DE35D5EC80}

Un lettore basato su Primetime TVSDK su Xbox non deve fornire parametri di query aggiuntivi oltre a quelli di base.

## Inserimento di annunci da TVSDK su iOS con Safari {#section_250E493A125E4F82940D19C7DA2AAB2E}

Un lettore basato su Primetime TVSDK su iOS che utilizza il browser Safari deve specificare i parametri `ptplayer` e `live` oltre ai parametri di query di base.

Il server manifest riconosce il valore `ptplayer` `ios-mobileweb` ed elimina il pre-roll dal manifesto ad-stitched che restituisce.

Il parametro `live` indica al server manifesto se restituire contenuto live o VOD.

Ecco un esempio di URL che mostra i parametri relativi a iOS con Safari:

```URL
https://. . .master.m3u8?. . .&ptplayer=ios-mobileweb&live=false
```

## Inserimento di annunci utilizzando un formato di cue annuncio personalizzato {#section_82AF880AAABE4BD4B593D906434D4D89}

Adobe fornisce nomi per i formati di cue degli annunci che non supportano direttamente nel pacchetto Primetime. Per utilizzare tale formato, fornisci il nome fornito dall’Adobe come valore del parametro `ptcueformat` .

Ecco un esempio di URL che specifica un formato di cue annuncio personalizzato:

```URL
https://. . .master.m3u8?. . .&ptcueformat=[custom format name]
```

## Inserimento di annunci utilizzando suggerimenti per creare una timeline FreeWheel per VOD {#section_E0D830F5EEE24639819B975B90F6999F}

Per il contenuto VOD contenente suggerimenti per gli annunci da analizzare e includere in una richiesta di annunci FreeWheel, imposta il valore del parametro `ptcueformat` su `DPIsimple`.

Ecco un esempio di URL che specifica l&#39;utilizzo di una timeline FreeWheel per VOD:

```URL
https://. . .master.m3u8?. . .&ptcueformat=DPISimple&live=false
```

## Inserimento di annunci utilizzando una timeline personalizzata per VOD {#section_F398F7659164463FA886A4CC787C7B5A}

Per chiedere al server manifest di inserire annunci nel contenuto VOD in base alla timeline fornita, imposta il valore del parametro `pttimeline` su una stringa che specifica la timeline. Vedere [Formato della timeline VOD](/help/primetime-ad-insertion/~old-msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md).

Ecco un esempio di URL che utilizza una timeline personalizzata per VOD:

```URL
https://. . .master.m3u8?. . .&live=false&pttimeline=B,60,2,p;C,120,1;B,30,2,m;C,300,1
```

Specifica un’interruzione iniziale di un minuto contenente fino a due annunci, seguita da un segmento di contenuto di due minuti, seguita da un’interruzione di 30 secondi contenente fino a due annunci, seguita da un segmento di contenuto di cinque minuti.

L’unione degli annunci per una timeline di contenuti personalizzati per i contenuti VOD si comporta come segue:

* L’annuncio viene visualizzato al limite di interruzione più vicino dopo il tempo di posizionamento dell’annuncio specificato dal server di annunci.

* I segmenti sono lunghi almeno due secondi.

## Autorizzazione dei segmenti TS {#section_BF855A4399DC42CB8C0586113A416BBC}

Adobe supporta questa funzione solo per la rete CDN Akamai. Lo streaming live HTTP (HLS) fornisce segmenti di flussi di trasporto (TS) utilizzando una playlist a livello di flusso M3U8. Le playlist a livello di flusso multipli vengono fornite al client in una playlist variant M3U8. Il client seleziona un flusso di playlist dall&#39;elenco delle varianti, quindi scarica i segmenti TS in quella playlist a livello di flusso uno per uno. In condizioni normali, il contenuto richiesto può richiedere un&#39;autorizzazione dei cookie, che il server manifest gestisce in modo invisibile in background. Estrae il cookie dal contenuto non elaborato e aggiunge un token appropriato all’URL da utilizzare per richiedere il flusso di playlist selezionato.

Quando i parametri di query Bootstrap URL includono `pttoken=true`, l’editore richiede l’utilizzo di un cookie per richiedere ogni segmento TS, anziché una sola volta per l’intero flusso. Il server manifest allega questo cookie come parametro di query a ogni URL del segmento TS nella playlist del flusso che invia.
