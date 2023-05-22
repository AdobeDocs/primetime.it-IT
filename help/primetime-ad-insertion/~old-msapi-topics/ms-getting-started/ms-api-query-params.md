---
title: Parametri query server manifesto
description: I parametri di query indicano al server manifesto il tipo di client che ha inviato la richiesta e cosa il client desidera che il server manifesto esegua. Alcuni sono obbligatori e altri hanno specifici formati o valori accettabili.
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---


# Parametri query server manifesto {#ms-query-params}

I parametri di query indicano al server manifesto il tipo di client che ha inviato la richiesta e cosa il client desidera che il server manifesto esegua. Alcuni sono obbligatori e altri hanno specifici formati o valori accettabili.

L’URL completo è costituito dall’URL di base seguito da un punto interrogativo, quindi `parameterName=value` argomenti, separati da e commerciali: `Base URL?name1=value1&name2=value2& . . .&name n=value n`.

## Parametri riconosciuti {#section_072845B7FA94468C8068E9092983C9E6}

Il server manifest riconosce i seguenti parametri. Le elabora o le trasmette, insieme a tutti i parametri non riconosciuti, al server di annunci.

| Chiave | Descrizione | Obbligatorio | Valori validi |
|---|---|---|---|
| `__sid__` | ID univoco utilizzato dal server manifest per generare l’ID sessione. | Sì | Alfanumerico |
| g | Tipo di dispositivo client | Quando le regole di targeting dipendono dal tipo di dispositivo | Vedi elenco in [Tipi di client](https://adobeprimetime.zendesk.com). Richiede l&#39;accesso a Zendesk. |
| k | Parole chiave per il targeting di annunci personalizzati | No | Stringa URL-safe in formato `key1=value1;key2=value2;. . .` |
| u | ID risorsa per inserimento e Primetime. | Sì | Valore hash MD5 |
| z | ID della zona di inserimento e di Primetime per la risorsa. | Sì | Intero |
| enableC3 | Il client si trova in una finestra C3. Se true, sostituire solo le disponibilità locali; in caso contrario, sostituire tutte le disponibilità. | No | Booleano |
| live | Indica se il contenuto è un flusso Live o VOD (video on-demand). | Client Akamai Ad Scaler o iOS Safari. | Booleano |
| `pabimode` | [Abilita inserimento interruzione pubblicitaria parziale](/help/primetime-ad-insertion/~old-msapi-topics/ms-insert-ads/partial-ad-break-insetion.md) supporto. <br> Attiva se true o start.<br> Disattiva se false. | No (l&#39;impostazione predefinita è disabilitata) | start, true o false |
| `ptadwindow` | Durata (secondi) della finestra di unione degli annunci: quanto indietro nel tempo per cercare annunci quando un utente DVR si unisce allo streaming. | No (impostazione predefinita = 1800) | da 0 a 1800 |
| `ptassetid` | ID univoco del contenuto assegnato e gestito dall’editore. | Akamai Ad Scaler | Stringa URL-safe |
| `ptcdn` | Elenco di una o più CDN per l’hosting delle risorse transcodificate. Consulta [Supporto di più reti CDN](/help/primetime-ad-insertion/~old-creative-repackaging-service/multi-cdn-supportt.md). | No (predefinito=Akamai) | Esempio: Akamai, Level3, Limelight, Comcast |
| `ptcueformat` | Il nome del formato personalizzato di Ad Cue presente in M3U8. | No | DPISimple, DPIScte35, Elemental, NBC, NFL o Turner |
| `ptfailover` | Segnala al server manifesto di identificare i flussi primari e di failover specificati nella playlist principale e di trattarli come set disgiunti. Ciò semplifica il failover e impedisce errori di temporizzazione. (Solo per dispositivi Apple HLS). Consulta  [Facilitazione della commutazione del lettore HLS](/help/primetime-ad-insertion/~old-msapi-topics/ms-insert-ads/hls-switching-to-failover.md). | No | true |
| `ptmulticall` | Se è impostato su true, vengono effettuate più chiamate di annunci Auditude per FER; una per ogni interruzione pubblicitaria. Se assente o impostato su false, viene effettuata una chiamata pubblicitaria all’audience per FER. | No | Booleano <br> **Nota**: i seguenti requisiti: <ul><li>`ptcueformat` il parametro deve essere impostato su nbc</li><li>Il parametro pttimeline viene ignorato.</li></ul> |
| `ptplayer` | Lettore che effettua la richiesta. | iOS/Safari | ios-mobileweb |
| `ptrendition` | Generato automaticamente dall’inserimento di annunci e utilizzato da Akamai. Non aggiungere o rimuovere. | Akamai Ad Scaler |  |
| `pttagds` | Abilita [EXT-X- DISCONTINUITY- SEQUENZA](https://tools.ietf.org/html/draft-pantos-http-live-streaming-19#section-4.3.3.3) tag | No | true: il server manifest include un tag di sequenza prima del contenuto in ogni file m3u8 inviato; se il parametro non è presente o non è true, il server manifest non include un tag di sequenza. |
| `pttimeline` | Stringa contenente la timeline desiderata per il posizionamento e il contenuto degli annunci, che si sovrappone e si interrompe nel flusso di contenuto. | No | [Timeline VOD](/help/primetime-ad-insertion/~old-msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md) |
| `pttoken` | Abilitare i token di autorizzazione dei segmenti di Servizi terminal.<br> **Nota**: supportati solo token CDN Akamai | Per i token di autorizzazione dei segmenti TS | Booleano |
| `pttrackingmode` | Abilita il tracciamento degli annunci; personalizzato lato client (semplice), lato server (sstm) o ibrido (simplesstm). | No | simple, sstm o simplesstm.<br> **Nota**: se questo parametro non è incluso, il #EX-X-MARKER viene inserito nel manifesto. Consulta [Direttiva EXT-X-MARKER](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/ms-api-playlists.md). |
| `pttrackingposition` | Indica al server manifesto di restituire solo le informazioni di tracciamento degli annunci. Non specificare questo parametro nella richiesta bootstrap. | Tracciamento lato client | Nota alfanumerica: il server manifest ignora tutti i valori passati. Tuttavia, se si passa una stringa nulla o vuota, il server manifesto restituisce M3U8 invece delle informazioni di tracciamento. |
| `pttrackingversion` | Versione in formato delle informazioni di tracciamento lato client. | Tracciamento lato client | v1, v2, v3 o vmap |
| `scteTracking` | Recupera M3U8, prima che le informazioni di tracciamento SCTE possano essere recuperate in JSON V2 sidecar. <br>Questo parametro indica al server manifest che il lettore che recupera il file M3U8 deve recuperare le informazioni del tag SCTE. | No (impostazione predefinita: false) | true o false. <br> **Nota**: i dati SCTE-35 vengono restituiti nella barra laterale JSON con la seguente combinazione di valori dei parametri di query: <ul><li>`ptcueformat=turner | elemental | nfl | DPIScte35`</li><li>`pttrackingversion=v2`</li><li>`scteTracking=true`</li></ul> |
| `vetargetmultiplier` | Il numero di segmenti dal punto di attivazione L’offset pre-roll è configurato utilizzando: `(vetargetmultiplier * targetduration + vebufferlength`<br/><br/>**Nota**: solo Live/Linear | No (impostazione predefinita: 3.0) | Mobile |
| `vebufferLength` | Il numero di secondi dal punto di attivazione. **Nota**: solo Live/Linear. | No (impostazione predefinita: 3.0) | Mobile |
