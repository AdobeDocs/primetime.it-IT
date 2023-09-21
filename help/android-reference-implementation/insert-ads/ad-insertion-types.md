---
description: TVSDK attualmente fornisce il supporto integrato dei metadati del provider di annunci per annunci TVSDK, interruzioni pubblicitarie dirette e marcatori di annunci personalizzati.
title: Tipi di inserimento di annunci
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# Tipi di inserimento di annunci {#ad-insertion-types}

TVSDK attualmente fornisce il supporto integrato dei metadati del provider di annunci per annunci TVSDK, interruzioni pubblicitarie dirette e marcatori di annunci personalizzati.

Supporta i seguenti tipi di flussi di lavoro di inserimento di annunci per contenuti VOD e live/lineari.

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
   <td colname="col1"> annunci di Adobe Primetime ad decisioning </td> 
   <td colname="col2">VOD <p>Live </p> <p>Lineare </p> </td> 
   <td colname="col3">L’implementazione di riferimento fornisce <span class="codeph"> AuditudeMetadata</span> informazioni per la connessione al server per Primetime ad decisioning (precedentemente noto come Auditude), in base alle informazioni fornite nella sezione annunci di Primetime</a> del file di configurazione JSON</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Interruzioni pubblicitarie dirette </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">Devi fornire gli URL dell’annuncio nel file JSON di input. Quando TVSDK tenta di risolvere un annuncio, chiama il risolutore dell’interruzione pubblicitaria diretta e risolve gli annunci in base alle informazioni sull’interruzione pubblicitaria diretta fornite nel file di configurazione JSON</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Marcatori annuncio personalizzati </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">I marcatori di annunci personalizzati sono utili quando il flusso video contiene sia il contenuto principale che gli annunci, ma non include informazioni relative alle posizioni e alla tempistica degli annunci. Se le informazioni sul posizionamento dell’annuncio vengono ottenute in un altro modo, ad esempio tramite un CMS esterno, puoi definire marcatori di annuncio personalizzati e passarli alla timeline del lettore. <p>Per impostare un lettore per l’inserimento di annunci, devi passare i metadati degli annunci nella sezione dei metadati degli annunci personalizzati del file di configurazione JSON</a>, che dispone di un'implementazione di supporto e provider nell'implementazione di riferimento. </p> </td>
  </tr>
 </tbody>
</table>
