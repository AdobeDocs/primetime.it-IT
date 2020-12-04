---
description: Oltre ai parametri di query di base, i parametri di query facoltativi consentono al server manifesto di lavorare con client e situazioni diverse.
seo-description: Oltre ai parametri di query di base, i parametri di query facoltativi consentono al server manifesto di lavorare con client e situazioni diverse.
seo-title: Parametri di query opzionali per client e situazione
title: Parametri di query opzionali per client e situazione
uuid: e3fae41e-9f7d-4f01-9a01-52a1d5f5dad5
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---


# Parametri di query opzionali per client e situazione {#optional-query-parameters-by-client-and-situation}

Oltre ai parametri di query di base, i parametri di query facoltativi consentono al server manifesto di lavorare con client e situazioni diverse.

## Inserimento annunci con Akamai Ad Scaler {#section_120FEC75C34D4F4587B77D842166D68A}

Nella rete di distribuzione dei contenuti di Akamai (CDN), il server Akamai Edge funziona come intermediario tra il client e il server manifesto. Se utilizzate anche Ad Scaler, i parametri di query `ptassetid` e `live` forniscono le informazioni necessarie ad Akamai Edge.

Il parametro `ptassetid` è l&#39;ID dell&#39;editore per la risorsa. Akamai utilizza questo URL, anziché l&#39;URL con codifica base64 fornito come parte dell&#39;URL della richiesta, per identificare la playlist da fornire al server manifesto per l&#39;inserimento di annunci.

Il parametro `live` distingue tra contenuti live e video on demand (VOD). Il server manifesto necessita di queste informazioni per supportare la sua interfaccia semplificata con Akamai.

Di seguito è riportato un URL di esempio che mostra i parametri relativi a Akamai:

```
https://. . .master.m3u8?. . .&ptassetid=pubAsset&live=true
```

## Inserimento di annunci da TVSDK su Xbox {#section_5DB405F4647240A0B83E72DE35D5EC80}

Un lettore basato su Primetime TVSDK su Xbox non deve fornire ulteriori parametri di query oltre a quelli di base.

## Inserimento di annunci da TVSDK su iOS con Safari {#section_250E493A125E4F82940D19C7DA2AAB2E}

Un lettore basato su Primetime TVSDK su iOS che utilizza il browser Safari deve specificare i parametri `ptplayer` e `live` oltre ai parametri di query di base.

Il server manifesto riconosce il valore `ptplayer` `ios-mobileweb` ed elimina il pre-roll dal manifesto ad-cucite che restituisce.

Il parametro `live` indica al server manifesto se restituire contenuto live o VOD.

Di seguito è riportato un URL di esempio che mostra i parametri relativi a iOS con Safari:

```
https://. . .master.m3u8?. . .&ptplayer=ios-mobileweb&live=false
```

## Inserimento di annunci utilizzando un formato personalizzato di cue point {#section_82AF880AAABE4BD4B593D906434D4D89}

 Adobe fornisce i nomi per i formati dei cue di annunci che non supporta direttamente nel pacchetto Primetime. Per utilizzare tale formato, fornire il nome  Adobe fornito come valore del parametro `ptcueformat`.

Di seguito è riportato un esempio di URL che specifica un formato personalizzato per il cue point:

```
https://. . .master.m3u8?. . .&ptcueformat=[custom format name]
```

## Inserimento di annunci tramite segnali pubblicitari per creare una timeline FreeWheel per VOD {#section_E0D830F5EEE24639819B975B90F6999F}

Per il contenuto VOD contenente suggerimenti per gli annunci da analizzare e includere in una richiesta di annunci FreeWheel, impostate il valore del parametro `ptcueformat` su `DPIsimple`.

Esempio di URL che specifica l’utilizzo di una timeline FreeWheel per il VOD:

```
https://. . .master.m3u8?. . .&ptcueformat=DPISimple&live=false
```

## Inserimento di annunci tramite una timeline personalizzata per VOD {#section_F398F7659164463FA886A4CC787C7B5A}

Per chiedere al server di manifesto di inserire annunci nel contenuto VOD in base alla timeline fornita, impostate il valore del parametro `pttimeline` su una stringa che specifica la timeline. Vedere [formato della timeline VOD](../../msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md)

Di seguito è riportato un URL di esempio che utilizza una timeline personalizzata per i VOD:

```
https://. . .master.m3u8?. . .&live=false&pttimeline=B,60,2,p;C,120,1;B,30,2,m;C,300,1
```

Specifica un&#39;interruzione iniziale di un minuto contenente fino a due annunci, seguita da un segmento di contenuto di due minuti, seguita da un&#39;interruzione di 30 secondi contenente fino a due annunci, seguita da un segmento di contenuto di cinque minuti.

L’aggiunta di punti di giunzione per una timeline di contenuto personalizzata per il contenuto VOD si comporta come segue:

* L&#39;annuncio viene visualizzato al limite di interruzione più vicino dopo il tempo di posizionamento dell&#39;annuncio specificato dal server dell&#39;annuncio.
* I segmenti sono lunghi almeno due secondi.

## Autorizzazione di segmenti TS {#section_BF855A4399DC42CB8C0586113A416BBC}

 Adobe supporta questa funzione solo per la rete CDN Akamai. Lo streaming live HTTP (HLS) distribuisce segmenti di flussi di trasporto (TS) utilizzando una playlist M3U8 a livello di flusso. Più playlist a livello di flusso vengono fornite al client in una playlist M3U8 variante. Il client seleziona un flusso di playlist dall&#39;elenco delle varianti, quindi scarica i segmenti TS in quella playlist a livello di flusso uno per uno. Nel normale funzionamento, il contenuto richiesto può richiedere l&#39;autorizzazione dei cookie, che il server manifesto gestisce in modo invisibile in background. Estrae il cookie dal contenuto non elaborato e aggiunge un token appropriato all&#39;URL da utilizzare per richiedere il flusso di playlist selezionato.

Quando i parametri di query URL Bootstrap includono `pttoken=true`, l&#39;editore richiede l&#39;utilizzo di un cookie per richiedere ogni segmento TS, anziché una sola volta per l&#39;intero flusso. Il server manifesto associa questo cookie come parametro di query a ogni URL del segmento TS nella playlist del flusso che invia.
