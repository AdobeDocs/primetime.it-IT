---
title: Dettagli per la notifica NATIVE_ERROR
description: Dettagli per la notifica NATIVE_ERROR
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---


# Dettagli per la notifica NATIVE_ERROR {#details-for-the-native-error-notification}

Quando TVSDK gestisce un errore nativo, imposta alcuni o tutti i seguenti valori chiave di metadati.

<table id="table_86A21619515B435DBB65DC4DFBB64B29"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Nome chiave metadati </th> 
   <th colname="col2" class="entry"> Valore metadati </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> NATIVE_ERROR_CODE  </span> </td> 
   <td colname="col2"> 
    <pre>
      Codice di errore nativo dall'AVE. 
    </pre> Questi codici rappresentano quanto segue: 
    <ul id="ul_330C626DE27B45A09E8851CC24768A07"> 
     <li id="li_0845A9BBB55545BDB49BD4F4802C0E54">Errori DRM (codici da 3300 a 3367). Sono gli stessi codici di errore Flash Player equivalenti. </li> 
     <li id="li_98A571480C154CF0AE1DC101FF0834C4">Errori di riproduzione video (-1 a 89). </li> 
     <li id="li_D7C19955DEF94DA88B822C8C57D6D2F4">Errori di crittografia (da 300 a 307). </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> NATIVE_ERROR_NAME  </span> </td> 
   <td colname="col2"> Una stringa contenente il nome dell'errore; ad esempio, <span class="codeph"> AAXS_InvalidVoucher </span> o <span class="codeph"> DECODER_FAILED </span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> NATIVE_SUBERROR_CODE  </span> </td> 
   <td colname="col2"> Per gli errori DRM, vengono restituiti anche i codici di errore secondario. Questi codici corrispondono al codice del sottoerrore <span class="codeph"> DRMErrorEvents </span> restituito dal Flash Player. Quando si segnalano errori all’Adobe, includere questo valore numerico per l’assistenza nella risoluzione dei problemi. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> DRM_ERROR_STRING  </span> </td> 
   <td colname="col2"> Per DRM, questa è la stringa di errore personalizzata dalla distribuzione del server DRM, se ne hai definita una. Includilo anche quando si segnalano gli errori agli Adobi. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> DESCRIZIONE  </span> </td> 
   <td colname="col2"> Descrizione stringa dell'errore. Di solito l'URL del contenuto multimediale. </td> 
  </tr> 
 </tbody> 
</table>

TVSDK riceve questi codici di errore e stringhe dal motore video.

>[!IMPORTANT]
>
>Per un elenco completo dei codici di errore client DRM di Adobe Primetime, consulta [Riferimento messaggio di errore client DRM](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_client_error_message_reference.pdf).