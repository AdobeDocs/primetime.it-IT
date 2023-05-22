---
description: Questa tabella fornisce informazioni dettagliate sulle notifiche di tipo ERRORE.
title: Codici di notifica ERROR
exl-id: 4f8882b5-2c2b-4f17-a9c9-834816265e1f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 4%

---

# Codici di notifica ERROR{#error-notification-codes}

Questa tabella fornisce informazioni dettagliate sulle notifiche di tipo ERRORE.

<!--<a id="section_D29404228F5E4B818642CBA6A0D39546"></a>-->

La maggior parte degli errori contiene metadati rilevanti, ad esempio l’URL della risorsa che non è stata scaricata. Alcune notifiche contengono metadati che consentono di specificare se il problema si è verificato nel contenuto video principale, nel contenuto audio alternativo o in un annuncio.

<table frame="all" colsep="1" rowsep="1" id="table_8B61210A406A45ACBE37FC29729DDE22"> 
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
   <td colname="1"><b>DRM</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 100000 </span> </td> 
   <td colname="2"><span class="codeph"> DRM_ERROR </span> </td> 
   <td colname="3"> </td> 
   <td colname="4"><span class="codeph"> MAJOR_DRM_CODE </span><span class="codeph"> MINOR_DRM_CODE </span><span class="codeph"> DESCRIZIONE </span> </td> 
   <td colname="5">Fai riferimento anche a 106000 (
     <span class="codeph"> ERRORE_NATIVO</span>).
   </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Riproduzione</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101000 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_ERROR </span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE </span> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101004 </span> </td> 
   <td colname="2"><span class="codeph"> CONTENT_ERROR </span> </td> 
   <td colname="3"><span class="codeph"> DOWNLOAD_ERROR </span> </td> 
   <td colname="4"> </td> 
   <td colname="5"> <p>Si è verificato un errore durante il download di un frammento o di un segmento (sia video che audio). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101006 </span> </td> 
   <td colname="2"><span class="codeph"> SECURITY_ERROR </span> </td> 
   <td colname="3"> </td> 
   <td colname="4"><span class="codeph"> URL </span> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101008</span> </td> 
   <td colname="2"><span class="codeph"> PAUSA_ERRORE </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"> <span class="codeph"> DESCRIZIONE </span> </td> 
   <td colname="5"> <p>Si è verificato un errore durante l'esecuzione di un'operazione di pausa. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101009 </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_ERROR </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> NATIVE_ERROR_CODE </span><span class="codeph"> DESIRED_SEEK_POSITION </span><span class="codeph"> DESIRED_SEEK_PERIOD </span> </td> 
   <td colname="5"> <p>Si è verificato un errore durante l'esecuzione di un'operazione di ricerca. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101102 </span> </td> 
   <td colname="2"><span class="codeph"> PERIOD_INFO_ERROR </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE </span> </td> 
   <td colname="5"> <p>Si è verificato un errore durante il recupero delle informazioni su un periodo di contenuto. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101103 </span> </td> 
   <td colname="2"><span class="codeph"> RETRIEVE_TIME_ERROR </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE </span> </td> 
   <td colname="5"> <p>Si è verificato un errore durante il tentativo di recuperare la posizione di riproduzione. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101104 </span> </td> 
   <td colname="2"><span class="codeph"> GET_QOS_DATA_ERROR </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE </span> </td> 
   <td colname="5"> <p>Si è verificato un errore durante il tentativo di recuperare le informazioni QOS. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101200 </span> </td> 
   <td colname="2"><span class="codeph"> DOWNLOAD_ERROR </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> URL </span> </td> 
   <td colname="5"> <p>Si è verificato un errore durante il tentativo di download dei dati. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Risorsa non valida </b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 102100 </span> </td> 
   <td colname="2"><span class="codeph"> RESOURCE_LOAD_ERROR </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE </span><span class="codeph"> RISORSA </span> </td> 
   <td colname="5"> <p>Errore durante il caricamento di un elemento di risorsa. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 102101 </span> </td> 
   <td colname="2"><span class="codeph"> RESOURCE_PLACEMENT_ NON RIUSCITO </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> CONTENT_ID </span> </td> 
   <td colname="5"> <p>Si è verificato un errore durante il posizionamento di una risorsa sulla timeline di riproduzione. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Elaborazione degli annunci </b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104000 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_FAIL </span> </td> 
   <td colname="3"><span class="codeph"> AD_METADATA _NON VALIDO </span><span class="codeph"> AD_RESOLVER_INITIALIZATION_FAIL </span><span class="codeph"> AD_RESOLVER_RESOLVE_FAIL </span><span class="codeph"> AD_RESOLVER_SERVER_UNREACHABLE </span> </td> 
   <td colname="4"> Nessuno </td> 
   <td colname="5"> Nessuno </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104001 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_METADATA_ NON VALIDO </span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"> </td> 
   <td colname="5"> <p>Risoluzione annuncio non riuscita a causa di un formato di metadati annuncio non valido. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104003 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_RESOLVE_ FAIL </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> NATIVE_ERROR_CODE </span> </td> 
   <td colname="5"> <p>Il plug-in dell’annuncio non è riuscito a risolvere gli annunci. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104005 </span> </td> 
   <td colname="2"><span class="codeph"> AD_INSERTION_FAIL </span> </td> 
   <td colname="3">Nessuno</td> 
   <td colname="4"><span class="codeph"> ROTTURA_ANNUNCIO_PROPOSTO</span> </td> 
   <td colname="5"> <p>La fase di risoluzione dell’annuncio non è riuscita. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104006 </span> </td> 
   <td colname="2"><span class="codeph"> AD_UNREACH </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"> Nessuno </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Nativa</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106000 </span> </td> 
   <td colname="2"><span class="codeph"> ERRORE_NATIVO </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> RUNTIME_CODE</span> <span class="codeph"> RUNTIME_CODE_MESSAGE</span> <span class="codeph"> URL_RISORSA</span> <span class="codeph"> TIPO_RISORSA</span> <span class="codeph"> RESOURCE_ID</span> <p><b>Dettagli DRM:</b> </p> <span class="codeph"> DRM_ERROR_STRING</span> <span class="codeph"> RUNTIME_SUBERROR_CODE</span> </td> 
   <td colname="5"> <p>Errore della libreria AVE di basso livello. </p> <p>Consulta <a href="../../c-psdk-dhls-1.4-events-and-notifications/notification-codes/c-psdk-dhls-1.4-native-error-summary.md" format="html" scope="external"> Dettagli per le notifiche NATIVE_ERROR</a> per informazioni sui valori di queste chiavi di metadati. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106001 </span> </td> 
   <td colname="2"><span class="codeph"> ERRORE ENGINE_CREATION_ </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE </span> </td> 
   <td colname="5"> <p>Si è verificato un errore durante la creazione di un'istanza della libreria di basso livello AVE. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106002 </span> </td> 
   <td colname="2"><span class="codeph"> ERRORE ENGINE_RELEASE_ </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE </span> </td> 
   <td colname="5"> <p>Si è verificato un errore durante il rilascio della libreria di basso livello AVE. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106003 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RESOURCES_ RELEASE_ERROR </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE </span> </td> 
   <td colname="5"> <p>Si è verificato un errore durante il rilascio delle risorse GPU utilizzate dalla libreria AVE. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106004 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RESET_ERROR </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE </span> </td> 
   <td colname="5"> <p>Si è verificato un errore durante il ripristino della libreria AVE. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106005 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_SET_ VIEW_ERROR </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE </span> </td> 
   <td colname="5"> <p>Si è verificato un errore durante il collegamento di una vista alla libreria AVE. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Audio alternativo</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 109000 </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_ERROR </span> </td> 
   <td colname="3"><span class="codeph"> DOWNLOAD_ERROR </span> </td> 
   <td colname="4"><span class="codeph"> AUDIO_TRACK_NAME </span><span class="codeph"> AUDIO_TRACK_LANGUAGE </span> </td> 
   <td colname="5"> <p>Si è verificato un errore relativo a una traccia audio. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Generico</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> 199999 </span> </td> 
   <td colname="2"><span class="codeph"> GENERIC_ERROR </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"> Nessuno </td> 
   <td colname="5"> <p>Contrassegna un evento di errore generico. Non effettivamente emesso da TVSDK. È solo un indicatore della fine dell’intervallo di codici numerici corrispondenti agli eventi di errore TVSDK. </p> </td> 
  </tr> 
 </tbody> 
</table>
