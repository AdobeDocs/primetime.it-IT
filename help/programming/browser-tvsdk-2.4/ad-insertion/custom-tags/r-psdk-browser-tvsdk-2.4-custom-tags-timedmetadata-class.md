---
description: Quando Browser TVSDK rileva un tag con iscrizione nella playlist o nel manifesto, il lettore tenta automaticamente di elaborare il tag ed esporlo come oggetto TimedMetadata.
seo-description: Quando Browser TVSDK rileva un tag con iscrizione nella playlist o nel manifesto, il lettore tenta automaticamente di elaborare il tag ed esporlo come oggetto TimedMetadata.
seo-title: Classe di metadati temporizzati
title: Classe di metadati temporizzati
uuid: 3f276618-5f61-4b41-bd2d-78e7f32178d9
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Classe di metadati temporizzati{#timed-metadata-class}

Quando Browser TVSDK rileva un tag con iscrizione nella playlist o nel manifesto, il lettore tenta automaticamente di elaborare il tag ed esporlo come oggetto TimedMetadata.

La `TimedMetadata` classe fornisce gli elementi seguenti:

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
   <td colname="col1"> <p>type </p> </td> 
   <td colname="col02"> <p><span class="codeph"> TimedMetadataType</span> </p> </td> 
   <td colname="col2"> <p>Di seguito sono elencati i tipi di metadati temporizzati: 
     <ul id="ul_E79C375A54C64BF09A927EE8983E98E3"> 
      <li id="li_F1907521CDBE47E282A87AF0A7A1477A">TAG: i metadati temporizzati sono stati creati da un tag nella playlist o nel manifesto. </li> 
      <li id="li_5B0C0B0F247144709F86E6654A5AB500">ID3 - i metadati temporizzati sono stati creati da un tag ID3 nel flusso multimediale. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>time </p> </td> 
   <td colname="col02"> <p>Numero </p> </td> 
   <td colname="col2"> <p>La posizione dell'ora locale (millisecondi) rispetto all'inizio del contenuto principale in cui sono presenti i metadati temporizzati nel flusso. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>id </p> </td> 
   <td colname="col02"> <p>Stringa </p> </td> 
   <td colname="col2"> <p>Identificatore univoco dei metadati temporizzati. </p> <p>In genere viene estratto dall’attributo cue/tag ID, se presente. In caso contrario, si tratta di un valore casuale univoco. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>name </p> </td> 
   <td colname="col02"> <p>Numero </p> </td> 
   <td colname="col2"> <p>Nome dei metadati temporizzati. </p> <p>Se il tipo è TAG, il valore rappresenta il nome del cue/tag. Se il tipo è ID3, il valore è null. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>content </p> </td> 
   <td colname="col02"> <p>Stringa </p> </td> 
   <td colname="col2"> <p>Contenuto non elaborato dei metadati temporizzati. </p> <p>Se il tipo è TAG, il valore rappresenta l'intero elenco di attributi del cue/tag. Se il tipo id ID3, il valore è null. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>metadata </p> </td> 
   <td colname="col02"> <p><span class="codeph"> Metadati</span> </p> </td> 
   <td colname="col2"> <p>Informazioni elaborate/estratte dal tag personalizzato playlist/manifest. </p> </td> 
  </tr> 
 </tbody> 
</table>

