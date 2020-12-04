---
title: Note sulla versione di TVSDK 2.1 PlayStation 4
seo-title: Note sulla versione di TVSDK 2.1 PlayStation 4
description: Le note sulla versione di TVSDK 2.1 per PlayStation 4 descrivono le funzioni supportate e i problemi noti di TVSDK 2.1 PlayStation 4.
seo-description: Le note sulla versione di TVSDK 2.1 per PlayStation 4 descrivono le funzioni supportate e i problemi noti di TVSDK 2.1 PlayStation 4.
uuid: 494569cf-07e2-476a-b88e-e46c9cca4cdc
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
discoiquuid: ebfc8819-f5a9-47a2-b454-0e4e6f9e4640
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 0%

---


# Note sulla versione di TVSDK 2.1 PlayStation 4 {#tvsdk-playstation-release-notes}

Le note sulla versione di TVSDK 2.1 per PlayStation 4 descrivono le funzioni supportate e i problemi noti di TVSDK 2.1 PlayStation 4.

## Problemi risolti {#resolved-issues}

Di seguito sono riportati i problemi risolti per TVSDK 2.1 per PlayStation 4:

**Versione 2.1.0.638**

* **PTPLAY-10439:**
Quando il collegamento del wrapper VMAP veniva interrotto, il lettore si bloccava nello stato Preparazione (non inviava 
`onComplete` al chiamante).

* **PTPLAY-10179:**

   `creativeRepackaging` e  `fallbackOnInvalidCreative` i valori ora sono disattivati per impostazione predefinita. Inoltre, quando il flag `creativeRepackaging` è stato impostato ma non è stato fornito il formato `creativeRepackaging`, `onRepackagingComplete` veniva chiamato il numero di volte in cui erano presenti annunci nell&#39;interruzione dell&#39;annuncio, causando la creazione di interruzioni pubblicitarie più volte.

* **Zendesk #10304**: La variabile di forveness on/off del feed non è stata inizializzata. È ora possibile inizializzare la variabile dal `DataSetEntry's` ctor.

* **PTPLAY-10318:**
È stato introdotto il supporto per la modalità in background.
* **Zendesk # 17409:**
Quando si passa alla modalità di riproduzione ingannevole, si ritorna alla modalità di riproduzione normale, poi alla modalità di riproduzione ingannevole, la posizione di riproduzione saltava.
* **PTPLAY-9552:**
Dopo l&#39;analisi dei file XML della risposta, il codice di errore 1108 viene ora inserito in un ping ogni volta che non sono presenti annunci pubblicitari.
* **PTPLAY-9551:**
In assenza di interruzioni pubblicitarie dopo l&#39;elaborazione di Auditude, il CRS richiama 
**** onPrefetchCompleteche decrementa il valore groupCount. Poiché non è presente alcuna interruzione di annuncio, il **groupCount** è 0 e decrementato di 1. In precedenza **groupCount** era **uint32_t** a causa del quale veniva utilizzato per passare al valore massimo. Ora è **int32_t**.

**Versione 2.1.0.621**

* **Zendesk #4555**
Instant on Memory - Errori di caricamento iniziali - 
`MediaItemLoader` Correzione dell&#39;arresto anomalo in fase di rilascio  `mediaitemloader`

* **Zendesk #17223**
2.x CSAI: Non tutti gli URL di tracciamento annunci attivati
   * Alcuni annunci VAST che a loro volta puntavano a un annuncio in linea mancavano gli url di tracciamento.
   * Quando in un annuncio in VAST XML sono presenti più tag di impression, solo il primo URL di impression è stato salvato e il resto è stato ignorato. Ora tutte le urle di impressione saranno salvate e pinged più tardi.
* **Zendesk #17224**
PS4 User agent spostare le informazioni primetime alla fine di UAString
* **Zendesk #17226**
2.x CSAI: Non tutti gli annunci sono rimasti bloccati.
\
   La correzione ha lo scopo di indicare che la timeline è cambiata a causa delle operazioni insertBy o eraseBy e che l&#39;opzione punto è stata modificata di conseguenza.

* **Zendesk #17284**
   [Tutte ] le piattaformeI sottotitoli codificati non vengono visualizzati.\
   HLS - supporto per il tag `EXT-X-MEDIA-TIME` per i file di sottotitoli VTT.

* **Zendesk #17889**
Riproduzione &quot;lattea&quot; su PS4
\
   yoffset corretto applicato (per conversione colore)

* **Zendesk #17954**
Logica di fallback degli annunci + gestione di un vasto vuoto
\
   È stato risolto il problema che si verificava se uno degli involucri Vast era vuoto, il parser Vast utilizzato per continuare a elaborare l&#39;involucro.

* **Zendesk #17807**
Impossibile superare vuoto vasto Come Zendesk #3103

* **Zendesk #17865**
Logica di fallback su PS4 e XBox One
\
   Come Zendesk #3103

**Versione 2.1.0.591**

* **Snippet di codice annuncio Zendesk #3767**
PS4. La risoluzione degli annunci non riesce durante l&#39;elaborazione dei reindirizzamenti VMAP.
* **Zendesk #4096**
PS4 CSAI: Errore di segmentazione Risolto l&#39;arresto anomalo quando TVSDK genera un errore di segmentazione quando la libreria di annunci elabora una risposta VMAP.

* **Zendesk #4161**
Trickplay 16x alla fine del filmato blocca Blocco fisso in caso di ritorno del trickplay alla riproduzione normale

* **Zendesk #4208**
Casuale Crash quando i sottotitoli codificati sono attivati Perdita di memoria fissa quando i sottotitoli codificati sono abilitati

* **Zendesk #4213**
PS4 CSAI: Modifica la stringa agente utente predefinita per tutte le chiamate relative agli annunci La stringa agente utente viene creata utilizzando la stessa stringa UA utilizzata dal browser con l&#39;aggiunta di una stringa Primetime

* **PTPLAY-7675** (interno) Gli annunci transcodificati non riproducevano Creative Repackage non riusciva quando veniva chiamato all&#39;interno di una risposta VMAP o VAST. Fix è semplicemente leggere il file multimediale da pubblicità invece di leggere da asset in caso di vasti annunci.

* **PTPLAY-7895** (interno) Quando  `allowMultipleAds=false`nessun annuncio viene riprodotto, viene riprodotto un bug fisso in cui  `allowMultipleAds` il parametro non veniva seguito correttamente.

* **PTPLAY-7896** (interno) Gli annunci pubblicitari vengono riprodotti in ordine di sequenza su PS4 Problema risolto: gli annunci non erano nell&#39;ordine in cui gli annunci comparivano nelle risposte XML.

* PS4 TVSDK testato all&#39;interno di una mini-app invece di un gioco.

**Versione 2.1.0.563**

* **Zendesk #3868**
Dispone di TVSDK per Playstation SDK 2.5 Il TVSDK è ora creato con l’SDK di Playstation 2.5.

* **Zendesk #4093**
targetingCoppie chiave-valore Info nella richiesta Pt Ads.
\
   È stato aggiunto un carattere nuova riga che separa le coppie chiave/valore.

## Funzioni supportate {#supported-features}

Le seguenti funzionalità sono supportate in TVSDK 2.1 per PlayStation 4:

**Versione 2.1.0.621**

* Ad Fallback, catena a margherita nella logica di selezione degli annunci (Zendesk #3103)
Per gli annunci VAST (creativi) con la regola di fallback abilitata, TVSDK tratta un annuncio con un tipo MIME non valido come un annuncio vuoto e tenta di utilizzare gli annunci di fallback al suo posto. È possibile configurare alcuni aspetti del comportamento di fallback

**Versione 2.1.0.538**

* Riproduzione HLS VOD, compresa riproduzione, pausa, ricerca
* Streaming bitrate adattivo
* Riproduzione di contenuti crittografati con DRM Primetime e contenuto protetto con vaniglia AES
* Inserimento di annunci lato client con comportamenti annunci predefiniti e perdono di annunci
* Reimballaggio creativo
* Sottotitoli codificati WebVTT
* Instant on con posizione iniziale personalizzata
* Gioco di mattoni con avanzamento rapido e riavvolgimento rapido
* Reindirizzamento 302

## Risorse utili {#helpful-resources}

* Consulta la documentazione completa della guida in linea alla pagina [ Informazioni e supporto per Adobe Primetime](https://helpx.adobe.com/support/primetime.html).