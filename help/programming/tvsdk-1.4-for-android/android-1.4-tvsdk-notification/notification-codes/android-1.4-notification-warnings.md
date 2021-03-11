---
description: Questa tabella illustra informazioni dettagliate sulle notifiche di tipo WARN.
title: Codici di notifica di AVVISO
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 2%

---


# CODICI DI NOTIFICA {#warning-notification-codes}

Questa tabella illustra informazioni dettagliate sulle notifiche di tipo WARN.

<!--<a id="section_F25366B6703040E3ADA993C113618F01"></a>-->

La maggior parte degli avvisi contiene metadati rilevanti, ad esempio l’URL della risorsa che non è stato possibile scaricare. Alcune notifiche contengono metadati per specificare se il problema si è verificato nel contenuto video principale, nel contenuto audio alternativo o in un annuncio.

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
   <td colname="1"><span class="codeph"> 200000  </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_OPERATION_FAIL  </span> </td> 
   <td colname="3"><span class="codeph"> AUDIO_TRACK_ERROR  </span><span class="codeph"> SEEK_ERROR  </span> </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE  </span> </td> 
   <td colname="5"> <p>Operazione relativa alla riproduzione non riuscita, ma la riproduzione potrebbe continuare. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Risoluzione degli annunci</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201000  </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_FAIL  </span> </td> 
   <td colname="3"><span class="codeph"> AD_RESOLVER_ RESOLVE_FAIL  </span><span class="codeph"> RESOURCE_PLACEMENT_ FAILED  </span><span class="codeph"> AD_RESOLVER_ METADATA_INVALID  </span> </td> 
   <td colname="4"> <p>Nessuno </p> </td> 
   <td colname="5"> <p>Ad-resolver: impossibile risolvere/inserire il contenuto dell'annuncio. La riproduzione potrebbe continuare. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201002</span> </td> 
   <td colname="2"><span class="codeph"> AD_ASSET_ FAILED_TO_LOAD</span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"><span class="codeph"> AD_ASSET, INTERNAL_ERROR</span> </td> 
   <td colname="5"> <p>Si è verificato un errore durante il tentativo di caricamento di un annuncio creativo. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201003</span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_RETURNED_NO_ADS</span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"><span class="codeph"> INTERNAL_ERROR, AD_ID,DESCRIPTION</span> </td> 
   <td colname="5"> <p>Risoluzione dell'annuncio non riuscita a causa di un URL VAST non valido o perché non è stato restituito alcun annuncio dal wrapper VAST. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Manifesti di fondo</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204000  </span> </td> 
   <td colname="2"><span class="codeph"> BACKGROUND_MANIFEST_ WARNING</span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"><span class="codeph"> BACKGROUND_MANIFEST_WARNING_</span> <span class="codeph"> ERRORBACKGROUND_MANIFEST_WARNING_</span> <span class="codeph"> NAMEDESCRIPTION</span> </td> 
   <td colname="5"> <p> Errore nel download del manifesto in background. Qualsiasi problema nell'aggiornamento del manifesto di sfondo viene inviato come avviso TVSDK e non causa l'arresto della riproduzione. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204001  </span> </td> 
   <td colname="2"><span class="codeph"> AVVERTENZA INVALID_SEEK_</span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE</span> </td> 
   <td colname="5"> <p> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Nativo</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"><span class="codeph"> 209100  </span> </td> 
   <td colname="2" morerows="1"><span class="codeph"> NATIVE_WARNING  </span> </td> 
   <td colname="3" morerows="1"> <p>Nessuno </p> </td> 
   <td colname="4"><b>AVE</b> <p><span class="codeph"> NATIVE_ERROR_CODE  </span><span class="codeph"> NATIVE_ERROR_NAME  </span><span class="codeph"> DESCRIPTION  </span> </p> </td> 
   <td colname="5"> <p>La libreria AVE di basso livello ha generato un errore. </p> <p>Consulta <a href="../../../tvsdk-1.4-for-android/android-1.4-tvsdk-notification/notification-codes/native-error-summary/android-1.4-native-error-summary.md" format="html" scope="external"> Dettagli per le notifiche NATIVE_ERROR</a> per informazioni dettagliate sui valori per questi campi di metadati. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="4"><b>DRM</b> <p><span class="codeph"> NATIVE_SUBERROR_</span> <span class="codeph"> CODEDRM_ERROR_STRING</span> </p> </td> 
   <td colname="5"> Codice di errore minore DRM e stringa di errore del server DRM. Consulta <a href="../../../tvsdk-1.4-for-android/android-1.4-tvsdk-notification/notification-codes/native-error-summary/android-1.4-native-error-summary.md" format="html" scope="external"> Dettagli per le notifiche NATIVE_ERROR</a> per informazioni dettagliate sui valori per questi campi di metadati.</td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>TimeRangeCollection</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 210000  </span> </td> 
   <td colname="2"><span class="codeph"> UNDEFINED_ TIME_RANGES  </span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"> Nessuno </td> 
   <td colname="5"> La modalità di segnalazione degli annunci è definita come intervalli personalizzati, ma non sono definiti intervalli. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 210001  </span> </td> 
   <td colname="2"><span class="codeph"> INTERVALLI INVALID_TIME_  </span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE  </span> </td> 
   <td colname="5"> <p> Uno o più intervalli di tempo non sono validi e verranno ignorati o modificati. </p> <p> DESCRIPTION è una stringa contenente la descrizione degli intervalli non validi. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Modalità Trick</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 280000  </span> </td> 
   <td colname="2"><span class="codeph"> TRICKPLAY_RATE_CHANGE_FAIL</span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE</span> </td> 
   <td colname="5"> <p> Modifica del tasso non riuscita. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Generico</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> 299999  </span> </td> 
   <td colname="2"><span class="codeph"> GENERIC_WARNING  </span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"> <p>Nessuno </p> </td> 
   <td colname="5"> <p>Contrassegna un evento di avviso generico. Non in realtà emesso da TVSDK. È solo un indicatore della fine dell'intervallo di codici numerici corrispondenti agli eventi di avviso. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[NOTA!] AdID e sorgente (URL) possono essere recuperati tramite PTAdAsset nei metadati di notifica con la  `AD_ASSET` chiave .
