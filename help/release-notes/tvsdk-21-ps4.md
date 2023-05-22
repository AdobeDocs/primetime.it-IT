---
title: Note sulla versione di TVSDK 2.1 PlayStation 4
description: Le note sulla versione di TVSDK 2.1 per PlayStation 4 descrivono le funzioni supportate e i problemi noti di TVSDK 2.1 PlayStation 4.
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

Le note sulla versione di TVSDK 2.1 per PlayStation 4 descrivono le funzioni supportate e i problemi noti di TVSDK 2.1 PlayStation 4.

## Problemi risolti {#resolved-issues}

Di seguito sono riportati i problemi risolti per TVSDK 2.1 per PlayStation 4:

**Versione 2.1.0.638**

* **PTPLAY-10439:**
Quando il collegamento dell’annuncio wrapper VMAP era interrotto, il lettore si bloccava in stato di preparazione (non veniva inviato 
`onComplete` al chiamante).

* **PTPLAY-10179:**

   `creativeRepackaging` e `fallbackOnInvalidCreative` I valori sono disattivati per impostazione predefinita. Inoltre, quando `creativeRepackaging` il contrassegno è stato impostato ma non `creativeRepackaging` è stato fornito, il `onRepackagingComplete` veniva chiamato tante volte quante erano gli annunci nell’interruzione pubblicitaria, causando la creazione di più interruzioni pubblicitarie.

* **#10304 Zendesk**: la variabile di attivazione/disattivazione della forveness dell’annuncio non è stata inizializzata. Ora inizializziamo la variabile da `DataSetEntry's` attore.

* **PTPLAY-10318:**
È stato introdotto il supporto per la modalità in background.
* **Zendesk # 17409:**
Quando si passa alla modalità di riproduzione con trucco, quindi si torna alla modalità di riproduzione normale, quindi di nuovo alla modalità di riproduzione con trucco, la posizione di riproduzione stava saltando.
* **PTPLAY-9552**
Dopo aver analizzato i file XML di risposta, il codice di errore 1108 viene ora eseguito il ping ogni volta che non sono presenti annunci.
* **PTPLAY-9551**
Quando non c’è un’interruzione pubblicitaria dopo l’elaborazione di Auditude, il CRS chiama 
**onPrefetchComplete** che decrementa groupCount. Non essendoci pubblicità, la **groupCount** è 0 e diminuito di 1. Precedentemente il **groupCount** è stato **uint32_t** a causa del quale è stato utilizzato per passare al valore massimo. Questo è ora **int32_t**.

**Versione 2.1.0.621**

* **#4555 Zendesk**
Problemi di memoria immediata che causano errori di caricamento - 
`MediaItemLoader` Correzione per l’arresto anomalo durante il rilascio `mediaitemloader`

* **#17223 Zendesk**
CSAI 2.x: non tutti gli URL di tracciamento degli annunci vengono attivati
   * In alcuni annunci VAST, che a loro volta indicavano un annuncio in linea, mancavano gli URL di tracciamento.
   * Quando in un annuncio in VAST XML sono presenti più tag di impression, è stato salvato solo il primo URL di impression e gli altri sono stati ignorati. Ora tutti gli URL di impression verranno salvati e ping in un secondo momento.
* **#17224 Zendesk**
Agente utente PS4: spostare le informazioni primetime alla fine di UAString
* **#17226 Zendesk**
2.x CSAI: non tutti gli annunci uniti in.
\
   Correggi indica che la timeline è stata modificata a causa delle operazioni insertBy o eraseBy ed esegui di conseguenza il passaggio del periodo.

* **#17284 Zendesk**
   [Tutte le piattaforme] I sottotitoli non vengono visualizzati.\
   HLS: supporto per `EXT-X-MEDIA-TIME` per i file di didascalia VTT.

* **#17889 Zendesk**
Riproduzione &quot;Milky&quot; su PS4
\
   yoffset corretto applicato (per la conversione del colore)

* **#17954 Zendesk**
Logica di fallback dell’annuncio + gestione di un vasto vuoto
\
   È stato risolto il problema che si verificava se uno dei wrapper Vast era vuoto, ovvero il parser Vast utilizzato per continuare l’elaborazione del wrapper.

* **#17807 Zendesk**
Impossibile superare vaste vuote Come Zendesk #3103

* **#17865 Zendesk**
Logica di fallback su PS4 e XBox One
\
   Come Zendesk #3103

**Versione 2.1.0.591**

* **#3767 Zendesk**
Frammento di codice annuncio PS4, la risoluzione degli annunci non riesce durante l&#39;elaborazione dei reindirizzamenti VMAP.
* **#4096 Zendesk**
PS4 CSAI: errore di segmentazione È stato corretto un arresto anomalo quando TVSDK genera un errore di segmentazione quando la libreria di annunci elabora una risposta VMAP.

* **#4161 Zendesk**
Trickplay 16x alla fine del filmato si blocca Fisso deadlock che si verifica quando il trickplay ritorna alla riproduzione normale

* **#4208 Zendesk**
Arresto anomalo casuale quando i sottotitoli codificati sono attivati Perdita di memoria fissa quando i sottotitoli codificati sono attivati

* **#4213 Zendesk**
CSAI PS4: modificare la stringa predefinita dell’agente utente per tutte le chiamate relative agli annunci La stringa dell’agente utente viene creata utilizzando la stessa stringa UA utilizzata dal browser + aggiungi stringa Primetime

* **PTPLAY-7675** (interno) Gli annunci transcodificati non riproducono Creative Repackaging che non riusciva quando veniva chiamato all’interno di una risposta VMAP o VAST. La correzione consiste nel leggere semplicemente il file multimediale dall’annuncio invece di leggere dalla risorsa in caso di annunci vasti.

* **PTPLAY-7895** (interno) Quando `allowMultipleAds=false`, no ads play Correzione bug in cui `allowMultipleAds` il parametro non veniva seguito correttamente.

* **PTPLAY-7896** (interno) Gli annunci vengono riprodotti fuori sequenza su PS4 Fixed problema in cui gli annunci non erano nell&#39;ordine in cui gli annunci sono apparsi nelle risposte XML.

* TVSDK PS4 riprovato all&#39;interno di una mini-app invece che nel gioco.

**Versione 2.1.0.563**

* **#3868 Zendesk**
TVSDK supporta Playstation SDK 2.5 TVSDK è ora integrato con l’SDK 2.5 Playstation.

* **#4093 Zendesk**
coppie chiave-valore targetingInfo nella richiesta Pt Ads.
\
   È stato aggiunto un carattere di nuova riga che separa le coppie chiave/valore.

## Funzioni supportate {#supported-features}

TVSDK 2.1 supporta le seguenti funzioni per PlayStation 4:

**Versione 2.1.0.621**

* Fallback di annunci, concatenamento a margherita nella logica di selezione degli annunci (#3103 Zendesk) Per gli annunci VAST (creativi) con la regola di fallback abilitata, TVSDK tratta un annuncio con un tipo MIME non valido come un annuncio vuoto e tenta di utilizzare gli annunci di fallback al suo posto.Puoi configurare alcuni aspetti del comportamento di fallback

**Versione 2.1.0.538**

* Riproduzione VOD HLS, tra cui riproduzione, pausa, ricerca
* Streaming bitrate adattivo
* Riproduzione di contenuti crittografati con DRM Primetime e contenuti protetti da AES Vanilla
* Inserimento di annunci lato client con comportamenti di annunci predefiniti e perdono degli annunci
* Repackaging creativo
* Sottotitoli WebVTT
* Attivazione immediata con posizione iniziale personalizzata
* Gioco a trucchetto con avanzamento rapido e riavvolgimento rapido
* Reindirizzamento 302

## Risorse utili {#helpful-resources}

* Consulta la documentazione completa dell’Aiuto all’indirizzo [Informazioni e supporto per Adobe Primetime](https://experienceleague.adobe.com/docs/primetime.html) pagina.
