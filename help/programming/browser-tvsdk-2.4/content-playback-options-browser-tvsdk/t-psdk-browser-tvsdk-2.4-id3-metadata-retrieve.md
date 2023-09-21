---
description: I tag ID3 forniscono informazioni su un file audio o video, ad esempio il titolo del file o il nome dell'artista. Il browser TVSDK rileva i tag ID3 a livello del segmento del flusso di trasporto (TS) nei flussi HLS e invia un evento. L’applicazione può estrarre dati dal tag.
title: Tag ID3
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Tag ID3{#id-tags}

I tag ID3 forniscono informazioni su un file audio o video, ad esempio il titolo del file o il nome dell&#39;artista. Il browser TVSDK rileva i tag ID3 a livello del segmento del flusso di trasporto (TS) nei flussi HLS e invia un evento. L’applicazione può estrarre dati dal tag.

Quando si trova un nuovo metadati ID3 nel flusso HLS sottostante, il TVSDK del browser attiva un `AdobePSDK.TimedMetadataEvent` evento.

Il `TimedMetadata` l&#39;oggetto per ID3 ha le seguenti proprietà:

<table id="table_6C61886187FB44B4B9821E4B00200018"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Nome proprietà </th> 
   <th colname="col2" class="entry"> Dettagli </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> tipo </span> </p> </td> 
   <td colname="col2"> <p>Un tipo di <span class="codeph"> TimedMetadata </span> oggetto. </p> <p>Per i metadati ID3, il valore è <span class="codeph"> AdobePSDK.TimedMetadataType.ID3 </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> tempo </span> </p> </td> 
   <td colname="col2"> <p> L’ora del lettore in cui sono stati rilevati i metadati temporizzati. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> id </span> </p> </td> 
   <td colname="col2"> <p>ID del <span class="codeph"> TimedMetadata </span> oggetto. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> nome </span> </p> </td> 
   <td colname="col2"> <p>Nome di <span class="codeph"> TimedMetadata </span> oggetto. Per i metadati ID3, il valore è "ID3". </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> contenuto </span> </p> </td> 
   <td colname="col2"> <p>Il contenuto dei metadati temporizzati. Per i tag ID3, questo valore rappresenta la matrice di byte serializzata. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> metadati </span> </p> </td> 
   <td colname="col2"> <p> <span class="codeph"> TimedMetadata </span> informazioni elaborate, che è un'istanza di <span class="codeph"> AdobePSDK.Metadata </span> in cui sono memorizzati i fotogrammi ID3. </p> <p> <p>Nota: per Safari <span class="codeph"> video </span> tag, i dati del frame specifico del tag ID3 vengono esposti sotto forma di oggetto attraverso un <span class="codeph"> AdobePSDK.Metadata </span> mentre per altri browser, i dati del frame del tag ID3 sono esposti sotto forma di matrice di byte tramite <span class="codeph"> AdobePSDK.Metadata </span> oggetto. </p> </p> </td> 
  </tr> 
 </tbody> 
</table>

&#x200B;

I vari tag ID3 memorizzati in `TimedMetadata` può essere recuperato dall’applicazione nei due modi seguenti:

* Nel listener di eventi AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE.

  ```
  var isSafari = function () { 
      var nAgt = navigator.userAgent; 
      var appName = navigator.appName; 
      if ((nAgt.indexOf('MSIE') === -1) && //is not MS IE 
          (appName !== 'Netscape' || nAgt.indexOf('Trident/') === -1) && //is not MS IE11 
          (appName !== 'Netscape' || nAgt.indexOf('Edge') === -1) && // is not edge 
          (nAgt.indexOf('Chrome') === -1) && // is not chrome 
          (nAgt.indexOf('Safari') !== -1) //is Safari 
      ){ 
          return true; 
      } 
      return false; 
  }; 
  var hex2a = function (hex, offset, max) { 
      var str = ''; 
      if (!hex) 
          return str; 
      for (var i = offset; i < hex.length && i < offset + max; i++) 
          str += String.fromCharCode(hex[i]); 
      return str; 
  }; 
  var mediaPlayer = new AdobePSDK.MediaPlayer(); 
  mediaPlayer.addEventListener( AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE ,function(event){ 
      var td = event.timedMetadata; 
      if(td.type == AdobePSDK.TimedMetadataType.ID3){ 
          var md = td.metadata; 
          var keySet = md.keySet; 
          var onSafari = isSafari(); 
          if(keySet && keySet.length){ 
              var msg = ''; 
              for(var j = 0; j < keySet.length; j++){ 
                  var idTag = keySet[j]; 
                  msg += idTag; 
                  if(idTag.indexOf("T") == 0){ 
                      /* text frame*/ 
                      if(onSafari){ 
                          /* text frame data is exposed in object format 
                           * where corresponding text data is exposed through 
                           * data key of text frame data object 
                           * */ 
                          var frameDataObject = md.getObject(idTag); 
                          msg += " : " + frameDataObject.data; 
                      } else { 
                          var buff = md.getByteArray(idTag); 
                          msg += " : " + hex2a(buff, 0, buff.length - 1); 
                      } 
                  } 
                  msg += " ; "; 
              } 
          } 
      } 
  }); 
  ```

* Utilizzo di `MediaPlayerItem`di `timedMetadata` proprietà.

  ```
  var isSafari = function () { 
      var nAgt = navigator.userAgent; 
      var appName = navigator.appName; 
      if ((nAgt.indexOf('MSIE') === -1) && //is not MS IE 
          (appName !== 'Netscape' || nAgt.indexOf('Trident/') === -1) && //is not MS IE11 
          (appName !== 'Netscape' || nAgt.indexOf('Edge') === -1) && // is not edge 
          (nAgt.indexOf('Chrome') === -1) && // is not chrome 
          (nAgt.indexOf('Safari') !== -1) //is Safari 
      ){ 
          return true; 
      } 
      return false; 
  }; 
  var hex2a = function (hex, offset, max) { 
      var str = ''; 
      if (!hex) 
          return str; 
      for (var i = offset; i < hex.length && i < offset + max; i++) 
          str += String.fromCharCode(hex[i]); 
      return str; 
  }; 
  var timedMetadataList = player.currentItem.timedMetadata; 
  for(var i = 0; i < timedMetadataList.length; i++){ 
      var td = timedMetadataList[i]; 
      if(td.type == AdobePSDK.TimedMetadataType.ID3){ 
          var md = td.metadata; 
          var keySet = md.keySet; 
          var onSafari = isSafari(); 
          if(keySet && keySet.length){ 
              var msg = ''; 
              for(var j = 0; j < keySet.length; j++){ 
                  var idTag = keySet[j]; 
                  msg += idTag; 
                  if(idTag.indexOf("T") == 0){ 
                      /* text frame*/ 
                      if(onSafari){ 
                          /* text frame data is exposed in object format 
                           * where corresponding text data is exposed through 
                           * data key of text frame data object 
                           * */ 
                          var frameDataObject = md.getObject(idTag); 
                          msg += " : " + frameDataObject.data; 
                      } else { 
                          var buff = md.getByteArray(idTag); 
                          msg += " : " + hex2a(buff, 0, buff.length - 1); 
                      } 
                  } 
                  msg += " ; "; 
              } 
          } 
      } 
  } 
  ```
