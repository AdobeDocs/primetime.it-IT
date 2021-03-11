---
description: Questa tabella fornisce informazioni dettagliate sulle notifiche di tipo ERROR.
title: Codici di notifica ERRORI
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 4%

---


# Codici di notifica ERRORE{#error-notification-codes}

Questa tabella fornisce informazioni dettagliate sulle notifiche di tipo ERROR.

<!--<a id="section_D29404228F5E4B818642CBA6A0D39546"></a>-->

La maggior parte degli errori contiene metadati rilevanti, ad esempio l’URL della risorsa che non è stato possibile scaricare. Alcune notifiche contengono metadati per specificare se il problema si è verificato nel contenuto video principale, nel contenuto audio alternativo o in un annuncio.

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
   <td colname="1"><b>Riproduzione</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101000  </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_ERROR  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE</span> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101004  </span> </td> 
   <td colname="2"><span class="codeph"> CONTENT_ERROR</span> </td> 
   <td colname="3"><span class="codeph"> DOWNLOAD_ERROR</span> </td> 
   <td colname="4"> </td> 
   <td colname="5"> Errore durante il download di un frammento o segmento (sia video che audio). </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101008  </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_ERROR  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> NATIVE_ERROR_CODE  </span><span class="codeph"> DESIRED_SEEK_POSITION  </span><span class="codeph"> DESIRED_SEEK_PERIOD  </span> </td> 
   <td colname="5"> Errore durante l'esecuzione di un'operazione di ricerca. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101009  </span> </td> 
   <td colname="2"><span class="codeph"> PAUSE_ERROR  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE</span> </td> 
   <td colname="5"> Errore durante l'esecuzione di un'operazione di pausa. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101102  </span> </td> 
   <td colname="2"><span class="codeph"> PERIOD_INFO_ERROR  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE  </span> </td> 
   <td colname="5"> Errore durante il recupero delle informazioni su un periodo di contenuto. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101103  </span> </td> 
   <td colname="2"><span class="codeph"> RETRIEVE_TIME_ERROR  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE  </span> </td> 
   <td colname="5"> Errore durante il tentativo di recuperare la posizione di riproduzione. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101104  </span> </td> 
   <td colname="2"><span class="codeph"> GET_QOS_DATA_ERROR  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE  </span> </td> 
   <td colname="5"> Errore durante il tentativo di recupero delle informazioni QOS. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101200  </span> </td> 
   <td colname="2"><span class="codeph"> DOWNLOAD_ERROR  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> URL  </span> </td> 
   <td colname="5"> Errore durante il tentativo di download dei dati. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Risorsa non valida</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 102100  </span> </td> 
   <td colname="2"><span class="codeph"> RESOURCE_LOAD_ERROR  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE  </span><span class="codeph"> RISORSA  </span> </td> 
   <td colname="5"> Errore durante il caricamento di un elemento di risorsa. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 102101  </span> </td> 
   <td colname="2"><span class="codeph"> RESOURCE_PLACEMENT_ FAILED  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> CONTENT_ID  </span> </td> 
   <td colname="5"> Errore durante il posizionamento di una risorsa sulla timeline di riproduzione. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Elaborazione di annunci</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104000  </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_FAIL  </span> </td> 
   <td colname="3"><span class="codeph"> AD_METADATA_INVALID  </span><span class="codeph"> AD_RESOLVER_INITIALIZATION_FAIL  </span><span class="codeph"> AD_RESOLVER_RESOLVE_FAIL  </span><span class="codeph"> AD_RESOLVER_SERVER_UNREACHABLE  </span> </td> 
   <td colname="4"> Nessuno </td> 
   <td colname="5"> Nessuno </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104001  </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_METADATA_ INVALID  </span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE</span> </td> 
   <td colname="5"> Risoluzione dell'annuncio non riuscita a causa di un formato di metadati dell'annuncio non valido. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104003  </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_RESOLVE_FAIL  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> NATIVE_ERROR_CODE  </span> </td> 
   <td colname="5"> Il plug-in dell'annuncio non è riuscito a risolvere gli annunci. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104005  </span> </td> 
   <td colname="2"><span class="codeph"> AD_INSERTION_FAIL  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> PROPOSED_AD_BREAK</span> </td> 
   <td colname="5"> La fase di risoluzione degli annunci non è riuscita. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Nativo</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106000  </span> </td> 
   <td colname="2"><span class="codeph"> NATIVE_ERROR  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"> <span class="codeph"> NATIVE_ERROR_CODE  </span> <span class="codeph"> NATIVE_ERROR_NAME  </span> <span class="codeph"> DESCRIPTION  </span> <span class="codeph"> DESCRIPTION</span> <p><b>Dettagli DRM:</b> </p> <span class="codeph"> DRM_ERROR_</span> <span class="codeph"> STRINGNATIVE_SUBERROR_CODE</span> </td> 
   <td colname="5"> <p>La libreria AVE di basso livello ha generato un errore. </p> <p>Consulta <a href="../../../tvsdk-1.4-for-android/android-1.4-tvsdk-notification/notification-codes/native-error-summary/android-1.4-native-error-summary.md" format="html" scope="external"> Dettagli per le notifiche NATIVE_ERROR</a> per informazioni sui valori per queste chiavi di metadati. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106001  </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_CREATION_ERROR  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE  </span> </td> 
   <td colname="5"> Errore durante la creazione dell'istanza della libreria di basso livello AVE. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106002  </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RELEASE_ERROR  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE  </span> </td> 
   <td colname="5"> Errore durante il rilascio della libreria di basso livello AVE. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106003  </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RESOURCES_RELEASE_ERROR  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE  </span> </td> 
   <td colname="5"> Errore durante il rilascio delle risorse GPU utilizzate dalla libreria AVE. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106004  </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RESET_ERROR  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE  </span> </td> 
   <td colname="5"> Errore durante il ripristino della libreria AVE. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106005  </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_SET_VIEW_ERROR  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE</span> </td> 
   <td colname="5"> Errore durante il collegamento di una visualizzazione alla libreria AVE. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Configurazione</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107000  </span> </td> 
   <td colname="2"><span class="codeph"> SET_VOLUME_ERROR  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> VOLUME DESCRIZIONE  </span> </td> 
   <td colname="5"> Errore durante il tentativo di impostare il livello del volume. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107001  </span> </td> 
   <td colname="2"><span class="codeph"> SET_BUFFER_TIME_ERROR  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE  </span><span class="codeph"> PLAY_BUFFER_TIME  </span> </td> 
   <td colname="5"> Errore durante il tentativo di modificare i parametri di buffering. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107002  </span> </td> 
   <td colname="2"><span class="codeph"> SET_CC_VISIBILITY_ERROR  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE</span> </td> 
   <td colname="5"> Errore durante il tentativo di modificare la visibilità dei brani CC. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107003  </span> </td> 
   <td colname="2"><span class="codeph"> SET_CC_STYLING_ERROR  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE</span> </td> 
   <td colname="5"> Errore durante il tentativo di modificare le opzioni di stile per i brani CC. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107004  </span> </td> 
   <td colname="2"><span class="codeph"> SET_ABR_PARAMETERS_ ERROR  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE  </span> </td> 
   <td colname="5"> Errore durante il tentativo di modificare i parametri di controllo ABR. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107005  </span> </td> 
   <td colname="2"><span class="codeph"> SET_BUFFER_PARAMETERS_ERROR  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE  </span><span class="codeph"> INITIAL_BUFFER_TIME  </span><span class="codeph"> PLAY_BUFFER_TIME  </span> </td> 
   <td colname="5"> Errore durante il tentativo di modificare i parametri del controllo buffering. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Audio alternativo</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 109000  </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_ERROR  </span> </td> 
   <td colname="3"><span class="codeph"> DOWNLOAD_ERROR  </span> </td> 
   <td colname="4"><span class="codeph"> AUDIO_TRACK_NAME  </span><span class="codeph"> AUDIO_TRACK_LANGUAGE  </span> </td> 
   <td colname="5"> Errore relativo a una traccia audio. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Generico</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> 19999  </span> </td> 
   <td colname="2"><span class="codeph"> GENERIC_ERROR</span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"> Nessuno </td> 
   <td colname="5"> Contrassegna un evento di errore generico. Non in realtà emesso da TVSDK. Questo è solo un marcatore per la fine dell’intervallo di codici numerici corrispondenti agli eventi di errore TVSDK. </td> 
  </tr> 
 </tbody> 
</table>

