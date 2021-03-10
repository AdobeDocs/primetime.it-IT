---
description: Quality of Service (QoS) offre una visualizzazione dettagliata delle prestazioni del motore video. TVSDK fornisce statistiche dettagliate sulla riproduzione, il buffering e i dispositivi.
title: Tracciare a livello di frammento utilizzando le informazioni sul caricamento
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# Tracciare a livello di frammento utilizzando le informazioni sul caricamento{#track-at-the-fragment-level-using-load-information}

Quality of Service (QoS) offre una visualizzazione dettagliata delle prestazioni del motore video. TVSDK fornisce statistiche dettagliate sulla riproduzione, il buffering e i dispositivi.

TVSDK fornisce anche informazioni sulle seguenti risorse scaricate:

1. Playlist/file manifest
1. Frammenti di file
1. Tracciamento delle informazioni sui file

   Dalla classe `LoadInfo` è possibile leggere informazioni sulla qualità del servizio (QoS) relative alle risorse scaricate, ad esempio frammenti e tracce.

1. Implementa il listener di eventi di callback `onLoadInfo` .
1. Registra il listener di eventi, che TVSDK chiama ogni volta che un frammento viene scaricato.
1. Leggi i dati di interesse dal parametro `LoadInfo` passato al callback.

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
      <td colname="col01"> <span class="codeph"> downloadDuration  </span> </td> 
      <td colname="col1"> <span class="codeph"> long  </span> </td> 
      <td colname="col2"> <p>Durata del download in millisecondi. </p> <p>TVSDK non distingue tra il tempo impiegato dal client per connettersi al server e il tempo impiegato per scaricare l’intero frammento. Ad esempio, se il download di un segmento da 10 MB richiede 8 secondi, TVSDK fornisce tali informazioni, ma non indica che sono necessari 4 secondi fino al primo byte e altri 4 secondi per scaricare l’intero frammento. </p> </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration  </span> </td> 
      <td colname="col1"> <span class="codeph"> long  </span> </td> 
      <td colname="col2"> Durata dei frammenti scaricati in millisecondi. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> periodIndex  </span> </td> 
      <td colname="col1"> <span class="codeph"> int  </span> </td> 
      <td colname="col2"> L’indice del periodo temporale associato alla risorsa scaricata. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> size  </span> </td> 
      <td colname="col1"> <span class="codeph"> long  </span> </td> 
      <td colname="col2"> Dimensione della risorsa scaricata in byte. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex  </span> </td> 
      <td colname="col1"> <span class="codeph"> int  </span> </td> 
      <td colname="col2"> l'indice del binario corrispondente, se noto; altrimenti, 0. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackName  </span> </td> 
      <td colname="col1"> <span class="codeph"> Stringa  </span> </td> 
      <td colname="col2"> il nome del brano corrispondente, se noto; altrimenti, null. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackType  </span> </td> 
      <td colname="col1"> <span class="codeph"> Stringa  </span> </td> 
      <td colname="col2"> il tipo di binario corrispondente, se noto; altrimenti, null. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> type  </span> </td> 
      <td colname="col1"> <span class="codeph"> Stringa  </span> </td> 
      <td colname="col2"> Cos’è stato scaricato TVSDK. Una delle seguenti opzioni: 
      <ul id="ul_9C3BDEBD878544DA95C7FF81114F9B5C"> 
      <li id="li_A093552B492A44FD8B30785E465F6886">MANIFEST - Una playlist/manifesto </li> 
      <li id="li_DEF9AC71AA564F9BB4C5D4E834432EE5">FRAMMENTO - Un frammento </li> 
      <li id="li_57821F47B6F04CD38570BCE6447A01B8">TRACK - Un frammento associato a una traccia specifica </li> 
      </ul> A volte potrebbe non essere possibile rilevare il tipo di risorsa. In questo caso, viene restituito FILE. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> url  </span> </td> 
      <td colname="col1"> <span class="codeph"> Stringa  </span> </td> 
      <td colname="col2"> URL che punta alla risorsa scaricata. </td> 
      </tr> 
    </tbody> 
   </table>
