---
title: Panoramica
description: Panoramica
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---


# Embedder della licenza DRM {#license-embedder}

Utilizza [!DNL AdobeLicenseEmbedder.jar] per incorporare le licenze pregenerate nei contenuti protetti da Media Packager.

## Uso della riga di comando Embedder della licenza {#license-embedder-command-line-usage}

```
java -jar AdobeLicenseEmbedder.jar sourcefile destfile [options]
```

* `sourcefile` rappresenta un file crittografato.
* `destfile` specifica il nome del file in cui viene salvato il contenuto crittografato con la licenza incorporata.

   Se si specifica una directory, il file viene salvato nella directory di destinazione. Il nome del file di origine diventa anche il nome del file salvato nella directory di destinazione.

Nella tabella seguente sono descritte le opzioni della riga di comando che è possibile specificare:

**Tabella 7: Opzioni**

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
   <td colname="2" class="- topic/entry "> Nome del file che include la licenza da incorporare. È possibile specificare più opzioni <span class="codeph"> -l </span> per incorporare più licenze. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -m metadata-nomefile  </span> </td> 
   <td colname="2" class="- topic/entry "> Specifica i metadati del contenuto per i quali è possibile generare una licenza. Questa opzione è necessaria per generare una licenza. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt  </span> </td> 
   <td colname="2" class="- topic/entry "> Non chiedere se il file di destinazione deve essere sovrascritto. Se il file di destinazione esiste già e il <span class="codeph"> -o </span> non è stato applicato, si verifica un errore. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o  </span> </td> 
   <td colname="2" class="- topic/entry "> Se il file di destinazione esiste già, puoi sovrascriverlo senza che venga richiesto di farlo. </td> 
  </tr> 
 </tbody> 
</table>
