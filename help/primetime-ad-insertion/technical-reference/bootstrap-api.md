---
title: API BOOTSTRAP
description: API BOOTSTRAP
exl-id: bc7fe244-8664-43ac-b9a1-3967ea8749b1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 0%

---

# API BOOTSTRAP {#bootstrap-api}

L’API Bootstrap è in genere l’URL inviato alle API di riproduzione client/video.  Per informazioni sulle opzioni e i parametri che possono essere configurati, consulta [Bootstrap parametri API](#bootstrap-api-parameters).

## Invia un comando al server manifesto {#send-a-command-to-the-manifest-server}

1. Invia un `HTTP GET` richiesta di un URL di avvio costruito utilizzando il seguente pattern:

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.[m3u8 or mpd]
    ?{query parameters}
   ```

   * **Estensione file** Definito. `.m3u8` se il manifesto di destinazione è HLS, `.mpd` se i manifesti di destinazione si trovano nel DASH.

   * **PublisherAssetID** Obbligatorio. ID univoco dell’editore per il contenuto specifico.

   * **URL contenuto** Obbligatorio. URL del file di contenuto M3U8, con codifica Base64 per essere sicuro nell’URL del server manifesto. L’URL del contenuto deve puntare a un file M3U8 variante, anche se è presente un solo flusso di velocità in bit.

   * **Parametri di query** Questi costituiscono la parte più variegata della richiesta. Indicano al server manifesto il tipo di client che effettua la richiesta e cosa desidera che faccia il server manifesto.

   Ad esempio:

   ```
   https://manifest.auditude.com/auditude/variant/
    {publisherAssetID}/{Content URL (base64)}.[m3u8 or mpd]?
   u={Asset ID}&z={zone}&_sid_=0&pttrackingmode=simple
   &pttrackingversion=v2&live=false
   ```

   **Richieste HTTP e HTTPS**

   Il server manifesto crea URL utilizzando lo stesso protocollo HTTP della richiesta del client. Se un lettore effettua una richiesta HTTP (http) non sicura, il server manifesto restituisce gli URL del manifesto e gli URL di tracciamento di Auditude con il protocollo http. Se un lettore effettua una connessione HTTP sicura (https), il server manifest, restituisce gli URL manifest e gli URL di tracciamento Auditude con il protocollo https.

   >[!NOTE]
   >
   >Il server manifesto non può modificare il protocollo (HTTP o HTTPS) dei beacon di tracciamento di terze parti. Contatta i contenuti e i provider di annunci di terze parti per richiedere la configurazione dei protocolli desiderati.  I protocolli URL dei segmenti possono essere modificati, tuttavia, per impostazione predefinita, utilizzano gli stessi protocolli definiti nei manifesti di destinazione.

## Bootstrap parametri API {#bootstrap-api-parameters}

I parametri di query indicano al server manifesto il tipo di client che ha inviato la richiesta e cosa il client desidera che il server manifesto esegua. Alcuni sono obbligatori e altri hanno specifici formati o valori accettabili.
L’URL completo è costituito dall’URL di base seguito da un punto interrogativo, quindi `parameterName=value` argomenti separati da e commerciali. Ad esempio: `Base URL?name1=value1&name2=value2& . . .&name n=value n`.

Il server manifest riconosce i seguenti parametri. All querystring\
I parametri vengono passati al server di annunci.

| parametro | descrizione | formati |
|---|---|---|
| _sid_ | ID univoco che il server manifesto utilizzerà per generare l&#39;ID sessione. | Obbligatorio sia per DASH che per HLS |
| live | Notifica all’Ad Insertion di Primetime che l’elemento di contenuto passato è un flusso live.  Se questo parametro non viene passato, l’inserimento di Primetime Ad eseguirà una richiesta secondaria nella chiamata del manifesto iniziale per determinare se il manifesto è live o vod.<br>Valori possibili:<br>true per i contenuti live<br>false per il contenuto vod<br>ometti per rilevamento automatico | Facoltativo per HLS.  Obbligatorio per DASH |
| z | ID di zona della risorsa da fornire all’Ad Insertion di Primetime. Fornito dal tuo Adobe Technical Account Manager. | Obbligatorio sia per DASH che per HLS |
| pabimode | Abilita [inserimento parziale di interruzioni pubblicitarie](/help/primetime-ad-insertion/getting-started/ad-insertion-live-linear-stream.md#partial-ad-break-support) per flussi live.<br>Valori possibili:<br>true per abilitare<br>ometti per disabilitare (impostazione predefinita disabilitata) | HLS/TRATTINO |
| ptadtimeout | Consente di limitare il tempo complessivo di risoluzione degli annunci, se i provider a valle impiegano troppo tempo per rispondere.  Le risposte con tempi di esecuzione lunghi possono causare problemi di riproduzione, consentendo a Primetime DAI di forzare una risposta entro un limite di tempo specifico.<br>Valori possibili:<br>stringa numerica in millisecondi.<br>ometti per disabilitare (impostazione predefinita disabilitata) | HLS/TRATTINO |
| ptadwindow | Durata (in secondi) dell’intervallo di lookback e decisione: quanto indietro nel tempo l’Ad Insertion Primetime cercherà i segnali pubblicitari quando un utente DVR si unisce al flusso. Un valore pari a zero disabilita il mid-roll ad decisioning nel manifesto iniziale, con il decisioning che riprende solo dopo il primo aggiornamento. Questo parametro è utile per disabilitare l’inserimento di annunci nelle sessioni che possono durare solo pochi secondi (ossia la riflessione del canale).<br>Valori possibili:<br>stringa numerica 0-1800 (valore predefinito 1800) | Solo HLS |
| ptassetid | ID univoco del contenuto assegnato e gestito dall’editore.  Obbligatorio se utilizzato con Akamai Ad Scaler. | HLS/TRATTINO |
| ptcdn | Elenco di una o più CDN per l’hosting delle risorse transcodificate. Per ulteriori informazioni, consulta [Consegna e archiviazione](/help/primetime-ad-insertion/just-in-time-transcoding/delivery-and-storage.md).<br>Valori possibili:<br>akamai, level3, llnw (limelight networks), comcast.<br>Per impostazione predefinita, vengono utilizzate le reti CDN Ad Insertion di Primetime. | HLS/TRATTINO |
| ptcueformat | Il formato specificato dei tag per eseguire le decisioni sugli annunci (ad esempio, scte35).<br>Valori possibili:<br>dpisimple, dpiscte35, elementare<br>Per i formati di cue personalizzati, contatta il rappresentante del tuo account tecnico per conoscere il valore da utilizzare per il tuo caso d’uso | HLS/TRATTINO |
| ptfailover | Segnala al server manifesto di identificare i flussi primari e di failover specificati nella playlist principale e di trattarli come set disgiunti. Ciò semplifica il failover e impedisce errori di temporizzazione. (Solo per dispositivi Apple HLS). Per ulteriori informazioni, consulta [Facilitazione della commutazione del lettore HLS](hls-switching-to-failover.md) | Solo HLS |
| ptmulticall | Se l’opzione è abilitata, viene effettuata una richiesta di annuncio separata per ogni risultato trovato in una risorsa VOD.  Per impostazione predefinita, Primetime Ad Insertion tenterà di raccogliere tutte le informazioni disponibili e di inviarle al server di annunci in un’unica richiesta. Valori possibili:true per abilitare, <br>ometti per disabilitare (impostazione predefinita disabilitata) | HLS/TRATTINO |
| ptparallelstream | Consente ai clienti con lettori che richiedono flussi audio o video demussi CMAF in parallelo per garantire che gli annunci nelle tracce audio e video siano coerenti. | Solo HLS |
| ptprotoswitch | Abilita le regole di riscrittura del manifesto denominate e le regole di recupero degli annunci, che in genere vengono impostate dal rappresentante del supporto tecnico.<br>Esempio: adfetch_fw, cdn_akm | HLS/TRATTINO |
| pttagds | Consente l&#39;inserimento di tag EXT-X-DISCONTINUITY-SEQUENCE nelle intestazioni HLS.Valori possibili:true per attivare la disattivazione (impostazione predefinita disattivata) | Solo HLS |
| pttimeline | Stringa contenente la timeline desiderata per il posizionamento e il contenuto degli annunci, che si sovrappone e si interrompe nel flusso di contenuto. [ Consulta Formato timeline VOD ] | HLS/TRATTINO |
| pttoken | Abilita gli schemi di protezione dei token di autorizzazione di frammenti di contenuto/segmenti per le reti CDN<br>Valori possibili:<br>akamai, lnw (limelight), ctl (centurylink) (la tokenizzazione predefinita è disabilitata) | HLS/TRATTINO |
| pttrackingmode | Abilita gli schemi di tracciamento degli annunci.<br>Valori possibili:<br>semplice per il tracciamento degli annunci lato client<br>sstm per il tracciamento degli annunci lato server<br>simplesstm per il tracciamento degli annunci ibridi client/server (per impostazione predefinita, non viene eseguito alcun tracciamento degli annunci) | HLS/TRATTINO |
| pttrackingposition | Indica al server manifesto di restituire solo le informazioni di tracciamento degli annunci. Non specificare questo parametro nella richiesta bootstrap.<br>Nota: il server manifest ignora tutti i valori passati. Tuttavia, se si passa una stringa nulla o vuota, il server manifesto restituisce M3U8 | HLS/TRATTINO<br>Tracciamento lato client |
| pttrackingversion | Imposta la versione del formato da restituire.<br>Valori possibili:<br>v1, v2, v3 o vmap | HLS/TRATTINO<br>Tracciamento lato client |
| scteTracking | Questo parametro indica al server manifest che il lettore che recupera il file M3U8 deve recuperare le informazioni del tag SCTE.<br>Valori possibili:<br>true o false (valore predefinito false)<br>Nota: i dati SCTE-35 vengono restituiti nella barra laterale JSON con la seguente combinazione di valori dei parametri di query:<br>ptcueformat=turner | elementare | nfl | DPIScte35<br>pttrackingversion=v2<br>scteTracking=true<br> | Solo HLS |
| vetargetmultiplier | Il numero di segmenti dal punto di attivazione L’offset pre-roll è configurato utilizzando: ( vetargetmultiplier * targetduration ) + vebufferlength<br>Nota: questo parametro si applica solo ai flussi HLS live/lineari<br>Valori possibili:<br>virgola mobile numerico<br>(impostazione predefinita: 3.0 - come specifica HLS) | Solo HLS |
| vebufferLength | Il numero di secondi dal punto di attivazione, utilizzato in combinazione con vetargetmultiplier.<br>Nota: questo parametro si applica solo ai flussi HLS live/lineari<br>Valori possibili:<br>virgola mobile numerico<br>(impostazione predefinita: 3.0) | Solo HLS |
