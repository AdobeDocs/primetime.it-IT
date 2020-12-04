---
description: Il comportamento della riproduzione multimediale è influenzato dalla ricerca, dalla messa in pausa e dall'inclusione della pubblicità.
seo-description: Il comportamento della riproduzione multimediale è influenzato dalla ricerca, dalla messa in pausa e dall'inclusione della pubblicità.
seo-title: Comportamento di riproduzione predefinito e personalizzato con gli annunci
title: Comportamento di riproduzione predefinito e personalizzato con gli annunci
uuid: cc996e5c-bee2-451b-96cb-088df1694188
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---


# Comportamento di riproduzione predefinito e personalizzato con annunci{#default-and-customized-playback-behavior-with-ads}

Il comportamento della riproduzione multimediale è influenzato dalla ricerca, dalla messa in pausa e dall&#39;inclusione della pubblicità.

Per ignorare il comportamento predefinito, utilizzare `PTAdPolicySelector`.

>[!IMPORTANT]
>
>Per i VOD e lo streaming live/lineare, non è possibile modificare le regolazioni della timeline. Questo significa che un annuncio non può essere rimosso dalla timeline dopo che è stato riprodotto. Se l&#39;utente torna indietro, lo stesso annuncio viene riprodotto anche se il normale criterio sarebbe stato quello di rimuoverlo.

>[!IMPORTANT]
>
>TVSDK non fornisce un modo per disabilitare la ricerca durante gli annunci.  Adobe consiglia di configurare l&#39;applicazione per disabilitare la ricerca durante gli annunci.

La tabella seguente descrive come TVSDK gestisce gli annunci e le interruzioni di annunci durante la riproduzione:

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Attività video </th> 
   <th colname="col2" class="entry"> Criterio di comportamento TVSDK predefinito </th> 
   <th colname="col3" class="entry">Personalizzazione disponibile tramite <span class="codeph"> PTAdPolicySelector</span> </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Durante la riproduzione normale, viene rilevata un'interruzione di annuncio. </td> 
   <td colname="col2"></td> 
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
   <td colname="col3">Specificate un altro criterio di annuncio per l'interruzione di annuncio e per l'annuncio specifico in cui la ricerca è terminata utilizzando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L'applicazione cerca in avanti o all'indietro gli annunci controllati nel contenuto principale. </td> 
   <td colname="col2"> Se l’ultima interruzione annuncio è già stata osservata, passa alla posizione di ricerca selezionata dall’utente. </td> 
   <td colname="col3">Selezionare una delle interruzioni ignorate da riprodurre con <span class="codeph"> selectAdBreaksToPlay</span> e determinare quali interruzioni sono già state osservate utilizzando <span class="codeph"> PTAdBreak.isWatched</span>. <p> <p>Importante:  Per impostazione predefinita, TVSDK contrassegna un'interruzione di annuncio come visualizzata subito dopo l'immissione del primo annuncio nell'interruzione di annuncio. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L'applicazione cerca in avanti o indietro su uno o più annunci pubblicitari si interrompe e cade in un'interruzione pubblicitaria controllata. </td> 
   <td colname="col2"> Consente di saltare l'interruzione dell'annuncio e di cercare la posizione immediatamente dopo l'interruzione dell'annuncio. </td> 
   <td colname="col3">Specificate un altro criterio di annuncio per l'interruzione dell'annuncio (con lo stato guardato impostato su true) e per l'annuncio specifico a cui è terminata la ricerca utilizzando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L'applicazione cerca in avanti rispetto agli annunci che sono stati inseriti utilizzando indicatori di annunci personalizzati. </td> 
   <td colname="col2"> Passa alla posizione di ricerca selezionata dall’utente. </td> 
   <td colname="col3"></td> 
  </tr> 
 </tbody> 
</table>

