---
description: Questa tabella fornisce informazioni dettagliate sulle notifiche dei tipi di errore.
seo-description: Questa tabella fornisce informazioni dettagliate sulle notifiche dei tipi di errore.
seo-title: Codici di notifica di errore
title: Codici di notifica di errore
uuid: 50624782-3d0b-4ac4-b883-355c1f7e9bff
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Codici di notifica di errore{#error-notification-codes}

Questa tabella fornisce informazioni dettagliate sulle notifiche dei tipi di errore.

<!--<a id="section_D29404228F5E4B818642CBA6A0D39546"></a>-->

La maggior parte degli errori contiene metadati rilevanti, ad esempio l’URL della risorsa che non è stato possibile scaricare. Alcune notifiche contengono metadati per specificare se il problema si è verificato nel contenuto video principale, nel contenuto audio alternativo o in un annuncio.

<table frame="all" colsep="1" rowsep="1" id="table_8B61210A406A45ACBE37FC29729DDE22"> 
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
   <td colname="4"><span class="codeph"> MAJOR_DRM_CODE </span><span class="codeph"> MINOR_DRM_CODE </span><span class="codeph"> DESCRIPTION </span> </td> 
   <td colname="5">Fare riferimento anche a 106000 ( <span class="codeph"> NATIVE_ERROR</span>).
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
   <td colname="3"> <p>None </p> </td> 
   <td colname="4"><span class="codeph"> DESCRIPTION </span> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101004 </span> </td> 
   <td colname="2"><span class="codeph"> CONTENT_ERROR </span> </td> 
   <td colname="3"><span class="codeph"> DOWNLOAD_ERROR </span> </td> 
   <td colname="4"> </td> 
   <td colname="5"> <p>Si è verificato un errore durante il download di un frammento o segmento (sia video che audio). </p> </td> 
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
   <td colname="2"><span class="codeph"> PAUSE_ERROR </span> </td> 
   <td colname="3"> None </td> 
   <td colname="4"> <span class="codeph"> DESCRIPTION </span> </td> 
   <td colname="5"> <p>Si è verificato un errore durante un'operazione di pausa. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101009 </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_ERROR </span> </td> 
   <td colname="3"> None </td> 
   <td colname="4"><span class="codeph"> NATIVE_ERROR_CODE </span><span class="codeph"> DESIRED_SEEK_POSITION </span><span class="codeph"> DESIRED_SEEK_PERIOD </span> </td> 
   <td colname="5"> <p>Errore durante l'esecuzione di un'operazione di ricerca. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101102 </span> </td> 
   <td colname="2"><span class="codeph"> PERIOD_INFO_ERROR </span> </td> 
   <td colname="3"> None </td> 
   <td colname="4"><span class="codeph"> DESCRIPTION </span> </td> 
   <td colname="5"> <p>Errore durante il recupero delle informazioni su un periodo di contenuto. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101103 </span> </td> 
   <td colname="2"><span class="codeph"> RETRIEVE_TIME_ERROR </span> </td> 
   <td colname="3"> None </td> 
   <td colname="4"><span class="codeph"> DESCRIPTION </span> </td> 
   <td colname="5"> <p>Errore durante il tentativo di recuperare la posizione di riproduzione. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101104 </span> </td> 
   <td colname="2"><span class="codeph"> GET_QOS_DATA_ERROR </span> </td> 
   <td colname="3"> None </td> 
   <td colname="4"><span class="codeph"> DESCRIPTION </span> </td> 
   <td colname="5"> <p>Si è verificato un errore durante il tentativo di recuperare le informazioni QOS. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101200 </span> </td> 
   <td colname="2"><span class="codeph"> DOWNLOAD_ERROR </span> </td> 
   <td colname="3"> None </td> 
   <td colname="4"><span class="codeph"> URL </span> </td> 
   <td colname="5"> <p>Errore durante il tentativo di scaricare i dati. </p> </td> 
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
   <td colname="3"> None </td> 
   <td colname="4"><span class="codeph"> RISORSA </span><span class="codeph"> DESCRIZIONE </span> </td> 
   <td colname="5"> <p>Errore durante il caricamento di un elemento di risorsa. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 102101 </span> </td> 
   <td colname="2"><span class="codeph"> RESOURCE_PLACEMENT_FAILED </span> </td> 
   <td colname="3"> None </td> 
   <td colname="4"><span class="codeph"> CONTENT_ID </span> </td> 
   <td colname="5"> <p>Si è verificato un errore durante l'inserimento di una risorsa nella timeline di riproduzione. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Elaborazione annunci </b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104000 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_FAIL </span> </td> 
   <td colname="3"><span class="codeph"> AD_METADATA_INVALID </span><span class="codeph"> AD_RESOLVER_INITIALIZATION_FAIL </span><span class="codeph"> AD_RESOLVER_RESOLVE_FAIL </span><span class="codeph"> AD_RESOLVER_SERVER_UNREACHABLE </span> </td> 
   <td colname="4"> None </td> 
   <td colname="5"> None </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104001 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_METADATA_INVALID </span> </td> 
   <td colname="3"> <p>None </p> </td> 
   <td colname="4"> </td> 
   <td colname="5"> <p>Risoluzione annunci non riuscita a causa di un formato di metadati annuncio non valido. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104003 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_RESOLVE_FAIL </span> </td> 
   <td colname="3"> None </td> 
   <td colname="4"><span class="codeph"> NATIVE_ERROR_CODE </span> </td> 
   <td colname="5"> <p>Impossibile risolvere gli annunci. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104005 </span> </td> 
   <td colname="2"><span class="codeph"> AD_INSERTION_FAIL </span> </td> 
   <td colname="3">None</td> 
   <td colname="4"><span class="codeph"> PROPOSED_AD_BREAK</span> </td> 
   <td colname="5"> <p>La fase di risoluzione degli annunci non è riuscita. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104006 </span> </td> 
   <td colname="2"><span class="codeph"> AD_UNREACHABLE </span> </td> 
   <td colname="3"> None </td> 
   <td colname="4"> None </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Native</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106000 </span> </td> 
   <td colname="2"><span class="codeph"> NATIVE_ERROR </span> </td> 
   <td colname="3"> None </td> 
   <td colname="4"><span class="codeph"> RUNTIME_CODE</span> <span class="codeph"> RUNTIME_CODE_MESSAGE</span> <span class="codeph"> RESOURCE_URL</span> <span class="codeph"> RESOURCE_TYPE</span> <span class="codeph"> RESOURCE_ID</span> <p><b>Dettagli DRM:</b> </p> <span class="codeph"> DRM_ERROR_STRING</span> RUNTIME_SUBERROR_CODE <span class="codeph"></span> </td> 
   <td colname="5"> <p>Errore della libreria AVE di basso livello. </p> <p>Consultate <a href="../../c-psdk-dhls-1.4-events-and-notifications/notification-codes/c-psdk-dhls-1.4-native-error-summary.md" format="html" scope="external"> Dettagli per le notifiche</a> NATIVE_ERROR per informazioni sui valori di queste chiavi di metadati. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106001 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_CREATION_ERROR </span> </td> 
   <td colname="3"> None </td> 
   <td colname="4"><span class="codeph"> DESCRIPTION </span> </td> 
   <td colname="5"> <p>Errore durante la creazione dell'istanza della libreria di livello inferiore AVE. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106002 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RELEASE_ERROR </span> </td> 
   <td colname="3"> None </td> 
   <td colname="4"><span class="codeph"> DESCRIPTION </span> </td> 
   <td colname="5"> <p>Si è verificato un errore durante il rilascio della libreria di basso livello AVE. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106003 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RESOURCES_RELEASE_ERROR </span> </td> 
   <td colname="3"> None </td> 
   <td colname="4"><span class="codeph"> DESCRIPTION </span> </td> 
   <td colname="5"> <p>Si è verificato un errore durante il rilascio delle risorse GPU utilizzate dalla libreria AVE. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106004 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RESET_ERROR </span> </td> 
   <td colname="3"> None </td> 
   <td colname="4"><span class="codeph"> DESCRIPTION </span> </td> 
   <td colname="5"> <p>Errore durante il ripristino della libreria AVE. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106005 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_SET_VIEW_ERROR </span> </td> 
   <td colname="3"> None </td> 
   <td colname="4"><span class="codeph"> DESCRIPTION </span> </td> 
   <td colname="5"> <p>Si è verificato un errore durante l'associazione di una visualizzazione alla libreria AVE. </p> </td> 
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
   <td colname="5"> <p>Si è verificato un errore correlato a una traccia audio. </p> </td> 
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
   <td colname="3"> None </td> 
   <td colname="4"> None </td> 
   <td colname="5"> <p>Contrassegna un evento di errore generico. Non emesso da TVSDK. È solo un indicatore per la fine dell'intervallo di codici numerici corrispondenti agli eventi di errore TVSDK. </p> </td> 
  </tr> 
 </tbody> 
</table>

