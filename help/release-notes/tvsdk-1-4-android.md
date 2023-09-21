---
title: Note sulla versione di TVSDK 1.4 per Android
description: Le note sulla versione di TVSDK 1.4 per Android descrivono le novità o le modifiche, i problemi risolti e noti e i problemi del dispositivo in TVSDK Android 1.4.
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '7802'
ht-degree: 0%

---

# Note sulla versione di TVSDK 1.4 per Android {#tvsdk-for-android-release-notes}

Le note sulla versione di TVSDK 1.4 per Android descrivono le novità o le modifiche, i problemi risolti e noti e i problemi del dispositivo in TVSDK Android 1.4.

## Nuove funzioni {#new-features}

**Versione 1.4.43**

**Caricamento sicuro degli annunci tramite HTTPS**

Adobe Primetime fornisce un’opzione per richiedere la prima chiamata al server di annunci primetime e a CRS tramite HTTPS.

**alwaysUseAudioOutputLatency(valore booleano) nella classe MediaPlayer**

Quando questo parametro è impostato, utilizzate la latenza di uscita audio nel calcolo della marca temporale audio.

Accetta un valore di parametri booleani. Se il relativo valore è `True`, il client utilizza la latenza di output audio nel calcolo della marca temporale audio.

**Versione 1.4.42**

**Inserimento interruzione annuncio parziale:**
Esperienza simile alla TV, ovvero partecipare nel mezzo di un annuncio senza attivare il tracciamento dell’annuncio parzialmente guardato.
Esempio: l’utente si unisce al centro (a 40 secondi) di un’interruzione pubblicitaria di 90 secondi composta da tre annunci di 30 secondi. Questo è a 10 secondi dal secondo annuncio nell’interruzione.
* Il secondo annuncio viene riprodotto per la durata rimanente (20 secondi) seguito dal terzo annuncio.
* I tracker degli annunci per l’annuncio parziale riprodotto (secondo annuncio) non vengono attivati. I tracker solo per il terzo annuncio vengono sparati.

**Versione 1.4.41**

Nessuna nuova funzione.

**Versione 1.4.40**

Nessuna nuova funzione.

>[!NOTE]
>
>Se utilizzi una versione precedente al 1.4.39, non dovrai apportare modifiche API.

**Versione 1.4.39**

* TVSDK è certificato con VHL 2.0.1 e con VHL 2.0.1 con Nielsen.
* Android TVSDK è stato aggiornato per effettuare richieste CRS dal nuovo host Akamai `primetime-a.akamaihd.net`.
* La nuova configurazione del nome host fornisce la distribuzione delle risorse CRS tramite HTTP e HTTPS (SSL) su scala più ampia.
* TVSDK supporta la versione Android Oreo.
* Viene aggiunta una nuova funzione a `AdClientFactory` classe per supportare la registrazione di più rilevatori opportunità:

  ```
  public List<PlacementOpportunityDetector> createOpportunityDetectors(MediaPlayerItem item);
  ```

  Questo dovrebbe restituire un array di PlacementOpportunityDetector. Ora è possibile registrare più rilevatori di opportunità. Ad esempio, per la funzione di uscita anticipata dagli annunci, erano necessari due rilevatori di opportunità, uno per l’inserimento di annunci e un altro per l’uscita anticipata dagli annunci. È necessario implementare questa nuova funzione solo se è stato implementato AdvertisingFactory (e non si utilizza DefaultAdvertisingfactory). Per ottenere il comportamento esistente, è necessario creare un singolo rilevatore di opportunità, come nella funzione createOpportunityDetector(), inserirlo in un array e restituire:

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
>Se utilizzi una versione precedente al 1.4.39, non dovrai apportare modifiche API.

**Versione 1.4.36**

Correzione di bug per il contenuto Ignora su Android.

**Versione 1.4.35**

* **Informazioni sugli annunci di rete**

  Le API TVSDK ora forniscono informazioni aggiuntive sulle risposte VAST di terze parti. L’ID annuncio, il sistema di annunci e le estensioni degli annunci VAST sono forniti nella classe NetworkAdInfo accessibile tramite la proprietà networkAdInfo su una risorsa annuncio. Queste informazioni possono essere utilizzate per l’integrazione con altre piattaforme Ad Analytics come **Moat Analytics**.

**Versione 1.4.31**

**Supporto multi-CDN per annunci CRS**
* Per impostazione predefinita, tutte le risorse trascodificate saranno ospitate su CDN di proprietà dell’Adobe in Akamai. Con la versione più recente, Adobe Creative Repackaging Service (CRS) consente di caricare i contenuti creativi transcodificati su più CDN come specificato dal cliente.
* Vengono aggiunte nuove API a TVSDK per abilitare la specifica dell’URL creativo CRS finale quando non viene utilizzato l’URL predefinito. Per informazioni su come utilizzare queste nuove API, consulta la documentazione.

**Versione 1.4.18**
Primetime Android TVSDK ora supporta i creativi JavaScript VPAID 2.0 per consentire un’esperienza pubblicitaria interattiva in-stream avanzata. Per ulteriori informazioni su VPAID 2.0, vedere [Supporto per annunci VPAID](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/vpaid-ads/android-3x-vpaid-ads.md).

**Versione 1.4.17**

AC-3 5.1 è supportato solo su Amazon FireTV.

**Versione 1.4.11**

* **Fallback degli annunci, concatenamento a margherita nella logica di selezione degli annunci (#3103 Zendesk** Per gli annunci VAST (creativi) con la regola di fallback abilitata, TVSDK tratta un annuncio con un tipo MIME non valido come annuncio vuoto e tenta di utilizzare gli annunci di fallback al suo posto. Puoi configurare alcuni aspetti del comportamento di fallback.

Per ulteriori informazioni, consulta [Fallback degli annunci per annunci VAST e VMAP](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-fallback/android-3x-ad-fallback.md).

* **Video Heartbeats Library (VHL) aggiornato alla versione 1.5**
   * Possibilità di inviare metadati con avvio video e/o inizio video/annuncio/capitolo come dati contestuali
   * Traffico di rete ridotto: gli heartbeat sono in media meno numerosi e di dimensioni più ridotte

**Versione 1.4.7**

* **Supporto per la personalizzazione on-premise** Supporto per le installazioni on-premise di Adobe Individualization Server per personalizzare la richiesta di personalizzazione del client in modo da passare a un endpoint diverso.

**Versione 1.4.6**

* **Crittografia AES di esempio (richiede la versione di Flash Player 17.0.0.134)**La crittografia AES basata su esempio è ora supportata.

**Versione 1.4.2**

* **Aggiornamento Video Heartbeats Library (VHL) alla versione 1.4.0.1**

   * Con Adobe Analytics Video Essentials è stata aggiunta la possibilità di unire diversi casi di utilizzo di analisi da altri SDK o lettori.
   * Il tracciamento degli annunci è stato ottimizzato rimuovendo i metodi trackAdBreakStart e trackAdBreakComplete. L’interruzione pubblicitaria viene dedotta dalle chiamate dei metodi trackAdStart e trackAdComplete.
   * La proprietà della testina di riproduzione non è più necessaria durante il tracciamento degli annunci.

* **Integrazione di Nielsen SDK** TVSDK ora supporta l’invio di informazioni di tracciamento degli utenti all’SDK Nielsen senza alcuna integrazione personalizzata.

**Versione 1.4.0**

* **Segnalazione Di Sospensione Attività Con Sostituzione Contenuti Alternativa** Come parte dell’aggiornamento 1.4 TVSDK, ora TVSDK supporta anche l’entrata e la restituzione da blackout regionali rispetto ai contenuti lineari. TVSDK è ora in grado di elaborare due file manifest in parallelo, principale e alternativo, per monitorare i segnali di blackout anche quando viene mostrata una programmazione alternativa al posto della programmazione originale.

* **Rimuovi/Sostituisci annunci C3** Ora non è necessario alcun lavoro di preparazione aggiuntivo per inserire dinamicamente nuovi annunci nelle risorse video on demand (VOD) che escono dalla finestra C3. TVSDK ora fornisce un’API per rimuovere intervalli di contenuti personalizzati e inserire dinamicamente nuovi annunci. Questa nuova potente funzionalità è utile anche nei casi in cui i contenuti live/lineari vengano trasmessi durante la trasmissione e vengono immediatamente abbassati per essere utilizzati come contenuti on-demand senza il tempo necessario per &quot;ripulire&quot; la risorsa.

* L&#39;interfaccia PlaybackEventListener dispone di un nuovo metodo denominato onReplaceMediaPlayerItem, che è possibile utilizzare per ascoltare un nuovo evento. `ITEM_REPLACED`. Questo evento viene inviato ogni volta che un&#39;istanza MediaPlayeritem viene sostituita in MediaPlayer. L&#39;applicazione client che implementa PlaybackEventListener deve implementare o eseguire l&#39;override del nuovo metodo.
* AdClientFactory ha aggiunto una nuova funzione alla classe per la registrazione di più rilevatori di opportunità:

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

* L&#39;interfaccia PlaybackEventListener dispone di un nuovo metodo denominato onReplaceMediaPlayerItem, che può essere utilizzato per ascoltare un nuovo evento, ITEM_SUBSTITUTE. Questo evento viene inviato ogni volta che un&#39;istanza MediaPlayeritem viene sostituita in MediaPlayer. L&#39;applicazione client che implementa PlaybackEventListener deve implementare o eseguire l&#39;override del nuovo metodo.

* AdClientFactory ha aggiunto una nuova funzione alla classe per la registrazione di più rilevatori di opportunità:

```
public List`<PlacementOpportunityDetector>` createOpportunityDetectors(MediaPlayerItem item);
```

Ad esempio, per la funzione di uscita anticipata da un annuncio, sono necessari due rilevatori di opportunità, uno per l’inserimento di annunci e l’altro per l’uscita anticipata dall’annuncio.

Per ignorare questa nuova funzione, crea un singolo rilevatore di opportunità, inseriscilo in un array e restituisce:

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
>Le seguenti funzioni sono **non** supportato in TVSDK:
>
>* Slow motion, su qualsiasi piattaforma o versione.
>* Gioco di trucco dal vivo.

**Versione 1.4.43**

TVSDK 1.4.43 è stato certificato con dispositivi Android con Android 6.0.1/ 7.0 e 8.1 (Oreo).

* **Versione 1.4.23:**

   * TVSDK 1.4.23 è stato certificato per dispositivi Android con Android N.

* **Versione 1.4.18:**

   * Primetime è stato certificato per Amazon Fire TV.
   * VPAID 2.0 è supportato solo su dispositivi con Android 4.0 e versioni successive.

## Problemi risolti in 1.4 {#resolved-issues-in}

>[!NOTE]
>
>Tutti i clienti TVSDK che utilizzano CRS sono vivamente invitati ad effettuare l’aggiornamento a TVSDK 1.4.39 o versione più recente su iOS e Android. Questo aggiornamento sostituisce l’implementazione dell’app esistente. Dopo l’aggiornamento, controlla le richieste dell’URL creativo di CRS in uno strumento proxy (ad esempio, Charles) per verificare che la versione nel percorso rifletta la versione 3.1. Ad esempio:
>
>`https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8`

**Versione 1.4.43**

* Ticket #27143 - Impossibile riprodurre la traccia audio 5.1 sui dispositivi FireTV

   * TVSDK è ora in grado di riprodurre audio AC3 su dispositivi FireTV. La riproduzione è sempre in stereo.

* #33902 ticket - Consegna sicura degli annunci tramite HTTPS

   * Adobe Primetime fornisce un’opzione per richiedere la prima chiamata a primetime ad server e CRS su https.

* #34493 ticket - Ritardo audio Bluetooth

   * Aggiunto `alwaysUseAudioOutputLatency` nella classe MediaPlayer che, se impostata, determinerà l&#39;utilizzo della latenza di output audio nel calcolo della marca temporale audio.

* Ticket #34949: nuova versione della libreria heartbeat video (VHL) integrata.

**Versione 1.4.42 (1791)**

* Zendesk #33719: FireTV 4k Adaptive Bitrate si adatta lentamente. È stato aggiunto il supporto per ABR per dispositivi FireTV 4K.
* #33338 Zendesk: resetDRM cancella tutti i dati dell&#39;applicazione.  È stato gestito un caso aggiuntivo in cui le eccezioni nei thread non TVSDK causavano il riempimento delle code delle operazioni TVSDK.

**Versione 1.4.41 (1776)**

* Zendesk #33002 - Dati sugli asset da TVSDK su Fire TV. È stata implementata una nuova classe AdBannerAsset che restituirà i dati Companion come Elenco. &lt;adbannerasset> e AdAsset::id ora è una stringa invece di una lunga.
* Zendesk #32821 - Il lettore Android Primetime si blocca quando incontra la marca temporale della presentazione (PTS) per WWE. Questo problema è stato risolto con questa versione.
* #33572 Zendesk - Arresto anomalo di VideoAnalyticsProvider Ad Start. Questo problema è stato risolto utilizzando la giusta combinazione della versione SDK congiunta VHL+Nielsen di VideoHeartbeat.jar.
* Zendesk #33355 - Fire TV: Scrub back 15 secondo numero. Nessuna correzione dal lato TVSDK e il cliente sta verificando questo problema alla propria Fine e terze parti.

**Versione 1.4.40 (1764)**

* Zendesk #33068 - Problema di sincronizzazione labiale di Amazon sul nuovo dispositivo. In queste versioni è stato risolto un problema di sincronizzazione delle labbra.
* Zendesk #32215 - Problemi di sicurezza di Android TVSDK 1.4.38 `[Hotlist]`. Aggiornato ai più recenti OpenSSL-1.1.0 e curl-7.55.1.
* #32920 Zendesk - Schermata vuota all’interno di un’interruzione pubblicitaria e nessun completamento di interruzione pubblicitaria. È stato risolto un problema che causava il blocco di un contenitore VPAID e gestiva un problema a causa del quale gli annunci VPAID di Facebook spesso restituivano più blocchi CDATA in un singolo nodo \&amp;lt;AdParameters\&amp;gt; VAST.

**Versione 1.4.39 (1744)**

* #28976 Zendesk - La richiesta di licenza richiede più di un secondo. Durante l’esecuzione delle chiamate di richiesta della licenza DRM che utilizzano POST, Curl aggiunge un’intestazione aggiuntiva &quot;Expect: 100-continue&quot;. Intestazione &quot;Expect:&quot; rimossa in TVSDK.
* Zendesk #27707 - Ambienti CSAI che non rispettano i marker CUE IN per un ritorno anticipato al contenuto. Fornito supporto per più generatori di opportunità.

**Versione 1.4.38 (1722)**

* #21590 Zendesk - Prestazioni video e monitoraggio nelle build più recenti

Integrazione e certificazione VHL 2.0 in TVSDK per ridurre la barriera nell’implementazione VideoHeartbeatLibrary riducendo la complessità delle API.

* Zendesk #29688 - Supporto per i clienti Android O Beta.

Supporto TVSDK per la nuova versione Android Beta.

**Versione 1.4.36 (1713)**

* Zendesk #27392 - Contenuto da saltare su Android

Per adattarsi alla decrittografia, il TVSDK per Android stava erroneamente ampliando l&#39;intervallo di byte del contenuto non-iframe di 16 byte. L’allargamento è necessario per i flussi Iframe ma non per i flussi non-iframe.

**Versione 1.4.34 (1702)**

* #27638 Zendesk - Perdita nell’oggetto INet cURL

Perdita dell&#39;oggetto INet cURL Posix in corso durante il mantenimento nella gestione delle condivisioni e nella cache DNS utilizzate nelle connessioni cURL.

Questo problema è stato risolto eliminando l&#39;oggetto INet cURL Posix dal decostruttore INet.

**Versione 1.4.33 (1694)**

* **Libreria OpenSSL**

La libreria OpenSSL è stata aggiornata con la versione 1.0.2j di OpenSSL.

* Zendesk #21701 - Invia l’URL creativo originale per la richiesta 1401 CRS invece dell’URL normalizzato.
Questo problema viene risolto inviando gli URL creativi originali.

* Zendesk #25023 - Riproduzione video di lunga durata: blocco video, sfarfallio dello schermo Questo problema è stato risolto impostando le dimensioni massime del formato video per i dispositivi set-top box CenturyLink.

* #27460 Zendesk - Il nuovo account Akamai non è in grado di gestire una richiesta CDN di POST.
Il codice è stato aggiornato per rendere `cdn.auditude.com` richiesta annuncio da GET anziché POST.

* Zendesk #28245 - Lo stato di riproduzione non viene notificato correttamente quando l’app passa dal background al primo piano. Questo problema è stato risolto ripristinando correttamente lo stato di riproduzione in modo che venga riprodotto o messo in pausa quando l’applicazione ritorna in primo piano.

**Versione 1.4.32 (1682)**

* Zendesk #25779 - La vulnerabilità di sicurezza rilevata con TVSDK Android 4.2 e versioni successive presenta una vulnerabilità di sicurezza quando JavaScript è abilitato in un WebView. L&#39;utilizzo di WebView da TVSDK è stato disattivato per i dispositivi che eseguono OS 4.2 o versione successiva. Questo disabilita l’uso degli annunci VPAID in TVSDK su questi dispositivi.

* Zendesk #26890 - Problema nello stato SCREEN (ON/OFF) gestione Rif. Lettore Quando il motore video di Adobe (AVE) riprende da uno stato SUSPENDED, DefaultMediaPlayer non aggiorna il proprio stato. Di conseguenza, DefaultMediaPlayer rimane in stato SOSPESO anche se AVE è in stato RIPRODUZIONE. Questo problema è stato risolto impostando lo stato DefaultMediaPlayer su PLAY quando si riceve lo stato PLAY dall&#39;AVE, anche se lo stato corrente di DefaultMediaPlayer è SUSPENDED.

**Versione 1.4.31 (1675)**

* #21974 Zendesk - Eccezioni dovute a oggetti nulli
   * AdIndex viene raramente incrementato quando null. Ciò potrebbe essere dovuto a chiamate API non corrette ricevute per adBreak pre-roll. Sono stati corretti i tipi di dati per evitare tali eccezioni.

* Zendesk #24714 - Disattiva registrazione estranea
   * TVSDK è stato aggiornato per disattivare la registrazione estranea

* Zendesk #24488 - Problemi di sincronizzazione AV su Fire TV
   * Risolto migliorando la gestione dei thread del decodificatore AV. Nello specifico, ogni volta che vengono modificate le code dei frame di input o di output, viene eseguito il thread di decodificazione specifico per il tipo di contenuto del frame.

* #26551 Zendesk - Correzione degli errori CRS
   * Quando la richiesta è HEAD (http head), non è necessario leggere il contenuto perché è vuoto. Anche se va bene provare a leggerlo, il vecchio Android (4.0.x) si blocca mentre si chiama read() e il nuovo Android restituiscono il valore corretto (-1) quando si chiama read(). In base a questo, è stato modificato il codice in modo da non leggere il contenuto per &quot;head&quot;

* Eccezione Zendesk #26696 Null Pointer durante l’accesso a TrickPlayManager
   * È stato corretto verificando se l’oggetto TrickPlayManager non è nullo prima di utilizzarlo.

**Versione 1.4.30 (1659)**

* Zendesk #22675 la durata della risorsa non viene aggiornata per i flussi live/lineari. Questo problema è stato risolto fornendo una nuova API, assetDuration, in PTVideoAnalyticsTrackingMetadata che fornisce la durata della risorsa per i flussi live e lineari.

* Zendesk #25853 Perdita di memoria in TVSDK quando si passa da un canale all’altro Il problema di una perdita di buffer di lettura file quando MediaPlayer viene reimpostato o rilasciato durante il download di un file è stato risolto.

**Versione 1.4.29 (1653)**

* Zendesk #21200 - Il lettore non viene ripristinato dallo stato sospeso quando l’app era in background Quando il lettore è stato sospeso dopo il segnale di passaggio di flusso, la risoluzione consente al lettore di eseguire il passaggio di flusso quando ripristina il lettore dallo stato di sospensione, invece di ripristinare la posizione precedente.

* Zendesk #23412 - Il lettore è bloccato con una scatola nera se si fa clic su qualsiasi annuncio entro gli ultimi 3 secondi dell&#39;interruzione pubblicitaria Questo problema è lo stesso di Zendesk #21200.

* #23616 Zendesk - L’interruzione pubblicitaria saltata è troppo lontana nel futuro A seconda del tipo di inserimento dell’annuncio (inserisci/sostituisci), TVSDK determina se la durata dell’annuncio viene utilizzata nel calcolo per determinare il punto finale dell’interruzione pubblicitaria.

* Zendesk #25078 - Perdita di memoria DRM TVSDK su STB TV Android La perdita di memoria per l&#39;oggetto adattatore DRM è stata individuata e risolta.

* #25067 Zendesk - Arresto anomalo in VideoEngineTimeline Questo problema si verifica perché gli oggetti non sono stati puliti correttamente e gli eventi sono stati chiamati dopo la distruzione degli oggetti. Il problema è stato risolto aggiungendo assegni per evitare eccezioni Null.

* Zendesk #25352 - Impostare un’intestazione HTTP personalizzata Questo problema è stato risolto aggiungendo una nuova intestazione personalizzata all’elenco consentiti su TVSDK.

* Zendesk #25617 - Rollover del PTS in streaming live che causa discontinuità del lettore e arresto anomalo della memoria Questo problema è stato risolto aggiungendo una gestione del rollover del PTS in FragmentedHTTPStreamer quando si verifica un rollover nel mezzo di un segmento.

**Versione 1.4.28 (1637)**

* #23618 Zendesk - Gli eventi di interruzione dell’annuncio si attivano prima che venga consultato il criterio dell’annuncio. Questo problema è stato risolto non attivando gli eventi AD_BREAK_START e AD_START quando l’annuncio viene saltato a causa di adForgiveness. Viene invece inviato l&#39;evento AD_BREAK_SKIPPED.

**Versione 1.4.27 (1631)**

* Zendesk #23174 - Problema di prestazioni durante il ridimensionamento del video Questo problema è stato risolto fornendo una nuova API, MediaPlayerView.setSurfaceFixedSize, che consente a TVSDK di accedere a SurfaceHolder.setFixedSize() da MediaPlayerView.

* Zendesk #24450 - TVSDK effettua richieste di annunci duplicate Questo problema si è verificato quando il tempo trascorso è stato convertito in lungo e non in doppio e il problema è stato risolto.

**Versione 1.4.26 (1627)**

* Zendesk #21436 - Aggiornamento libreria OpenSSL alla versione 1.0.2h Aggiornamento libreria OpenSSL alla versione 1.0.2h
* Zendesk #23825 - I cookie non vengono inclusi nei callback corretti fornendo il supporto per i cookie android.

**Versione 1.4.25 (1620)**

* Zendesk #22900 - Il flusso DRM Live Adobe Primetime non viene riprodotto sul lettore di riferimento Android. Il problema di allocazione della memoria è stato risolto.
* Zendesk #23176 - L’applicazione si blocca quando si tenta di riprodurre annunci VPAID L’arresto anomalo si è verificato perché l’applicazione non crea una visualizzazione annuncio personalizzata per il rendering di un annuncio VPAID. Questo problema è stato risolto ignorando gli annunci VPAID nella risposta dell’ad server quando non è presente una visualizzazione annuncio personalizzata.

* Zendesk #23153 - SampleAES DRM Stream - Arresto della riproduzione nel lettore di riferimento TVSDK Questo problema è lo stesso di Zendesk #22900.

**Versione 1.4.24 (1612)**

* Zendesk #20784 - Analytics: attivazione della completezza dei contenuti per le transizioni video live Questo problema è stato risolto aggiungendo un’API (trackVideoComplete) per attivare manualmente il completamento dei contenuti durante una sessione di tracciamento video live/lineare.

* Arresto anomalo di Zendesk #21977 VideoEngineTimeline durante l’operazione placeAdBreak/acceptAd
   * In questo problema sono state aggiornate le seguenti librerie:
      * Libreria AdobeMobile alla versione 4.10.0
      * Libreria VHL alla versione 1.5.6
      * VHL-Nielsen alla versione 1.6.7

Questo problema è stato risolto aggiungendo un controllo null prima di aggiungere annunci all’elenco di annunci accettati.

* Zendesk #22313 Il bitrate per gli STB con chipset Amilogic non va oltre 1,2 MB. Questo problema è stato risolto precaricando le funzionalità del codec multimediale e disabilitando lo switch senza soluzione di continuità per i dispositivi chipset Amilogic.

* Zendesk #19520 la risorsa campione AES HLS non viene riprodotta nei lettori TVSDK. Questo problema è stato risolto gestendo più descrittori PMT per i flussi HLS crittografati AES di esempio.

**Versione 1.4.23 (1602)**

* Zendesk #18852 - Aggiorna la logica di selezione creativa in base alle regole CRS Questo problema è stato risolto aggiungendo un file di configurazione JSON per specificare la priorità della selezione creativa.

* Zendesk #20861 - Android N Questa versione fornisce il supporto per Android N rimuovendo la possibilità di utilizzare direttamente le librerie native della piattaforma Android che non sono più accessibili alle applicazioni che vengono eseguite su Android N.

* Zendesk #21018 - Arresto anomalo di Android N Stessa risoluzione di ZD# 20861.

* Zendesk #21266 - VideoEngineAdapter si arresta in modo anomalo in seguito a un errore Invalid_Key L&#39;errore Invalid_Key non include una descrizione da AVE, pertanto l&#39;analisi del testo ha generato un errore NPE. Il problema è stato risolto aggiungendo un controllo null per la descrizione durante onError prima di analizzare la descrizione.

* Zendesk #22286 - La libreria nativa sta allocando memoria lettura chiave/frammento causando l&#39;arresto anomalo Questo arresto anomalo che si è verificato su Android durante il tentativo di caricare un manifesto con più chiavi contemporaneamente è stato corretto.

**Versione 1.4.22 (1581)**

* Zendesk #17236 - Tempo di riproduzione inaffidabile per i video HLS con DRM È stato corretto il salto temporale con i flussi LBA, in cui l’ora di inizio del segmento audio non corrisponde all’ora di inizio del segmento video.

* Zendesk #17680 - La riproduzione video è bloccata sulla finestra Selevision Andredo Box Il decodificatore video su questo dispositivo a volte restituisce un salto significativo del tempo di uscita quando si rimuove il fotogramma video dal buffer di uscita, e questo timestamp di uscita rimane alto. Il problema è stato risolto restituendo un *profilo video non supportato* errore che non forza il lettore a riprovare lo stesso profilo o a scegliere un profilo diverso.

* #19074 Zendesk - Blocco video durante la riproduzione con i trucchi FFWD e REW Questo problema è stato risolto aggiungendo un nuovo avviso TRICKPLAY_ENDED_DUE_TO_ERROR per notificare all’applicazione l’uscita dal gioco e la sospensione del video a causa di un errore irreversibile.

* Zendesk #19574 - TVSDK non restituisce i dati di risposta M3U8 per contenuti DRM o non DRM Questo problema è stato risolto nei seguenti modi:

* Zendesk #19986 - Comportamento OP interrotto per alcuni dispositivi come Android TV
* Aggiunta di un errore FILE_NOT_FOUND alla condizione.
* Quando l’errore proviene da un *file non trovato* errore, separando l’URL e la risposta dalla descrizione dell’errore, se la risposta è disponibile.
L’errore logico introdotto dal supporto di NVidia shield OP è stato corretto. Sui dispositivi di schermatura non NVidia, considerare attendibili i flag di protezione della visualizzazione anche quando il tipo di visualizzazione è sconosciuto.

* Zendesk #20549 - Gestione di playlist obsolete. Questo problema è stato risolto riducendo l’intervallo tra l’aggiornamento del manifesto live a metà della durata prevista del segmento, se il recupero precedente non riceve nuovi segmenti.

* #20742 Zendesk - L&#39;utilizzo della memoria continua a crescere durante la riproduzione di contenuti in diretta su FireTV.L&#39;arresto anomalo è causato dalla tabella di riferimento degli oggetti JNI che ha raggiunto il limite. Il problema è stato risolto eliminando il riferimento all&#39;oggetto MediaFormat creato durante il riavvio del decodificatore.

* #21125 Zendesk - Ritorno dal live/lineare ad break early (CSAI). È stata aggiunta una funzione che consente al lettore di tornare al contenuto principale durante un’interruzione pubblicitaria se registra il giunto nei segnali pubblicitari utilizzando il giunto nel rilevatore di opportunità.

* #21334 Zendesk - Valore di timeout della richiesta di annunci TVSDK per richieste di annunci di terze parti. A AdvertisingMetadata è stata aggiunta l’impostazione adRequestTimeout che abilita un timeout globale per la chiamata dell’annuncio.

**Versione 1.4.21 (1566)**

* Zendesk #17781 - L’acquisizione schermata ADB non funziona più Questo problema è stato risolto aggiungendo l’API DefaultMediaPlayer.create(Context context, boolean secureSurface), che consente l’acquisizione schermo.
Per consentire le acquisizioni dello schermo, passare false per secureSurface.
Importante: si consiglia vivamente di non abilitare questa funzione di acquisizione schermo in un&#39;impostazione di produzione.

* Zendesk #19074 - Blocco video durante la riproduzione dei trucchi FFWD e REW Sono stati risolti i seguenti problemi che si verificavano quando il trickPlay poteva bloccarsi nella riproduzione:

* #19532 Zendesk - La funzione Close Caption non è nell&#39;ordine corretto
   * FHS avvia il trickplay, ma il primo segmento iframe non aveva un frame in esso.
   * Durante il download di un segmento iframe, se FHS riscontra una condizione di errore, esce dalla modalità trickplay e mette in pausa la riproduzione.
   * L’implementazione di Andorid MediaCodec attende per sempre la disponibilità della coda di input mentre gli è stato richiesto di scaricare tutti i buffer di input/output.
Questo problema è stato risolto invertendo l’ordine dei cue WebVTT in modo che più cue sovrapposti appaiano &quot;scorrere verso l’alto&quot;.

* #19574 Zendesk - TVSDK non restituisce i dati di risposta M3U8 per contenuto DRM o non DRM Nel caricamento iniziale del file manifesto in PTMediaPlayerItem.preparationToPlay, se il caricamento non riesce, TVSDK non segnala il corpo della risposta di errore all&#39;applicazione.
Questo problema è stato risolto consentendo a TVSDK di segnalare la risposta di errore come errore all’applicazione.

* Zendesk #19701 - Blocco della riproduzione con SAP/Discontinuità Il lettore si blocca quando audio e video non sono allineati alla discontinuità è stato risolto.

* #PTPLAY-11162 bug: l’aggiornamento della libreria OpenSSL alla versione 1.0.2f è stato risolto.

**Versione 1.4.20 (1546)**

* Zendesk #17384 - Richiesta di funzionalità: il supporto dei metadati ID3 per il supporto della riproduzione AAC per i tag ID3 nei supporti AAC è stato fornito in TVSDK per Android a partire dalla versione 1.4.20.

* Zendesk #18358 - Il lettore si blocca sullo switch bitrate con discontinuità fuori sincronizzazione. Questo problema è stato risolto gestendo in modo appropriato i casi limite di unione ABR.

* Zendesk #19232 - L’app che utilizza TVSDK 1.4.18 si comporta in modo anomalo sulla versione precedente del sistema operativo Amazon 4. Questo problema è stato risolto rimuovendo la creazione della visualizzazione web nascosta nel processo di inizializzazione del lettore TVSDK per evitare conflitti con dispositivi che non supportano Android Webview.

* Zendesk #19585 - Riproduzione slow-motion in caso di transizione del bitrate adattivo.
Durante l&#39;interruttore ABR, se il nuovo profilo ha una frequenza di campionamento audio diversa rispetto al profilo corrente, la riproduzione diventa veloce o slow motion. Ciò si verifica perché il presentatore video non riceve alcuna notifica relativa alla modifica del formato audio.
Questo problema è stato risolto accertandosi che il flag di notifica sia impostato nel punto corretto.

* #19683 Zendesk - Riproduzione DAI SAP - Audio assente per alcuni secondi.
Per diversi casi nella logica di TVSDK, quando è stata confrontata la marca temporale di due segmenti di rendering, è stato utilizzato RENDITION_TIMEOUT_THRESHOLD come intervallo di valori accettabile, perché la marca temporale non può sempre essere associata a una differenza di 0 ms. Se il gap è compreso nell&#39;intervallo RENDITION_TIMEOUT_THRESHOLD, si presume che corrisponda.

RENDITION_TIMEOUT_THRESHOLD è stato impostato su 100 ms, ma è risultato insufficiente per alcuni flussi. Questo problema è stato risolto aumentando la soglia RENDITION_TIMEOUT_THRESHOLD a 200 ms.

* Zendesk #19699 - Il TVSDK non riesce a passare da un brano all’altro dei sottotitoli VTT Questo problema è stato risolto effettuando il dump del lettore e ricaricando il manifesto quando un brano cambia e correggendo il problema di conversione delle stringhe UTF8 che interessava i nomi dei brani dei sottotitoli WebVTT a doppio byte.

* Zendesk #19717 - Problema di visualizzazione delle opzioni CC Questo problema è stato risolto gestendo correttamente la stringa Unicode.

* Zendesk #19910 - Non è stato possibile rilevare i tag TIT2 ID3 Questo problema è stato risolto fornendo un supporto più completo per le codifiche delle stringhe ID3 v2.4 e per il supporto di ID3 v2.3.

* #20135 Zendesk - TVSDK sta attivando più onComplete per il contenuto VOD.
Questo problema è stato risolto aggiungendo il listener di eventi post_roll_complete nella posizione giusta, invece che nel caso completo dell’evento di modifica dello stato.

**Versione 1.4.19 (1521)**

* #4180 Zendesk - TVSDK non applica HDCP.
   * Questa è una correzione parziale per questo ticket e risolve solo il problema dei dispositivi di protezione NVidia.
È necessario utilizzare l&#39;API di rilevamento HDCP implementata correttamente in Nvidia Shield per tenere traccia in modo dinamico dello stato HDCP.

* Zendesk #18358 - TVSDK blocca lo switch bitrate con discontinuità fuori sincronizzazione.
   * Questo problema è stato risolto aggiungendo un nuovo avviso per rilevare la discontinuità del PTS e obbligando il PTS check a ripetere la ricerca del segmento corretto per ogni switch ABR.
Per correggere il blocco, la chiamata al metodo mediaPlayer.setCustomConfiguration deve includere forcePTSCheckForABR come argomento.

* #19038 Zendesk - Nessun flusso in diretta su Asus Zenpad 10.

  Questo problema è stato risolto precaricando le informazioni del codec multimediale, in modo da non eseguire query sulla funzione in fase di esecuzione.

* I seguenti problemi sono gli stessi di Zendesk #19038:
   * Zendesk #19483 - Il TVSDK si sta bloccando sulla piattaforma Intel.
   * Zendesk #19171 - Arresti anomali su Asus Memo Pad 7 con Android 5.0.

**Versione 1.4.18 (1503)**

* Zendesk #3324 - La generazione di rapporti sugli annunci Primetime non tiene traccia delle interruzioni pubblicitarie quando non sono presenti annunci multimediali in una VMAP.
Quando un’interruzione pubblicitaria è vuota, non veniva eseguito il ping degli eventi di inizio e di tracciamento completo dell’interruzione pubblicitaria. Questo problema è stato risolto inviando ping di avvio dell’interruzione pubblicitaria su interruzioni pubblicitarie vuote, come ad esempio VMAP AdBreak, con un nodo AdSource valido.

* Zendesk #18229 - SetCCVisiblity(VISIBLE) viene ignorato dopo la chiamata di MediaPlayer.reset() Questo problema è stato risolto aggiungendo setCCVisibility(Visibility.INVISIBLE); alla funzione reset() nella classe MediaPlayer.

* Zendesk #18328 - Problema relativo ai fotogrammi persi sui dispositivi Amazon Fire TV di seconda generazione per i contenuti con 60 FPS Questo problema è stato risolto applicando il FPS codificato per il processo decisionale relativo al tempo di sospensione e con una logica di previsione FPS codificata migliore.

**Versione 1.4.17 (1472)**

* #2231 Zendesk - Errore restituito dal recupero del manifesto non disponibile in MediaPlayerNotification Questo problema è stato risolto includendo il corpo della risposta del manifesto in caso di errore di analisi.

* Zendesk #17703 - VideoEngineView non impedisce le schermate durante la riproduzione del video Il metodo setSecure è disponibile a partire dall’API 17, ma poiché l’API 17 copre le versioni 4.2, 4.2.1 e 4.2.2, non è noto quale genererà un’eccezione o se è specifico per il dispositivo. Questo problema è stato risolto racchiudendo VideoEngineView.setSecure nella clausola try catch.

* Zendesk #17919 - La ricerca di contenuti causa un errore di heartbeat A seguito della chiamata heartbeat generata all’avvio della ricerca dopo il pre-roll, si verificava un errore di posizione di dati di input non valido. Questo problema è stato risolto.

**1.4.16 bis** (1454 bis)

* Zendesk #18215 - Alcuni flussi AES non sono in grado di essere caricati.
Questo problema è stato risolto verificando le dimensioni dei metadati DRM del profilo prima di caricare la chiave AES.

**Versione 1.4.16 (1454)**

* Zendesk #3875 - Tab S Si blocca durante la riproduzione Ripristinare la dipendenza di OKHTTP sull’Auditude di CRS perché TVSDK ora utilizza direttamente httpurlconnection anziché curl. Il problema è stato risolto cancellando le eccezioni prima di effettuare qualsiasi altra chiamata JNI.

* Zendesk #4487 - Tracciamento del canale lineare del contenuto Il problema è stato risolto consentendo la reinizializzazione del tracciamento heartbeat video durante una sessione di riproduzione lineare.

* Zendesk #17919 - Android - la ricerca di contenuti causa un errore heartbeat Il problema quando l’heartbeat si trova in uno stato di errore quando è presente una ricerca in un capitolo è stato risolto.

* Zendesk #18053 - Adobe Primetime si blocca su Marshmallow Il TVSDK si bloccava su Android M OS quando la libreria TVSDK utilizzava un codice al neon che eseguiva la conversione del colore YUV -> RGB. Il problema è stato risolto aggiornando le funzioni che causano il problema utilizzando la versione del codice non neon.

* Zendesk #18072 - Android M - Arresto anomalo dell’applicazione Quando si controlla se il profilo e il livello sono supportati, si verifica un arresto anomalo durante la chiamata delle API MediaCodecList e MediaCodecInfo. Il problema è stato risolto fornendo un lavoro temporaneo caricando in anticipo tutte le informazioni del codec per evitare di chiamare queste API solo quando sono necessarie informazioni del codec.

* Zendesk #18074 - I sottotitoli in arabo non funzionano su Nexus con Android 6.0 Il problema è stato risolto fornendo il supporto per la mappa font CTS per Android.

**Aggiornamento versione 1.4.15 (1438)**

* Zendesk #17437 - Ritardo prolungato nell’avvio dei contenuti VOD con alcuni flussi AES.
Per risolvere questo problema, se nel manifesto sono elencate più chiavi, scarica tutte le chiavi AES in parallelo.

**Versione 1.4.15 (1435)**

* Zendesk #4278 - Glitches sui set top box Android quando si cambia il bitrate adattivo (ABR).
La correzione consisteva nell’aggiungere il supporto per lo switch ABR senza soluzione di continuità con il codec multimediale Android più recente.

* Zendesk #17063 - La chiamata a mediaPlayer.reset() causa un errore di ripristino del motore video.
È stato corretto includere il MediaErrorCode originale da VideoEngineExceptions durante l’invio di ErrorEvents.

* Zendesk #17130 - Breve ma notevole pausa durante la modifica del bit rate visualizzato su FireTV.
(Come #4278 in precedenza) La correzione è stata introdotta per aggiungere il supporto per lo switch ABR senza soluzione di continuità con il codec multimediale Android più recente.

* #17666 Zendesk - Marcatori annuncio aggiuntivi, imprevisti o nessun annuncio durante la ripresa del contenuto.
La correzione è stata un problema che si verificava durante l’esecuzione di preparationToPlay su contenuto video-on-demand (VOD); la ricerca iniziale viene eseguita nell’ora locale invece che nell’ora virtuale.

* Zendesk #17437 - Ritardo prolungato nell’avvio dei contenuti VOD con alcuni flussi AES.
La correzione consisteva nel scaricare tutte le chiavi AES in parallelo quando nel manifesto sono elencate più chiavi.

* Zendesk #17851 - Android TV - Black Frame durante ABR La correzione doveva specificare KEY_MAX_WIDTH e KEY_MAX_HEIGHT per abilitare la riproduzione adattiva.

**Versione 1.4.14 (1415)**

* Zendesk #3875 - La scheda S si blocca durante la riproduzione.
È stata necessaria una correzione aggiuntiva per evitare l’arresto anomalo.

* Zendesk #17245 - Fallback su Android TV non funziona.
È stato risolto un ulteriore problema che causava l’interruzione della riproduzione se il fallback era abilitato e la risposta VMAP conteneva un’interruzione pubblicitaria vuota.

**Versione 1.4.14 (1412)**

* Zendesk #17245 - Fallback su Android TV non funziona.
È stata rimossa una restrizione per disabilitare il repackaging creativo negli annunci di fallback.

**Versione 1.4.13 (1388)**

* Zendesk #3502: supporto del failover basato su client HLS durante un’interruzione pubblicitaria Consenti il failover nel manifesto principale quando si verifica un errore di profilo live durante il periodo di interruzione pubblicitaria.

* #3875 Zendesk - Arresti anomali della scheda durante la riproduzione Per risolvere il conflitto tra HttpUrlConnection e cURLm, utilizza una libreria di terze parti.

* Zendesk #4450: problema durante l’impostazione di metadati personalizzati per un singolo posizionamento in un risolutore di contenuti Aggiungere un’impostazione alle impostazioni Opportunità.

**Versione 1.4.12 (1388)**

* #2751 Zendesk - CSAI e CRS | Miglioramento: gestisci gli elementi dinamici in determinati URL di file multimediali.
È stato aggiornato il servizio Creative Repackaging per gestire correttamente gli annunci con URL creativi dinamici.

* #3965 Zendesk - Tornare alla riproduzione normale dalla modalità di riproduzione &quot;trickplay&quot; si ottiene un salto in avanti prima di iniziare la riproduzione.
   * La correzione include TVSDK che restituisce il tempo prima della modifica della frequenza fino a quando tutte le variabili non vengono aggiornate, invece di provare a calcolare GetStreamTime.
   * È stato corretto un arresto anomalo quando si modificava la velocità di riproduzione del trucco in prossimità della fine del flusso.
   * È stato corretto il calcolo del tempo corrente durante la riproduzione con il trucco.

* Zendesk #3978 - Trickplay a 8x e 16x si blocca frequentemente.
   * Scegli sempre il profilo di riproduzione con la velocità bit più bassa per evitare il buffering costante.
   * Aumenta l&#39;intervallo di salto fotogramma per un&#39;elevata velocità di riproduzione con trick-play.
   * È stato risolto un problema che impediva la continua crescita del buffer dopo aver raggiunto la lunghezza di destinazione durante la riproduzione con trucco.

* #3992 Zendesk - Ulteriori velocità di gioco.
TrickPlay è stato aggiornato per accettare tassi superiori a 16x; ora sono consentiti anche +/- 32, +/-64 e +/-128.

* #4007 Zendesk - Interpretazione dell’oggetto GEOB come parte dei metadati della timeline (Android e Web).
Aggiunte le API setByteArray e getByteArray.

* PTPLAY-7301 - Inizio istantaneo con punto di accesso casuale.
Instant On è stato aggiornato per consentire un punto di partenza diverso da zero.

**Versione 1.4.11 (1363)**

* Zendesk #2076 - Frequente balbuzie durante la riproduzione di video su Motorola Xoom con Android 4.0.3 Aggiunti dispositivi all&#39;elenco consentiti per impedire loro di provare a riprodurre contenuti di alto profilo.

* #2197 Zendesk - `[Ads]` Rilevamento ed errori invio OperationFailedEvent con notifica di avviso.

* #3304 Zendesk - VAST 3.0 `[ERRORCODE]` la macro non viene compilata
   * se l’annuncio in linea non è creativo, viene visualizzato il codice di errore 400.
   * `[ERRORCODE]` la macro verrà codificata in URL

**Versione 1.4.10 (1354)**

* Zendesk #2941 - Le risorse live non hanno &quot;0&quot; nell’intervallo ricercabile In precedenza era presente un buffer di 3 segmenti quando si cercava l’inizio di un flusso live, ora è possibile cercare l’inizio di un flusso live (ovvero l’inizio del primo segmento).

* Zendesk #3169 - Aggiornare il lettore di riferimento con l’integrazione di Adobe AnalyticsIl lettore di riferimento è stato aggiornato con la libreria Adobe Analytics come esempio di impianto.
* Zendesk #3299 - Comportamento di gioco di trucco inspiegabile
   * È stato corretto un bug a causa del quale il ritorno allo stato di riproduzione dopo l’interruzione della riproduzione con trucco poteva richiedere diversi secondi (a volte più di 25).
   * È stato corretto un bug a causa del quale, se si richiamava l’esecuzione di un trucco una seconda volta sullo stesso supporto, il flusso poteva bloccarsi all’ora corrente.
* Zendesk #3433 - Android e Flash - Problemi con i sottotitoli

GetLine per WebVTT non rispettava un &lt;cr>&lt;lf> lunghezza regolata per un pacchetto; l&#39;ultima didascalia potrebbe contenere caratteri di didascalie precedenti.

* PTPLAY-6243 - Ottimizzazione del lettore di riferimento per l&#39;acquisizione delle informazioni di debug

I lettori di riferimento di esempio Android sono stati migliorati con un’opzione per attivare i registri di debug e inviare i risultati tramite e-mail. Questa opzione si trova nel menu Registro nel lettore di riferimento.

**Versione 1.4.9 (1332)**

* #2649 Zendesk - Il completamento del buffer avviene prima che il buffer iniziale sia pieno

Dopo una ricerca, possibile caso in cui il motore video imposta lo stato su RIPRODUZIONE prima che il presentatore video sia pronto per la riproduzione. Si verifica quando lo stato del buffer è elevato prima della ricerca. Correzione tramite notifica al motore video dello stato del buffer insufficiente. Con lo stato del buffer basso del motore video, la chiamata Play causa la modifica dello stato in BUFFERING invece di PLAY. La riproduzione riprende quando lo stato cambia in RIPRODUZIONE.

* Zendesk #2846 - Richiesta di miglioramento: consente di impostare una stringa agente utente diversa per le chiamate effettuate dalla libreria di Auditudi

È stata aggiunta una nuova API per impostare l’agente utente per le chiamate relative agli annunci, auditudeSettings.setUserAgent(&quot;user/agent&quot;). Se non è impostato alcun agente utente, verrà utilizzato il valore predefinito. Questo influisce solo sull’agente utente per le chiamate relative agli annunci; l’agente utente per le chiamate multimediali è invariato, ovvero &quot;Adobe Primetime&quot;+&lt;default useragent=&quot;&quot;>.

**Versione 1.4.8 (1324)**

* #1218 Zendesk - 106000.33 Errore con locale ... Se il caricamento del manifesto in FragmentedHTTPStreamer::ThreadParseManifest() non riesce, verifica se il dominio URL è localhost e, in tal caso, modifica il dominio in 127.0.0.1 e richiama ThreadParseManifest.
* Zendesk #3072 - Passaggio automatico a bitrate inferiori. Il calcolo della lunghezza del buffer è stato modificato per saltare il payload PTS pari a zero.
* Zendesk #3168 - Sottotitoli WebVTT visualizzati solo per i primi 10 secondi.
* Zendesk #3193 - È stata aggiunta la richiesta di un’API per la modifica del profilo in TVSDK, PlaybackEventListener.onProfileChanged().

**Versione 1.4.7 (1311)**

* Zendesk #2197 - Tracciamento degli errori pubblicitari. La notifica aggiunta per la risorsa non è riuscita a caricare il manifesto
* #2575 Zendesk - PSDK ignora l’annuncio in-stream personalizzato MARK prima del video
* Zendesk #2719 - Win Death with auditude ads, monitoraggio dei beacon corretto quando reindirizzato all&#39;URL relativo nel plug-in di controllo dell&#39;audience
* #2760 Zendesk - Tag DISCONTINUITY ignorato durante la modalità TrickPlay
* Zendesk #2805 - Arresto anomalo del lettore all’inizio della riproduzione, stessa correzione di Zendesk #2719
* Zendesk #2817 - lettore Android - Il lettore a volte si blocca e smette di giocare, risolto estendendo i buffer di decodifica da 2,0 a 3,0 secondi
* Zendesk #2839 - Adobe Primetime PSDK supporta i chipset ARMv8?, è stata aggiunta una correzione per arresti anomali rilevati su Galaxy S6.
* Zendesk #2885 - Auditude della riproduzione in arresto anomalo, stessa correzione di Zendesk #2719
* #2895 Zendesk - Errore HLS in tempo reale dopo 10 minuti di riproduzione
* Zendesk #2925 - Feedback riguardante Android dev build (1.4.5), su alcuni dispositivi quando mettiamo in coda il pacchetto alla coda di input, se il PTS è negativo, il decodificatore va in uno stato strano che otteniamo sempre un PTS di output negativo per i pacchetti futuri. La correzione imposta il PTS di input su zero se è negativo per evitare questo problema.
* PTPLAY-4645 - Disattivare il supporto cifratura RC4 in openssl. Ci sono exploit noti per RC4. Ciò significa che se si tenta di connettersi a un server che supporta solo RC4, questo non riuscirà.

**Versione 1.4.6 (1282)**

* Zendesk #2192 - Il bitrate non sempre diminuisce in condizioni di rete scadenti, risolte rimuovendo l&#39;implementazione rapida dello switch.
* Zendesk #2631 - Sottotitoli in arabo su Android: il testo su più righe appare tagliato, corretto regolando la dimensione del font per i font in arabo.
* Zendesk #2844 - Il buffering su Note 4 e il tempo di download dei frammenti non sono precisi.

Questo problema è stato risolto aggiungendo la latenza tra i download dei segmenti video nel calcolo della larghezza di banda e facendo in modo che la logica di calcolo del tempo di download utilizzi la durata completa del ciclo di richiesta.

* Zendesk #2908 - I sottotitoli arabi non funzionano su Nexust 5, 6 e 7, risolti aggiungendo altri 2 font di fallback per gli script arabi.
* PTPLAY-4627 - aggiorna Nielson appsdk alla versione 1.2.3.7
* PTPLAY-5084 - Supporto del failover dell&#39;aggiornamento Live Master Manifest

**Versione 1.4.5 (1248)**

* Zendesk #1757 - Solo l&#39;audio riprodotto o il lettore si blocca per alcuni profili di velocità bit video, nexus 4 e Nexus 7 si bloccano
* Zendesk #2072 - TimedMetadata per AdEvent non contiene l’URL completo solo &quot;http&quot;
* Zendesk #2192 - Il bitrate non sempre è inferiore in condizioni di rete scadenti
* Zendesk #2256 - Accesso alla playlist principale, PSDK aggiornato per l’invio di eventi timedMetadata per i tag abbonati alla playlist principale.
* #2269 Zendesk - Sullo schermo vengono visualizzate due diverse lingue per i sottotitoli contemporaneamente a WebVTT
* Zendesk #2417 - Lettore che stava tentando di scaricare i sottotitoli prima dell’inizio della riproduzione, WebVTT stava utilizzando la variabile del numero di segmento errata per la corrispondenza del numero di segmento. Il bug viene visualizzato solo per i file multimediali con indici di segmento a partire da zero.
* Zendesk #2470 - PSDK non ritorna dallo stato SUSPENDED quando si verifica una modifica del bitrate dopo la sospensione. In una situazione speciale in cui la ricerca avanzata viene chiamata da RestoreGPUResource (ripristino del lettore dallo stato di sospensione) e viene rilevato un commutatore di flusso prima di tale momento, la ricerca avanzata non è in grado di completare e si traduce in un buffering costante.
* Zendesk #2451 - Sottotitoli codificati &quot;bottom inset&quot;, aggiunto il parametro &quot;bottomInset&quot; al codice della didascalia
* Zendesk #2480 - disabilitazione dell’ottimizzazione del reindirizzamento HTTP 302, è stato aggiunto il supporto per l’impostazione della proprietà useRedirectedUrl
* Zendesk #2486 - beacon di terze parti
* Zendesk #2547 - Sottotitoli in arabo: il testo deve essere allineato e giustificato a destra

**Versione 1.4.4 (1195)**

* Zendesk #1158 - Riproduzione non riuscita su Huawei Valiant (Y301A1)
* Zendesk #1709 - Dimensioni dei supporti non corrette e video allungato
* #1757 Zendesk - Solo audio riprodotto dopo il passaggio del profilo tra flussi con identici dati spa/pps
* Zendesk #2095 - Stato HTTP 307 (reindirizzamento) causa l’arresto della riproduzione da parte del lettore Adobe
* #2126 Zendesk - Evento TimedMetaData mancante per l’ultimo ADEVENT. I tag sottoscritti che esistono dopo l’ultimo segmento non sono stati segnalati a PSDK da AVE
* #2227 Zendesk - Blocchi in VideoEngine nativeReset e nativePause
* Bug #3921755 - Aggiornamento della libreria OpenSSL alla versione 1.0.1L

**Versione 1.4.3 (1173)**

* #1591 Zendesk - RENDITION_M3U8_ERROR
* Zendesk #1870 - Attivazione e disattivazione sottotitoli
* PTPLAY-1818 - La riproduzione con il trick di riavvolgimento si interrompe all&#39;annuncio invece di riavvolgerla oltre
* PTPLAY-2736 - Quando viene completato un flusso con didascalia WebVTT, sullo schermo viene visualizzata una didascalia WebVTT visualizzata in precedenza
* PTPLAY-3773 - Un annuncio mid-roll non viene riprodotto quando la riproduzione in streaming viene avviata dopo la posizione dell&#39;annuncio

**Versione 1.4.2**

* Zendesk #1561: supporto del failover basato su client HLS in prima serata. Utilizzerà la data/ora del programma per risolvere il failover
* Zendesk #1590 - LoadInfo.MediaDuration è sempre 0 (non fisso solo per audio)
* #1626 Zendesk - Potenziale perdita di memoria nel lettore. Non si è verificata alcuna perdita di memoria, il problema si è verificato quando NotificationHistory ha salvato le ultime 1000 notifiche, che sono state ridotte a 100.
* Zendesk #2192 - Il bitrate non sempre è inferiore in condizioni di rete scadenti

**Versione 1.4.1 (1121)**

* #1951 Zendesk - Blocco in VideoEngine.nativeReset() su dispositivi 4.0.x
* Zendesk #2064 - Arresto anomalo nativo di SIGSEGV su dispositivi Android specifici basati su Intel
* Zendesk #2075 - Blocco in VideoEngine.nativeReleaseGPUResource su dispositivi 4.0.x Nota: questa build è &#42;&#42;&#42;obbligatorio&#42;&#42;&#42; per il supporto di Android 5.0 (Lollipop)
* Zendesk #1513 - Supporto per Android Lollipop
* Zendesk #1709 - Dimensioni dei supporti non corrette e video allungato
* #1871 Zendesk - I sottotitoli WebVTT scompaiono di tanto in tanto e vengono rivisualizzati quando si visualizza un livestream con sottotitoli WebVTT
* #1996 Zendesk - Nessun marcatore timeline visualizzato nel PSDK 1.4.0
* Zendesk #2046 - Arresto anomalo con PSDK 1.4.1.1113, è stato corretto un arresto anomalo per i flussi live quando non vengono restituiti annunci dal pubblico
* #3769657 bug: aggiorna la versione di curl a 7.38.0
* PTPLAY-1575 - Quando la riproduzione ABR inizia con uno streaming solo audio e poi passa a uno streaming audio/video, il video non viene mai riprodotto mentre l&#39;audio continua
* PTPLAY-2499 - Aggiornamento a OpenSSL alla versione 1.0.1j per risolvere le vulnerabilità recenti
* PTPLAY-2632 - Il video non viene ripristinato dopo il mid roll Annuncio completato su Android Lollipop
* PTPLAY-2678 - Arresto del video durante i test di longevità live su Android Lollipop

**Versione 1.4.0**

* #1024 Zendesk - Funzione per rimuovere un annuncio dal flusso tramite manifesto
* Zendesk #1293 - Problema con la selezione della traccia dei sottotitoli.
* Zendesk #1590 - LoadInfo.MediaDuration è sempre 0, mediaDuration sta ora mostrando il valore corretto.
* Zendesk #1629 - arresto anomalo del lettore/app al termine della riproduzione dell’annuncio su Galaxy S4
* Zendesk #1674 - ClosedCaption Non viene visualizzato, vengono visualizzati i sottotitoli 708 corretti quando mancano i codici ETX 0x03.
* PTPLAY-2157 - Gli stili predefiniti dei sottotitoli codificati venivano restituiti dai getter anche se dopo l’impostazione e la verifica visiva di stili diversi sul flusso. Le proprietà di stile Sottotitoli codificati mostrano ora il valore su cui sono stati impostati.

## Problemi noti in 1.4 {#known-issues-in}

**Versione 1.4.31**

* PTPLAY-16803 - I sottotitoli codificati non funzionano solo con contenuti audio, in quanto il sistema di sottotitoli necessita di video per funzionare. Senza video, non vi è alcuna dimensione del riquadro di visualizzazione e senza una dimensione del riquadro di visualizzazione, non è possibile visualizzare alcuna grafica per i sottotitoli.
* PTPLAY-1634 - Lo stesso tag Abbonato ha marche temporali diverse in finestre live diverse. Quando si sposta la finestra live, lo stesso tag deve avere gli stessi timestamp. Tuttavia, a volte, anche gli stessi tag hanno marche temporali diverse.
* PTPLAY-3197 - Arresto anomalo con segnale di errore 11 SIGSEGV sul dispositivo Acer Iconia dopo ~ 1 ora di riproduzione continua
* PTPLAY-3310 - Con una minore quantità di bit rate audio, l&#39;audio diventa discontinuo su Acer Iconia
* PTPLAY-3355 - WIN DEATH crash su Motorola Xoom con 4.0.x dopo ~ 1 ora di riproduzione continua.
* PTPLAY-3557 - Il riavvolgimento in corrispondenza di un’interruzione pubblicitaria sta causando il completamento del flusso
* PTPLAY-7079 - La finestra di riproduzione su un client Android non funziona con l&#39;arresto sicuro/hard stop
* Bug #3760144 - La risoluzione può cambiare o apparire pulsare quando il flusso viene messo in pausa su alcuni dispositivi come Kindle Fire 7 e Samsung Galaxy Nexus. Osservabili solo sotto stretta ispezione
* #3761170 di bug: seekToLocal in Live with Ads non può effettuare ricerche nel contenuto degli annunci; è consigliabile utilizzare le API currentTime per i flussi live
* #3763370 bug: i flussi live con annunci mostrano occasionalmente due marcatori di annunci vicini quando dovrebbe esserci un solo. Questi marcatori annuncio rappresentano lo stesso annuncio, e solo uno verrà riprodotto
* #3763373 bug: il marcatore dell’annuncio potrebbe scomparire brevemente quando si cerca oltre un annuncio nei flussi VOD. Il marcatore dell’annuncio viene ripristinato e non vi sono altri effetti avversi sulla timeline
* Alcuni dispositivi presentano problemi noti di riproduzione. Consulta [Problemi noti relativi al dispositivo in 1.4](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14).
* Implementazione di riferimento: la funzione Trick play non è implementata nell’applicazione di esempio
* Su alcuni dispositivi Android TV è possibile visualizzare un fotogramma nero a causa di un ripristino del decodificatore nei seguenti punti di transizione:
   * entrata e uscita dalla modalità trickplay
   * passaggio tra tracce audio di associazione tardiva
   * da un annuncio al contenuto principale.

**Versione 1.4.23**

* I sottotitoli codificati non funzionano con contenuti solo audio perché il sistema dei sottotitoli richiede un video per funzionare. Senza video, non esiste alcuna dimensione del riquadro di visualizzazione e senza una dimensione del riquadro di visualizzazione non è possibile visualizzare elementi grafici per i sottotitoli.
* A partire dalla versione 1.4.23, TVSDK non supporterà Gingerbread OS 2.3. Questo perché TVSDK ha utilizzato le seguenti librerie Android private per raccogliere informazioni hardware sui dispositivi con sistema operativo Gingerbread:

   * `libstagefright.so`
   * `libcutils.so`

Nella versione Android N, Google ha rimosso l’accesso a queste librerie private. Il sistema operativo Gingerbread attualmente rappresenta meno dell&#39;1% della quota di mercato del sistema operativo Android a livello globale, quindi dopo la versione 1.4.23, il sistema operativo Gingerbread non sarà più supportato dal TVSDK.
Quando utilizzi la versione 1.4.23 (che include il supporto per Android N) o successiva:
* Aggiorna le app per utilizzare la versione 11 di minSdkVersion.
* Se l’utente finale esegue OS 2.3, la versione dell’SDK è inferiore alla versione minSdkVersion dell’applicazione. L&#39;installazione o l&#39;aggiornamento dell&#39;applicazione viene interrotto.
* Se l&#39;utente finale esegue una versione successiva a OS 2.3, l&#39;applicazione verrà installata correttamente.

Se si aggiorna minSdkVersion:

* Se l&#39;utente finale esegue OS 2.3, l&#39;applicazione viene installata ma la riproduzione non funziona.
Questo vale sia per l&#39;aggiornamento che per la nuova installazione.
* Se l’utente finale utilizza un sistema superiore a OS 2.3, l’app viene installata correttamente e il contenuto viene riprodotto correttamente.

**Versione 1.4.22**

* L’uscita anticipata dagli annunci non funziona con alcuni degli annunci mid-roll quando i tag di splice-out e splice-in sono troppo vicini tra loro.

**Versione 1.4.2**

* Il riavvolgimento a un’interruzione pubblicitaria causa il completamento del flusso.

Media Player invia erroneamente MediaPlayer PlayerState.Complete durante l&#39;operazione di riavvolgimento della riproduzione dei brani quando raggiunge un limite di annuncio. Il lettore deve ignorare questo evento quando si trova in modalità di riproduzione con trucco, altrimenti l’SDK gestisce correttamente lo stato.

**Versione 1.4.0 (1086)**

* PTPLAY-1634 - Lo stesso tag Abbonato ha marche temporali diverse in finestre live diverse. Quando si spostano le finestre live, lo stesso tag in ciascuna di esse deve avere gli stessi timestamp. Tuttavia, a volte, anche gli stessi tag hanno marche temporali diverse.
* PTPLAY-2541 - COMPONENT_CREATION_FAILURE viene talvolta visualizzato dopo diversi switch al/dal flusso alternativo nelle sospensioni attività
* #3726865 bug: se un flusso LBA MultiBitrate inizia da un flusso solo audio, il video non viene visualizzato se viene passato a un flusso Audio/Video. L&#39;avvio da un flusso Audio/Video non visualizza questo problema e può essere eseguito con successo tra i flussi Audio e Audio/Video
* Bug #3760144 - La risoluzione può cambiare o apparire pulsare quando un flusso viene messo in pausa su alcuni dispositivi come Kindle Fire 7 e Samsung Galaxy Nexus. Osservabili solo sotto stretta ispezione
* #3761170 bug: seekToLocal in Live with Ads non può effettuare ricerche nel contenuto degli annunci; è consigliabile utilizzare le API currentTime per i flussi live
* #3763370 bug: i flussi live con annunci mostrano occasionalmente due marcatori di annunci vicini quando dovrebbe esserci un solo. Questi marcatori annuncio rappresentano lo stesso annuncio, e solo uno verrà riprodotto
* #3763373 bug: il marcatore dell’annuncio potrebbe scomparire brevemente quando si cerca oltre un annuncio nei flussi VOD. Il marcatore dell’annuncio viene ripristinato e non vi sono altri effetti avversi sulla timeline
* Alcuni dispositivi presentano problemi noti di riproduzione. Per ulteriori informazioni, consulta [Problemi noti relativi al dispositivo in 1.4](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14).
* Implementazione di riferimento: la funzione Trick play non è implementata nell’applicazione di esempio.

## Problemi noti relativi al dispositivo in 1.4 {#known-device-issues-in}

| Dispositivo | Chipset | Problema | Causa | Soluzione alternativa |
|--- |--- |--- |--- |--- |
| Droid X | TI OMAP3 | Si prevede un ritardo di ABR dal riavvio del decodificatore. |  |  |
| HTC Desire (diverso da HTC Desire HD) | QSD8250 | Impossibile riprodurre il video. Restituisce l’errore VIDEO_PROFILE_NOT_SUPPORTED. | Desire non fornisce un decoder HW appropriato. Fornisce il decodificatore SW di Stagefright. | Riavviare il dispositivo. |
| HTC EVO 4G | QSD8650 | Nessun decodificatore hardware. | Qualcomm non dispone di un decodificatore HW. | Aggiornamento ad Android 4.x. |
| Kindle FireSystem versione 6.0 | OMAP4 TI | Non riproduce i flussi HLS. Il video su AIR non funziona. |  | Eseguire l&#39;aggiornamento alla versione 6.3 del sistema. |
| Kindle Fire HD | OMAP4 TI | Può entrare in uno stato in cui non può riprodurre il video. Restituisce gli errori VIDEO_PROFILE_NOT_SUPPORTED e UNRECOVERABLE_ERROR. | Il decodificatore HW entra in uno stato irrecuperabile quando l’app non arresta completamente il decodificatore HW, ad esempio dopo un arresto anomalo. Si verifica anche sulle app native del dispositivo. | Riavviare il dispositivo. |
| Kindle Fire HD 8.9 | Snapdragon 800 | AVE si blocca dopo più switch ABR. |  |  |
| Motorola Atrix | Tegra2 | Problemi generali di prestazioni con AVE rispetto ad AIR. Uscita audio/video dalla sincronizzazione, la riproduzione video si blocca dopo 9-15 minuti di riproduzione. Arresti anomali | Possibilmente correlato ad openGLES che abilitiamo su AIR. In fase di investigazione. |  |
| Nexus 7 (2a gen.) | S4Pro APQ8064 (Qualcomm) | Il dispositivo si blocca quando un filmato viene messo in pausa per più di 30 minuti. | Problema del dispositivo segnalato a Google. | L’app deve subire un timeout in modo da non consentire uno stato di pausa lungo. |
| Nexus S (GB) | Uccello che canta | Non è possibile riprodurre alcun video con il decodificatore hardware. | Non esiste un decodificatore HW basato su Stagefright in Nexus S, quindi per Android 2.3 utilizziamo un decodificatore SW. | Eseguire l&#39;aggiornamento a ICS. |
| Nexus S (ICS) | Uccello che canta | Il video occasionalmente sfarfallio. | Dati non validi possono causare il malfunzionamento del decodificatore. | Riavviare il dispositivo. |
| Nook tabletSistema operativo Android: 2.3 | OMAP TI 4 | Il video non viene riprodotto e l’app si blocca. | Stagefright entra in uno stato instabile dopo aver eseguito l’app per alcune volte. Chiamate a mediaplayer::QueryCodec bloccate. | Riavviare il dispositivo per ripristinare lo stato. |
| Samsung Galaxy ACE | Qualcomm MSM7227 | Impossibile installare l&#39;app SampleMediaPlayer. | Utilizza ARM v6 invece del più comune chipset ARM v7. FP/AIR non supporta questo dispositivo. |  |
| Samsung Galaxy ACE2Android OS: 2.3.6 | NovaThor U8500 | Impossibile riprodurre il video. | Questo chipset è un decoder sconosciuto per Android pre-ICS in AVE. |  |
| Samsung Galaxy S2 (GT-I9100) | Exynos | Le prestazioni video non sono all&#39;altezza per questo dispositivo. | Il decodificatore HW restituisce fotogrammi decodificati con il PTS errato. Sembra che il decodificatore utilizzi il tempo di decodifica invece del tempo di presentazione. |  |
| Samsung Galaxy S2 GAndroid OS: 2.3.6 | OMAP4 TI | Arresti anomali all’avvio del video. |  | Esegui l’aggiornamento ad Android 2.3.7 o 4.x. |
| Samsung Galaxy S3 (I747) | Qualcomm MSM8960 | A intermittenza, il video si blocca e viene riprodotto solo l’audio, quindi non risponde. |  |  |
| Samsung Galaxy S3 I747M | SAMSUNG_M2ATT | Il video si blocca. | Indagare. |  |
| Samsung Galaxy Tab 1 v10.1 | Tegra 2 | La transizione MBR potrebbe richiedere fino a tre secondi. | Per risolvere gli arresti anomali del MBR, riavviamo il decoder per ogni switch di flusso, che può richiedere fino a tre secondi. |  |
| Samsung Galaxy Y |  | Impossibile installare l&#39;app SampleMediaPlayer. | Utilizza ARM v6 invece del più comune chipset ARM v7. FP/AIR non supporta questo dispositivo. |  |
| Xoom | Tegra | Alcuni fotogrammi vengono persi per il passaggio. Il decodificatore non viene riavviato. | Limitazione OMXAL. |  |

## Risorse utili {#helpful-resources}

* Consulta la documentazione completa dell’Aiuto all’indirizzo [Informazioni e supporto per Adobe Primetime](https://helpx.adobe.com/support/primetime.html) pagina.
