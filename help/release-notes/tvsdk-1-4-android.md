---
title: Note sulla versione di TVSDK 1.4 per Android
description: Le note sulla versione TVSDK 1.4 per Android descrivono le novità o le modifiche, i problemi risolti e noti e i problemi del dispositivo in TVSDK Android 1.4.
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '7802'
ht-degree: 0%

---


# Note sulla versione TVSDK 1.4 per Android {#tvsdk-for-android-release-notes}

Le note sulla versione TVSDK 1.4 per Android descrivono le novità o le modifiche, i problemi risolti e noti e i problemi del dispositivo in TVSDK Android 1.4.

## Nuove funzioni {#new-features}

**Versione 1.4.43**

**Caricamento sicuro degli annunci tramite HTTPS**

Adobe Primetime fornisce un&#39;opzione per richiedere la prima chiamata al server ad primetime e a CRS su HTTPS.

**alwaysUseAudioOutputLatency(valore booleano) nella classe MediaPlayer**

Quando questo parametro è impostato, utilizza la latenza di uscita audio nel calcolo della marca temporale audio.

Accetta un valore di parametri booleani. Se il suo valore è `True`, il client utilizza la latenza di uscita audio nel calcolo della marca temporale audio.

**Versione 1.4.42**

**Inserimento parziale di annunci:**
esperienza simile a quella televisiva di partecipare nel mezzo di un annuncio senza attivare il tracciamento per l’annuncio parzialmente guardato.
Esempio: L&#39;utente si unisce al centro (a 40 secondi) di un&#39;interruzione pubblicitaria di 90 secondi costituita da tre annunci da 30 secondi. Questo è a 10 secondi dal secondo annuncio dell&#39;interruzione.
* Il secondo annuncio viene riprodotto per la durata rimanente (20 sec) seguita dal terzo annuncio.
* I tracciatori degli annunci per l’annuncio parziale riprodotto (secondo annuncio) non vengono attivati. I tracciatori solo per il terzo annuncio vengono attivati.

**Versione 1.4.41**

Nessuna nuova funzionalità.

**Versione 1.4.40**

Nessuna nuova funzionalità.

>[!NOTE]
>
>Se utilizzi una versione precedente alla 1.4.39, non sarà necessario apportare modifiche all’API.

**Versione 1.4.39**

* TVSDK è certificato con VHL 2.0.1 e con VHL 2.0.1 con Nielsen.
* Android TVSDK viene aggiornato per effettuare richieste CRS dal nuovo host Akamai `primetime-a.akamaihd.net`.
* La nuova configurazione del nome host fornisce la distribuzione delle risorse CRS tramite HTTP e HTTPS (SSL) su larga scala.
* TVSDK supporta la versione Android Oreo.
* Viene aggiunta una nuova funzione alla classe `AdClientFactory` per supportare la registrazione di più rilevatori opportunità:

   ```
   public List<PlacementOpportunityDetector> createOpportunityDetectors(MediaPlayerItem item);
   ```

   Dovrebbe restituire un array di PlacementOpportunityDetector. Ora è possibile registrare più rilevatori opportunità. Ad esempio, per la funzione di individuazione rapida e in uscita, erano necessari due rilevatori opportunità, uno per l’inserimento di annunci e un altro per l’uscita anticipata dall’annuncio. È necessario implementare questa nuova funzione solo se hai implementato la tua AdvertisingFactory (e non utilizzando DefaultAdvertisingfactory). Per ottenere il comportamento esistente, è necessario creare un singolo rilevatore opportunità, come nella funzione createOpportunityDetector() e inserirlo in un array e restituire:

   ```
   public class MyAdvertisingFactory extends AdvertisingFactory {  
   …  
   @Override  
   public List&lt;PlacementOpportunityDetector&gt; createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {  
   List&lt;PlacementOpportunityDetector&gt; opportunityDetectors = new ArrayList&lt;PlacementOpportunityDetector&gt;();  
   opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));  
   return opportunityDetectors;  
   } }
   ```

>[!NOTE]
>
>Se utilizzi una versione precedente alla 1.4.39, non sarà necessario apportare modifiche all’API.

**Versione 1.4.36**

Correzione di bug per Salta contenuto su Android.

**Versione 1.4.35**

* **Informazioni sugli annunci in rete**

   Le API TVSDK ora forniscono informazioni aggiuntive sulle risposte VAST di terze parti. Gli Ad ID, il sistema di annunci e le estensioni VAST Ad sono forniti nella classe NetworkAdInfo accessibile tramite la proprietà networkAdInfo su una Ad Asset. Queste informazioni possono essere utilizzate per l&#39;integrazione con altre piattaforme di Ad Analytics come **Analytics principale**.

**Versione 1.4.31**

**Supporto multi-CDN per annunci CRS**
* Per impostazione predefinita, tutte le risorse transcodificate saranno ospitate su CDN di proprietà di Adobe in Akamai. Con l’ultima versione, Adobe Creative Repackaging Service (CRS) consente di caricare le creatività transcodificate in più CDN come specificato dal cliente.
* Vengono aggiunte nuove API a TVSDK per abilitare la specifica dell’url creativo CRS finale quando l’URL predefinito non viene utilizzato. Per informazioni su come utilizzare queste nuove API, consulta la documentazione .

**La versione 1.4.18**
Primetime Android TVSDK ora supporta i creativi JavaScript VPAID 2.0 per abilitare un’esperienza pubblicitaria interattiva ricca. Per ulteriori informazioni su VPAID 2.0, consulta [Supporto di annunci VPAID](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/vpaid-ads/android-3x-vpaid-ads.md).

**Versione 1.4.17**

AC-3 5.1 è supportato solo su Amazon FireTV.

**Versione 1.4.11**

* **Ad Fallback, concatenamento margherita nella logica di selezione degli annunci (Zendesk #3103** Per gli annunci VAST (creativi) con la regola di fallback abilitata, TVSDK tratta un annuncio con un tipo MIME non valido come un annuncio vuoto e tenta di utilizzare al suo posto gli annunci di fallback. Puoi configurare alcuni aspetti del comportamento di fallback.

Per ulteriori informazioni, consulta [Fallback per annunci VAST e VMAP](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-fallback/android-3x-ad-fallback.md).

* **Video Heartbeat Library (VHL) aggiornato alla versione 1.5**
   * Possibilità di inviare i metadati con inizio video e/o inizio video/ad/capitolo come dati contestuali
   * Meno traffico di rete - Gli heartbeat sono in media meno e le dimensioni sono più piccole

**Versione 1.4.7**

* **On-Premise Individualization** SupportSupport per le installazioni on-premise di Adobe Individualization Server per personalizzare la richiesta di individualizzazione del client per passare a un endpoint diverso.

**Versione 1.4.6**

* **È ora supportata la crittografia AES campione (richiede la versione di Flash Player 17.0.0.134)**È ora supportata la crittografia AES basata su esempio.

**Versione 1.4.2**

* **Aggiornamento della Video Heartbeat Library (VHL) alla versione 1.4.0.1**

   * Aggiunta la possibilità di raggruppare diversi casi d’uso di analytics, da altri SDK o lettori, con Adobe Analytics Video Essentials.
   * Il tracciamento degli annunci è stato ottimizzato rimuovendo i metodi trackAdBreakStart e trackAdBreakComplete . L’interruzione pubblicitaria viene dedotta dalle chiamate dei metodi trackAdStart e trackAdComplete.
   * La proprietà playhead non è più necessaria durante il tracciamento degli annunci.

* **SDK Nielsen** IntegrazioneTVSDK ora supporta l’invio di informazioni di tracciamento degli utenti all’SDK Nielsen senza alcuna integrazione personalizzata.

**Versione 1.4.0**

* **Segnalazione blackout con** sostituzione di contenuti alternativiNell’ambito dell’aggiornamento TVSDK 1.4, TVSDK supporta ora anche l’accesso e il ritorno da blackout regionali rispetto a contenuti lineari. Il TVSDK può ora elaborare due file manifest in parallelo, principale e alternativo, per monitorare i segnali di blackout anche quando viene mostrata una programmazione alternativa al posto della programmazione originale.

* **Rimuovi/sostituisci C3** AdsNow, non è necessario alcun lavoro di preparazione aggiuntivo per inserire dinamicamente nuovi annunci nelle risorse video-on-demand (VOD) che escono dalla finestra C3. Il TVSDK fornisce ora un’API per rimuovere intervalli di contenuto personalizzati e inserire nuovi annunci in modo dinamico. Questa nuova potente funzionalità è utile anche nei casi in cui i contenuti live/lineari vengono trasmessi durante la trasmissione e immediatamente disattivati per l’utilizzo come contenuti on demand senza il tempo necessario per &quot;pulire&quot; la risorsa.

* L&#39;interfaccia PlaybackEventListener dispone di un nuovo metodo chiamato onReplaceMediaPlayerItem, che è possibile utilizzare per ascoltare un nuovo evento, `ITEM_REPLACED`. Questo evento viene inviato ogni volta che un&#39;istanza MediaPlayeritem viene sostituita su MediaPlayer. L&#39;applicazione client che implementa questo PlaybackEventListener deve implementare o ignorare questo nuovo metodo.
* AdClientFactory ha una nuova funzione aggiunta alla classe per la registrazione per più rilevatori opportunità:

   ```
   public List&lt;PlacementOpportunityDetector&gt; createOpportunityDetectors(MediaPlayerItem item);
   
   For example for early ad exit feature, you need two Opportunity Detectors - one for ad insertion and another for  early  exit from  `ad`.
   
   To override this new function create a single Opportunity Detector, and put into an array and return:
   
   @Override
   
   public List&lt;PlacementOpportunityDetector&gt; createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {
   
   List&lt;PlacementOpportunityDetector&gt; opportunityDetectors = new ArrayList&lt;PlacementOpportunityDetector&gt;();
   
   opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));
   
   return opportunityDetectors;
   }
   
   }
   ```

## Modifiche TVSDK per 1.4 {#tvsdk-changes}

* L&#39;interfaccia PlaybackEventListener ha un nuovo metodo chiamato onReplaceMediaPlayerItem, che è possibile utilizzare per ascoltare un nuovo evento, ITEM_REPLACED. Questo evento viene inviato ogni volta che un&#39;istanza MediaPlayeritem viene sostituita su MediaPlayer. L&#39;applicazione client che implementa questo PlaybackEventListener deve implementare o ignorare questo nuovo metodo.

* AdClientFactory ha una nuova funzione aggiunta alla classe per la registrazione per più rilevatori opportunità:

```
public List`<PlacementOpportunityDetector>` createOpportunityDetectors(MediaPlayerItem item);
```

Ad esempio, per la funzione di individuazione rapida e in uscita, sono necessari due rilevatori opportunità, uno per l’inserimento di annunci e un altro per l’uscita anticipata dall’annuncio.

Per ignorare questa nuova funzione, crea un singolo rilevatore opportunità e inserisci in un array e restituisce:

```
@Override

public List`<PlacementOpportunityDetector>` createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {

List`<PlacementOpportunityDetector>` opportunityDetectors = new ArrayList`<PlacementOpportunityDetector>`();

opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));

return opportunityDetectors;

}

}
```

## Certificazione e supporto dei dispositivi in 1.4 {#device-certification-and-support-in}

>[!NOTE]
>
>Le seguenti funzioni sono **non** supportate nel TVSDK :
>
>* Slow motion, su qualsiasi piattaforma o versione.
>* Giochi di trucco dal vivo.


**Versione 1.4.43**

TVSDK 1.4.43 è stato certificato con dispositivi Android con Android 6.0.1/ 7.0 e 8.1 (Oreo).

* **Versione 1.4.23:**

   * TVSDK 1.4.23 è stato certificato per dispositivi Android con Android N.

* **Versione 1.4.18:**

   * Primetime è stata certificata per Amazon Fire TV.
   * VPAID 2.0 è supportato solo sui dispositivi con Android 4.0 e versioni successive.

## Problemi risolti in 1.4 {#resolved-issues-in}

>[!NOTE]
>
>Tutti i clienti TVSDK che utilizzano CRS sono invitati ad effettuare l’aggiornamento a TVSDK 1.4.39 o versione più recente su iOS e Android. Questo aggiornamento sostituisce l’implementazione dell’app esistente. Dopo l&#39;aggiornamento, controlla le richieste CRS creative URL in uno strumento proxy (ad esempio, Charles) per verificare che la versione nel percorso rifletta la versione 3.1. Ad esempio:
>
>`https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8`

**Versione 1.4.43**

* Biglietto #27143 - Impossibile riprodurre la traccia audio 5.1 sui dispositivi FireTV

   * TVSDK ora in grado di riprodurre audio AC3 su dispositivi FireTV. La riproduzione è sempre in stereo.

* Ticket #33902 - Consegna sicura degli annunci tramite HTTPS

   * Adobe Primetime fornisce un&#39;opzione per richiedere la prima chiamata al server di annunci primetime e al CRS su https.

* Biglietto #34493 - Ritardo audio Bluetooth

   * È stato aggiunto `alwaysUseAudioOutputLatency` nella classe MediaPlayer che, se impostata, si traduce in uso della latenza di uscita audio nel calcolo della marca temporale audio.

* Biglietto #34949 - Nuova versione della libreria heartbeat video (VHL) integrata.

**Versione 1.4.42 (1791)**

* Zendesk #33719: FireTV 4k Adaptive Bitrate viene ridimensionato lentamente. È stato aggiunto il supporto per ABR per dispositivi FireTV 4K.
* Zendesk #33338:  resetDRM cancella tutti i dati dell&#39;applicazione.  È stato gestito un caso aggiuntivo in cui le eccezioni nei thread non TVSDK causavano la compilazione delle code di operazione TVSDK.

**Versione 1.4.41 (1776)**

* Zendesk #33002 - Dati delle risorse Companion da TVSDK su Fire TV. È stata implementata una nuova classe AdBannerAsset che restituirà i dati Companion come List &lt;AdBannerAsset> e AdAsset::id è ora un String anziché long.
* Zendesk #32821 - Android Primetime Player si blocca quando incontra Presentation Timestamp (PTS) per WWE. Questo problema è stato risolto in questa versione.
* Zendesk #33572 - VideoAnalyticsProvider Ad Start Crash. Questo problema è stato risolto utilizzando la giusta combinazione della versione SDK congiunta VHL+Nielsen di VideoHeartbeat.jar.
* Zendesk #33355 - Fire TV: Esegui lo scrub indietro di 15 secondi. Non è stata apportata alcuna correzione dal lato TVSDK e dai clienti che ne stanno verificando la conformità al proprio End e a terze parti.

**Versione 1.4.40 (1764)**

* Zendesk #33068 - Problema di sincronizzazione labiale Amazon sul nuovo dispositivo. Il problema di sincronizzazione ip è stato risolto in queste versioni.
* Zendesk #32215 - Android TVSDK 1.4.38 Problemi di sicurezza `[Hotlist]`. Aggiornato alle ultime OpenSSL-1.1.0 e curl-7.55.1.
* Zendesk #32920 - Schermo vuoto all’interno di un’interruzione pubblicitaria e senza completamento di un’interruzione pubblicitaria. È stato risolto un problema a causa del quale un contenitore VPAID poteva trovarsi in uno stato bloccato e gestiva un problema a causa del quale gli annunci VPAID di Facebook spesso restituivano più blocchi CDATA in un singolo \&amp;lt;AdParameters\&amp;gt; Nodo VAST.

**Versione 1.4.39 (1744)**

* Zendesk #28976 - La richiesta di licenza dura più di un secondo. Mentre le chiamate di richiesta di licenza DRM che utilizzano POST sono in esecuzione, Curl aggiunge ulteriori &quot;Aspettative: intestazione 100-continue&quot;. Intestazione &quot;Expect:&quot; rimossa in TVSDK .
* Zendesk #27707 - Ambienti CSAI che non rispettano i marcatori CUE IN per un ritorno anticipato o al contenuto. Supporto per più generatori di opportunità.

**Versione 1.4.38 (1722)**

* Zendesk #21590 - Prestazioni video e tracciamento nelle build di origine più recenti

Integrazione e certificazione di VHL 2.0 in TVSDK per ridurre la barriera nell’implementazione di VideoHeartbeatLibrary riducendo la complessità delle API.

* Zendesk #29688 - Supporto per i clienti Android O Beta.

Supporto TVSDK per la nuova versione Android Beta.

**Versione 1.4.36 (1713)**

* Zendesk #27392 - Salta dei contenuti su Android

Per adattarsi alla decrittografia, Android TVSDK stava ampliando erroneamente l&#39;intervallo di byte del contenuto non iframe di 16 byte. L&#39;ampliamento è necessario per i flussi Iframe, ma non per i flussi non iframe.

**Versione 1.4.34 (1702)**

* Zendesk #27638 - Perdita nell&#39;oggetto cURL INet

L&#39;oggetto POsix cURL INet si verificava una perdita mentre si teneva in share manager e nella cache DNS utilizzata nelle connessioni cURL.

Questo problema è stato risolto eliminando l&#39;oggetto POsix cURL INet dal decostruttore INet.

**Versione 1.4.33 (1694)**

* **Libreria OpenSSL**

La libreria OpenSSL è stata aggiornata con la versione 1.0.2j di OpenSSL.

* Zendesk #21701 - Invia l&#39;URL creativo originale per la richiesta CRS 1401 invece dell&#39;URL normalizzato.
Questo problema viene risolto inviando gli URL creativi originali.

* Zendesk #25023 - Riproduzione video a lunga durata: fermo video, sfarfallii dello schermo
Questo problema è stato risolto impostando le dimensioni massime del formato video per i dispositivi set-top box CenturyLink.

* Zendesk #27460 - Il nuovo account Akamai non è in grado di gestire una richiesta cdn di POST.
Il codice è stato aggiornato per fare in modo che la richiesta di annuncio `cdn.auditude.com` sia GET invece di POST.

* Zendesk #28245 - Lo stato di riproduzione non viene notificato correttamente quando l&#39;app va dallo sfondo al primo piano
Questo problema è stato risolto ripristinando correttamente lo stato di riproduzione per la riproduzione o la pausa quando l&#39;applicazione torna in primo piano.

**Versione 1.4.32 (1682)**

* Zendesk #25779 - Vulnerabilità di sicurezza trovata con TVSDK
Android 4.2 e versioni precedenti presenta una vulnerabilità di sicurezza quando JavaScript è abilitato in una WebView. L&#39;utilizzo di WebView da TVSDK è stato disattivato per i dispositivi con sistema operativo 4.2 o inferiore. In questo modo viene disabilitato l’uso degli annunci VPAID in TVSDK su questi dispositivi.

* Zendesk #26890 - Problema nello stato dello schermo (ON/OFF) Manipolazione Ref. Lettore
Quando il motore video di Adobe (AVE) riprende da uno stato SOSPESO, DefaultMediaPlayer non ne aggiorna lo stato. Di conseguenza, DefaultMediaPlayer rimane in uno stato SOSPESO anche se l&#39;AVE è in uno stato di riproduzione. Questo problema è stato risolto impostando lo stato DefaultMediaPlayer su PLAYING quando si riceve uno stato PLAY dall&#39;AVE, anche se lo stato corrente di DefaultMediaPlayer è SOSPESO.

**Versione 1.4.31 (1675)**

* Zendesk #21974 - Eccezioni dovute a oggetti nulli
   * AdIndex raramente viene incrementato quando null. Ciò potrebbe essere dovuto a chiamate API errate ricevute per pre-roll adBreak. Sono stati corretti i tipi di dati per evitare tali eccezioni

* Zendesk #24714 - Disattivare il logging estraneo
   * Aggiornamento del TVSDK per disattivare la registrazione estranea

* Zendesk #24488 - Problemi di sincronizzazione AV su Fire TV
   * Risolto migliorando la gestione dei thread del decoder AV. In particolare, ogni volta che le code dei fotogrammi di input o di output vengono modificate, viene eseguito il thread di decodifica specifico per il tipo di contenuto del fotogramma.

* Zendesk #26551 - Correggere gli errori CRS
   * Quando la richiesta è HEAD (http head), non è necessario leggere il contenuto perché è vuoto. Mentre va bene cercare di leggerlo, il vecchio Android (4.0.x) si blocca mentre chiamiamo read() e il più recente Android restituisce il valore corretto (-1) quando chiamiamo read(). In base a questo, il codice è stato modificato in non per leggere il contenuto per &quot;head&quot;

* Zendesk #26696 Eccezione Null Pointer quando si accede a TrickPlayManager
   * È stato corretto controllando se l’oggetto TrickPlayManager non è nullo prima di utilizzarlo.

**Versione 1.4.30 (1659)**

* Zendesk #22675 La durata delle risorse non viene aggiornata per i flussi live/lineari
Questo problema è stato risolto fornendo una nuova API, assetDuration, in PTVideoAnalyticsTrackingMetadata che fornisce la durata della risorsa per i flussi in tempo reale e in tempo reale.

* Zendesk #25853 Perdita di memoria in TVSDK quando si cambiano i canali
È stato risolto il problema relativo alla perdita di un buffer di lettura del file quando MediaPlayer viene reimpostato o rilasciato durante il download di un file.

**Versione 1.4.29 (1653)**

* Zendesk #21200 - Il giocatore non si riprende dallo stato sospeso quando l&#39;applicazione era in background
Quando il lettore è stato sospeso dopo che l&#39;interruttore del flusso è stato segnalato, la risoluzione consente al lettore di eseguire l&#39;interruttore del flusso durante il ripristino dello stato di sospensione, invece di tornare alla posizione precedente.

* Zendesk #23412 - Il giocatore è bloccato con una scatola nera se si clicca su qualsiasi Ads entro gli ultimi 3 s dell&#39;interruzione annuncio
Questo problema è lo stesso di Zendesk #21200.

* Zendesk #23616 - Saltato annuncio break cerca troppo lontano in futuro
A seconda del tipo di inserimento dell’annuncio (inserimento/sostituzione), TVSDK determina se la durata dell’annuncio viene utilizzata nel calcolo per determinare il punto finale dell’interruzione dell’annuncio.

* Zendesk #25078 - Perdita di memoria TVSDK DRM su Android TV STB
La perdita di memoria per l&#39;oggetto adattatore DRM è stata individuata e fissata.

* Zendesk #25067 - Arresto anomalo in VideoEngineTimeline
Questo accade perché gli oggetti non sono stati puliti correttamente e gli eventi sono stati chiamati dopo la distruzione degli oggetti. Il problema è stato risolto aggiungendo controlli per impedire eccezioni nulle.

* Zendesk #25352 - Imposta intestazione HTTP personalizzata
Questo problema è stato risolto aggiungendo una nuova intestazione personalizzata all’elenco consentiti su TVSDK.

* Zendesk #25617 - Il rollover Live Stream PTS causa discontinuità del lettore e crash di memoria
Questo problema è stato risolto aggiungendo una gestione di rollover PTS in FragmentalHTTPStreamer quando si verifica un rollover nel mezzo di un segmento.

**Versione 1.4.28 (1637)**

* Zendesk #23618 - Gli eventi di interruzione dell&#39;annuncio si attivano prima che la politica dell&#39;annuncio venga consultata
Questo problema è stato risolto impedendo l&#39;attivazione degli eventi AD_BREAK_START e AD_START quando l&#39;annuncio viene ignorato a causa di adForgiveness. Viene invece inviato l&#39;evento AD_BREAK_SKIPPED .

**Versione 1.4.27 (1631)**

* Zendesk #23174 - Problema di prestazioni durante il ridimensionamento del video
Questo problema è stato risolto dimostrando una nuova API, MediaPlayerView.setSurfaceFixedSize, che consente a TVSDK di accedere a SurfaceHolder.setFixedSize() da MediaPlayerView.

* Zendesk #24450 - TVSDK effettua richieste di annunci duplicate
Questo problema si verificava quando il tempo trascorso veniva convertito in lungo e non doppio e questo problema era stato risolto.

**Versione 1.4.26 (1627)**

* Zendesk #21436 - Aggiornamento della libreria OpenSSL alla versione 1.0.2h Aggiornamento della libreria OpenSSL a OpenSSL versione 1.0.2h
* Zendesk #23825 - I cookie non vengono inclusi nei callback Corretti fornendo il supporto per i cookie android.

**Versione 1.4.25 (1620)**

* Zendesk #22900 - Lo streaming DRM di Adobe Primetime Live non viene riprodotto sul lettore di riferimento Android
Il problema di allocazione della memoria è stato risolto.
* Zendesk #23176 - Arresto anomalo dell&#39;applicazione quando si sta tentando di riprodurre annunci VPAID
L&#39;arresto anomalo si è verificato perché l&#39;applicazione non crea una visualizzazione annunci personalizzata per il rendering di un annuncio VPAID. Questo problema è stato risolto ignorando gli annunci VPAID nella risposta del server di annunci quando non è presente una visualizzazione di annunci personalizzata.

* Zendesk #23153 - SampleAES DRM Stream - Stallo della riproduzione nel lettore di riferimento TVSDK
Questo problema è lo stesso di Zendesk #22900.

**Versione 1.4.24 (1612)**

* Zendesk #20784 - Analytics: Attivazione di contenuti completi per transizioni video in tempo reale
Questo problema è stato risolto aggiungendo un’API (trackVideoComplete) per attivare manualmente il completamento del contenuto durante una sessione di tracciamento video in tempo reale/lineare.

* Arresto anomalo della timeline di VideoEngine #21977 durante il funzionamento di placeAdBreak/acceptAd
   * In questo problema sono state aggiornate le seguenti librerie:
      * Libreria Adobe Mobile alla versione 4.10.0
      * Libreria VHL alla versione 1.5.6
      * Libreria VHL-Nielsen alla versione 1.6.7

Questo problema è stato risolto aggiungendo un controllo null prima di aggiungere annunci all’elenco di annunci accettati.

* Zendesk #22313 Il bitrate per gli STB con chipset Amilogico non va oltre 1,2M
Questo problema è stato risolto precaricando le funzionalità del codec multimediale e disabilitando l&#39;interruttore senza soluzione di continuità per i dispositivi del chipset Amilogic.

* Zendesk #19520 Esempio di risorsa AES HLS non in esecuzione nei lettori TVSDK
Questo problema è stato risolto gestendo più descrittori PMT per i flussi HLS crittografati AES di esempio.

**Versione 1.4.23 (1602)**

* Zendesk #18852 - Aggiorna la logica di selezione creativa in base alle regole CRS
Questo problema è stato risolto aggiungendo un file di configurazione JSON per specificare la priorità di selezione creativa.

* Zendesk #20861 - Android N
Questa versione fornisce supporto per Android N rimuovendo la possibilità di utilizzare direttamente le librerie native della piattaforma Android che non sono più accessibili per le applicazioni che vengono eseguite su Android N.

* Zendesk #21018 - Android N crash
Stessa risoluzione di ZD# 20861.

* Zendesk #21266 - VideoEngineAdapter si blocca in caso di errore Invalid_Key
L&#39;errore Invalid_Key non include una descrizione da AVE, quindi l&#39;analisi del testo è risultato in NPE. Il problema è stato risolto aggiungendo un controllo null per la descrizione durante onError prima di analizzare la descrizione.

* Zendesk #22286 - La libreria nativa sta continuando ad allocare la chiave/frammento di lettura della memoria causando crash
Questo arresto anomalo che si è verificato su Android quando si tenta di caricare un manifesto con più chiavi contemporaneamente è stato corretto.

**Versione 1.4.22 (1581)**

* Zendesk #17236 - Tempo di testa di riproduzione inaffidabile per i video HLS con DRM
È stato corretto il salto temporale con i flussi LBA, dove l’ora di inizio del segmento audio non corrisponde all’ora di inizio del segmento video.

* Zendesk #17680 - La riproduzione video si sta congelando nella casella Selevision Andredo
Il decodificatore video su questo dispositivo a volte restituisce un significativo salto del tempo di uscita quando si depone il fotogramma video dal buffer di output, e questo timestamp di output rimane alto. Questo problema è stato risolto restituendo un errore *profilo video non supportato* che non obbliga il lettore a ripetere lo stesso profilo o a scegliere un profilo diverso.

* Zendesk #19074 - Il fermo video durante il gioco di trucco FFWD e REW
Questo problema è stato risolto aggiungendo un nuovo avviso TRICKPLAY_ENDED_DUE_TO_ERROR per notificare all&#39;applicazione che trickplay è uscito e che il video è stato messo in pausa a causa di un errore irreversibile.

* Zendesk #19574 - TVSDK non restituisce i dati di risposta M3U8 per contenuti DRM o non DRM
Questo problema è stato risolto nei seguenti modi:

* Zendesk #19986 - Comportamento OP rotto per alcuni dispositivi come Android TV
* Aggiunta di un errore FILE_NOT_FOUND alla condizione.
* Quando l&#39;errore proviene da un errore *file non trovato*, separando l&#39;URL e la risposta dalla descrizione dell&#39;errore se la risposta è disponibile.
L&#39;errore logico introdotto dal supporto OP di NVidia è stato corretto. Sui dispositivi di protezione non NVidia, fidarsi dei flag di protezione del display anche quando il tipo di visualizzazione è sconosciuto.

* Zendesk #20549 - Gestione di playlist datate. Questo problema è stato risolto riducendo l’intervallo tra l’aggiornamento del manifesto live a metà della durata del segmento prevista, se il recupero precedente non riceve nuovi segmenti.

* Zendesk #20742 - L&#39;utilizzo della memoria sembra continuare ad aumentare durante la riproduzione di contenuti live su FireTV.L&#39;arresto anomalo è causato dalla tabella di riferimento degli oggetti JNI che ha raggiunto il limite. Questo problema è stato risolto eliminando il riferimento all&#39;oggetto MediaFormat creato durante il riavvio del decoder.

* Zendesk #21125 - Ritorno dall&#39;annuncio live/lineare all&#39;inizio (CSAI). È stata aggiunta una funzione che consente al lettore di tornare al contenuto principale durante un’interruzione pubblicitaria se il lettore registra la giunzione nei segnali pubblicitari utilizzando la giunzione nel rilevatore di opportunità.

* Zendesk #21334 - Valore di timeout della richiesta di annunci TVSDK per richiesta di annunci di terze parti. È stata aggiunta un’impostazione adRequestTimeout a AdvertisingMetadata che abilita un timeout globale per la chiamata dell’annuncio.

**Versione 1.4.21 (1566)**

* Zendesk #17781 - La schermata ADB non funziona più
Questo problema è stato risolto aggiungendo l&#39;API DefaultMediaPlayer.create(Context context, boolean secureSurface), che consente l&#39;acquisizione dello schermo.
Per consentire le acquisizioni dello schermo, passare false per secureSurface.
Importante: È consigliabile non abilitare questa funzione di acquisizione dello schermo in un’impostazione di produzione.

* Zendesk #19074 - Il fermo video durante il gioco di trucco FFWD e REW
Sono stati risolti i seguenti problemi che si verificavano durante il blocco del playback da parte di trickPlay:

* Zendesk #19532 - Chiudi didascalia appare fuori ordine
   * FHS avvia il trickplay, ma il primo segmento iframe non aveva un frame al suo interno.
   * Durante il download di un segmento iframe, se FHS raggiunge una condizione di errore, esce dal trickplay e mette in pausa la riproduzione.
   * L’implementazione di Android MediaCodec attende per sempre la disponibilità della coda di ingresso, mentre è stato richiesto di scaricare tutti i buffer di ingresso/uscita.
Questo problema è stato risolto invertendo l&#39;ordine dei suggerimenti WebVTT in modo che più suggerimenti sovrapposti sembrano &quot;scorrere verso l&#39;alto&quot;.

* Zendesk #19574 - Il TVSDK non restituisce i dati di risposta M3U8 per il contenuto DRM o non DRM
Nel caricamento iniziale del file manifesto in PTMediaPlayerItem.PrepareToPlay, se il caricamento non riesce, il TVSDK non segnala il corpo della risposta di errore all&#39;applicazione.
Questo problema è stato risolto consentendo al TVSDK di segnalare la risposta di errore come un errore all’applicazione.

* Zendesk #19701 - Blocco della riproduzione con SAP/Discontinuità
Il lettore si blocca quando l&#39;audio e il video non sono allineati a discontinuità è stato risolto.

* Bug #PTPLAY-11162 - È stato risolto l&#39;aggiornamento della libreria OpenSSL alla versione 1.0.2f.

**Versione 1.4.20 (1546)**

* Zendesk #17384 - Richiesta di funzioni: Supporto dei metadati ID3 per la riproduzione AAC
Il supporto per i tag ID3 nei file multimediali AAC è stato fornito nel TVSDK per Android a partire dalla versione 1.4.20.

* Zendesk #18358 - Il lettore blocca l&#39;interruttore del bitrate con discontinuità fuori sincrono
Questo problema è stato risolto gestendo in modo appropriato i casi limite di unione ABR.

* Zendesk #19232 - L&#39;app che utilizza TVSDK 1.4.18 si comporta stranamente sul vecchio sistema operativo Amazon versione 4
Questo problema è stato risolto rimuovendo la creazione della visualizzazione web nascosta nel processo di inizializzazione del lettore TVSDK per evitare conflitti con i dispositivi che non supportano Android Webview.

* Zendesk #19585 - Riproduzione slow-motion in caso di transizione a bitrate adattivo.
Durante lo switch ABR, se il nuovo profilo ha una frequenza di campionamento audio diversa dal profilo corrente, la riproduzione diventa veloce o slow motion. Questo perché al presentatore video non viene notificato che il formato audio è cambiato.
Questo problema è stato risolto assicurandosi che il flag di notifica sia impostato nel punto corretto.

* Zendesk #19683 - Riproduzione SAP DAI - Nessun audio per pochi secondi.
Per diversi casi nella logica di TVSDK, quando la marca temporale di due segmenti di rendering è stata confrontata, RENDITION_TIMEOUT_THRESHOLD è stato utilizzato come intervallo di valore accettabile, perché alla marca temporale non può sempre corrispondere una differenza di 0 ms. Se l&#39;intervallo è compreso nell&#39;intervallo di RENDITION_TIMEOUT_THRESHOLD, si presume che si tratti di una corrispondenza.

RENDITION_TIMEOUT_THRESHOLD è stato impostato a 100 ms, ma è risultato insufficiente per alcuni flussi. Questo problema è stato risolto aumentando il RENDITION_TIMEOUT_THRESHOLD a 200 ms.

* Zendesk #19699 - Il TVSDK non riesce a passare tra le tracce dei sottotitoli VTT
Questo problema è stato risolto creando il dump del lettore e ricaricando il manifesto quando un brano cambia e correggendo il problema di conversione delle stringhe UTF8 che influenzava i nomi dei brani della didascalia WebVTT a doppio byte.

* Zendesk #19717 - Problema di visualizzazione delle opzioni CC
Questo problema è stato risolto gestendo correttamente la stringa Unicode.

* Zendesk #19910 - I tag TIT2 ID3 non vengono rilevati
Questo problema è stato risolto fornendo supporto più completo per le codifiche di stringhe ID3 v2.4 e per il supporto per ID3 v2.3.

* Zendesk #20135 - Il TVSDK sta attivando più eventi onComplete per il contenuto VOD.
Questo problema è stato risolto aggiungendo il listener di eventi post_roll_complete al posto giusto, anziché al caso completo dell&#39;evento di modifica dello stato.

**Versione 1.4.19 (1521)**

* Zendesk #4180 - Il TVSDK non applica HDCP.
   * Questa è una correzione parziale per questo ticket e risolve solo il problema per i dispositivi di protezione NVidia.
Per tenere traccia dinamica dello stato HDCP, è necessario utilizzare l&#39;API di rilevamento HDCP correttamente implementata in Nvidia Shield.

* Zendesk #18358 - Il TVSDK si blocca su switch bitrate con discontinuità fuori sincrono.
   * Questo problema è stato risolto aggiungendo un nuovo avviso per rilevare la discontinuità PTS e forzando il controllo PTS a ripetere la ricerca del segmento corretto per ogni interruttore ABR.
Per correggere il blocco, la chiamata al metodo mediaPlayer.setCustomConfiguration deve includere forcePTSCheckForABR come argomento.

* Zendesk #19038 - Nessun flusso dal vivo su Asus Zenpad 10.

   Questo problema è stato risolto precaricando le informazioni del codec multimediale in modo da non eseguire query sulla funzione in fase di esecuzione.

* I seguenti problemi sono gli stessi di Zendesk #19038:
   * Zendesk #19483 - Il TVSDK si blocca sulla piattaforma Intel.
   * Zendesk #19171 - Arresti anomali su Asus Memo Pad 7 con Android 5.0.

**Versione 1.4.18 (1503)**

* Zendesk #3324 - Il reporting degli annunci Primetime non tiene traccia delle interruzioni pubblicitarie quando non vi sono annunci multimediali in un VMAP.
Quando un&#39;interruzione pubblicitaria è vuota, gli eventi di inizio e fine dell&#39;annuncio non venivano inseriti in un ping. Questo problema è stato risolto inviando ping di inizio dell&#39;interruzione pubblicitaria su interruzioni pubblicitarie vuote, come VMAP AdBreak, con un nodo AdSource valido.

* Zendesk #18229 - SetCCVisiblity(VISIBLE) viene ignorato dopo la chiamata a MediaPlayer.reset()
Questo problema è stato risolto aggiungendo setCCVisibility(Visibility.INVISIBLE); alla funzione reset() nella classe MediaPlayer.

* Zendesk #18328 - Problema di frame saltato su dispositivi Amazon Fire TV di seconda generazione per i contenuti con 60FPS
Questo problema è stato risolto applicando il FPS codificato per il processo decisionale del tempo di sonno e con una logica di previsione FPS meglio codificata.

**Versione 1.4.17 (1472)**

* Zendesk #2231 - Errore restituito dal recupero del manifesto non disponibile in MediaPlayerNotification
Questo problema è stato risolto includendo il corpo della risposta del manifesto in caso di errore di analisi.

* Zendesk #17703 - VideoEngineView non impedisce le schermate durante la riproduzione del video
Il metodo setSecure è disponibile dall’API 17, ma poiché l’API 17 copre le versioni 4.2, 4.2.1 e 4.2.2, non è noto quale genererà un’eccezione o se è specifico per il dispositivo. Questo problema è stato risolto racchiudendo VideoEngineView.setSecure nella clausola try catch.

* Zendesk #17919 - La ricerca del contenuto causa un errore di battito cardiaco
Errore di posizione dei dati di input non valido a causa della chiamata heartbeat generata quando la ricerca è stata avviata dopo il pre-roll. Questo problema è stato risolto.

**1.4.16a**  (1454a)

* Zendesk #18215 - Alcuni flussi AES non sono in grado di caricare.
Questo problema è stato risolto controllando la dimensione dei metadati DRM del profilo prima di caricare la chiave AES.

**Versione 1.4.16 (1454)**

* Zendesk #3875 - Tab S Arresto anomalo durante la riproduzione
Ripristino della dipendenza di OKHTTP su Auditude per CRS perché TVSDK ora utilizza direttamente httpurlconnection anziché curl. Il problema è stato risolto cancellando le eccezioni prima di effettuare qualsiasi altra chiamata JNI.

* Zendesk #4487 - Tracciamento del canale lineare dei contenuti
Il problema è stato risolto consentendo la riinizializzazione del tracciatore heartbeat video durante una sessione di riproduzione del flusso lineare.

* Zendesk #17919 - Android - la ricerca del contenuto causa l&#39;errore heartbeat
Il problema quando l&#39;heartbeat si trova in uno stato di errore quando si verifica una ricerca in un capitolo è stato risolto.

* Zendesk #18053 - Adobe Primetime si blocca su Marshmallow
Il TVSDK si bloccava su Android M OS quando la libreria TVSDK utilizzava il codice neon che esegue la conversione del colore YUV -> RGB. Il problema è stato risolto aggiornando le funzioni che causano questo problema utilizzando la versione non neon del codice.

* Zendesk #18072 - Android M - Arresto anomalo dell&#39;applicazione
Quando si controlla se il profilo e il livello sono supportati, si verifica un arresto anomalo durante la chiamata delle API MediaCodecList e MediaCodecInfo . Il problema è stato risolto caricando anticipatamente tutte le informazioni sul codec per evitare di chiamare queste API solo quando sono necessarie informazioni sul codec.

* Zendesk #18074 - Sottotitoli arabi non funzionanti su Nexus con Android 6.0
Il problema è stato risolto fornendo il supporto per la mappa dei font CTS per Android.

**Aggiornamento versione 1.4.15 (1438)**

* Zendesk #17437 - Ritardo lungo nell&#39;avvio dei contenuti VOD con alcuni flussi AES.
Per risolvere questo problema, se sono presenti più chiavi elencate in manifest, scarica in parallelo tutte le chiavi AES.

**Versione 1.4.15 (1435)**

* Zendesk #4278 - Glitches su Android set top box quando il bitrate adattivo cambia (ABR).
La correzione era di aggiungere il supporto per switch ABR senza soluzione di continuità con il codec multimediale Android più recente.

* Zendesk #17063 - Chiamando mediaPlayer.reset() si verifica un errore di reimpostazione del motore video.
La correzione consisteva nell&#39;includere il codice MediaErrorCode originale da VideoEngineExceptions durante l&#39;invio di ErrorEvents.

* Zendesk #17130 - Una pausa breve ma notevole quando si cambia il bit rate visto su FireTV.
(Come #4278 precedente) La correzione era quella di aggiungere il supporto per lo switch ABR senza soluzione di continuità con il codec multimediale Android più recente.

* Zendesk #17666 - Annunci aggiuntivi, Inaspettati o No Ads durante la ripresa del contenuto.
La correzione si è verificato un problema durante l&#39;esecuzione del contenuto PreparatoToPlay su video-on-demand (VOD), la ricerca iniziale viene eseguita sull&#39;ora locale anziché sull&#39;ora virtuale.

* Zendesk #17437 - Ritardo lungo nell&#39;avvio dei contenuti VOD con alcuni flussi AES.
La correzione era di scaricare tutte le chiavi AES in parallelo quando più chiavi sono elencate nel manifesto.

* Zendesk #17851 - Android TV - Black Frame durante ABR
La correzione era di specificare KEY_MAX_WIDTH e KEY_MAX_HEIGHT per abilitare la riproduzione adattiva.

**Versione 1.4.14 (1415)**

* Zendesk #3875 - Tab S Arresto anomalo durante la riproduzione.
Per evitare l&#39;arresto anomalo era necessaria un&#39;ulteriore correzione.

* Zendesk #17245 - Fallback su Android TV non funziona.
È stato risolto un problema aggiuntivo per cui la riproduzione si blocca quando il fallback è abilitato e la risposta VMAP ha un&#39;interruzione pubblicitaria vuota.

**Versione 1.4.14 (1412)**

* Zendesk #17245 - Fallback su Android TV non funziona.
È stata rimossa una restrizione per disabilitare la ricompilazione creativa sugli annunci di fallback.

**Versione 1.4.13 (1388)**

* Zendesk #3502 - Supporto di failover basato su client HLS durante un&#39;interruzione pubblicitaria
Consenti il failover al manifesto principale durante l&#39;aggiornamento dell&#39;errore del profilo attivo durante il periodo di interruzione degli annunci.

* Zendesk #3875 - Tab S Arresto anomalo durante la riproduzione
Per risolvere il conflitto tra HttpUrlConnection e cURLm, utilizza una libreria di terze parti.

* Zendesk #4450 - problema di impostazione di metadati personalizzati per un singolo posizionamento in un risolutore di contenuti
Aggiungi un setter alle impostazioni Opportunità.

**Versione 1.4.12 (1388)**

* Zendesk #2751 - CSAI e CRS | Miglioramento: Gestisci gli elementi dinamici in determinati URL di file multimediali.
È stato aggiornato Creative Repackaging Service per gestire correttamente gli annunci con URL creativi dinamici.

* Zendesk #3965 - Il passaggio alla riproduzione normale dal trickplay comporta un salto in avanti un po&#39; prima di avviare la riproduzione.
   * La correzione include TVSDK che restituisce il tempo prima della modifica della velocità fino a quando tutte le variabili non vengono aggiornate, invece di cercare di calcolare il GetStreamTime.
   * È stato corretto un arresto anomalo quando si cambiava la velocità di riproduzione del trucco vicino alla fine del flusso.
   * È stato corretto il calcolo del tempo corrente durante il gioco a tre.

* Zendesk #3978 - Trickplay a 8x e 16x spesso si congela.
   * Scegli sempre il profilo di gioco a trucco con il bit rate più basso per evitare buffering costante.
   * Aumenta l&#39;intervallo di salti per l&#39;alto tasso di gioco-trucco.
   * È stato corretto un problema a causa del quale il buffer continua a crescere dopo aver raggiunto la lunghezza di destinazione durante la riproduzione dei trucchi.

* Zendesk #3992 - Velocità aggiuntive di Trickplay.
TrickPlay è stato aggiornato per accettare tassi superiori a 16x; Sono ora consentiti anche +/- 32, +/-64 e +/-128.

* Zendesk #4007 - Interpretazione dell&#39;oggetto GEOB come parte dei metadati della timeline (Android e Web).
Sono state aggiunte le API setByteArray e getByteArray.

* PTPLAY-7301 - Avvio istantaneo al punto di accesso casuale.
Instant On è stato aggiornato per consentire un punto iniziale diverso da zero.

**Versione 1.4.11 (1363)**

* Zendesk #2076 - Otturatore frequente durante la riproduzione di video su Motorola Xoom con Android 4.0.3
Sono stati aggiunti dispositivi ad elenco consentiti per impedire che tentassero di riprodurre contenuti di alto profilo.

* Zendesk #2197 - `[Ads]` Tracciamento degli errori di annuncio
invia OperationFailedEvent con notifica di avviso.

* La macro Zendesk #3304 - VAST 3.0 `[ERRORCODE]` non viene compilata
   * il codice di errore 400 sarà esposto se l’annuncio in linea ha un’ottima creatività.
   * `[ERRORCODE]` macro sarà codificata in URL

**Versione 1.4.10 (1354)**

* Zendesk #2941 - Le risorse live non hanno &quot;0&quot; nell&#39;intervallo ricercabile
Precedentemente c&#39;era un buffer di 3 segmenti quando si cercava l&#39;inizio di un flusso live, ora è possibile cercare all&#39;inizio di un flusso live (cioè l&#39;inizio del primo segmento).

* Zendesk #3169 - Aggiorna il lettore di riferimento con l&#39;integrazione Adobe AnalyticsIl lettore di riferimento è stato aggiornato con la libreria Adobe Analytics come impianto di esempio.
* Zendesk #3299 - Comportamento inspiegabile del gioco di trucco
   * È stato corretto un bug a causa del quale il ritorno allo stato di riproduzione dopo l’arresto della riproduzione a trucco poteva richiedere diversi secondi (a volte più di 25 secondi).
   * È stato corretto un bug a causa del quale il trucco di richiamo può essere riprodotto una seconda volta sullo stesso supporto e il flusso può bloccarsi all’ora corrente.
* Zendesk #3433 - Android e Flash - Problemi con i sottotitoli

GetLine per WebVTT non rispettava una lunghezza &lt;CR>&lt;LF> regolata per un pacchetto; l’ultima didascalia può contenere caratteri provenienti da didascalie precedenti.

* PTPLAY-6243 - Migliora il lettore di riferimento per acquisire le informazioni di debug

I lettori di riferimento di esempio Android sono stati migliorati con un&#39;opzione per attivare i registri di debug e inviare i risultati via e-mail. Questa opzione si trova nel menu Log del lettore di riferimento.

**Versione 1.4.9 (1332)**

* Zendesk #2649 - Il buffer completo si verifica prima che il buffer iniziale sia pieno

Dopo una ricerca, possibile caso in cui il motore video imposta lo stato su PLAYING prima che il presentatore video sia pronto per la riproduzione. Si verifica quando lo stato del buffer è alto prima della ricerca. Correggere il problema notificando al motore video lo stato del buffer basso. Con il motore video a basso stato di buffer, la chiamata a Play causa la modifica dello stato a BUFFERING invece di PLAYING. La riproduzione riprende quando lo stato cambia in PLAYING.

* Zendesk #2846 - Richiesta di miglioramento: Fornire la possibilità di impostare diverse stringhe dell&#39;agente utente per le chiamate effettuate dalla libreria Auditude

È stata aggiunta una nuova API per impostare l’agente utente per le chiamate correlate agli annunci, auditudeSettings.setUserAgent(&quot;user/agent&quot;). Se non è impostato alcun agente utente, verrà utilizzato il valore predefinito. Questo influisce solo sull’agente utente per le chiamate correlate all’annuncio, l’agente utente per le chiamate multimediali rimane invariato, che è &quot;Adobe Primetime&quot;+&lt;agente utente predefinito>.

**Versione 1.4.8 (1324)**

* Zendesk #1218 - 106000.33 Errore con locale ... Se il caricamento del manifesto in FragmentalHTTPStreamer::ThreadParseManifest() non riesce, controlla se il dominio URL è localhost e, in tal caso, modifica il dominio in 127.0.0.1 e richiama ThreadParseManifest.
* Zendesk #3072 - Passaggio automatico a bit rate inferiori. È stato modificato il calcolo della lunghezza del buffer per saltare il payload PTS zero.
* Zendesk #3168 - Sottotitoli WebVTT visualizzati solo per i primi 10 secondi.
* Zendesk #3193 - È stata aggiunta la richiesta di una modifica API del profilo in TVSDK, PlaybackEventListener.onProfileChanged().

**Versione 1.4.7 (1311)**

* Zendesk #2197 - Tracciamento degli errori di annuncio. Aggiunta notifica per la risorsa non riuscita a caricare il manifesto
* Zendesk #2575 - PSDK ignora gli annunci in-stream personalizzati MARK prima del video
* Zendesk #2719 - Win Death with auditude ads, monitoraggio del beacon fisso quando reindirizzato all&#39;url relativo nel plugin auditude
* Zendesk #2760 - Tag DISCONTINUITY ignorato durante la modalità TrickPlay
* Zendesk #2805 - Arresto del giocatore all&#39;inizio della riproduzione, lo stesso fix di Zendesk #2719
* Zendesk #2817 - Lettore Android - Il giocatore a volte si blocca e smette di giocare, risolto estendendo i buffer di decodifica da 2.0 a 3.0 secondi
* Zendesk #2839 - Adobe Primetime PSDK supporta i chipset ARMv8?, aggiunta correzione per l&#39;arresto anomalo trovato su Galaxy S6.
* Zendesk #2885 - Riproduzione Auditude Crashing, stesso fix di Zendesk #2719
* Zendesk #2895 - Guasto HLS in tempo reale dopo 10 minuti di riproduzione
* Zendesk #2925 - Feedback sulla build Android dev (1.4.5), su alcuni dispositivi quando mettiamo in coda il pacchetto alla coda di ingresso, se il PTS è negativo, il decoder va in uno stato strano che otteniamo sempre un output negativo PTS per i pacchetti futuri. La correzione imposta l&#39;input PTS su zero se è negativo per evitare questo problema.
* PTPLAY-4645 - Disattivare il supporto crittografico RC4 in openssl. Sono disponibili sfruttazioni note per RC4. Ciò significa che se si tenta di connettersi a un server che supporta solo RC4, si verificherà un errore.

**Versione 1.4.6 (1282)**

* Zendesk #2192 - Il bitrate non diminuisce sempre in condizioni di rete scadenti, risolto rimuovendo l&#39;implementazione rapida dello switch.
* Zendesk #2631 - Sottotitoli in arabo su Android: Il testo su più righe appare tagliato, corretto regolando la dimensione del font per i font arabi.
* Zendesk #2844 - Buffering on Note 4 e il tempo di download del frammento non è accurato.

Questo problema è stato risolto aggiungendo la latenza tra i download dei segmenti video nel calcolo della larghezza di banda e avendo la logica di calcolo del tempo di download utilizzato il tempo di ciclo di richiesta completo.

* Zendesk #2908 - Sottotitoli arabi non funzionanti su Nexust 5, 6 e 7, risolti aggiungendo altri 2 font di fallback per gli script arabi.
* PTPLAY-4627 - aggiorna l&#39;appsdk di Nielson alla versione 1.2.3.7
* PTPLAY-5084 - Supporto di failover dell&#39;aggiornamento del manifesto Live Master

**Versione 1.4.5 (1248)**

* Zendesk #1757 - Solo l&#39;audio riprodotto o il lettore si arresta per alcuni profili di bit rate video, Nexus 4 e Nexus 7 crash fisso
* Zendesk #2072 - TimedMetadata per AdEvent non contiene l&#39;URL completo solo &quot;http&quot;
* Zendesk #2192 - Il bitrate non diminuisce sempre in condizioni di rete scadenti
* Zendesk #2256 - Accesso alla playlist principale, aggiornamento PSDK per l&#39;invio di eventi timedMetadata per tag sottoscritti sulla playlist principale.
* Zendesk #2269 - Sullo schermo compaiono due diverse lingue dei sottotitoli contemporaneamente a WebVTT
* Zendesk #2417 - Lettore che tenta di scaricare i sottotitoli prima dell&#39;avvio della riproduzione, WebVTT utilizzava la variabile del numero di segmento errata per la corrispondenza del numero di segmento. Un bug compariva solo per i file multimediali con indici di segmento a partire da zero.
* Zendesk #2470 - PSDK che non ritorna dallo stato SOSPESO quando il cambiamento del bitrate si verifica dopo la sospensione. In una situazione speciale quando la ricerca intelligente viene chiamata da RestoreGPUResource (ripristina il lettore dallo stato di sospensione) e l&#39;interruttore di flusso rilevato in precedenza, la ricerca intelligente non è in grado di completare e portare a buffering costante.
* Zendesk #2451 - Sottotitoli codificati &quot;bottom inset&quot;, aggiunto il parametro &quot;bottomInset&quot; al codice della didascalia
* Zendesk #2480 - Disabilitazione dell&#39;ottimizzazione del reindirizzamento HTTP 302. È stato aggiunto il supporto per l&#39;impostazione della proprietà useReindirizzaUrl
* Zendesk #2486 - beacon di terze parti
* Zendesk #2547 - Sottotitoli in arabo: Il testo deve essere allineato a destra

**Versione 1.4.4 (1195)**

* Zendesk #1158 - La riproduzione non riesce su Huawei Valiant (Y301A1)
* Zendesk #1709 - Dimensioni dei supporti errate e video allungato
* Zendesk #1757 - Solo audio riprodotto dopo l&#39;interruttore del profilo tra flussi con dati spa/pps identici
* Lo stato Zendesk #2095 - HTTP 307 (reindirizzamento) causa l&#39;arresto della riproduzione da parte del lettore Adobe
* Zendesk #2126 - Evento TimedMetaData mancante per l&#39;ultimo ADEVENT, i tag sottoscritti esistenti dopo l&#39;ultimo segmento non sono stati segnalati a PSDK da AVE
* Zendesk #2227 - Blocchi in VideoEngine nativeReset e nativePause
* Bug #3921755 - Aggiornamento della libreria OpenSSL alla versione 1.0.1L

**Versione 1.4.3 (1173)**

* Zendesk #1591 - RENDITION_M3U8_ERROR
* Zendesk #1870 - Accensione e spegnimento dei sottotitoli
* PTPLAY-1818 - Il gioco di trucco di riavvolgimento si ferma all&#39;annuncio invece di riavvolgere oltre di esso
* PTPLAY-2736 - Una didascalia WebVTT visualizzata in precedenza viene visualizzata sullo schermo al termine della riproduzione di un flusso con didascalia WebVTT
* PTPLAY-3773 - Un annuncio mid-roll non viene riprodotto quando si avvia la riproduzione del flusso dopo la posizione dell&#39;annuncio

**Versione 1.4.2**

* Zendesk #1561 - Supporto di failover basato su client HLS in primetime. Utilizzerà l&#39;ora della data del programma per risolvere il failover
* Zendesk #1590 - LoadInfo.MediaDuration è sempre 0 (non fisso per solo audio)
* Zendesk #1626 - Potenziale perdita di memoria nel lettore. Non si è verificata una perdita effettiva di memoria, si è verificato un problema con il salvataggio delle ultime 1000 notifiche da NotificationHistory, che è stato ridotto a 100.
* Zendesk #2192 - Il bitrate non diminuisce sempre in condizioni di rete scadenti

**Versione 1.4.1 (1121)**

* Zendesk #1951 - Blocco in VideoEngine.nativeReset() su dispositivi 4.0.x
* Zendesk #2064 - Nativo Crash SIGSEGV su specifici dispositivi Android basati su intel
* Zendesk #2075 - Blocco in VideoEngine.nativeReleaseGPUResource su dispositivi 4.0.x
Nota: Questa build è ***required*** per il supporto di Android 5.0 (Lollipop)
* Zendesk #1513 - Supporto Lollipop Android
* Zendesk #1709 - Dimensioni dei supporti errate e video allungato
* Zendesk #1871 - I sottotitoli WebVTT scompaiono occasionalmente e riappaiono quando si visualizza un livestream con i sottotitoli WebVTT
* Zendesk #1996 - Nessun indicatore della timeline visibile in PSDK 1.4.0
* Zendesk #2046 - Arresto anomalo con PSDK 1.4.1.1113, arresto anomalo corretto per i flussi live quando nessun annuncio viene restituito dall&#39;audience
* Bug #3769657 - Aggiorna la versione di curl a 7.38.0
* PTPLAY-1575 - Quando la riproduzione ABR inizia con lo streaming solo audio, passa allo streaming audio/video, il video non viene mai riprodotto mentre l&#39;audio continua
* PTPLAY-2499 - Aggiornamento a OpenSSL alla versione 1.0.1j per risolvere le vulnerabilità recenti
* PTPLAY-2632 - Il video non si recupera dopo il mid roll Ad completato su Android Lollipop
* PTPLAY-2678 - Fermo video durante i test di longevità in tempo reale su Android Lollipop

**Versione 1.4.0**

* Zendesk #1024 - Funzione per rimuovere l&#39;annuncio dal flusso tramite manifesto
* Zendesk #1293 - Problema di selezione della traccia dei sottotitoli codificati.
* Zendesk #1590 - LoadInfo.MediaDuration è sempre 0, mediaDuration mostra ora il valore corretto.
* Zendesk #1629 - il giocatore/l&#39;app si blocca alla fine della riproduzione dell&#39;annuncio su Galaxy S4
* Zendesk #1674 - ClosedCaption Non visualizzato, corretta visualizzazione della didascalia 708 quando mancano i codici ETX 0x03.
* PTPLAY-2157 - Gli stili di sottotitoli predefiniti sono stati restituiti da getters anche se dopo aver impostato e verificato visivamente uno stile diverso sul flusso. Le proprietà dello stile Didascalia chiusa ora mostrano il valore a cui sono state impostate.

## Problemi noti in 1.4 {#known-issues-in}

**Versione 1.4.31**

* PTPLAY-16803 - I sottotitoli non funzioneranno solo con contenuti audio, in quanto il sistema di sottotitoli necessita di video per funzionare. Senza video, non esiste una dimensione di visualizzazione e senza una dimensione di visualizzazione, non è possibile visualizzare alcun elemento grafico per i sottotitoli.
* PTPLAY-1634 - Lo stesso tag Sottoscritto ha marche temporali diverse in diverse finestre live. Quando le finestre attive si spostano, lo stesso tag deve avere le stesse marche temporali. Tuttavia, a volte anche gli stessi tag hanno marche temporali diverse.
* PTPLAY-3197 - Arresto anomalo con segnale 11 errore SIGSEGV sul dispositivo Acer Iconia dopo ~ 1 ora di riproduzione continua
* PTPLAY-3310 - Con un audio a bit rate inferiore, l&#39;audio diventa choppy/stuttery su Acer Iconia
* PTPLAY-3355 - WIN DEATH crash su Motorola Xoom con 4.0.x dopo ~ 1 ora di riproduzione continua.
* PTPLAY-3557 - Il riavvolgimento ad una pausa pubblicitaria sta portando il flusso a termine
* PTPLAY-7079 - La finestra di riproduzione sul client android non funziona con Secure Stop/Hard Stop
* Bug #3760144 - La risoluzione può cambiare o apparire all&#39;impulso quando il flusso viene messo in pausa su alcuni dispositivi come Kindle Fire 7 e Samsung Galaxy Nexus. Osservabile solo in stretta ispezione
* Bug #3761170 - findToLocal in Live with Ads non può cercare di nuovo i contenuti degli annunci, ma è meglio utilizzare le API CurrentTime per i flussi live
* Bug #3763370 - I flussi live con annunci mostreranno occasionalmente due ad markers vicini tra loro quando dovrebbe esserci solo uno. Questi ad marker rappresentano lo stesso annuncio e ne verrà riprodotto uno solo
* Bug #3763373 - Il marcatore pubblicitario può scomparire brevemente quando cerca oltre un annuncio nei flussi VOD. L&#39;indicatore pubblicitario viene ripristinato e non vi sono altri effetti negativi sulla timeline
* Alcuni dispositivi presentano problemi di riproduzione noti. Consulta [Problemi noti relativi ai dispositivi in 1.4](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14).
* Implementazione di riferimento: la riproduzione a blocchi non è implementata nell&#39;applicazione di esempio
* Su alcuni dispositivi Android TV è possibile visualizzare un fotogramma nero a causa di una reimpostazione del decoder ai seguenti punti di transizione:
   * in e fuori dalla modalità trickplay
   * commutazione tra le tracce audio in ritardo
   * da un annuncio al contenuto principale.

**Versione 1.4.23**

* La funzione Didascalia chiusa non funziona con contenuto solo audio, perché il sistema di didascalie richiede il funzionamento di un video. Senza video, non esiste una dimensione di visualizzazione e senza una dimensione di visualizzazione, non è possibile visualizzare alcun elemento grafico per i sottotitoli.
* A partire dalla versione 1.4.23, TVSDK non supporterà Gingerpane OS 2.3. Questo perché il TVSDK ha utilizzato le seguenti librerie Android private per raccogliere informazioni hardware sui dispositivi con Gingerpane OS:

   * `libstagefright.so`
   * `libcutils.so`

Nella versione Android N, Google ha rimosso l’accesso a queste librerie private. Il sistema operativo Gingerpane attualmente rappresenta meno dell&#39;1% della quota di mercato del sistema operativo Android a livello globale, quindi dopo la versione 1.4.23, il sistema operativo Gingerpane non sarà più supportato dal TVSDK.
Quando utilizzi la versione 1.4.23 (che include il supporto per Android N) o successiva:
* Aggiorna le tue app per utilizzare minSdkVersion 11.
* Se l&#39;utente finale esegue OS 2.3, la versione SDK è inferiore alla versione minSdkVersion dell&#39;applicazione. Il sistema interrompe l&#39;installazione o l&#39;aggiornamento dell&#39;applicazione.
* Se l&#39;utente finale esegue una versione superiore a OS 2.3, l&#39;applicazione verrà installata correttamente.

Se aggiorni minSdkVersion:

* Se l&#39;utente finale esegue il sistema operativo 2.3, l&#39;applicazione viene installata ma la riproduzione non funzionerà.
Questo vale sia per l&#39;aggiornamento che per la nuova installazione.
* Se l&#39;utente finale esegue un sistema superiore a OS 2.3, l&#39;app viene installata correttamente e il contenuto viene riprodotto correttamente.

**Versione 1.4.22**

* L’uscita anticipata dagli annunci non funziona con alcuni degli annunci mid-roll quando i tag splice-out e splice-in sono troppo vicini tra loro.

**Versione 1.4.2**

* Il riavvolgimento a un&#39;interruzione pubblicitaria sta portando il flusso a termine.

Media Player invia in modo errato MediaPlayer Player PlayerState.Completato durante l&#39;operazione di riavvolgimento di Trick Play quando raggiunge un limite pubblicitario. In caso contrario, l’SDK gestisce correttamente lo stato.

**Versione 1.4.0 (1086)**

* PTPLAY-1634 - Lo stesso tag Sottoscritto ha marche temporali diverse in diverse finestre live. Quando le finestre live si spostano, lo stesso tag in ognuna di esse deve avere le stesse marche temporali. Tuttavia, a volte anche gli stessi tag hanno marche temporali diverse.
* PTPLAY-2541 - COMPONENT_CREATION_FAILURE è talvolta visto dopo diversi switch a/dal flusso alternativo in blackout
* Bug #3726865 - Se un flusso LBA MultiBitrate inizia da un flusso solo audio, il video non verrà visualizzato se si passa a un flusso audio/video. L&#39;avvio da un flusso audio/video non visualizza questo problema e può passare con successo da un flusso audio a un flusso audio/video
* Bug #3760144 - La risoluzione può cambiare o apparire all&#39;impulso quando un flusso viene messo in pausa su alcuni dispositivi come Kindle Fire 7 e Samsung Galaxy Nexus. Osservabile solo in stretta ispezione
* Bug #3761170 - cercaToLocal in Live with Ads non può cercare di nuovo nel contenuto dell&#39;annuncio; è meglio utilizzare le API currentTime per i flussi live
* Bug #3763370 - I flussi live con annunci mostreranno occasionalmente due ad markers vicini tra loro quando dovrebbe esserci solo uno. Questi ad marker rappresentano lo stesso annuncio e ne verrà riprodotto uno solo
* Bug #3763373 - Il marcatore pubblicitario può scomparire brevemente quando cerca oltre un annuncio nei flussi VOD. L&#39;indicatore pubblicitario viene ripristinato e non vi sono altri effetti negativi sulla timeline
* Alcuni dispositivi presentano problemi di riproduzione noti. Per ulteriori informazioni, consulta [Problemi noti relativi ai dispositivi in 1.4](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14).
* Implementazione di riferimento: la riproduzione a blocchi non è implementata nell&#39;applicazione di esempio.

## Problemi noti relativi ai dispositivi in 1.4 {#known-device-issues-in}

| Dispositivo | Chipset | Problema | Causa | Soluzione alternativa |
|--- |--- |--- |--- |--- |
| Droid X | TI OMAP3 | È previsto un ritardo ABR poiché sta riavviando il decodificatore. |  |  |
| Desiderio HTC (diverso da HTC Desire HD) | QSD8250 | Impossibile riprodurre il video. Restituisce l&#39;errore VIDEO_PROFILE_NOT_SUPPORTED. | Desire non fornisce un decodificatore HW corretto. Fornisce il decodificatore SW di Stagefright. | Riavvia il dispositivo. |
| HTC EVO 4G | QSD8650 | Nessun decodificatore HW. | Qualcomm non ha un decodificatore HW. | Aggiornamento a Android 4.x. |
| Kindle FireSystem versione 6.0 | IT OMAP4 | Non riproduce flussi HLS. Il video su AIR non funziona. |  | Aggiornamento alla versione 6.3 del sistema. |
| Kindle Fire HD | IT OMAP4 | Può entrare in uno stato in cui non può riprodurre video. Restituisce gli errori VIDEO_PROFILE_NOT_SUPPORTED e UNRECOVERABLE_ERROR . | Il decodificatore HW si trova in uno stato irrecuperabile quando l’app non arresta completamente il decodificatore HW, ad esempio dopo un arresto anomalo. Si verifica anche sulle app native sul dispositivo. | Riavvia il dispositivo. |
| Kindle Fire HD 8.9 | Snapdragon 800 | L&#39;AVE si blocca dopo più interruttori ABR. |  |  |
| Motorola Atrix | Tegra2 | Problemi generali di prestazioni con AVE rispetto a AIR. Audio/video fuori sincronia, la riproduzione video si blocca dopo la riproduzione tra 9 e 15 minuti. Arresti anomali. | Possibilmente collegato a openGLES che attiviamo su AIR. Essere indagati. |  |
| Nexus 7 (2a generazione) | S4Pro APQ8064 (Qualcomm) | Il dispositivo si blocca quando un filmato viene messo in pausa per più di 30 minuti. | Problema del dispositivo segnalato a Google. | L&#39;app dovrebbe timeout per non consentire uno stato di pausa lungo. |
| Nexus S (GB) | Uccello Umanitario | Non è possibile riprodurre alcun video utilizzando il decodificatore HW. | Non esiste un decodificatore HW basato su Stagefright in Nexus S, quindi per Android 2.3 stiamo utilizzando un decoder SW. | Aggiornamento a ICS. |
| Nexus S (ICS) | Uccello Umanitario | I video di tanto in tanto lampeggiano. | Dati errati possono causare uno stato errato del decodificatore. | Riavvia il dispositivo. |
| Sistema operativo tablet Android Nook: 2.3. | IT OMAP 4 | Il video non viene riprodotto e l&#39;app si blocca. | Stagefright entra in uno stato instabile dopo aver eseguito l’app per alcune volte. Chiamate a mediaplayer::QueryCodecs appeso. | Riavvia il dispositivo per ripristinare lo stato. |
| Samsung Galaxy ACE | Qualcomm MSM7227 | Impossibile installare l&#39;app SampleMediaPlayer. | Utilizza ARM v6 invece del chipset ARM v7 più comune. FP/AIR non supporta questo dispositivo. |  |
| Samsung Galaxy ACE2Android OS: 2.3.6 | NovaThor U8500 | Impossibile riprodurre il video. | Questo chipset è un decodificatore sconosciuto per Android pre-ICS in AVE. |  |
| Samsung Galaxy S2 (GT-I9100) | Exynos | Le prestazioni video non sono all&#39;altezza di questo dispositivo. | Il decodificatore HW restituisce fotogrammi decodificati con PTS errato. Il decodificatore utilizza il tempo di decodifica anziché il tempo di presentazione. |  |
| Samsung Galaxy S2 GAndroid OS: 2.3.6 | IT OMAP4 | Arresto anomalo all’avvio del video. |  | Aggiornamento a Android 2.3.7 o 4.x. |
| Samsung Galaxy S3 (I747) | Qualcomm MSM8960 | A intermittenza, il video si blocca e solo l&#39;audio riproduce, quindi diventa non reattivo. |  |  |
| Samsung Galaxy S3 I747M | SAMSUNG_M2ATT | Il video si congela. | Indagare. |  |
| Samsung Galaxy Tab 1 v10.1 | Tegra 2 | La transizione MBR potrebbe richiedere fino a tre secondi. | Come correzione per gli arresti anomali di MBR, riavviamo il decodificatore per ogni interruttore di flusso, che può richiedere fino a tre secondi. |  |
| Samsung Galaxy Y |  | Impossibile installare l&#39;app SampleMediaPlayer. | Utilizza ARM v6 invece del chipset ARM v7 più comune. FP/AIR non supporta questo dispositivo. |  |
| Xoom | Tegra | Alcuni fotogrammi vengono eliminati per il passaggio. Il decodificatore non viene riavviato. | Limitazione OMXAL. |  |

## Risorse utili {#helpful-resources}

* Consulta la documentazione completa della guida nella pagina [Informazioni e supporto per Adobe Primetime](https://helpx.adobe.com/support/primetime.html) .
