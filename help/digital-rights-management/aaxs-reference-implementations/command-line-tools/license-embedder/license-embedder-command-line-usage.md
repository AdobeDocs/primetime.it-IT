---
title: Utilizzo della riga di comando
description: Utilizzo della riga di comando
copied-description: true
exl-id: 51b11ef8-438e-4747-be3e-e1774dc9f31a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Utilizzo della riga di comando {#command-line-usage}

Per incorporare una licenza, utilizzare la sintassi seguente:

```
    java -jar AdobeLicenseEmbedder.jar  
<i class="+ topic ph hi-d="" i "="">
  sourcefile destfile [options] 
</i class="+ topic>
```

* `sourcefile` è un file FLV o F4V crittografato.
* `destfile` specifica dove verranno scritti i contenuti crittografati con la licenza incorporata. Se si specifica una directory, il file verrà salvato in questa directory utilizzando lo stesso nome del file di origine, ma la directory non deve essere quella che contiene il file di origine.

La tabella seguente descrive le opzioni della riga di comando che possono essere specificate insieme alla sintassi precedentemente indicata:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_hnl_2sy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opzione della riga di comando </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrizione </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l nome-file-licenza </span> </td> 
   <td colname="2" class="- topic/entry "> Nome del file contenente la licenza da incorporare. Più <span class="codeph"> -l </span> è possibile specificare opzioni per incorporare più licenze. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -m nome-file-metadati </span> </td> 
   <td colname="2" class="- topic/entry "> Specifica i metadati di contenuto per i quali generare una licenza. (necessario per generare la licenza) </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> Non chiedere se il file di destinazione deve essere sovrascritto. Se il file di destinazione esiste già e <span class="codeph"> -o </span> non è impostato, verrà restituito un errore. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> Se il file di destinazione esiste già, sovrascriverlo senza chiedere conferma. </td> 
  </tr> 
 </tbody> 
</table>
