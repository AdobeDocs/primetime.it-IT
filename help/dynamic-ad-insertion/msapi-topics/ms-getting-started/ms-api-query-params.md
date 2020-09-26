---
description: I parametri di query indicano al server di manifesto quale tipo di client ha inviato la richiesta e cosa desidera che esegua il server di manifesto. Alcuni sono obbligatori e alcuni hanno formati o valori accettabili specifici.
seo-description: I parametri di query indicano al server di manifesto quale tipo di client ha inviato la richiesta e cosa desidera che esegua il server di manifesto. Alcuni sono obbligatori e alcuni hanno formati o valori accettabili specifici.
seo-title: Parametri query server manifesto
title: Parametri query server manifesto
uuid: 03632da3-ae20-427c-bd24-4794ab627cc8
translation-type: tm+mt
source-git-commit: 6d25fc11bc4ca91556cae0b944322cd224c89fb5
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 0%

---


# Parametri query server manifesto {#manifest-server-query-parameters}

I parametri di query indicano al server di manifesto quale tipo di client ha inviato la richiesta e cosa desidera che esegua il server di manifesto. Alcuni sono obbligatori e alcuni hanno formati o valori accettabili specifici.

L’URL completo è costituito dall’URL di base seguito da un punto interrogativo, quindi `parameterName=value` da argomenti, separati da e-mail: `Base URL?name1=value1&name2=value2& . . .&name n=value n`.

## Parametri riconosciuti {#recognized-parameters}

Il server manifesto riconosce i seguenti parametri. Li elabora o li trasmette, insieme a tutti i parametri non riconosciuti, al server di annunci.

| Key | Descrizione | Obbligatorio | Valori validi |
|--- |--- |--- |--- |
| `__sid__` | ID univoco utilizzato dal server manifesto per generare l’ID sessione. | Yes | Alfanumerico |
| g | Tipo di dispositivo client | Quando le regole di targeting dipendono dal tipo di dispositivo | Vedi elenco in Tipi [](https://adobeprimetime.zendesk.com) client (richiede l&#39;accesso a Zendesk) |
| k | Parole chiave per il targeting di annunci personalizzato | No | Stringa sicura per l’URL in formato key1=value1;key2=value2;. . . |
| u | ID risorsa di inserimento Primetime. | Yes | Valore Hash MD5 |
| z | ID zona di inserimento Primetime per la risorsa. | Yes | Integer |
| enableC3 | Il client si trova in una finestra C3. Se true, sostituire solo le disponibilità locali; in caso contrario, sostituite tutte le risorse disponibili. | No | Booleano |
| live | Indica se il contenuto è un flusso Live o VOD (video su richiesta). | Akamai Ad Scaler o client iOS Safari | Booleano |
| pabimode | [Abilita il supporto per l&#39;inserimento](../../msapi-topics/ms-insert-ads/partial-ad-break-insetion.md) di interruzioni pubblicitarie parziali Abilita se true o avvia Disattiva se false | No (il valore predefinito è disabilitato) | start , true o false |
| ptadwindow | Durata (secondi) della finestra con punti di sutura: la distanza di ricerca degli annunci pubblicitari quando un utente DVR accede allo streaming. | No (predefinito = 1800) | da 0 a 1800 |
| ptassetid | ID univoco del contenuto assegnato e gestito dall&#39;editore. | Akamai Ad Scaler | Stringa URL-safe |
| ptcdn | Elenco di uno o più CDN per l’hosting di risorse transcodificate. Consultate Supporto per [più CDN](../../creative-repackaging-service/multi-cdn-supportt.md). | No (predefinito=Akamai) | Esempio: Akamai, Level3, Limelight, Comcast |
| ptcueformat | Il nome del formato personalizzato dell&#39;annuncio presente in M3U8. | No | DPISsimple, DPIScte35, Elemental,NBC, NFL o Turner |
| ptfailover | Segnala al server manifesto di identificare i flussi primari e di failover specificati nella playlist principale e di trattarli come set disgiunti. Questo semplifica il failover e impedisce gli errori di temporizzazione. (solo per i dispositivi Apple HLS). Vedere [Facilitazione della commutazione](../../msapi-topics/ms-insert-ads/hls-switching-to-failover.md) del lettore HLS. | No | true |
| ptmulticall | Se impostato su true , più chiamate ad Auditude per FER effettuate; uno per ogni annuncio.  Se assente o impostato su false, viene effettuata una chiamata ad auditude per FER. | No | Nota booleana:  I seguenti requisiti: <ul><li>il parametro ptcueformat deve essere impostato su nbc</li><li>il parametro pttimeline viene ignorato.</li></ul> |
| ptplayer | Lettore che effettua la richiesta. | iOS/Safari | ios-mobileweb |
| tendenza | Generato automaticamente dall&#39;inserimento di annunci e utilizzato da Akamai. Non aggiungere o rimuovere. | Akamai Ad Scaler |  |
| pttagds | Abilita tag [EXT-X-DISCONTINUITY-SEQUENCE](https://tools.ietf.org/html/draft-pantos-http-live-streaming-19#section-4.3.3.3) | No | true - il server manifesto include un tag di sequenza prima del contenuto in ciascun file m3u8 che invia; se il parametro non è presente o non è true, il server manifesto non include un tag di sequenza. |
| pitimeline | Una stringa contenente la timeline desiderata per la posizione e il contenuto degli annunci, che esclude e interrompe il flusso di contenuti. | No | Timeline VOD (vedere il formato [della timeline](../../msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md)VOD) |
| pattoken | Attiva token di autorizzazione del segmento TS Nota:  Sono supportati solo i token CDN Akamai | Per i token di autorizzazione del segmento TS | Booleano |
| pttrackingmode | Abilita tracciamento annunci; client-side personalizzato (semplice), server-side (sstm) o ibrido (semplificato). | No | semplice, sstm o semplice Nota:  Se questo parametro non è incluso, il #EX-X-MARKER viene inserito nel manifesto. Cfr. direttiva [EXT-X-MARKER](../../msapi-topics/ms-at-effectiveness/ms-api-playlists.md). |
| pttrackingposition | Indica al server manifesto di restituire solo le informazioni di tracciamento annunci. Non specificate questo parametro nella richiesta di avvio automatico. | Tracciamento lato client | Nota alfanumerica:  Il server manifesto ignora tutti i valori passati. Tuttavia, se si passa una stringa null o vuota, il server manifesto restituisce M3U8 invece delle informazioni di tracciamento. |
| pttrackingversion | Versione formato delle informazioni di tracciamento lato client. | Tracciamento lato client | v1 , v2 , v3 , o vmap |
| scteTracking | Recupera M3U8 , prima che le informazioni di tracciamento SCTE possano essere recuperate nel sidecar JSON V2.  <br/>Questo parametro indica al server manifesto che il lettore che recupera M3U8 deve recuperare le informazioni del tag SCTE. | No (predefinito:  false ) | true o false Note:  I dati SCTE-35 vengono restituiti nel sidecar JSON con la seguente combinazione di valori dei parametri di query: <ul><li>`ptcueformat=turner | elemental | nfl | DPIScte35` </li><li>pttrackingversion=v2 </li><li>scteTracking=true</li></ul> |
| vetargetmoltiplicatore | Il numero di segmenti dal punto vivo L&#39;offset pre-roll è configurato utilizzando:   `(  vetargetmultiplier  *  targetduration ) +  vebufferlength`  <br/><br/>**Nota**:  Solo Live/Linear | No (predefinito:  3.0 ) | Mobile |
| vebufferLength | Il numero di secondi dalla nota del punto attivo:  Solo Live/Linear | No (predefinito:  3.0 ) | Mobile |
| ptadtimeout | Per limitare il tempo complessivo di risoluzione degli annunci, se i fornitori richiedono troppo tempo per rispondere. | Sì, per abilitare | valore in millisecondi |
| ptparallelstream | Consente ai clienti con lettori che richiedono flussi audio o video demussati CMAF in parallelo per garantire la coerenza degli annunci nelle tracce audio e video. | Sì, per abilitare la funzione o omettere di disattivarla. | true |
