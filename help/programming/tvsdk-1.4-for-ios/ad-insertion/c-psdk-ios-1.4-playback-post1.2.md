---
description: Il comportamento della riproduzione dei contenuti multimediali è influenzato dalla ricerca, dalla sospensione e dall'inclusione della pubblicità.
title: Comportamento di riproduzione predefinito e personalizzato con annunci pubblicitari
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---


# Comportamento di riproduzione predefinito e personalizzato con annunci{#default-and-customized-playback-behavior-with-ads}

Il comportamento della riproduzione dei contenuti multimediali è influenzato dalla ricerca, dalla sospensione e dall&#39;inclusione della pubblicità.

Per ignorare il comportamento predefinito, utilizza `PTAdPolicySelector`.

>[!IMPORTANT]
>
>Per i VOD e lo streaming live/lineare, non è possibile rivedere le regolazioni della timeline. Questo significa che un annuncio non può essere rimosso dalla timeline dopo la riproduzione. Se l’utente cerca di nuovo, lo stesso annuncio viene riprodotto anche se il criterio normale sarebbe stato quello di rimuoverlo.

>[!IMPORTANT]
>
>TVSDK non fornisce un modo per disabilitare la ricerca durante gli annunci. Adobe consiglia di configurare l&#39;applicazione per disabilitare la ricerca durante gli annunci.

La tabella seguente descrive come TVSDK gestisce gli annunci e le interruzioni pubblicitarie durante la riproduzione:

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
   <td colname="col1"> Durante la riproduzione normale, si verifica un'interruzione pubblicitaria. </td> 
   <td colname="col2"></td> 
   <td colname="col3">Specifica un criterio diverso per l'interruzione pubblicitaria utilizzando <span class="codeph"> selectPolicyForAdBreak</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L'applicazione cerca in avanti e suddivide i contenuti principali. </td> 
   <td colname="col2"> Riproduce l'ultima interruzione pubblicitaria non osservata saltata e riprende la riproduzione nella posizione di ricerca desiderata al termine della riproduzione delle interruzioni. </td> 
   <td colname="col3">Selezionare l'interruzione saltata da riprodurre utilizzando <span class="codeph"> selectAdBreaksToPlay</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L'applicazione cerca all'indietro le interruzioni pubblicitarie nel contenuto principale. </td> 
   <td colname="col2"> Salta alla posizione di ricerca desiderata senza giocare ad break. </td> 
   <td colname="col3">Selezionare l'interruzione saltata da riprodurre utilizzando <span class="codeph"> selectAdBreaksToPlay</span>.                      </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La tua applicazione cerca in avanti in un annuncio break. </td> 
   <td colname="col2"> Riproduce dall’inizio dell’annuncio in cui la ricerca è terminata. </td> 
   <td colname="col3">Specifica un diverso criterio di annunci per l'interruzione pubblicitaria e per l'annuncio specifico in cui la ricerca è terminata utilizzando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L'applicazione cerca all'indietro in un'interruzione pubblicitaria. </td> 
   <td colname="col2"> Riproduce dall’inizio dell’annuncio in cui la ricerca è terminata. </td> 
   <td colname="col3">Specifica un diverso criterio per l'interruzione pubblicitaria e per l'annuncio specifico in cui la ricerca è terminata utilizzando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L'applicazione cerca in avanti o all'indietro gli annunci osservati e li suddivide in contenuti principali. </td> 
   <td colname="col2"> Se l’ultima interruzione pubblicitaria è già stata osservata, passa alla posizione di ricerca selezionata dall’utente. </td> 
   <td colname="col3">Seleziona quale delle interruzioni saltate da riprodurre utilizzando <span class="codeph"> selectAdBreaksToPlay</span> e determina quali interruzioni sono già state controllate utilizzando <span class="codeph"> PTAdBreak.isWatched</span>. <p> <p>Importante:  Per impostazione predefinita, TVSDK contrassegna un’interruzione pubblicitaria come osservata immediatamente dopo l’accesso al primo annuncio nell’interruzione pubblicitaria. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L'applicazione cerca in avanti o all'indietro su uno o più annunci break e drops in un annuncio break guardato. </td> 
   <td colname="col2"> Ignora l’interruzione pubblicitaria e cerca la posizione immediatamente dopo l’interruzione pubblicitaria. </td> 
   <td colname="col3">Specifica un diverso criterio di annunci per l'interruzione pubblicitaria (con lo stato guardato impostato su true) e per l'annuncio specifico in cui la ricerca è terminata utilizzando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L’applicazione cerca in avanti rispetto agli annunci inseriti utilizzando marcatori di annunci personalizzati. </td> 
   <td colname="col2"> Passa alla posizione di ricerca selezionata dall’utente. </td> 
   <td colname="col3"></td> 
  </tr> 
 </tbody> 
</table>

