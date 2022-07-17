---
title: Note sulla versione di TVSDK 2.1 PlayStation 4
description: Le note sulla versione di TVSDK 2.1 per PlayStation 4 descrivono le funzioni supportate e i problemi noti di TVSDK 2.1 PlayStation 4 .
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
exl-id: 32af3fe4-c730-41f6-a558-987bd14c9bae
source-git-commit: 3b051c3188c81673129e12dfeb573aaf85c15c97
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---

# Note sulla versione di TVSDK 2.1 PlayStation 4 {#tvsdk-playstation-release-notes}

Le note sulla versione di TVSDK 2.1 per PlayStation 4 descrivono le funzioni supportate e i problemi noti di TVSDK 2.1 PlayStation 4 .

## Problemi risolti {#resolved-issues}

Di seguito sono riportati i problemi risolti per TVSDK 2.1 per PlayStation 4:

**Versione 2.1.0.638**

* **PTPLAY-10439:**
Quando il wrapper dell&#39;annuncio VMAP veniva interrotto, il lettore si bloccava nello stato di preparazione (non inviava 
`onComplete` al suo chiamante).

* **PTPLAY-10179:**

   `creativeRepackaging` e `fallbackOnInvalidCreative` ora i valori sono disattivati per impostazione predefinita. Inoltre, quando `creativeRepackaging` flag impostato ma no `creativeRepackaging` è stato fornito il formato `onRepackagingComplete` veniva chiamato il numero di volte in cui erano presenti annunci nell’interruzione pubblicitaria, causando la creazione di interruzioni pubblicitarie più volte.

* **Zendesk #10304**: Variabile di attivazione/disattivazione annunci non inizializzata. Ora inizializziamo la variabile da `DataSetEntry's` del trattore.

* **PTPLAY-10318:**
È stato introdotto il supporto per la modalità in background.
* **Zendesk n. 17409:**
Quando si passa alla modalità di riproduzione a trucco, poi si torna alla modalità di riproduzione normale, poi di nuovo alla modalità di riproduzione a trucco, la posizione di riproduzione saltava.
* **PTPLAY-9552:**
Dopo l’analisi dei file XML di risposta, il codice di errore 1108 viene aggiunto al ping ogni volta che non sono presenti annunci.
* **PTPLAY-9551:**
Quando non c&#39;è alcuna interruzione pubblicitaria dopo l&#39;elaborazione di Auditude, il CRS chiama 
**onPrefetchComplete** che diminuisce il valore groupCount. Dal momento che non c&#39;è nessuna pausa pubblicitaria, il **groupCount** è 0 e viene decrementato di 1. Precedentemente il **groupCount** era **uint32_t** a causa del quale veniva modificato il valore massimo. Questo è ora **int32_t**.

**Versione 2.1.0.621**

* **Zendesk #4555**
Problemi istantanei di memoria in caso di errori di caricamento principale - 
`MediaItemLoader` Correzione dell&#39;arresto anomalo in fase di rilascio `mediaitemloader`

* **Zendesk #17223**
2.x CSAI: Non tutti gli URL di tracciamento degli annunci attivano
   * Alcuni annunci VAST che a loro volta puntavano a un annuncio in linea mancavano gli url di tracciamento.
   * Quando ci sono più tag impression in un annuncio in VAST XML, solo il primo url impression è stato salvato e il resto è stato ignorato. Ora tutti gli url di impression verranno salvati e inseriti in un secondo momento.
* **Zendesk #17224**
L&#39;agente utente PS4 sposta le informazioni primetime alla fine di UAString
* **Zendesk #17226**
2.x CSAI: Non tutti gli annunci erano attaccati.
\
   Correzione per indicare che la timeline è cambiata a causa delle operazioni insertBy o eraseBy e fare di conseguenza cambiare il periodo.

* **Zendesk #17284**
   [Tutte le piattaforme] I sottotitoli non vengono visualizzati.\
   HLS - supporto per `EXT-X-MEDIA-TIME` tag per file di didascalie VTT.

* **Zendesk #17889**
Riproduzione &quot;Milky&quot; su PS4
\
   yoffset corretto applicato (per la conversione del colore)

* **Zendesk #17954**
Logica di fallback dell’annuncio + gestione di vaste quantità vuote
\
   Risolto il problema se uno dei wrapper Vast era vuoto, il parser Vast utilizzato per continuare l&#39;elaborazione del wrapper.

* **Zendesk #17807**
Non può superare vuoto vasto Come Zendesk #3103

* **Zendesk #17865**
Logica di fallback su PS4 e XBox One
\
   Come Zendesk #3103

**Versione 2.1.0.591**

* **Zendesk #3767**
Frammento di codice ad PS4, la risoluzione dell&#39;annuncio non riesce quando si elaborano reindirizzamenti VMAP.
* **Zendesk #4096**
PS4 CSAI: Errore di segmentazione È stato corretto un arresto anomalo quando TVSDK genera un errore di segmentazione quando la libreria annunci sta elaborando una risposta VMAP.

* **Zendesk #4161**
Trickplay 16x alla fine del film blocca Blocco critico che si verifica quando trickplay torna alla riproduzione normale

* **Zendesk #4208**
Arresto casuale quando i sottotitoli codificati sono attivati Perdita di memoria fissa quando i sottotitoli codificati sono abilitati

* **Zendesk #4213**
PS4 CSAI: Cambia la stringa agente utente predefinita per tutte le chiamate relative all&#39;annuncio La stringa agente utente viene creata utilizzando la stessa stringa UA che il browser sta utilizzando + aggiungi stringa Primetime

* **PTPLAY-7675** (interno) Gli annunci transcodificati non riproducevano Creative Repackaging non riusciva quando veniva chiamato all&#39;interno di una risposta VMAP o VAST. Fix è quello di leggere il mediafile dall&#39;annuncio invece di leggere dal bene in caso di grandi annunci.

* **PTPLAY-7895** (interno) Quando `allowMultipleAds=false`, nessun annuncio può essere visualizzato un bug fisso in cui `allowMultipleAds` Il parametro non veniva seguito correttamente.

* **PTPLAY-7896** (interno) Gli annunci vengono riprodotti in ordine sequenziale su PS4 Problema risolto: gli annunci non erano nell&#39;ordine in cui gli annunci comparivano nelle risposte XML.

* PS4 TVSDK testato in una mini-app invece che in un gioco.

**Versione 2.1.0.563**

* **Zendesk #3868**
TVSDK supporta Playstation SDK 2.5 Il TVSDK è ora generato con l&#39;SDK per Playstation 2.5.

* **Zendesk #4093**
coppie chiave-valore di targetingInfo nella richiesta Pt Ads.
\
   È stato aggiunto un nuovo carattere di riga che separa le coppie chiave/valore.

## Funzioni supportate {#supported-features}

Le seguenti funzioni sono supportate in TVSDK 2.1 per PlayStation 4:

**Versione 2.1.0.621**

* Ad Fallback, concatenamento margherita nella logica di selezione degli annunci (Zendesk #3103) Per gli annunci VAST (creativi) con la regola di fallback abilitata, TVSDK tratta un annuncio con un tipo MIME non valido come un annuncio vuoto e tenta di utilizzare al suo posto gli annunci di fallback.Puoi configurare alcuni aspetti del comportamento di fallback

**Versione 2.1.0.538**

* Riproduzione HLS VOD, compresa riproduzione, pausa, ricerca
* Streaming a bit rate adattivo
* Riproduzione di contenuti crittografati con contenuti protetti da AES e DRM di Primetime
* Inserimento lato client con comportamenti annunci predefiniti e perdoni gli annunci
* Repackaging creativo
* Sottotitoli codificati WebVTT
* Attiva istantaneamente con posizione iniziale personalizzata
* Gioco di mattoni con avanzamento veloce e riavvolgimento rapido
* Reindirizzamento 302

## Risorse utili {#helpful-resources}

* Consulta la documentazione completa dell’Aiuto all’indirizzo [Informazioni e supporto per Adobe Primetime](https://experienceleague.adobe.com/docs/primetime.html) pagina.
