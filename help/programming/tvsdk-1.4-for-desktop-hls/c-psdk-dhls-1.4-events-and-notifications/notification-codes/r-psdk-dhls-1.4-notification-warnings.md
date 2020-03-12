---
description: Questa tabella dimostra informazioni dettagliate sulla WARN. notifiche di tipo.
seo-description: Questa tabella dimostra informazioni dettagliate sulla WARN. notifiche di tipo.
seo-title: Codici di notifica di AVVISO
title: Codici di notifica di AVVISO
uuid: 1ce5be07-f5bf-443c-b907-9768633e1300
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Codici di notifica di AVVISO{#warning-notification-codes}

Questa tabella dimostra informazioni dettagliate sulla WARN. notifiche di tipo.

<!--<a id="section_F25366B6703040E3ADA993C113618F01"></a>-->

La maggior parte degli avvisi contiene metadati rilevanti, ad esempio l’URL della risorsa che non è stato possibile scaricare. Alcune notifiche contengono metadati per specificare se il problema si è verificato nel contenuto video principale, nel contenuto audio alternativo o in un annuncio.

<table frame="all" colsep="1" rowsep="1" id="table_C24772DF203B4DB2ACE6B475698C4C58"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Code </th> 
   <th colname="2" class="entry"> Nome </th> 
   <th colname="3" class="entry"> InnerNotification </th> 
   <th colname="4" class="entry"> Tasti metadati </th> 
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
   <td colname="1"><span class="codeph"> 200000 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_OPERATION_FAIL </span> </td> 
   <td colname="3"><span class="codeph"> AUDIO_TRACK_ERROR </span><span class="codeph"> SEEK_ERROR </span> </td> 
   <td colname="4"><span class="codeph"> DESCRIPTION </span> </td> 
   <td colname="5"> <p>Un'operazione relativa alla riproduzione non è riuscita, ma la riproduzione potrebbe continuare. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Risoluzione annunci </b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201000 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_FAIL </span> </td> 
   <td colname="3"><span class="codeph"> AD_RESOLVER_RESOLVE_FAIL </span><span class="codeph"> RESOURCE_PLACEMENT_ FAILED </span><span class="codeph"> AD_RESOLVER_METADATA_INVALID </span> </td> 
   <td colname="4"> <p>None </p> </td> 
   <td colname="5"> <p>Il risolutore annunci non è riuscito a risolvere/inserire il contenuto dell'annuncio. La riproduzione potrebbe continuare. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Manifesti in background</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204000 </span> </td> 
   <td colname="2"><span class="codeph"> BACKGROUND_MANIFEST_WARNING</span> </td> 
   <td colname="3"> <p>None </p> </td> 
   <td colname="4"><span class="codeph"> BACKGROUND_MANIFEST_WARNING_ERROR</span><span class="codeph"> BACKGROUND_MANIFEST_WARNING_NAME</span><span class="codeph"> DESCRIPTION</span> </td> 
   <td colname="5"> <p> Errore nel download del manifesto in background. Eventuali problemi durante l'aggiornamento del manifesto di sfondo vengono inviati come avviso TVSDK e non causano l'arresto della riproduzione. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204001 </span> </td> 
   <td colname="2"><span class="codeph"> INVALID_SEEK_WARNING</span> </td> 
   <td colname="3"> <p>None </p> </td> 
   <td colname="4"><span class="codeph"> DESCRIPTION</span> </td> 
   <td colname="5"> <p> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Native</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"><span class="codeph"> 209100 </span> </td> 
   <td colname="2" morerows="1"><span class="codeph"> NATIVE_WARNING </span> </td> 
   <td colname="3" morerows="1"> <p>None </p> </td> 
   <td colname="4"><b>AVE</b> <p><span class="codeph"> DESCRIZIONE NATIVE_ERROR_CODE </span><span class="codeph"> NATIVE_ERROR_NAME </span><span class="codeph"></span> </p> </td> 
   <td colname="5"> <p>Errore della libreria AVE di basso livello. </p> <p>Consultate <a href="../../c-psdk-dhls-1.4-events-and-notifications/notification-codes/c-psdk-dhls-1.4-native-error-summary.md" format="html" scope="external"> Dettagli per le notifiche</a> NATIVE_ERROR per informazioni dettagliate sui valori di questi campi di metadati. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="4"><b>DRM</b> <p><span class="codeph"> NATIVE_SUBERROR_CODE</span> <span class="codeph"> DRM_ERROR_STRING</span> </p> </td> 
   <td colname="5">Codice di errore secondario DRM e stringa di errore del server DRM. Consultate <a href="../../c-psdk-dhls-1.4-events-and-notifications/notification-codes/c-psdk-dhls-1.4-native-error-summary.md" format="html" scope="external"> Dettagli per le notifiche</a> NATIVE_ERROR per informazioni dettagliate sui valori di questi campi di metadati.
   </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Generico</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> 299999 </span> </td> 
   <td colname="2"><span class="codeph"> GENERIC_WARNING </span> </td> 
   <td colname="3"> <p>None </p> </td> 
   <td colname="4"> <p>None </p> </td> 
   <td colname="5"> <p>Contrassegna un evento di avviso generico. Non emesso da TVSDK. È solo un indicatore per la fine dell'intervallo di codici numerici corrispondenti agli eventi di avviso. </p> </td> 
  </tr> 
 </tbody> 
</table>

