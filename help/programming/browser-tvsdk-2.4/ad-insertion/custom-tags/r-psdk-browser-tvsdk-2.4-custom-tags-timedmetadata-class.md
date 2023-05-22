---
description: Quando il browser TVSDK rileva un tag sottoscritto nella playlist/manifesto, il lettore tenta automaticamente di elaborare il tag e di esporlo come oggetto TimedMetadata.
title: Classe metadati temporizzati
exl-id: 893879b5-03ed-4c11-80a6-b57b7d54a95c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Classe metadati temporizzati{#timed-metadata-class}

Quando il browser TVSDK rileva un tag sottoscritto nella playlist/manifesto, il lettore tenta automaticamente di elaborare il tag e di esporlo come oggetto TimedMetadata.

Il `TimedMetadata` La classe fornisce i seguenti elementi:

<table id="table_5827A0626EDC45F68DC3E7644F3EFF69"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Proprietà </th> 
   <th colname="col02" class="entry"> Tipo </th> 
   <th colname="col2" class="entry"> Descrizione </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>tipo </p> </td> 
   <td colname="col02"> <p><span class="codeph"> TimedMetadataType</span> </p> </td> 
   <td colname="col2"> <p>Di seguito sono elencati i tipi di metadati temporizzati: 
     <ul id="ul_E79C375A54C64BF09A927EE8983E98E3"> 
      <li id="li_F1907521CDBE47E282A87AF0A7A1477A">TAG: i metadati temporizzati sono stati creati da un tag nella playlist/manifesto. </li> 
      <li id="li_5B0C0B0F247144709F86E6654A5AB500">ID3: i metadati temporizzati sono stati creati da un tag ID3 nel flusso multimediale. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>tempo </p> </td> 
   <td colname="col02"> <p>Numero </p> </td> 
   <td colname="col2"> <p>La posizione temporale locale (millisecondi) relativa all’inizio del contenuto principale in cui sono presenti i metadati temporizzati nel flusso. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>id </p> </td> 
   <td colname="col02"> <p>Stringa </p> </td> 
   <td colname="col2"> <p>Identificatore univoco dei metadati temporizzati. </p> <p>Viene in genere estratto dall’attributo ID cue/tag, se presente. In caso contrario, si tratta di un valore casuale univoco. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>nome </p> </td> 
   <td colname="col02"> <p>Numero </p> </td> 
   <td colname="col2"> <p>Nome dei metadati temporizzati. </p> <p>Se il tipo è TAG, il valore rappresenta il nome del cue/tag. Se il tipo è ID3, il valore è null. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>contenuto </p> </td> 
   <td colname="col02"> <p>Stringa </p> </td> 
   <td colname="col2"> <p>Il contenuto non elaborato dei metadati temporizzati. </p> <p>Se il tipo è TAG, il valore rappresenta l'intero elenco di attributi del cue/tag. Se il tipo id ID3, il valore è null. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>metadati </p> </td> 
   <td colname="col02"> <p><span class="codeph"> Metadati</span> </p> </td> 
   <td colname="col2"> <p>Le informazioni elaborate/estratte dal tag personalizzato playlist/manifest. </p> </td> 
  </tr> 
 </tbody> 
</table>
