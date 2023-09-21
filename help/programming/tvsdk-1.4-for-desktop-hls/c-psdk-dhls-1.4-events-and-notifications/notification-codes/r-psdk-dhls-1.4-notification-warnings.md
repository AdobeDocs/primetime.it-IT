---
description: Questa tabella fornisce informazioni dettagliate su WARN. digita le notifiche.
title: Codici di notifica WARNING
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 2%

---

# Codici di notifica WARNING{#warning-notification-codes}

Questa tabella fornisce informazioni dettagliate su WARN. digita le notifiche.

<!--<a id="section_F25366B6703040E3ADA993C113618F01"></a>-->

La maggior parte degli avvisi contiene metadati rilevanti, ad esempio l’URL della risorsa che non è stata scaricata. Alcune notifiche contengono metadati che consentono di specificare se il problema si è verificato nel contenuto video principale, nel contenuto audio alternativo o in un annuncio.

<table frame="all" colsep="1" rowsep="1" id="table_C24772DF203B4DB2ACE6B475698C4C58"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Codice </th> 
   <th colname="2" class="entry"> Nome </th> 
   <th colname="3" class="entry"> InnerNotification </th> 
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
   <td colname="1"><span class="codeph"> 200000 </span> </td> 
   <td colname="2"><span class="codeph"> RIPRODUZIONE_OPERAZIONE _NON RIUSCITA </span> </td> 
   <td colname="3"><span class="codeph"> AUDIO_TRACK_ERROR </span><span class="codeph"> SEEK_ERROR </span> </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE </span> </td> 
   <td colname="5"> <p>Un'operazione relativa alla riproduzione non è riuscita, ma la riproduzione potrebbe continuare. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Risoluzione degli annunci </b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201000 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_FAIL </span> </td> 
   <td colname="3"><span class="codeph"> AD_RESOLVER_ RESOLVE_FAIL </span><span class="codeph"> RESOURCE_PLACEMENT_ NON RIUSCITO </span><span class="codeph"> AD_RESOLVER_ METADATA_INVALID </span> </td> 
   <td colname="4"> <p>Nessuno </p> </td> 
   <td colname="5"> <p>Ad-resolver non è riuscito a risolvere/inserire il contenuto dell’annuncio. La riproduzione potrebbe continuare. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Manifesti di sfondo</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204000 </span> </td> 
   <td colname="2"><span class="codeph"> BACKGROUND_MANIFEST_ WARNING</span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"><span class="codeph"> BACKGROUND_MANIFEST_ WARNING_ERROR</span> <span class="codeph"> BACKGROUND_MANIFEST_ WARNING_NAME</span> <span class="codeph"> DESCRIZIONE</span> </td> 
   <td colname="5"> <p> Errore nel download del manifesto in background. Qualsiasi problema nell’aggiornamento del manifesto in background viene inviato come avviso TVSDK e non causa l’interruzione della riproduzione. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204001 </span> </td> 
   <td colname="2"><span class="codeph"> INVALID_SEEK_ WARNING</span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE</span> </td> 
   <td colname="5"> <p> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Nativa</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"><span class="codeph"> 209100 </span> </td> 
   <td colname="2" morerows="1"><span class="codeph"> AVVISO_NATIVO </span> </td> 
   <td colname="3" morerows="1"> <p>Nessuno </p> </td> 
   <td colname="4"><b>AVE</b> <p><span class="codeph"> NATIVE_ERROR_CODE </span><span class="codeph"> NOME_ERRORE_NATIVO </span><span class="codeph"> DESCRIZIONE </span> </p> </td> 
   <td colname="5"> <p>Errore della libreria AVE di basso livello. </p> <p>Consulta <a href="../../c-psdk-dhls-1.4-events-and-notifications/notification-codes/c-psdk-dhls-1.4-native-error-summary.md" format="html" scope="external"> Dettagli per le notifiche NATIVE_ERROR</a> per informazioni dettagliate sui valori di questi campi di metadati. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="4"><b>DRM</b> <p><span class="codeph"> NATIVE_SUBERROR_CODE</span> <span class="codeph"> DRM_ERROR_STRING</span> </p> </td> 
   <td colname="5">Codice errore secondario DRM e stringa errore server DRM. Consulta <a href="../../c-psdk-dhls-1.4-events-and-notifications/notification-codes/c-psdk-dhls-1.4-native-error-summary.md" format="html" scope="external"> Dettagli per le notifiche NATIVE_ERROR</a> per informazioni dettagliate sui valori di questi campi di metadati.
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
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"> <p>Nessuno </p> </td> 
   <td colname="5"> <p>Contrassegna un evento di avviso generico. Non effettivamente emesso da TVSDK. È solo un indicatore della fine dell’intervallo di codici numerici corrispondenti agli eventi di avviso. </p> </td> 
  </tr> 
 </tbody> 
</table>
