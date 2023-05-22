---
description: Quality of Service (QoS) offre una visualizzazione dettagliata delle prestazioni del motore video. TVSDK fornisce statistiche dettagliate su riproduzione, buffering e dispositivi.
title: Tracciare a livello di frammento utilizzando le informazioni di caricamento
exl-id: 29e82a93-783f-4e32-ab5e-12713a60cfec
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# Tracciare a livello di frammento utilizzando le informazioni di caricamento{#track-at-the-fragment-level-using-load-information}

Quality of Service (QoS) offre una visualizzazione dettagliata delle prestazioni del motore video. TVSDK fornisce statistiche dettagliate su riproduzione, buffering e dispositivi.

TVSDK fornisce inoltre informazioni sulle seguenti risorse scaricate:

1. File playlist/manifest
1. Frammenti di file
1. Informazioni di tracciamento per i file

   È possibile leggere le informazioni QoS (Quality of Service) sulle risorse scaricate, come frammenti e brani, da `LoadInfo` classe.

1. Implementare `onLoadInfo` listener di eventi di callback.
1. Registra il listener di eventi, che TVSDK chiama ogni volta che un frammento è stato scaricato.
1. Leggi i dati di interesse da `LoadInfo` parametro passato al callback.

   <table id="table_06BD536A23AB4A73B510998426BAE143"> 
    <thead> 
      <tr> 
      <th colname="col01" class="entry"> Proprietà </th> 
      <th colname="col1" class="entry"> Tipo </th> 
      <th colname="col2" class="entry"> Descrizione </th> 
      </tr> 
    </thead>
    <tbody> 
      <tr> 
      <td colname="col01"> <span class="codeph"> downloadDuration </span> </td> 
      <td colname="col1"> <span class="codeph"> long </span> </td> 
      <td colname="col2"> <p>Durata del download in millisecondi. </p> <p>TVSDK non distingue tra il tempo impiegato dal client per connettersi al server e il tempo necessario per scaricare l’intero frammento. Ad esempio, se il download di un segmento da 10 MB richiede 8 secondi, TVSDK fornisce tali informazioni, ma non indica che sono occorsi 4 secondi prima del primo byte e altri 4 secondi per scaricare l’intero frammento. </p> </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration </span> </td> 
      <td colname="col1"> <span class="codeph"> long </span> </td> 
      <td colname="col2"> La durata media dei frammenti scaricati in millisecondi. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> periodIndex </span> </td> 
      <td colname="col1"> <span class="codeph"> int </span> </td> 
      <td colname="col2"> Indice del periodo della sequenza temporale associato alla risorsa scaricata. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> dimensione </span> </td> 
      <td colname="col1"> <span class="codeph"> long </span> </td> 
      <td colname="col2"> Dimensione della risorsa scaricata in byte. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex </span> </td> 
      <td colname="col1"> <span class="codeph"> int </span> </td> 
      <td colname="col2"> Indice del binario corrispondente, se noto; altrimenti, 0. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackName </span> </td> 
      <td colname="col1"> <span class="codeph"> Stringa </span> </td> 
      <td colname="col2"> Nome del brano corrispondente, se noto; in caso contrario, null. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackType </span> </td> 
      <td colname="col1"> <span class="codeph"> Stringa </span> </td> 
      <td colname="col2"> Tipo del brano corrispondente, se noto; altrimenti null. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> tipo </span> </td> 
      <td colname="col1"> <span class="codeph"> Stringa </span> </td> 
      <td colname="col2"> Informazioni scaricate da TVSDK. Uno dei seguenti elementi: 
      <ul id="ul_9C3BDEBD878544DA95C7FF81114F9B5C"> 
      <li id="li_A093552B492A44FD8B30785E465F6886">MANIFEST (MANIFESTO): playlist/manifesto </li> 
      <li id="li_DEF9AC71AA564F9BB4C5D4E834432EE5">FRAMMENTO: un frammento </li> 
      <li id="li_57821F47B6F04CD38570BCE6447A01B8">TRACK: frammento associato a un brano specifico </li> 
      </ul> A volte potrebbe non essere possibile rilevare il tipo di risorsa. In questo caso, viene restituito FILE. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> url </span> </td> 
      <td colname="col1"> <span class="codeph"> Stringa </span> </td> 
      <td colname="col2"> URL che punta alla risorsa scaricata. </td> 
      </tr> 
    </tbody> 
   </table>
