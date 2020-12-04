---
description: Il comportamento della riproduzione dei contenuti multimediali dipende dalla ricerca, la messa in pausa, l'avanzamento rapido o il riavvolgimento (modalità di riproduzione ingannevole) e l'inclusione di contenuti pubblicitari.
seo-description: Il comportamento della riproduzione dei contenuti multimediali dipende dalla ricerca, la messa in pausa, l'avanzamento rapido o il riavvolgimento (modalità di riproduzione ingannevole) e l'inclusione di contenuti pubblicitari.
seo-title: Comportamento di riproduzione predefinito e personalizzato con gli annunci
title: Comportamento di riproduzione predefinito e personalizzato con gli annunci
uuid: 45e6b0cd-fb0b-4896-b53a-d3bd78a3c1f3
translation-type: tm+mt
source-git-commit: fd686391df0fa711bba99bc1bc312c9ef619f184
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---


# Comportamento di riproduzione predefinito e personalizzato con annunci{#default-and-customized-playback-behavior-with-ads}

Il comportamento della riproduzione dei contenuti multimediali dipende dalla ricerca, la messa in pausa, l&#39;avanzamento rapido o il riavvolgimento (modalità di riproduzione ingannevole) e l&#39;inclusione di contenuti pubblicitari.

Per ignorare il comportamento predefinito, utilizzare `AdPolicySelector`.

>[!IMPORTANT]
>
>TVSDK non fornisce un modo per disabilitare la ricerca durante gli annunci.  Adobe consiglia di configurare l&#39;applicazione per disabilitare la ricerca durante gli annunci.

La tabella seguente descrive come TVSDK gestisce gli annunci e le interruzioni di annunci durante la riproduzione:

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Attività video </th> 
   <th colname="col2" class="entry"> Criterio di comportamento TVSDK predefinito </th> 
   <th colname="col3" class="entry">Personalizzazione disponibile tramite <span class="codeph"> AdPolicySelector</span> </th> 
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
   <td colname="col3">Selezionare l'interruzione saltata da riprodurre utilizzando <span class="codeph"> selectAdBreaksToPlay</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La tua applicazione cerca di andare avanti in un'interruzione pubblicitaria. </td> 
   <td colname="col2"> Viene riprodotto dall’inizio dell’annuncio nel quale la ricerca è terminata. </td> 
   <td colname="col3">Specificate un altro criterio di annuncio per l'interruzione dell'annuncio e per l'annuncio specifico a cui è terminata la ricerca utilizzando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L'applicazione cerca all'indietro in un'interruzione di annuncio. </td> 
   <td colname="col2"> Viene riprodotto dall’inizio dell’annuncio nel quale la ricerca è terminata. </td> 
   <td colname="col3">Specificate un altro criterio di annuncio per l'interruzione di annuncio e per l'annuncio specifico in cui la ricerca è terminata utilizzando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L'applicazione cerca in avanti o all'indietro gli annunci controllati nel contenuto principale. </td> 
   <td colname="col2"> Se l’ultima interruzione annuncio è già stata osservata, passa alla posizione di ricerca selezionata dall’utente. </td> 
   <td colname="col3">Selezionare una delle interruzioni ignorate da riprodurre con <span class="codeph"> selectAdBreaksToPlay</span> e determinare quali interruzioni sono già state osservate utilizzando <span class="codeph"> TimeLineItem.watching</span> . <p>Importante:  Per impostazione predefinita, TVSDK contrassegna un'interruzione di annuncio come visualizzata subito dopo l'immissione del primo annuncio nell'interruzione di annuncio. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L'applicazione cerca in avanti o indietro su uno o più annunci pubblicitari si interrompe e cade in un'interruzione pubblicitaria controllata. </td> 
   <td colname="col2"> Consente di saltare l'interruzione dell'annuncio e di cercare la posizione immediatamente dopo l'interruzione dell'annuncio. </td> 
   <td colname="col3">Specificate un altro criterio di annuncio per l'interruzione dell'annuncio (con lo stato guardato impostato su true) e per l'annuncio specifico a cui è terminata la ricerca utilizzando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L'applicazione entra in modalità "trucco-play" (DVR). La velocità di riproduzione può essere negativa (riavvolgimento) o maggiore di 1 (avanzamento rapido). </td> 
   <td colname="col2"> Consente di saltare tutti gli annunci durante l'avanzamento rapido o il riavvolgimento, di riprodurre l'ultima interruzione saltata dopo la fine del gioco del trucco e di passare alla posizione di riproduzione del trucco selezionata dall'utente al termine della riproduzione. </td> 
   <td colname="col3">Selezionare una delle interruzioni saltate da riprodurre al termine della riproduzione del trucco utilizzando <span class="codeph"> selectAdBreaksToPlay</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L'applicazione cerca in avanti rispetto agli annunci che sono stati inseriti utilizzando indicatori di annunci personalizzati. </td> 
   <td colname="col2"> Passa alla posizione di ricerca selezionata dall’utente. </td> 
   <td colname="col3">Per ulteriori informazioni, vedere <a href="../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-ui-configure/t-psdk-dhls-1.4-ui-seek-scrub-bar-display.md" format="dita" scope="local"> Visualizzare una barra di scorrimento della ricerca con la posizione di riproduzione corrente.</a> </td> 
  </tr> 
 </tbody> 
</table>

