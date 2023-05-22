---
description: Il comportamento della riproduzione multimediale è influenzato dalla ricerca, dalla messa in pausa, dall’avanzamento rapido o dal riavvolgimento (modalità di riproduzione con trucco) e dall’inclusione della pubblicità.
title: Comportamento di riproduzione predefinito e personalizzato con annunci
exl-id: 242a94e7-acc1-4676-b8a7-9652d4fd1e7e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 0%

---

# Comportamento di riproduzione predefinito e personalizzato con annunci {#default-and-customized-playback-behavior-with-ads}

Il comportamento della riproduzione multimediale è influenzato dalla ricerca, dalla messa in pausa, dall’avanzamento rapido o dal riavvolgimento (modalità di riproduzione con trucco) e dall’inclusione della pubblicità.

Per ignorare il comportamento predefinito, utilizza `AdBreakPolicySelector`.

>[!IMPORTANT]
>
>TVSDK non fornisce un modo per disabilitare la ricerca durante gli annunci. L’Adobe consiglia di configurare l’applicazione per disabilitare la ricerca durante gli annunci.

Ecco il comportamento di riproduzione per contenuti live/lineari:

* La ripresa della riproduzione dopo una pausa determina la riproduzione del contenuto memorizzato nel buffer al momento della pausa.

   Se la posizione di ripresa è ancora nell&#39;intervallo di riproduzione, la riproduzione deve essere continua. In caso contrario, TVSDK passa al nuovo punto di attivazione. È inoltre possibile eseguire un&#39;operazione di ricerca e selezionare un punto di riproduzione diverso.
* TVSDK risolve gli annunci tra i segnali dopo la posizione in cui l’applicazione entra in riproduzione dal vivo.

   La riproduzione inizia dopo la risoluzione del primo segnale. Il valore predefinito per l’immissione della riproduzione live è il punto live del client, ma puoi scegliere una posizione diversa. Tutti i segnali prima della posizione iniziale vengono risolti dopo che l&#39;applicazione esegue una ricerca nella finestra del DVR.

La tabella seguente descrive come TVSDK gestisce gli annunci e le interruzioni pubblicitarie durante la riproduzione:

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Attività video </th> 
   <th colname="col2" class="entry"> Criterio del comportamento predefinito di TVSDK </th> 
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
   <td colname="col3">Seleziona con quale delle interruzioni saltate riprodurre <span class="codeph"> selectAdBreaksToPlay</span> e determinare quali interruzioni sono già state osservate utilizzando <span class="codeph"> AdBreak.isWatched</span>. <p>Importante: per impostazione predefinita, TVSDK contrassegna un’interruzione pubblicitaria come guardata immediatamente dopo l’immissione del primo annuncio nell’interruzione pubblicitaria. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L’applicazione cerca in avanti o all’indietro attraverso una o più interruzioni pubblicitarie e cade in un’interruzione pubblicitaria osservata. </td> 
   <td colname="col2"> Ignora l’interruzione pubblicitaria e cerca la posizione immediatamente successiva all’interruzione pubblicitaria. </td> 
   <td colname="col3">Specifica un criterio di annuncio diverso per l’interruzione pubblicitaria (con lo stato di visualizzazione impostato su true) e per l’annuncio specifico in cui la ricerca si è conclusa utilizzando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L'applicazione entra nella modalità di riproduzione con trucco (modalità DVR). La velocità di riproduzione può essere negativa (riavvolgimento) o maggiore di 1 (avanzamento rapido). </td> 
   <td colname="col2"> Ignora tutti gli annunci durante l'avanzamento o il riavvolgimento rapido, riproduce l'ultima interruzione ignorata al termine della riproduzione con trucco e passa alla posizione di riproduzione con trucco selezionata dall'utente al termine dell'interruzione. </td> 
   <td colname="col3">Selezionare le interruzioni ignorate da riprodurre al termine della riproduzione con la tecnica del trucco <span class="codeph"> selectAdBreaksToPlay</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> L’applicazione cerca in avanti gli annunci inseriti utilizzando marcatori di annunci personalizzati. </td> 
   <td colname="col2"> Passa alla posizione di ricerca selezionata dall'utente. </td> 
   <td colname="col3">Per ulteriori informazioni, consulta <a href="../../tvsdk-1.4-for-android/ui-configure/android-1.4-ui-seek-scrub-bar-display.md">Visualizza una barra di scorrimento di ricerca con la posizione di riproduzione corrente</a>. </td> 
  </tr> 
 </tbody> 
</table>
