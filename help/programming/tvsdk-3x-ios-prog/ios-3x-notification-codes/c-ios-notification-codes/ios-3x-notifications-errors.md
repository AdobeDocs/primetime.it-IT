---
description: Il sistema di notifica TVSDK genera vari errori, avvisi e avvisi informativi che forniscono metadati diagnostici.
title: Codici di notifica ERRORI
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 5%

---


# Codici di notifica ERRORE {#error-notification-codes}

Questa tabella fornisce informazioni dettagliate sulle notifiche di tipo ERROR.

La maggior parte degli errori contiene metadati rilevanti, ad esempio l’URL della risorsa che non è stato possibile scaricare. Alcune notifiche contengono metadati per specificare se il problema si è verificato nel contenuto video principale, nel contenuto audio alternativo o in un annuncio.

<table frame="all" colsep="1" rowsep="1" id="table_8B61210A406A45ACBE37FC29729DDE22"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b>Codice</b></th> 
   <th colname="2" class="entry"><b>Nome</b></th> 
   <th colname="3" class="entry"><b>InnerNotification</b></th> 
   <th colname="4" class="entry"><b>Chiavi metadati</b></th> 
   <th colname="5" class="entry"><b>Commenti</b></th> 
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
   <td colname="1"><span class="codeph"> 100000  </span> </td> 
   <td colname="2"><span class="codeph"> DRM_ERROR  </span> </td> 
   <td colname="3"> </td> 
   <td colname="4"><span class="codeph"> MAJOR_DRM_CODE  </span><span class="codeph"> MINOR_DRM_CODE  </span><span class="codeph"> DESCRIZIONE  </span> </td> 
   <td colname="5"></td> 
  </tr> 
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
   <td colname="3"></td> 
   <td colname="4"></td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101001  </span> </td> 
   <td colname="2"><span class="codeph"> NATIVE_PLAYBACK_ERROR  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE  </span><span class="codeph"> INTERNAL_ERROR  </span><span class="codeph"> URL  </span> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101008  </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_ERROR  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE</span> </td> 
   <td colname="5"> <p>Errore durante l'esecuzione di un'operazione di ricerca. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101009  </span> </td> 
   <td colname="2"><span class="codeph"> PAUSE_ERROR  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"> <p>Nessuno </p> </td> 
   <td colname="5"> <p>Errore durante l'esecuzione di un'operazione di pausa. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101101  </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_CHANGE_FAIL  </span> </td> 
   <td colname="3"><span class="codeph"> PLAYER_NOT_READY  </span> </td> 
   <td colname="4"> Nessuno </td> 
   <td colname="5"> <p>  </p> <p>  </p>
    <!-- workaround for PDF having too much negative kerning in column 2 --> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Risorsa non valida</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 102000  </span> </td> 
   <td colname="2"><span class="codeph"> INVALID_MEDIA_PLAYER_ITEM  </span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"> Nessuno </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Elaborazione di annunci</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104001  </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_METADATA_ INVALID  </span> </td> 
   <td colname="3"> <span class="codeph"> AD_NOT_INSERTED</span> </td> 
   <td colname="4"> <p>Nessuno </p> </td> 
   <td colname="5"> <p>Risoluzione dell'annuncio non riuscita a causa di un formato di metadati dell'annuncio non valido. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104005  </span> </td> 
   <td colname="2"><span class="codeph"> AD_INSERTION_FAIL  </span> </td> 
   <td colname="3"> <span class="codeph"> AD_NOT_INSERTED  </span> </td> 
   <td colname="4"> <p>Nessuno </p> </td> 
   <td colname="5"> <p>La fase di risoluzione degli annunci non è riuscita. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104006  </span> </td> 
   <td colname="2"><span class="codeph"> AD_UNREACHABLE  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"> Nessuno </td> 
   <td colname="5"> </td> 
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
   <td colname="4"> <span class="codeph"> INTERNAL_ERROR  </span> </td> 
   <td colname="5"> <p>Errore iOS di basso livello. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Configurazione</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107002  </span> </td> 
   <td colname="2"><span class="codeph"> SET_CC_VISIBILITY_ERROR  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"> <p>Nessuno </p> </td> 
   <td colname="5"> <p>Errore durante il tentativo di modificare la visibilità dei brani CC. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107003  </span> </td> 
   <td colname="2"><span class="codeph"> SET_CC_STYLING_ERROR  </span> </td> 
   <td colname="3"> <span class="codeph"> NATIVE_ERROR  </span> </td> 
   <td colname="4"> <p>Nessuno </p> </td> 
   <td colname="5"> <p>Errore durante il tentativo di modificare le opzioni di stile per i brani CC. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>iOS univoco</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170000  </span> </td> 
   <td colname="2"><span class="codeph"> AD_HLS_VERSION_ INCOMPATIBILE  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"> <span class="codeph"> AD_ASSET</span> </td> 
   <td colname="5"> <p>La versione HLS degli annunci è più alta della versione HLS del contenuto. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170001  </span> </td> 
   <td colname="2"><span class="codeph"> ARGUMENT_ERROR  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"> Nessuno </td> 
   <td colname="5"> <p>Errore argomento </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170002  </span> </td> 
   <td colname="2"><span class="codeph"> M3U8_PARSER_ERROR  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE  </span> </td> 
   <td colname="5"> <p>Impossibile analizzare m3u8. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170003  </span> </td> 
   <td colname="2"><span class="codeph"> WEBVTT_PARSER_ERROR  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"> Nessuno </td> 
   <td colname="5"> <p>Impossibile analizzare Webvtt. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170004  </span> </td> 
   <td colname="2"><span class="codeph"> HLS_SEGMENT_ERROR  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE  </span><span class="codeph"> URL  </span><span class="codeph"> INTERNAL_ERROR  </span> </td> 
   <td colname="5"> <p>Il segmento supera la larghezza di banda specificata per la variante. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170005  </span> </td> 
   <td colname="2"><span class="codeph"> MBR_MEDIASEQUENCE_OFFSYNC  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"> Nessuno </td> 
   <td colname="5"> <p>Il numero di sequenza del supporto non è sincronizzato su tutti i flussi HLS di questo MBR. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170006  </span> </td> 
   <td colname="2"><span class="codeph"> MISSING_FILE_ERROR  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE  </span><span class="codeph"> URL  </span><span class="codeph"> INTERNAL_ERROR  </span> </td> 
   <td colname="5"> <p>File mancante o non rispondente. </p> <p>HTTP 404: File non trovato. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170007  </span> </td> 
   <td colname="2"><span class="codeph"> AD_EMPTY_RESPONSE  </span> </td> 
   <td colname="3"><span class="codeph"> AD_INSERTION_FAIL  </span> </td> 
   <td colname="4"> Nessuno </td> 
   <td colname="5"> <p>Impossibile recuperare gli annunci. Risposta vuota. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170008  </span> </td> 
   <td colname="2"><span class="codeph"> AD_TIMEOUT  </span> </td> 
   <td colname="3"><span class="codeph"> AD_INSERTION_FAIL  </span> </td> 
   <td colname="4"> Nessuno </td> 
   <td colname="5"> <p>Impossibile recuperare gli annunci. Errore di timeout. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170009  </span> </td> 
   <td colname="2"><span class="codeph"> SUBTITLES_TRACK_CHANGE_FAIL  </span> </td> 
   <td colname="3"><span class="codeph"> PLAYER_NOT_READY  </span> </td> 
   <td colname="4"> Nessuno </td> 
   <td colname="5"> <p>Errore durante la modifica del brano dei sottotitoli. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170010  </span> </td> 
   <td colname="2"><span class="codeph"> SITECATALYST_ERROR  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE  </span> </td> 
   <td colname="5"> <p>Errore del catalizzatore del sito. Vedere descrizione. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170011  </span> </td> 
   <td colname="2"><span class="codeph"> AD_TARGET_DURATION_INCOMPATIBLE  </span> </td> 
   <td colname="3"> Nessuno </td> 
   <td colname="4"> <span class="codeph"> AD_ASSET</span> </td> 
   <td colname="5"> <p>LA DURATA TARGET dell’annuncio è superiore alla DURATA TARGET del contenuto. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>adID e sorgente (URL) possono essere recuperati tramite `PTAdAsset` nei metadati della notifica con la chiave `AD_ASSET` .
>
>L&#39;attributo `[]` specifica una chiave opzionale per la notifica.
