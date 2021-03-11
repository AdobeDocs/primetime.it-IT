---
description: Il TVSDK fornisce attualmente il supporto integrato dei metadati del provider di annunci per gli annunci TVSDK, le interruzioni di annunci diretti e i marcatori di annunci personalizzati.
title: Tipi di inserimento annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# Tipi di inserimento annunci {#ad-insertion-types}

Il TVSDK fornisce attualmente il supporto integrato dei metadati del provider di annunci per gli annunci TVSDK, le interruzioni di annunci diretti e i marcatori di annunci personalizzati.

Supporta i seguenti tipi di flussi di lavoro di inserimento di annunci per VOD e contenuti live/lineari.

<table id="table_1C3A659BDDB7453CA953A103045FCA01"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Tipo di inserimento </th> 
   <th colname="col2" class="entry"> Supportato in... </th> 
   <th colname="col3" class="entry"> Descrizione </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Annunci ad decisioning Adobe Primetime </td> 
   <td colname="col2">VOD <p>Live </p> <p>Lineare </p> </td> 
   <td colname="col3">L'implementazione di riferimento fornisce <span class="codeph"> AuditudeMetadata</span> informazioni per la connessione al server per le decisioni relative agli annunci Primetime (precedentemente noto come Auditude), in base alle informazioni fornite nella porzione degli annunci Primetime</a> del file di configurazione JSON</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Interruzioni pubblicitarie dirette </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">Devi fornire URL di annunci nel file JSON di input. Quando il TVSDK tenta di risolvere un annuncio, chiama il risolutore di interruzioni pubblicitarie dirette e risolve gli annunci in base agli annunci diretti interrompe le informazioni fornite nel file di configurazione JSON</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Indicatori di annunci personalizzati </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">Gli indicatori di annunci personalizzati sono utili quando il flusso video contiene sia il contenuto principale che gli annunci, ma non includono informazioni relative alle posizioni e ai tempi degli annunci. Se le informazioni sul posizionamento dell’annuncio vengono ottenute in un altro modo, ad esempio tramite un CMS esterno, puoi definire marcatori di annunci personalizzati e passarli alla timeline del lettore. <p>Per impostare un lettore per l'inserimento di annunci, devi passare i metadati degli annunci nella sezione dei metadati degli annunci personalizzati del file di configurazione JSON</a>, che ha un'implementazione di supporto ad provider nell'implementazione di riferimento. </p> </td>
  </tr>
 </tbody>
</table>