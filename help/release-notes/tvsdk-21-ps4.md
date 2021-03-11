---
title: Note sulla versione di TVSDK 2.1 PlayStation 4
description: Le note sulla versione di TVSDK 2.1 per PlayStation 4 descrivono le funzioni supportate e i problemi noti di TVSDK 2.1 PlayStation 4 .
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
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
Quando il link dell&#39;annuncio del wrapper VMAP era rotto, il lettore si bloccava nello stato di Preparazione (non inviava 
`onComplete` al suo chiamante).

* **PTPLAY-10179:**

   `creativeRepackaging` e ora  `fallbackOnInvalidCreative` i valori sono disattivati per impostazione predefinita. Inoltre, quando il flag `creativeRepackaging` è stato impostato ma non è stato fornito il formato `creativeRepackaging`, il `onRepackagingComplete` veniva chiamato il numero di volte in cui erano presenti annunci nell&#39;interruzione pubblicitaria, causando la creazione di interruzioni pubblicitarie più volte.

* **Zendesk #10304**: Variabile di attivazione/disattivazione annunci non inizializzata. È stata inizializzata la variabile dal `DataSetEntry's` ctor.

* **PTPLAY-10318:**
È stato introdotto il supporto per la modalità di sfondo.
* **Zendesk # 17409:**
Quando si passa alla modalità di riproduzione a trucco, poi di nuovo alla modalità di riproduzione normale, poi di nuovo in modalità di riproduzione a trucco, la posizione di riproduzione saltava.
* **PTPLAY-9552:**
Dopo l&#39;analisi dei file XML di risposta, il codice di errore 1108 viene inserito quando non sono presenti annunci.
* **PTPLAY-9551:**
Quando non c&#39;è un&#39;interruzione pubblicitaria dopo l&#39;elaborazione di Auditude, il CRS chiama 
**** onPrefetchCompleteche diminuisce il valore groupCount. Poiché non vi è alcuna interruzione pubblicitaria, il **groupCount** è 0 e decrementato di 1. In precedenza **groupCount** era **uint32_t** a causa del quale veniva utilizzato per modificare il valore massimo. Ora è **int32_t**.

**Versione 2.1.0.621**

* **Zendesk #4555**
Instant su problemi di memoria che portano a errori di caricamento - 
`MediaItemLoader` Correzione dell&#39;arresto anomalo in fase di rilascio  `mediaitemloader`

* **Zendesk #17223**
2.x CSAI: Non tutti gli URL di tracciamento degli annunci attivano
   * Alcuni annunci VAST che a loro volta puntavano a un annuncio in linea mancavano gli url di tracciamento.
   * Quando ci sono più tag impression in un annuncio in VAST XML, solo il primo url impression è stato salvato e il resto è stato ignorato. Ora tutti gli url di impression verranno salvati e inseriti in un secondo momento.
* **Zendesk #17224**
PS4 L&#39;agente utente sposta le informazioni di primetime alla fine di UAString
* **Zendesk #17226**
2.x CSAI: Non tutti gli annunci erano attaccati.
\
   Correzione per indicare che la timeline è cambiata a causa delle operazioni insertBy o eraseBy e fare di conseguenza cambiare il periodo.

* **Zendesk #17284**
   [Tutte le ] piattaformeI sottotitoli codificati non vengono visualizzati.\
   HLS - supporto per il tag `EXT-X-MEDIA-TIME` per i file di didascalia VTT.

* **Zendesk #17889**
Riproduzione &quot;Milky&quot; su PS4
\
   yoffset corretto applicato (per la conversione del colore)

* **Zendesk #17954**
Logica di fallback degli annunci + gestione di un vasto spazio vuoto
\
   Risolto il problema se uno dei wrapper Vast era vuoto, il parser Vast utilizzato per continuare l&#39;elaborazione del wrapper.

* **Zendesk #17807**
Non può superare vuoto vasto Come Zendesk #3103

* **Zendesk #17865**
Logica di fallback su PS4 e XBox One
\
   Come Zendesk #3103

**Versione 2.1.0.591**

* **Snippet di codice ad Zendesk #3767**
PS4, la risoluzione dell&#39;annuncio non riesce quando si elaborano reindirizzamenti VMAP.
* **Zendesk #4096**
PS4 CSAI: Errore di segmentazione È stato corretto un arresto anomalo quando TVSDK genera un errore di segmentazione quando la libreria annunci sta elaborando una risposta VMAP.

* **Zendesk #4161**
Trickplay 16x alla fine del film si blocca Blocco critico che si verifica quando trickplay torna alla riproduzione normale

* **Zendesk #4208**
Arresto casuale quando i sottotitoli codificati sono attivati Perdita di memoria fissa quando i sottotitoli codificati sono abilitati

* **Zendesk #4213**
PS4 CSAI: Cambia la stringa agente utente predefinita per tutte le chiamate relative all&#39;annuncio La stringa agente utente viene creata utilizzando la stessa stringa UA che il browser sta utilizzando + aggiungi stringa Primetime

* **PTPLAY-7675** (interno) Gli annunci transcodificati non stanno giocando a Creative Repackaging non riusciva quando veniva chiamato all&#39;interno di una risposta VMAP o VAST. Fix è quello di leggere il mediafile dall&#39;annuncio invece di leggere dal bene in caso di grandi annunci.

* **PTPLAY-7895** (interno) Quando  `allowMultipleAds=false`, nessun annuncio riproduce un bug fisso in cui  `allowMultipleAds` il parametro non veniva seguito correttamente.

* **PTPLAY-7896** (interno) Gli annunci stanno riproducendo l&#39;ordine di sequenza su PS4 Problema risolto: gli annunci non erano nell&#39;ordine in cui gli annunci comparivano nelle risposte XML.

* PS4 TVSDK testato in una mini-app invece che in un gioco.

**Versione 2.1.0.563**

* **Zendesk #3868**
TVSDK supporta Playstation SDK 2.5. Il TVSDK è ora integrato con l’SDK della Playstation 2.5.

* **Coppie chiave-valore di Zendesk #4093**
targetingInfo nella richiesta Pt Ads.
\
   È stato aggiunto un nuovo carattere di riga che separa le coppie chiave/valore.

## Funzioni supportate {#supported-features}

Le seguenti funzioni sono supportate in TVSDK 2.1 per PlayStation 4:

**Versione 2.1.0.621**

* Ad Fallback, catena margherita nella logica di selezione degli annunci (Zendesk #3103)
Per gli annunci VAST (creativi) con la regola di fallback abilitata, TVSDK tratta un annuncio con un tipo MIME non valido come un annuncio vuoto e tenta di utilizzare gli annunci di fallback al suo posto.Puoi configurare alcuni aspetti del comportamento di fallback

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

* Consulta la documentazione completa della guida nella pagina [Informazioni e supporto per Adobe Primetime](https://helpx.adobe.com/support/primetime.html) .