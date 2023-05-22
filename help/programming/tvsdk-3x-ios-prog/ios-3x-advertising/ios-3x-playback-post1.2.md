---
description: Il comportamento della riproduzione dei contenuti multimediali è influenzato dalla ricerca, dalla sospensione e dall’inclusione di annunci pubblicitari.
title: Comportamento di riproduzione predefinito e personalizzato con annunci
exl-id: f4b2f317-c580-45a9-ad79-0cfa6c21848b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# Comportamento di riproduzione predefinito e personalizzato con annunci {#default-and-customized-playback-behavior-with-ads}

Il comportamento della riproduzione dei contenuti multimediali è influenzato dalla ricerca, dalla sospensione e dall’inclusione di annunci pubblicitari.

Per ignorare il comportamento predefinito, utilizza `PTAdPolicySelector`.

>[!IMPORTANT]
>
>Per VOD e streaming live/lineare, le regolazioni della timeline non possono essere riviste. Ciò significa che un annuncio pubblicitario non può essere rimosso dalla timeline dopo che è stato riprodotto. Se l’utente cerca indietro, lo stesso annuncio viene riprodotto nuovamente anche se la normale policy sarebbe stata quella di rimuoverlo.

>[!IMPORTANT]
>
>TVSDK non fornisce un modo per disabilitare la ricerca durante gli annunci. L’Adobe consiglia di configurare l’applicazione per disabilitare la ricerca durante gli annunci.

La tabella seguente descrive come TVSDK gestisce gli annunci e le interruzioni pubblicitarie durante la riproduzione:

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>Attività video</b></th> 
   <th colname="col2" class="entry"><b>Criterio del comportamento predefinito di TVSDK</b></th> 
   <th colname="col3" class="entry"><b>Personalizzazione disponibile tramite PTAdPolicySelector</b></th>
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Durante la riproduzione normale, si verifica un’interruzione pubblicitaria. </td> 
   <td colname="col2"></td> 
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
   <td colname="col3">Seleziona con quale delle interruzioni saltate riprodurre <span class="codeph"> selectAdBreaksToPlay</span> e determinare quali interruzioni sono già state osservate utilizzando <span class="codeph"> PTAdBreak.isWatched</span>. <p> <p>Importante: per impostazione predefinita, TVSDK contrassegna un’interruzione pubblicitaria come guardata immediatamente dopo l’immissione del primo annuncio nell’interruzione pubblicitaria. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L’applicazione cerca in avanti o all’indietro attraverso una o più interruzioni pubblicitarie e cade in un’interruzione pubblicitaria osservata. </td> 
   <td colname="col2"> Ignora l’interruzione pubblicitaria e cerca la posizione immediatamente successiva all’interruzione pubblicitaria. </td> 
   <td colname="col3">Specifica un criterio di annuncio diverso per l’interruzione pubblicitaria (con lo stato di visualizzazione impostato su true) e per l’annuncio specifico in cui la ricerca si è conclusa utilizzando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L’applicazione cerca in avanti gli annunci inseriti utilizzando marcatori di annunci personalizzati. </td> 
   <td colname="col2"> Passa alla posizione di ricerca selezionata dall'utente. </td> 
   <td colname="col3"></td> 
  </tr> 
 </tbody> 
</table>
