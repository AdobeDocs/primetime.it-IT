---
description: Questa tabella illustra informazioni dettagliate sulle notifiche di tipo WARN.
seo-description: Questa tabella illustra informazioni dettagliate sulle notifiche di tipo WARN.
seo-title: Codici di notifica di AVVISO
title: Codici di notifica di AVVISO
uuid: 32b54e6c-f107-4e8e-aad6-34e1057719b0
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 2%

---


# CODICI DI NOTIFICA DI AVVISO {#warning-notification-codes}

Questa tabella illustra informazioni dettagliate sulle notifiche di tipo WARN.

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
   <td colname="1"><span class="codeph"> 200000  </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_OPERATION_FAIL  </span> </td> 
   <td colname="3"><span class="codeph"> AUDIO_TRACK_ERROR  </span><span class="codeph"> SEEK_ERROR  </span> </td> 
   <td colname="4"><span class="codeph"> DESCRIPTION  </span> </td> 
   <td colname="5"> <p>Un'operazione relativa alla riproduzione non è riuscita, ma la riproduzione potrebbe continuare. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Risoluzione annunci</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201000  </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_FAIL  </span> </td> 
   <td colname="3"><span class="codeph"> AD_RESOLVER_RESOLVE_FAIL  </span><span class="codeph"> RESOURCE_PLACEMENT_ FAILED  </span><span class="codeph"> AD_RESOLVER_METADATA_INVALID  </span> </td> 
   <td colname="4"> <p>None </p> </td> 
   <td colname="5"> <p>Il risolutore annunci non è riuscito a risolvere/inserire il contenuto dell'annuncio. La riproduzione potrebbe continuare. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201002</span> </td> 
   <td colname="2"><span class="codeph"> AD_ASSET_FAILED_TO_LOAD</span> </td> 
   <td colname="3"> <p>None </p> </td> 
   <td colname="4"><span class="codeph"> AD_ASSET, INTERNAL_ERROR</span> </td> 
   <td colname="5"> <p>Si è verificato un errore durante il tentativo di caricare un annuncio creativo. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201003</span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_RETURNED_NO_ADS</span> </td> 
   <td colname="3"> <p>None </p> </td> 
   <td colname="4"><span class="codeph"> INTERNAL_ERROR, AD_ID,DESCRIPTION</span> </td> 
   <td colname="5"> <p>Risoluzione annunci non riuscita a causa di un URL VAST non valido o perché non è stato restituito nessun annuncio dal wrapper VAST. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Manifesti in background</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204000  </span> </td> 
   <td colname="2"><span class="codeph"> BACKGROUND_MANIFEST_WARNING</span> </td> 
   <td colname="3"> <p>None </p> </td> 
   <td colname="4"><span class="codeph"> BACKGROUND_MANIFEST_WARNING_</span> <span class="codeph"> ERRORBACKGROUND_MANIFEST_WARNING_</span> <span class="codeph"> NAMEDESCRIPTION</span> </td> 
   <td colname="5"> <p> Errore nel download del manifesto in background. Eventuali problemi durante l'aggiornamento del manifesto di sfondo vengono inviati come avviso TVSDK e non causano l'arresto della riproduzione. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204001  </span> </td> 
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
   <td colname="1" morerows="1"><span class="codeph"> 209100  </span> </td> 
   <td colname="2" morerows="1"><span class="codeph"> NATIVE_WARNING  </span> </td> 
   <td colname="3" morerows="1"> <p>None </p> </td> 
   <td colname="4"><b>AVE</b> <p><span class="codeph"> NATIVE_ERROR_CODE  </span><span class="codeph"> NATIVE_ERROR_NAME  </span><span class="codeph"> DESCRIPTION  </span> </p> </td> 
   <td colname="5"> <p>Errore della libreria AVE di basso livello. </p> <p>Per informazioni dettagliate sui valori di questi campi di metadati, consultate <a href="../../../tvsdk-1.4-for-android/android-1.4-tvsdk-notification/notification-codes/native-error-summary/android-1.4-native-error-summary.md" format="html" scope="external"> Dettagli per le notifiche NATIVE_ERROR</a>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="4"><b>DRM</b> <p><span class="codeph"> NATIVE_SUBERROR_</span> <span class="codeph"> CODEDRM_ERROR_STRING</span> </p> </td> 
   <td colname="5"> Codice di errore secondario DRM e stringa di errore del server DRM. Per informazioni dettagliate sui valori di questi campi di metadati, consultate <a href="../../../tvsdk-1.4-for-android/android-1.4-tvsdk-notification/notification-codes/native-error-summary/android-1.4-native-error-summary.md" format="html" scope="external"> Dettagli per le notifiche NATIVE_ERROR</a>.</td> 
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
   <td colname="2"><span class="codeph"> UNDEFINED_TIME_RANGES  </span> </td> 
   <td colname="3"> <p>None </p> </td> 
   <td colname="4"> None </td> 
   <td colname="5"> La modalità di segnalazione degli annunci è definita come intervalli personalizzati, ma non è definito alcun intervallo. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 210001  </span> </td> 
   <td colname="2"><span class="codeph"> INVALID_TIME_RANGES  </span> </td> 
   <td colname="3"> <p>None </p> </td> 
   <td colname="4"><span class="codeph"> DESCRIPTION  </span> </td> 
   <td colname="5"> <p> Uno o più intervalli di tempo non sono validi e verranno ignorati o modificati. </p> <p> DESCRIPTION è una stringa che contiene la descrizione degli intervalli non validi. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Modalità mattoni</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 280000  </span> </td> 
   <td colname="2"><span class="codeph"> TRICKPLAY_RATE_CHANGE_FAIL</span> </td> 
   <td colname="3"> <p>None </p> </td> 
   <td colname="4"><span class="codeph"> DESCRIPTION</span> </td> 
   <td colname="5"> <p> Modifica della tariffa non riuscita. </p> </td> 
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
   <td colname="3"> <p>None </p> </td> 
   <td colname="4"> <p>None </p> </td> 
   <td colname="5"> <p>Contrassegna un evento di avviso generico. Non emesso da TVSDK. È solo un indicatore per la fine dell'intervallo di codici numerici corrispondenti agli eventi di avviso. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[NOTA!] è possibile recuperare adID e origine (URL) tramite PTAdAsset nei metadati di notifica con la  `AD_ASSET` chiave.
