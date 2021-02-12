---
title: Bootstrap API
description: 'Bootstrap API '
translation-type: tm+mt
source-git-commit: bf99c76bbbb67560adc675cf84297b8d3b04e19d
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 0%

---


# Bootstrap API {#bootstrap-api}

L&#39;API Bootstrap è in genere l&#39;URL inviato alle API di riproduzione client/video.  Per le opzioni e i parametri che possono essere configurati, fare riferimento a [Bootstrap parametri API](#bootstrap-api-parameters).

## Inviare un comando al server manifesto {#send-a-command-to-the-manifest-server}

1. Inviate una richiesta `HTTP GET` per un URL del programma di avvio automatico creato con il seguente pattern:

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.[m3u8 or mpd]
    ?{query parameters}
   ```

   * **File** extensionDefined. `.m3u8` se il manifesto di destinazione è HLS,  `.mpd` se i manifesti di destinazione sono nel DASH.

   * **** PublisherAssetIDRequred. ID univoco dell&#39;editore per il contenuto specifico.

   * **Content** URLRequred. URL del contenuto del file M3U8, con codifica Base64 per garantire la sicurezza all&#39;interno dell&#39;URL del server manifesto. L&#39;URL del contenuto deve puntare a una variante del file M3U8, anche se è presente un solo flusso di bit rate.

   * **Parametri** di query: costituiscono la parte più varia della richiesta. Indica al server di manifesto quale tipo di client sta effettuando la richiesta e cosa desidera che esegua il server di manifesto.

   Ad esempio:

   ```
   https://manifest.auditude.com/auditude/variant/
    {publisherAssetID}/{Content URL (base64)}.[m3u8 or mpd]?
   u={Asset ID}&z={zone}&_sid_=0&pttrackingmode=simple
   &pttrackingversion=v2&live=false
   ```

   **Richieste HTTP e HTTPS**

   Il server manifesto crea URL utilizzando lo stesso protocollo HTTP della richiesta del client. Se un lettore effettua una richiesta HTTP non sicura (http), il server manifesto restituisce gli URL manifest e gli URL di tracciamento Auditude con il protocollo http. Se un lettore crea una connessione HTTP (https) protetta, un server manifesto, restituisce gli URL manifest e gli URL di tracciamento Auditude con il protocollo https.

   >[!NOTE]
   >
   >Il server manifesto non può modificare il protocollo (HTTP o HTTPS) dei beacon di tracciamento di terze parti. È necessario contattare il contenuto e i fornitori di annunci di terze parti per fare in modo che configurino i protocolli desiderati.  I protocolli URL dei segmenti possono essere modificati, tuttavia, per impostazione predefinita, utilizzano gli stessi protocolli definiti nei manifesti di destinazione.

## Bootstrap parametri API {#bootstrap-api-parameters}

I parametri di query indicano al server di manifesto quale tipo di client ha inviato la richiesta e cosa desidera che esegua il server di manifesto. Alcuni sono obbligatori e alcuni hanno formati o valori accettabili specifici.
L&#39;URL completo è composto dall&#39;URL di base seguito da un punto interrogativo, quindi da argomenti `parameterName=value` separati da e-mail. Ad esempio, `Base URL?name1=value1&name2=value2& . . .&name n=value n`.

Il server manifesto riconosce i seguenti parametri. Tutte le querystring\
i parametri vengono passati al server di annunci.

| parameter | description | format |
|---|---|---|
| _sid_ | Un ID univoco che il server manifesto utilizzerà per generare l’ID sessione. | Richiesto per DASH/HLS |
| live | Notifica a Primetime  Ad Insertion che l&#39;elemento di contenuto passato è un flusso live.  Se questo parametro non viene passato, l&#39;inserimento di Annunci Primetime effettuerà una richiesta secondaria nella chiamata manifest iniziale per determinare se il manifesto è live o vod.<br>Valori possibili:<br>true per il <br>contenuto live false per il <br>contenuto vod per il rilevamento automatico | Facoltativo per HLS.  Richiesto per DASH |
| z | L’ID di zona per la risorsa da fornire al Ad Insertion Primetime . Fornito dal responsabile dell&#39;account tecnico  Adobe. | Richiesto per DASH/HLS |
| pabimode | Abilita l&#39;inserimento di [interruzioni pubblicitarie parziali](/help/primetime-ad-insertion/getting-started/ad-insertion-live-linear-stream.md#partial-ad-break-support) per i flussi live.<br>Valori possibili:<br>true per <br>abilitare l&#39;opzione di disattivazione (impostazione predefinita disattivata) | HLS/DASH |
| ptadtimeout | Abilita la limitazione del tempo complessivo di risoluzione degli annunci, se i fornitori a valle impiegano troppo tempo per rispondere.  Risposte in esecuzione prolungate potrebbero causare problemi con la riproduzione, consentendo a Primetime DAI di forzare una risposta entro un determinato limite di tempo.<br>Valori possibili:stringa <br>numerica in millisecondi.<br>omit to disable (predefinito disabilitato) | HLS/DASH |
| ptadwindow | Durata (in secondi) della finestra di lookback e di decisione — quanto tempo indietro Primetime  Ad Insertion cercherà segnali pubblicitari quando un utente DVR partecipa allo streaming. Un valore pari a zero disattiverà il mid-roll e le decisioni nel manifesto iniziale, con la ripresa delle decisioni solo dopo il primo aggiornamento. Questo parametro è utile per disabilitare l&#39;inserimento di annunci nelle sessioni che possono durare solo pochi secondi (ovvero il capovolgimento del canale).<br>Valori possibili:stringa <br>numerica da 0 a 1800 (valore predefinito 1800) | Solo HLS |
| ptassetid | ID univoco del contenuto assegnato e gestito dall&#39;editore.  Obbligatorio se utilizzato in combinazione con Akamai Ad Scaler. | HLS/DASH |
| ptcdn | Elenco di uno o più CDN per l’hosting di risorse transcodificate. Per ulteriori informazioni, vedere [Consegna e archiviazione](/help/primetime-ad-insertion/just-in-time-transcoding/delivery-and-storage.md).<br>Valori possibili: <br>akamai, livello3, llnw (reti a luci ridotte), comcast.<br>Per impostazione predefinita, vengono utilizzati CDN  Ad Insertion Primetime. | HLS/DASH |
| ptcueformat | Il formato specificato dei tag da eseguire per la decisione degli annunci (ad esempio, scte35).<br>Valori possibili:<br>dpissingola, dpiscte35, <br>elementalPer i formati dei cue point personalizzati, contattare il rappresentante tecnico per il valore da utilizzare per il caso d&#39;uso | HLS/DASH |
| ptfailover | Segnala al server manifesto di identificare i flussi primari e di failover specificati nella playlist principale e di trattarli come set disgiunti. Questo semplifica il failover e impedisce gli errori di temporizzazione. (solo per i dispositivi Apple HLS). Per ulteriori informazioni, vedere [Facilitazione della commutazione del lettore HLS](hls-switching-to-failover.md) | Solo HLS |
| ptmulticall | Se abilitata, viene effettuata una richiesta di annuncio separata per ogni valore trovato in una risorsa VOD.  Per impostazione predefinita, Primetime  Ad Insertion tenterà di raccogliere tutte le informazioni disponibili e di inviarle al server di annunci in un’unica richiesta. Valori possibili:true per abilitare, <br>omettere per disabilitare (impostazione predefinita disattivata) | HLS/DASH |
| ptparallelstream | Consente ai clienti con lettori che richiedono flussi audio o video demussati CMAF in parallelo per garantire la coerenza degli annunci nelle tracce audio e video. | Solo HLS |
| ptprotoswitch | Abilita regole per la riscrittura di manifesti e il recupero di annunci denominati, che in genere vengono configurate dal rappresentante dell&#39;assistenza tecnica.<br>Esempio: adfetch_fw, cdn_akm | HLS/DASH |
| pttagds | Abilita l&#39;inserimento di tag EXT-X-DISCONTINUITY-SEQUENCE nelle intestazioni HLS.Valori possibili:true per abilitare la disattivazione (impostazione predefinita disattivata) | Solo HLS |
| pitimeline | Una stringa contenente la timeline desiderata per la posizione e il contenuto degli annunci, che esclude e interrompe il flusso di contenuti. [ Vedere Formato timeline VOD  ] | HLS/DASH |
| pattoken | Abilita schemi di protezione token di autorizzazione per frammenti di contenuto/segmenti per CDN<br>Valori possibili:<br>akamai, llnw (limelight), ctl (centurylink) (la token predefinita è disabilitata) | HLS/DASH |
| pttrackingmode | Abilita schemi di tracciamento annunci.<br>Valori possibili:<br>semplice per gli annunci <br>trackingstm lato client per gli annunci server-side <br>trackingssssistm per il monitoraggio ibrido di annunci client/server (per impostazione predefinita, non viene eseguito il tracciamento di annunci) | HLS/DASH |
| pttrackingposition | Indica al server manifesto di restituire solo le informazioni di tracciamento annunci. Non specificate questo parametro nella richiesta di avvio automatico.<br>Nota: Il server manifesto ignora tutti i valori passati. Tuttavia, se si passa una stringa null o vuota, il server manifesto restituisce M3U8 | HLS/DASH<br>Tracciamento lato client |
| pttrackingversion | Imposta la versione del formato da restituire.<br>Valori possibili:<br>v1, v2, v3 o vmap | HLS/DASH<br>Tracciamento lato client |
| scteTracking | Questo parametro indica al server manifesto che il lettore che recupera M3U8 deve recuperare le informazioni del tag SCTE.<br>Valori possibili:<br>true o false (false predefinito)<br>Nota: I dati SCTE-35 vengono restituiti nel sidecar JSON con la seguente combinazione di valori dei parametri di query:<br>ptcueformat=turner | elementare | nfl | DPIScte35<br>pttrackingversion=v2<br>scteTracking=true<br> | Solo HLS |
| vetargetmoltiplicatore | Il numero di segmenti dal punto vivo L&#39;offset pre-roll è configurato utilizzando: ( vetargetmultiplier * targetDuration ) + vebufferlength<br>Nota: Questo parametro si applica solo ai flussi Live/Linear HLS<br>Valori possibili:<br>float numerico<br>(impostazione predefinita: 3.0 - come specifica HLS) | Solo HLS |
| vebufferLength | Il numero di secondi dal punto attivo, utilizzato insieme a vetargetmultiplier.<br>Nota: Questo parametro si applica ai flussi HLS dinamici/lineari <br>solo valori possibili:<br>valore mobile<br> numerico (predefinito: 3,0) | Solo HLS |
