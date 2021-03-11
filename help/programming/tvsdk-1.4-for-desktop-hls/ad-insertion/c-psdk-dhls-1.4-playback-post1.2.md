---
description: Il comportamento della riproduzione dei contenuti multimediali è influenzato dalla ricerca, dalla sospensione, dall'avanzamento rapido o dal riavvolgimento (modalità di riproduzione a trucco) e dall'inclusione della pubblicità.
title: Comportamento di riproduzione predefinito e personalizzato con annunci pubblicitari
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---


# Comportamento di riproduzione predefinito e personalizzato con annunci{#default-and-customized-playback-behavior-with-ads}

Il comportamento della riproduzione dei contenuti multimediali è influenzato dalla ricerca, dalla sospensione, dall&#39;avanzamento rapido o dal riavvolgimento (modalità di riproduzione a trucco) e dall&#39;inclusione della pubblicità.

Per ignorare il comportamento predefinito, utilizza `AdPolicySelector`.

>[!IMPORTANT]
>
>TVSDK non fornisce un modo per disabilitare la ricerca durante gli annunci. Adobe consiglia di configurare l&#39;applicazione per disabilitare la ricerca durante gli annunci.

La tabella seguente descrive come TVSDK gestisce gli annunci e le interruzioni pubblicitarie durante la riproduzione:

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
   <td colname="col1"> Durante la riproduzione normale, si verifica un'interruzione pubblicitaria. </td> 
   <td colname="col2"> 
    <ul id="ul_10D2638676EA4ADDA718E61BD4FDC1D2"> 
     <li id="li_D5CC30F063934C738971E2E8AF00C137"> Per live/lineari, riproduce l'interruzione pubblicitaria, anche se l'interruzione pubblicitaria è già stata osservata. </li> 
     <li id="li_D962C0938DA74186AE99D117E5A74E38">Per VOD, riproduce la pausa pubblicitaria e contrassegna la pausa pubblicitaria come guardato. </li> 
    </ul> </td> 
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
   <td colname="col3">Selezionare l'interruzione saltata da riprodurre utilizzando <span class="codeph"> selectAdBreaksToPlay</span>. </td> 
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
   <td colname="col3">Seleziona quale delle interruzioni saltate da riprodurre utilizzando <span class="codeph"> selectAdBreaksToPlay</span> e determina quali interruzioni sono già state controllate utilizzando <span class="codeph"> TimeLineItem.watch</span> . <p>Importante:  Per impostazione predefinita, TVSDK contrassegna un’interruzione pubblicitaria come osservata immediatamente dopo l’accesso al primo annuncio nell’interruzione pubblicitaria. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L'applicazione cerca in avanti o all'indietro su uno o più annunci break e drops in un annuncio break guardato. </td> 
   <td colname="col2"> Ignora l’interruzione pubblicitaria e cerca la posizione immediatamente dopo l’interruzione pubblicitaria. </td> 
   <td colname="col3">Specifica un diverso criterio di annunci per l'interruzione pubblicitaria (con lo stato guardato impostato su true) e per l'annuncio specifico in cui la ricerca è terminata utilizzando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L'applicazione entra nel gioco-trucco (modalità DVR). La velocità di riproduzione può essere negativa (riavvolgimento) o superiore a 1 (avanzamento rapido). </td> 
   <td colname="col2"> Ignora tutti gli annunci durante avanzamento rapido o riavvolgimento, riproduce l'ultima interruzione saltata dopo le fine del gioco di trucco e salta alla posizione di gioco di trucco selezionata dall'utente quando quella interruzione termina la riproduzione. </td> 
   <td colname="col3">Seleziona quale delle interruzioni saltate da riprodurre dopo il termine della riproduzione del trucco con <span class="codeph"> selectAdBreaksToPlay</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L’applicazione cerca in avanti rispetto agli annunci inseriti utilizzando marcatori di annunci personalizzati. </td> 
   <td colname="col2"> Passa alla posizione di ricerca selezionata dall’utente. </td> 
   <td colname="col3">Per ulteriori informazioni, vedere <a href="../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-ui-configure/t-psdk-dhls-1.4-ui-seek-scrub-bar-display.md" format="dita" scope="local"> Visualizzare una barra di scorrimento con la posizione di riproduzione corrente..</a> </td> 
  </tr> 
 </tbody> 
</table>

