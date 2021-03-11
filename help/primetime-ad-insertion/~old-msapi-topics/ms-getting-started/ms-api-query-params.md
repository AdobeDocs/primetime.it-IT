---
title: Parametri query server manifesto
description: I parametri di query dicono al server manifesto che tipo di client ha inviato la richiesta e cosa desidera che faccia il server manifest. Alcuni sono necessari e altri hanno formati o valori accettabili specifici.
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---


# Parametri query server manifesto {#ms-query-params}

I parametri di query dicono al server manifesto che tipo di client ha inviato la richiesta e cosa desidera che faccia il server manifest. Alcuni sono necessari e altri hanno formati o valori accettabili specifici.

L’URL completo è costituito dall’URL di base seguito da un punto interrogativo e quindi da argomenti `parameterName=value` separati da e commerciale: `Base URL?name1=value1&name2=value2& . . .&name n=value n`.

## Parametri riconosciuti {#section_072845B7FA94468C8068E9092983C9E6}

Il server manifest riconosce i seguenti parametri. Li elabora o li trasmette, insieme a tutti i parametri non riconosciuti, al server di annunci.

| Chiave | Descrizione | Obbligatorio | Valori validi |
|---|---|---|---|
| `__sid__` | ID univoco utilizzato dal server manifesto per generare l&#39;ID sessione. | Sì | Alfanumerico |
| g | Tipo di dispositivo client | Quando le regole di targeting dipendono dal tipo di dispositivo | Vedi l&#39;elenco in [Tipi di client](https://adobeprimetime.zendesk.com). Richiede l&#39;accesso a Zendesk. |
| k | Parole chiave per il targeting di annunci personalizzati | No | Stringa sicura per URL in formato `key1=value1;key2=value2;. . .` |
| u | ID risorsa di inserimento annunci Primetime. | Sì | Valore hash MD5 |
| z | ID dell’area di inserimento Primetime per la risorsa. | Sì | Intero |
| enableC3 | Il client si trova in una finestra C3. Se true, sostituire solo le risorse locali; in caso contrario, sostituisci tutte le risorse disponibili. | No | Booleano |
| live | Indica se il contenuto è un flusso Live o VOD (video on-demand). | Akamai Ad Scaler o client iOS Safari. | Booleano |
| `pabimode` | [Abilita il supporto per ](/help/primetime-ad-insertion/~old-msapi-topics/ms-insert-ads/partial-ad-break-insetion.md) l’inserimento di interruzioni di annunci parziali. <br> Attiva se true o inizia.<br> Disabilita se false. | No (il valore predefinito è disabilitato) | start, true o false |
| `ptadwindow` | Durata (secondi) della finestra di unione annunci: quanto tempo fa per cercare gli annunci quando un utente DVR entra nel flusso. | No (predefinito = 1800) | da 0 a 1800 |
| `ptassetid` | ID univoco del contenuto assegnato e gestito dall&#39;editore. | Scalatore annunci Akamai | Stringa sicura URL |
| `ptcdn` | Elenco di una o più CDN per ospitare risorse transcodificate. Consulta [Supporto per più CDN](/help/primetime-ad-insertion/~old-creative-repackaging-service/multi-cdn-supportt.md). | No (predefinito=Akamai) | Esempio: Akamai, Livello3, Limelight, Comcast |
| `ptcueformat` | Nome del formato personalizzato dell&#39;annuncio presente nell&#39;M3U8. | No | DPISsimple, DPIScte35, Elemental, NBC, NFL o Turner |
| `ptfailover` | Segnala al server manifesto di identificare i flussi primari e di failover specificati nella playlist principale e di trattarli come set disgiunti. Questo facilita il failover ed evita gli errori di temporizzazione. (Solo per dispositivi Apple HLS). Consultare [Facilitazione della commutazione del lettore HLS](/help/primetime-ad-insertion/~old-msapi-topics/ms-insert-ads/hls-switching-to-failover.md). | No | true |
| `ptmulticall` | Se impostato su true, vengono effettuate più chiamate ad Auditude per FER; uno per ogni ad-break. Se assente o impostato su false, viene effettuata una chiamata ad auditude per FER. | No | Booleano <br> **Nota**: I seguenti requisiti: <ul><li>`ptcueformat` deve essere impostato su nbc</li><li>il parametro della linea temporale viene ignorato.</li></ul> |
| `ptplayer` | Lettore che effettua la richiesta. | iOS/Safari | ios-mobileweb |
| `ptrendition` | Generazione automatica tramite inserimento di annunci e utilizzata da Akamai. Non aggiungere o rimuovere. | Scalatore annunci Akamai |  |
| `pttagds` | Abilita i tag [EXT-X-DISCONTINUITY- SEQUENCE](https://tools.ietf.org/html/draft-pantos-http-live-streaming-19#section-4.3.3.3) | No | true - il server manifest include un tag di sequenza prima del contenuto in ogni file m3u8 che invia; se il parametro non è presente o non è true, il server manifest non include un tag di sequenza. |
| `pttimeline` | Una stringa contenente la timeline desiderata per il posizionamento e il contenuto degli annunci, che esclude e interrompe il flusso di contenuto. | No | [Timeline VOD](/help/primetime-ad-insertion/~old-msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md) |
| `pttoken` | Attiva i token di autorizzazione dei segmenti TS.<br> **Nota**: Sono supportati solo i token CDN di Akamai | Per i token di autorizzazione del segmento TS | Booleano |
| `pttrackingmode` | Abilitare il tracciamento degli annunci; personalizzato lato client (semplice), lato server (sstm) o ibrido (simplesstm). | No | semplice, sstm o simplesstm.<br> **Nota**: Se questo parametro non è incluso, il #EX-X-MARKER viene inserito nel manifesto. Vedere [Direttiva EXT-X-MARKER](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/ms-api-playlists.md). |
| `pttrackingposition` | Indica al server manifest di restituire solo le informazioni di tracciamento degli annunci. Non specificare questo parametro nella richiesta di avvio. | Tracciamento lato client | Nota alfanumerica:  Il server manifesto ignora tutti i valori passati. Tuttavia, se si passa una stringa null o vuota, il server manifesto restituisce M3U8 invece di tenere traccia delle informazioni. |
| `pttrackingversion` | Versione in formato delle informazioni di tracciamento lato client. | Tracciamento lato client | v1, v2, v3 o vmap |
| `scteTracking` | Recupera M3U8 , prima che le informazioni di tracciamento SCTE possano essere recuperate nel sidecar JSON V2 . <br>Questo parametro indica al server manifesto che il lettore che recupera l&#39;M3U8 deve recuperare le informazioni sul tag SCTE. | No (predefinito: false) | true o false. <br> **Nota**: I dati SCTE-35 vengono restituiti nel sidecar JSON con la seguente combinazione di valori dei parametri di query: <ul><li>`ptcueformat=turner | elemental | nfl | DPIScte35`</li><li>`pttrackingversion=v2`</li><li>`scteTracking=true`</li></ul> |
| `vetargetmultiplier` | Numero di segmenti dal punto attivo L&#39;offset di pre-roll è configurato utilizzando: `(vetargetmultiplier * targetduration + vebufferlength`<br/><br/>**Nota**:  Solo Live/Lineare | No (predefinito:  3,0) | Mobile |
| `vebufferLength` | Il numero di secondi dal punto attivo. **Nota**: Solo Live/Lineare. | No (predefinito: 3,0) | Mobile |
