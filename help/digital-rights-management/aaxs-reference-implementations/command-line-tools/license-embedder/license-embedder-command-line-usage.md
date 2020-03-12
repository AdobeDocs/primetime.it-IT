---
seo-title: Utilizzo della riga di comando
title: Utilizzo della riga di comando
uuid: 72117619-a723-49d3-9aa9-5eefcf5b0916
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

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
* `destfile` specifica dove verrà scritto il contenuto crittografato con la licenza incorporata. Se viene specificata una directory, il file verrà salvato in questa directory utilizzando lo stesso nome file del file di origine, ma la directory non deve essere la directory che contiene il file di origine.

Nella tabella seguente sono descritte le opzioni della riga di comando che è possibile specificare insieme alla sintassi di cui sopra:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_hnl_2sy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opzione della riga di comando </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrizione </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l license-filename </span> </td> 
   <td colname="2" class="- topic/entry "> Nome del file contenente la licenza da incorporare. È possibile specificare più opzioni <span class="codeph"> -l </span> per incorporare più licenze. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -m metadata-nomefile </span> </td> 
   <td colname="2" class="- topic/entry "> Specificate i metadati del contenuto per il quale generare una licenza. (Necessario per generare la licenza) </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> Non chiedere se il file di destinazione deve essere sovrascritto. Se il file di destinazione esiste già e <span class="codeph"> -o non </span> è impostato, viene restituito un errore. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> Se il file di destinazione esiste già, sovrascrivetelo senza richiedere l'invio di richieste. </td> 
  </tr> 
 </tbody> 
</table>

