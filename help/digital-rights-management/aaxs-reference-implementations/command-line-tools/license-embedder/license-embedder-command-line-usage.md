---
title: Uso della riga di comando
description: Uso della riga di comando
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---


# Uso della riga di comando {#command-line-usage}

Per incorporare una licenza, utilizza la sintassi seguente:

```
    java -jar AdobeLicenseEmbedder.jar  
<i class="+ topic ph hi-d="" i "="">
  sourcefile destfile [options] 
</i class="+ topic>
```

* `sourcefile` è un file FLV o F4V crittografato.
* `destfile` specifica dove verrà scritto il contenuto crittografato con la licenza incorporata. Se viene specificata una directory, il file verrà salvato in questa directory utilizzando lo stesso nome file del file di origine, ma la directory non deve essere la directory che contiene il file di origine.

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
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l license-filename  </span> </td> 
   <td colname="2" class="- topic/entry "> Nome del file contenente la licenza da incorporare. È possibile specificare più opzioni <span class="codeph"> -l </span> per incorporare più licenze. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -m metadata-nomefile  </span> </td> 
   <td colname="2" class="- topic/entry "> Specifica i metadati del contenuto per i quali generare una licenza. (Necessario per generare la licenza) </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt  </span> </td> 
   <td colname="2" class="- topic/entry "> Non chiedere se il file di destinazione deve essere sovrascritto. Se il file di destinazione esiste già e <span class="codeph"> -o </span> non è impostato, viene restituito un errore. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o  </span> </td> 
   <td colname="2" class="- topic/entry "> Se il file di destinazione esiste già, sovrascriverlo senza richiedere conferma. </td> 
  </tr> 
 </tbody> 
</table>

