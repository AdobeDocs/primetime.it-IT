---
description: Questa tabella fornisce informazioni dettagliate sulle notifiche di tipo WARN.
title: Codici di notifica WARNING
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 3%

---

# Codici di notifica WARNING {#warning-notification-codes}

Questa tabella fornisce informazioni dettagliate sulle notifiche di tipo WARN.

<!--<a id="section_F25366B6703040E3ADA993C113618F01"></a>-->

La maggior parte degli avvisi contiene metadati rilevanti, ad esempio l’URL della risorsa che non è stata scaricata. Alcune notifiche contengono metadati che consentono di specificare se il problema si è verificato nel contenuto video principale, nel contenuto audio alternativo o in un annuncio.

<table frame="all" colsep="1" rowsep="1" id="table_C24772DF203B4DB2ACE6B475698C4C58"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b>Codice</b></th> 
   <th colname="2" class="entry"><b>Nome</b></th> 
   <th colname="3" class="entry"><b>InnerNotification&gt;/b&gt;</th> 
   <th colname="4" class="entry"><b>Chiavi metadati</b></th> 
   <th colname="5" class="entry"><b>Commenti</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>Risoluzione degli annunci</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201002</span> </td> 
   <td colname="2"><span class="codeph"> AD_ASSET_ FAILED_TO_LOAD</span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"><span class="codeph"> AD_ASSET, INTERNAL_ERROR</span> </td> 
   <td colname="5"> <p>Si è verificato un errore durante il caricamento di un contenuto creativo dell’annuncio. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201003</span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_ RETURNS_NO_ADS</span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"><span class="codeph"> INTERNAL_ERROR, AD_ID,DESCRIZIONE</span> </td> 
   <td colname="5"> <p>Risoluzione dell'annuncio non riuscita a causa di un URL VAST non valido o perché non è stato restituito alcun annuncio dal wrapper VAST. </p> </td> 
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
   <td colname="5"> <p></p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>TimeRangeCollection</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 210000 </span> </td> 
   <td colname="2"><span class="codeph"> UNDEFINED_ TIME_RANGES </span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"> Nessuno </td> 
   <td colname="5"> La modalità di segnalazione degli annunci è definita come intervallo personalizzato, ma non sono definiti intervalli. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 210001 </span> </td> 
   <td colname="2"><span class="codeph"> INTERVALLI_TIME_NON VALIDI </span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE </span> </td> 
   <td colname="5"> <p> Uno o più intervalli di tempo non sono validi e verranno ignorati o modificati. </p> <p> DESCRIPTION è una stringa contenente la descrizione degli intervalli non validi. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Specifico di iOS</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270000 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYER_NOT_READY </span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE </span> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270001 </span> </td> 
   <td colname="2"><span class="codeph"> AD_NOT_INSERTED </span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"> <p>Nessuno </p> </td> 
   <td colname="5"> <p>AD non è stato inserito nel flusso. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270002 </span> </td> 
   <td colname="2"><span class="codeph"> AD_HLS_AUDIOONLY_MISSING </span> </td> 
   <td colname="3"><span class="codeph"> AD_NOT_INSERTED </span> </td> 
   <td colname="4"> <p>Nessuno </p> </td> 
   <td colname="5"> <p>L’annuncio non contiene un flusso di sola audio </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270003 </span> </td> 
   <td colname="2"><span class="codeph"> AD_HLS_MATCHING_BITRATE_MISSING </span> </td> 
   <td colname="3"><span class="codeph"> AD_NOT_INSERTED </span> </td> 
   <td colname="4"> <p>Nessuno </p> </td> 
   <td colname="5"> <p>Non è stato trovato alcun flusso di annunci corrispondente per il bitrate corrente del contenuto. </p> <p>  </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270005 </span> </td> 
   <td colname="2"><span class="codeph"> AVASSET_FAILED_TO_CREATE </span> </td> 
   <td colname="3"><span class="codeph"> PLAYBACK_ERROR </span> </td> 
   <td colname="4"> <p>Nessuno </p> </td> 
   <td colname="5"> <p>Errore durante la creazione dell’insieme AVA. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270006 </span> </td> 
   <td colname="2"><span class="codeph"> SITECATALYST_WARNING </span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"><span class="codeph"> DESCRIZIONE </span> </td> 
   <td colname="5"> <p>Avvertenza: consulta la descrizione dell’avviso sitecatalyst. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270007 </span> </td> 
   <td colname="2"><span class="codeph"> ERRORE_DI_RETE </span> </td> 
   <td colname="3"> <p>Nessuno </p> </td> 
   <td colname="4"><span class="codeph"> URL </span> </td> 
   <td colname="5"> <p>Errore nell’ottenere dati dalla rete. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>AdID e sorgente (URL) possono essere recuperati tramite PTAdAsset nei metadati di notifica con `AD_ASSET` chiave.
>
>Il [] attribute specifica una chiave facoltativa per la notifica.
