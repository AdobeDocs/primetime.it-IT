---
description: Quality of Service (QoS) offre una visualizzazione dettagliata delle prestazioni del motore video. TVSDK fornisce statistiche dettagliate su riproduzione, buffering e dispositivi.
seo-description: Quality of Service (QoS) offre una visualizzazione dettagliata delle prestazioni del motore video. TVSDK fornisce statistiche dettagliate su riproduzione, buffering e dispositivi.
seo-title: Tenere traccia a livello di frammento utilizzando le informazioni sul caricamento
title: Tenere traccia a livello di frammento utilizzando le informazioni sul caricamento
uuid: a6572823-d525-4ce0-806a-3feb20678cb0
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---


# Tenere traccia a livello di frammento utilizzando le informazioni sul caricamento{#track-at-the-fragment-level-using-load-information}

Quality of Service (QoS) offre una visualizzazione dettagliata delle prestazioni del motore video. TVSDK fornisce statistiche dettagliate su riproduzione, buffering e dispositivi.

TVSDK fornisce inoltre informazioni sulle seguenti risorse scaricate:

1. Sequenza di riproduzione/file manifesto
1. Frammenti di file
1. Informazioni di tracciamento per i file

   Dalla classe `LoadInfo` è possibile leggere informazioni sulla qualità del servizio (QoS) relative alle risorse scaricate, come frammenti e tracce.

1. Implementare il listener di eventi di callback `onLoadInfo`.
1. Registra il listener di eventi, che viene chiamato da TVSDK ogni volta che un frammento viene scaricato.
1. Leggete i dati di interesse dal parametro `LoadInfo` passato al callback.

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
      <td colname="col2"> <p>Durata del download, in millisecondi. </p> <p>TVSDK non fa distinzione tra il tempo impiegato dal client per connettersi al server e il tempo impiegato per scaricare l'intero frammento. Ad esempio, se il download di un segmento da 10 MB richiede 8 secondi, TVSDK fornisce tali informazioni, ma non indica che sono necessari 4 secondi prima del primo byte e altri 4 secondi per scaricare l’intero frammento. </p> </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration  </span> </td> 
      <td colname="col1"> <span class="codeph"> long  </span> </td> 
      <td colname="col2"> Durata media dei frammenti scaricati, in millisecondi. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> periodIndex  </span> </td> 
      <td colname="col1"> <span class="codeph"> int  </span> </td> 
      <td colname="col2"> Indice del periodo temporale associato alla risorsa scaricata. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> size  </span> </td> 
      <td colname="col1"> <span class="codeph"> long  </span> </td> 
      <td colname="col2"> La dimensione della risorsa scaricata, in byte. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex  </span> </td> 
      <td colname="col1"> <span class="codeph"> int  </span> </td> 
      <td colname="col2"> l’indice del binario corrispondente, se noto; altrimenti, 0. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackName  </span> </td> 
      <td colname="col1"> <span class="codeph"> Stringa  </span> </td> 
      <td colname="col2"> il nome del binario corrispondente, se noto; altrimenti, null. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackType  </span> </td> 
      <td colname="col1"> <span class="codeph"> Stringa  </span> </td> 
      <td colname="col2"> il tipo del binario corrispondente, se noto; altrimenti, null. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> type  </span> </td> 
      <td colname="col1"> <span class="codeph"> Stringa  </span> </td> 
      <td colname="col2"> Download di TVSDK. Una delle seguenti opzioni: 
      <ul id="ul_9C3BDEBD878544DA95C7FF81114F9B5C"> 
      <li id="li_A093552B492A44FD8B30785E465F6886">MANIFEST - Una playlist/un manifesto </li> 
      <li id="li_DEF9AC71AA564F9BB4C5D4E834432EE5">FRAMMENTO - Un frammento </li> 
      <li id="li_57821F47B6F04CD38570BCE6447A01B8">TRACK - Un frammento associato a una traccia specifica </li> 
      </ul> A volte potrebbe non essere possibile rilevare il tipo di risorsa. In questo caso, viene restituito FILE. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> url  </span> </td> 
      <td colname="col1"> <span class="codeph"> Stringa  </span> </td> 
      <td colname="col2"> L’URL che fa riferimento alla risorsa scaricata. </td> 
      </tr> 
    </tbody> 
   </table>
