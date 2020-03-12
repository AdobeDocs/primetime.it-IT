---
description: Il comportamento della riproduzione dei contenuti multimediali dipende dalla ricerca, dalla messa in pausa, dall’avanzamento rapido o dal riavvolgimento e dalla pubblicità.
seo-description: Il comportamento della riproduzione dei contenuti multimediali dipende dalla ricerca, dalla messa in pausa, dall’avanzamento rapido o dal riavvolgimento e dalla pubblicità.
seo-title: Comportamento di riproduzione predefinito e personalizzato con gli annunci
title: Comportamento di riproduzione predefinito e personalizzato con gli annunci
uuid: 272cdfd0-799f-41e5-bf41-1620d48c992a
translation-type: tm+mt
source-git-commit: 21d1eae53cea303221de00765724e787cf6e84ef

---


# Comportamento di riproduzione predefinito e personalizzato con gli annunci{#default-and-customized-playback-behavior-with-ads}

Il comportamento della riproduzione dei contenuti multimediali dipende dalla ricerca, dalla messa in pausa, dall’avanzamento rapido o dal riavvolgimento e dalla pubblicità.

Per ignorare il comportamento predefinito, utilizzate `AdBreakPolicySelector` .

>[!IMPORTANT]
>
>TVSDK non fornisce un modo per disabilitare la ricerca durante gli annunci. Adobe consiglia di configurare l&#39;applicazione per disabilitare la ricerca durante gli annunci.

Di seguito è riportato il comportamento di riproduzione per i contenuti live/lineari:

* La ripresa della riproduzione dopo una pausa comporta la riproduzione del contenuto memorizzato nel buffer al momento della pausa.

   Se la posizione di ripresa è ancora compresa nell’intervallo di riproduzione, la riproduzione deve essere continua. In caso contrario, TVSDK passa al nuovo punto attivo. È inoltre possibile eseguire un&#39;operazione di ricerca e selezionare un altro punto di riproduzione.
* TVSDK risolve gli annunci tra suggerimenti dopo la posizione in cui l&#39;applicazione entra in riproduzione dal vivo.

   La riproduzione inizia dopo la risoluzione del primo cue point. Il valore predefinito per l’immissione della riproduzione in diretta è il punto di attivazione del client, ma potete scegliere una posizione diversa. Tutti i suggerimenti prima della posizione iniziale vengono risolti dopo che l&#39;applicazione esegue una ricerca nella finestra DVR.

La tabella seguente descrive come TVSDK gestisce gli annunci e le interruzioni di annunci durante la riproduzione:

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Attività video </th> 
   <th colname="col2" class="entry"> Criterio di comportamento TVSDK predefinito </th> 
   <th colname="col3" class="entry">Personalizzazione disponibile tramite <span class="codeph"> AdBreakPolicySelector </span> </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Durante la riproduzione normale, viene rilevata un'interruzione di annuncio. </td> 
   <td colname="col2"> 
    <ul id="ul_10D2638676EA4ADDA718E61BD4FDC1D2"> 
     <li id="li_D5CC30F063934C738971E2E8AF00C137"> Per live/linear, riproduce l'interruzione dell'annuncio, anche se l'interruzione dell'annuncio è già stata osservata. </li> 
     <li id="li_D962C0938DA74186AE99D117E5A74E38">Per VOD, riproduce l'interruzione dell'annuncio e contrassegna l'interruzione dell'annuncio come osservata. </li> 
    </ul> </td> 
   <td colname="col3">Specificate un criterio diverso per l'interruzione dell'annuncio utilizzando <span class="codeph"> selectPolicyForAdBreak</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L'applicazione cerca in avanti gli annunci nel contenuto principale. </td> 
   <td colname="col2"> Riproduce l’ultima interruzione non osservata saltata e riprende la riproduzione nella posizione di ricerca desiderata al termine della riproduzione delle interruzioni. </td> 
   <td colname="col3">Selezionare l'interruzione saltata da riprodurre utilizzando <span class="codeph"> selectAdBreaksToPlay</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L'applicazione cerca all'indietro le interruzioni pubblicitarie nel contenuto principale. </td> 
   <td colname="col2"> Consente di saltare la posizione di ricerca desiderata senza la riproduzione di annunci pubblicitari interrotti. </td> 
   <td colname="col3">Selezionare l'interruzione saltata da riprodurre utilizzando <span class="codeph"> selectAdBreaksToPlay</span>.                      </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La tua applicazione cerca di andare avanti in un'interruzione pubblicitaria. </td> 
   <td colname="col2"> Viene riprodotto dall’inizio dell’annuncio nel quale la ricerca è terminata. </td> 
   <td colname="col3">Specificate un altro criterio di annuncio per l'interruzione dell'annuncio e per l'annuncio specifico a cui è terminata la ricerca utilizzando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L'applicazione cerca all'indietro in un'interruzione di annuncio. </td> 
   <td colname="col2"> Viene riprodotto dall’inizio dell’annuncio nel quale la ricerca è terminata. </td> 
   <td colname="col3">Specificate un diverso criterio di annuncio per l'interruzione di annuncio e per l'annuncio specifico in cui la ricerca è terminata utilizzando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L'applicazione cerca in avanti o all'indietro gli annunci controllati nel contenuto principale. </td> 
   <td colname="col2"> Se l’ultima interruzione annuncio è già stata osservata, passa alla posizione di ricerca selezionata dall’utente. </td> 
   <td colname="col3">Selezionare una delle interruzioni saltate da riprodurre utilizzando <span class="codeph"> selectAdBreaksToPlay</span> e determinare quali interruzioni sono già state osservate utilizzando <span class="codeph"> AdBreak.isWatched</span> . <p>Importante:  Per impostazione predefinita, TVSDK contrassegna un'interruzione di annuncio come visualizzata subito dopo l'immissione del primo annuncio nell'interruzione di annuncio. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L'applicazione cerca in avanti o indietro su uno o più annunci pubblicitari si interrompe e cade in un'interruzione pubblicitaria controllata. </td> 
   <td colname="col2"> Consente di saltare l'interruzione dell'annuncio e di cercare la posizione immediatamente dopo l'interruzione dell'annuncio. </td> 
   <td colname="col3">Specificate un altro criterio di annuncio per l'interruzione dell'annuncio (con lo stato guardato impostato su true) e per l'annuncio specifico a cui è terminata la ricerca utilizzando <span class="codeph"> selectPolicyForSeekInto</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L'applicazione entra in modalità "trucco-play" (DVR). La velocità di riproduzione può essere negativa (riavvolgimento) o maggiore di 1 (avanzamento rapido). </td> 
   <td colname="col2"> Consente di saltare tutti gli annunci durante l'avanzamento rapido o il riavvolgimento, di riprodurre l'ultima interruzione saltata dopo la fine del gioco del trucco e di passare alla posizione di riproduzione del trucco selezionata dall'utente al termine della riproduzione. </td> 
   <td colname="col3">Selezionare una delle interruzioni saltate da riprodurre al termine della riproduzione del trucco utilizzando <span class="codeph"> SelectAdBreaksToPlay</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L'applicazione cerca in avanti rispetto agli annunci che sono stati inseriti utilizzando indicatori di annunci personalizzati. </td> 
   <td colname="col2"> Passa alla posizione di ricerca selezionata dall’utente. </td> 
   <td colname="col3">Per ulteriori informazioni, consultate <a href="../../tvsdk-2.7-for-android/content-playback-options/ui-configure/t-psdk-android-2.7-ui-seek-scrub-bar-display.md" format="dita" scope="local"> Visualizzare una barra di scorrimento con la posizione di riproduzione corrente.</a> </td> 
  </tr> 
 </tbody> 
</table>