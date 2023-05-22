---
description: Questa tabella fornisce informazioni dettagliate su INFO. digita le notifiche.
title: Codici di notifica INFO
exl-id: 65cd0a63-c765-4624-9028-d46cb8fbec3a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 4%

---

# Codici di notifica INFO{#info-notification-codes}

Questa tabella fornisce informazioni dettagliate su INFO. digita le notifiche.

<!--<a id="section_ED4302E363AE48CBA2C3E0B71AE612D8"></a>-->

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
   <td colname="4"><span class="codeph"> SEEK_TIME</span> </td> 
   <td colname="5"> È stata avviata un’operazione di ricerca. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300003 </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_COMPLETE </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> SEEK_TIME</span> </td> 
   <td colname="5"> Operazione di ricerca completata. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300004 </span> </td> 
   <td colname="2"><span class="codeph"> CONTENT_CHANGE </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"> <span class="codeph"> CONTENT_ID</span> <span class="codeph"> CURRENT_MEDIA_TIME</span> </td> 
   <td colname="5"> Il tempo di riproduzione corrente ha superato il bordo tra il contenuto principale e quello alternativo. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300005 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYER_STATE_CHANGE </span> </td> 
   <td colname="3"> <p>Qualsiasi notifica di errore. </p> </td> 
   <td colname="4"><span class="codeph"> STATO </span> </td> 
   <td colname="5"> Lo stato del lettore è cambiato. Quando lo stato è ERROR, la notifica interna è l'oggetto di notifica dell'errore che ha attivato il passaggio allo stato ERROR. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300006 </span> </td> 
   <td colname="2"><span class="codeph"> MARCATORE_CONTENUTO </span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"><span class="codeph"> CONTENT_ID CURRENT_MEDIA_TIME </span> </td> 
   <td colname="5"> Marcatore contenuto ricevuto. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300100 </span> </td> 
   <td colname="2"><span class="codeph"> LOAD_INFO_AVAILABLE </span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"> <span class="codeph"> URL_FRAMMENTO</span> <span class="codeph"> FRAGMENT_SIZE</span> <span class="codeph"> FRAGMENT_DOWNLOAD_DURATION</span> <span class="codeph"> PERIOD_INDEX</span> </td> 
   <td colname="5"> Fornisce informazioni relative al modo in cui i segmenti video vengono scaricati. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300101 </span> </td> 
   <td colname="2"><span class="codeph"> VIDEO_SIZE_CHANGED </span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"> <span class="codeph"> ALTEZZA</span> <p><span class="codeph"> LARGHEZZA</span> </p> </td> 
   <td colname="5"> Le dimensioni della finestra di riproduzione del video sono state modificate. </td> 
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
   <td colname="4"><span class="codeph"> BITRATE </span><span class="codeph"> CURRENT_MEDIA_TIME </span> </td> 
   <td colname="5"> Il bitrate del video è cambiato. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Elaborazione annunci</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303000 </span> </td> 
   <td colname="2"><span class="codeph"> TIMELINE_CHANGE </span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"><span class="codeph"> CONTENT_ID </span><span class="codeph"> PERIOD_INDEX </span> </td> 
   <td colname="5"> La timeline è stata modificata (ad esempio, è stato aggiunto o rimosso contenuto alternativo). </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303001 </span> </td> 
   <td colname="2"><span class="codeph"> AD_BREAK_ PLACEMENT_COMPLETE </span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"> <span class="codeph"> ROTTURA_ANNUNCIO_PROPOSTO</span> <span class="codeph"> ACCEPTED_AD_BREAK</span> </td> 
   <td colname="5"> Un'interruzione pubblicitaria proposta è stata accettata da <code>primetime-sdk-name</code> e posizionato (interamente o parzialmente) sulla timeline di riproduzione. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303002 </span> </td> 
   <td colname="2"><span class="codeph"> AD_BREAK_START </span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"><span class="codeph"> AD_BREAK </span> </td> 
   <td colname="5"> La riproduzione di una particolare interruzione pubblicitaria è stata avviata. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303003 </span> </td> 
   <td colname="2"><span class="codeph"> AD_BREAK_COMPLETE </span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"><span class="codeph"> AD_BREAK </span> </td> 
   <td colname="5"> La riproduzione di una particolare interruzione pubblicitaria è stata completata. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303004 </span> </td> 
   <td colname="2"><span class="codeph"> AD_START </span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"> <span class="codeph"> AD_BREAK</span> <p><span class="codeph"> ANNUNCIO</span> </p> </td> 
   <td colname="5"> La riproduzione di un particolare annuncio è stata avviata. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303005 </span> </td> 
   <td colname="2"><span class="codeph"> AD_COMPLETE </span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"> <span class="codeph"> AD_BREAK</span> <p><span class="codeph"> ANNUNCIO</span> </p> </td> 
   <td colname="5"> La riproduzione di un particolare annuncio è stata completata. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303006 </span> </td> 
   <td colname="2"><span class="codeph"> AD_PROGRESS </span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"> <span class="codeph"> AD_BREAK</span> <p><span class="codeph"> ANNUNCIO</span> </p> <span class="codeph"> AVANZAMENTO</span> </td> 
   <td colname="5"> La riproduzione di un particolare annuncio ha raggiunto una certa percentuale di quel particolare annuncio. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303007 </span> </td> 
   <td colname="2"><span class="codeph"> TIMED_METADATA_ADD </span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"> <span class="codeph"> TIPO</span> <p><span class="codeph"> ID</span> </p> <span class="codeph"> NOME</span> <p><span class="codeph"> ORA</span> </p> </td> 
   <td colname="5"> Nel manifesto è stato rilevato un nuovo metadati temporizzati. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303008 </span> </td> 
   <td colname="2"><span class="codeph"> AD_CLICK </span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"> <span class="codeph"> AD_BREAK</span> <p><span class="codeph"> ANNUNCIO</span> </p> <span class="codeph"> AD_CLICK</span> </td> 
   <td colname="5"> Restituisce le informazioni su un annuncio su cui l’utente ha fatto clic. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303009</span> </td> 
   <td colname="2"><span class="codeph"> AD_BREAK_SKIPPED</span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"> <span class="codeph"> AD_BREAK</span> <p><span class="codeph"> ANNUNCIO</span> </p> <span class="codeph"> AD_CLICK</span> </td> 
   <td colname="5"> Un’interruzione pubblicitaria è stata ignorata. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname=""><b>Late-binding audio (LBA)</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 304000 </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_CHANGE </span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"><span class="codeph"> TRACK_ID </span><span class="codeph"> CURRENT_MEDIA_TIME </span> </td> 
   <td colname="5"> La traccia audio è cambiata. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>DRM</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 305000 </span> </td> 
   <td colname="2"><span class="codeph"> DRM_METADATA_AVAILABLE </span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"><span class="codeph"> PREFETCH_TIMESTAMP </span> </td> 
   <td colname="5"> Sono disponibili nuovi dati DRM. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Generico</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> 399999 </span> </td> 
   <td colname="2"><span class="codeph"> GENERIC_INFO </span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"> <p>Nessuno </p> </td> 
   <td colname="5"> <p>Contrassegna un evento informativo generico. Non effettivamente emesso da TVSDK. È solo un indicatore della fine dell’intervallo di codici numerici corrispondenti agli eventi informativi TVSDK. </p> </td> 
  </tr> 
 </tbody> 
</table>
