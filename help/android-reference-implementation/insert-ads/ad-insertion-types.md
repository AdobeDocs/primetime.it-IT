---
description: TVSDK fornisce attualmente il supporto di metadati del provider di annunci incorporati per annunci TVSDK, interruzioni di annunci diretti e marcatori di annunci personalizzati.
seo-description: TVSDK fornisce attualmente il supporto di metadati del provider di annunci incorporati per annunci TVSDK, interruzioni di annunci diretti e marcatori di annunci personalizzati.
seo-title: Tipi di inserimento annunci
title: Tipi di inserimento annunci
uuid: 6b5c3555-1ddd-4215-8bb2-03d16bb818c5
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---


# Tipi di inserimento annunci {#ad-insertion-types}

TVSDK fornisce attualmente il supporto di metadati del provider di annunci incorporati per annunci TVSDK, interruzioni di annunci diretti e marcatori di annunci personalizzati.

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
   <td colname="col1">  annunci pubblicitari su Adobe Primetime </td> 
   <td colname="col2">VOD <p>Live </p> <p>Linear </p> </td> 
   <td colname="col3">L'implementazione di riferimento fornisce <span class="codeph"> AuditudeMetadata</span> informazioni per la connessione al server per la decisione di annunci Primetime (precedentemente nota come Auditude), sulla base delle informazioni fornite nella porzione di annunci Primetime</a> del file di configurazione JSON</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Interruzioni annuncio dirette </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">Devi fornire gli URL degli annunci nel file JSON di input. Quando TVSDK tenta di risolvere un annuncio, chiama il risolutore di interruzioni pubblicitarie dirette e risolve gli annunci in base alle informazioni di interruzioni pubblicitarie dirette fornite nel file di configurazione JSON</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Indicatori di annunci personalizzati </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">I marcatori di annunci personalizzati sono utili quando il flusso video contiene sia il contenuto principale che gli annunci, ma non include informazioni relative alle posizioni e ai tempi degli annunci. Se le informazioni sul posizionamento dell’annuncio vengono ottenute in un altro modo, ad esempio tramite un CMS esterno, potete definire indicatori di annunci personalizzati e passarli alla timeline del lettore. <p>Per impostare un lettore per l'inserimento di annunci, è necessario trasmettere i metadati degli annunci nella sezione dei metadati degli annunci personalizzati del file di configurazione JSON</a>, che dispone di un'implementazione del provider di annunci di supporto nell'implementazione di riferimento. </p> </td>
  </tr>
 </tbody>
</table>