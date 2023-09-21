---
description: Il comportamento della riproduzione multimediale è influenzato dalla ricerca, dalla messa in pausa, dall’avanzamento rapido o dal riavvolgimento (modalità di riproduzione con trucco) e dall’inclusione della pubblicità.
title: Comportamento di riproduzione predefinito e personalizzato con annunci
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---

# Comportamento di riproduzione predefinito e personalizzato con annunci{#default-and-customized-playback-behavior-with-ads}

Il comportamento della riproduzione multimediale è influenzato dalla ricerca, dalla messa in pausa, dall’avanzamento rapido o dal riavvolgimento (modalità di riproduzione con trucco) e dall’inclusione della pubblicità.

Per ignorare il comportamento predefinito, utilizza `AdBreakPolicySelector`.

>[!IMPORTANT]
>
>Il TVSDK del browser non fornisce un modo per disabilitare la ricerca durante gli annunci. L’Adobe consiglia di configurare l’applicazione per disabilitare la ricerca durante gli annunci.

La tabella seguente descrive il modo in cui TVSDK del browser gestisce gli annunci e le interruzioni pubblicitarie durante la riproduzione:

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Attività video </th> 
   <th colname="col2" class="entry"> Criterio di comportamento predefinito TVSDK per browser </th> 
   <th colname="col3" class="entry">Personalizzazione disponibile tramite <span class="codeph"> AdBreakPolicySelector </span> </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Durante la riproduzione normale, si verifica un’interruzione pubblicitaria. </td> 
   <td colname="col2"> 
    <ul id="ul_10D2638676EA4ADDA718E61BD4FDC1D2"> 
     <li id="li_D5CC30F063934C738971E2E8AF00C137"> Per live/linear, riproduce l’interruzione pubblicitaria, anche se l’interruzione pubblicitaria è già stata guardata. </li> 
     <li id="li_D962C0938DA74186AE99D117E5A74E38">Per VOD, riproduce l’interruzione pubblicitaria e contrassegna l’interruzione pubblicitaria come guardata. </li> 
    </ul> </td> 
   <td colname="col3">Specifica un criterio diverso per l’interruzione pubblicitaria utilizzando <span class="codeph"> selectPolicyForAdBreak</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L’applicazione cerca tra le interruzioni pubblicitarie nel contenuto principale. </td> 
   <td colname="col2"> Riproduce l’ultima interruzione pubblicitaria non osservata che è stata ignorata e riprende la riproduzione nella posizione di ricerca desiderata al termine della riproduzione delle interruzioni. </td> 
   <td colname="col3">Seleziona l’interruzione saltata da riprodurre utilizzando <span class="codeph"> selectAdBreaksToPlay</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L’applicazione cerca all’indietro tra le interruzioni pubblicitarie nel contenuto principale. </td> 
   <td colname="col2"> Passa alla posizione di ricerca desiderata senza interruzioni pubblicitarie. </td> 
   <td colname="col3">Seleziona l’interruzione saltata da riprodurre utilizzando <span class="codeph"> selectAdBreaksToPlay</span>.                      </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L’applicazione cerca di creare un’interruzione pubblicitaria. </td> 
   <td colname="col2"> Riproduce dall’inizio dell’annuncio in cui si è conclusa la ricerca. </td> 
   <td colname="col3">Specifica un criterio di annuncio diverso per l’interruzione pubblicitaria e per l’annuncio specifico in cui la ricerca si è conclusa utilizzando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L’applicazione torna indietro e crea un’interruzione pubblicitaria. </td> 
   <td colname="col2"> Riproduce dall’inizio dell’annuncio in cui si è conclusa la ricerca. </td> 
   <td colname="col3">Specifica un criterio di annuncio diverso per l’interruzione pubblicitaria e per l’annuncio specifico in cui la ricerca si è conclusa utilizzando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L’applicazione cerca in avanti o all’indietro rispetto alle interruzioni pubblicitarie osservate nel contenuto principale. </td> 
   <td colname="col2"> Se l’ultima interruzione pubblicitaria saltata è già stata guardata, passa alla posizione di ricerca selezionata dall’utente. </td> 
   <td colname="col3">Seleziona con quale delle interruzioni saltate riprodurre <span class="codeph"> selectAdBreaksToPlay</span> e determinare quali interruzioni sono già state osservate utilizzando <span class="codeph"> isWatched</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L’applicazione cerca in avanti o all’indietro attraverso una o più interruzioni pubblicitarie e cade in un’interruzione pubblicitaria osservata. </td> 
   <td colname="col2"> Ignora l’interruzione pubblicitaria e cerca la posizione immediatamente successiva all’interruzione pubblicitaria. </td> 
   <td colname="col3">Specifica un criterio di annuncio diverso per l’interruzione pubblicitaria (con lo stato di visualizzazione impostato su true) e per l’annuncio specifico in cui la ricerca si è conclusa utilizzando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L’applicazione cerca in avanti gli annunci inseriti utilizzando marcatori di annunci personalizzati. </td> 
   <td colname="col2"> Passa alla posizione di ricerca selezionata dall'utente. </td> 
   <td colname="col3">Per ulteriori informazioni, consulta <a href="../../browser-tvsdk-2.4/content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-seek-scrub-bar-display.md" format="dita" scope="local"> Gestire la ricerca quando si utilizza la barra di ricerca</a> </td> 
  </tr> 
 </tbody> 
</table>

## Configurazione di comportamenti pubblicitari personalizzati {#section_custom_ad_behaviors}

Puoi impostare il comportamento desiderato nella factory del contenuto dell’annuncio in `retrieveAdPolicySelectorCallbackFunc` metodo. È possibile utilizzare `selectPolicyForAdBreak`, `selectWatchedPolicyForAdBreak`, `selectPolicyForSeekIntoAd`, e `selectAdBreaksToPlay` metodi nella content factory per selezionare un criterio.
