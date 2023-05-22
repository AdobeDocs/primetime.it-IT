---
description: Questa tabella fornisce informazioni dettagliate sulle notifiche di tipo INFO.
title: Codici di notifica INFO
exl-id: 162c73c2-c077-4b50-b340-76938b15783a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 4%

---

# Codici di notifica INFO{#info-notification-codes}

Questa tabella fornisce informazioni dettagliate sulle notifiche di tipo INFO.

La maggior parte delle notifiche informative contiene metadati rilevanti, ad esempio l’URL della risorsa che non è stata scaricata. Alcune notifiche contengono metadati che consentono di specificare se il problema si è verificato nel contenuto video principale, nel contenuto audio alternativo o in un annuncio.

<table frame="all" colsep="1" rowsep="1" id="table_503463046E764A87B10EB5D8B294EB23"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Codice </th> 
   <th colname="2" class="entry"> Nome </th> 
   <th colname="3" class="entry"> Notifica interna </th> 
   <th colname="4" class="entry"> Chiavi metadati </th> 
   <th colname="5" class="entry"> Commenti </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>Riproduzione</b> </td> 
   <td colname="2"> </td>
   <td colname="3"> </td>
   <td colname="4"> </td>
   <td colname="5"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300000 </span> </td> 
   <td colname="2"><span class="codeph"> INIZIO_RIPRODUZIONE </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"> Nessuno </td> 
   <td colname="5"> Riproduzione avviata. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300001 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_COMPLETE </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"> Nessuno </td> 
   <td colname="5"> Riproduzione completata. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300002 </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_START </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"> <p> Nessuno </p> </td> 
   <td colname="5"> È stata avviata un’operazione di ricerca. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300003 </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_COMPLETE </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"> <p>Nessuno </p> </td> 
   <td colname="5"> Operazione di ricerca completata. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300005 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYER_STATE_CHANGE </span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"> <p>Nessuno </p> </td> 
   <td colname="5"> Lo stato del lettore è cambiato. Quando lo stato è ERROR, la notifica interna è l'oggetto di notifica dell'errore che ha attivato il passaggio allo stato ERROR. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Velocità bit adattive (ABR)</b> </td> 
   <td colname="2"> </td>
   <td colname="3"> </td>
   <td colname="4"> </td>
   <td colname="5"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 302000 </span> </td> 
   <td colname="2"><span class="codeph"> BITRATE_CHANGE </span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"><span class="codeph"> BITRATE </span> </td> 
   <td colname="5"> Il bitrate del video è cambiato. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Late-binding audio (LBA)</b> </td> 
   <td colname="2"> </td>
   <td colname="3"> </td>
   <td colname="4"> </td>
   <td colname="5"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 304000 </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_CHANGE </span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"> <p>Nessuno </p> </td> 
   <td colname="5"> <p>La traccia audio è cambiata. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Sottotitoli</b> </td> 
   <td colname="2"> </td>
   <td colname="3"> </td>
   <td colname="4"> </td>
   <td colname="5"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 307000 </span> </td> 
   <td colname="2"><span class="codeph"> SUBTITLES_TRACK_CHANGE </span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"> <p>Nessuno </p> </td> 
   <td colname="5"> <p>La traccia dei sottotitoli è cambiata. </p> </td> 
  </tr> 
 </tbody> 
</table>
