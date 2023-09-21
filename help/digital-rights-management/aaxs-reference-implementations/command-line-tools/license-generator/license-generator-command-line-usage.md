---
title: Utilizzo della riga di comando
description: Utilizzo della riga di comando
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# Utilizzo della riga di comando {#command-line-usage}

Per generare una licenza, utilizzare la sintassi seguente:

```
    java -jar AdobeLicenseGenerator.jar -m 
<i class="+ topic ph hi-d="" i "="">
 metadata 
 <i class="+ topic ph hi-d="" i "="">
   [options]
 </i class="+ topic>
</i class="+ topic>
```

`metadata` è un file con estensione metadata contenente i metadati DRM di Access Adobe. Questo file può essere ottenuto da contenuto protetto utilizzando `-d -m` opzione di Media Packager.

Per visualizzare una licenza generata in precedenza, utilizzare la sintassi seguente:

```
    java -jar AdobeLicenseGenerator.jar -d 
<i class="+ topic ph hi-d="" i "="">
  license
</i class="+ topic>
```

`license` è un file contenente una licenza di accesso Adobe generata dal Generatore di licenze.

La tabella seguente descrive le opzioni della riga di comando che possono essere specificate insieme alla sintassi precedentemente indicata:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_skr_vry_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opzione della riga di comando </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrizione </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-c file di configurazione</span> </td> 
   <td colname="2" class="- topic/entry "> Specificare il percorso del file di configurazione. Se questa opzione non viene utilizzata, il Generatore di licenze cercherà flashaccesstools.properties nella directory di lavoro. Le opzioni specificate nella riga di comando hanno la precedenza su quelle presenti nel file di configurazione. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">d <i class="+ topic/ph hi-d/i "><span class="+ topic/ph pr-d/codeph codeph"> licensefile</span></i> </p> </td> 
   <td colname="2" class="- topic/entry "> Mostra informazioni su una licenza già generata. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-leaf leaf-filename</span> </td> 
   <td colname="2" class="- topic/entry "> Generare una licenza foglia e scrivere l'output in un file specificato. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-m nome-file-metadati</span> </td> 
   <td colname="2" class="- topic/entry "> Specifica i metadati di contenuto per i quali generare una licenza. (necessario per generare la licenza) </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry ">Non chiedere se il file di destinazione deve essere sovrascritto. Se il file di destinazione esiste già e <span class="codeph"> -o</span> non è impostato, verrà restituito un errore. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> Se il file di destinazione esiste già, sovrascriverlo senza chiedere conferma. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-policy-num</span> </td> 
   <td colname="2" class="- topic/entry "> Se i metadati contengono più criteri, specifica il numero di criteri da utilizzare (a partire da 1) per generare la licenza. Se non viene specificato, viene utilizzato il primo criterio. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-r certificato destinatario</span> </td> 
   <td colname="2" class="- topic/entry ">Genera una licenza per il destinatario specificato. È possibile utilizzare un dispositivo o un certificato di dominio. Più <span class="+ topic/ph pr-d/codeph codeph"> -r </span>è possibile specificare opzioni per creare una licenza per più destinatari. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-root-filename</span> </td> 
   <td colname="2" class="- topic/entry "> Generare una licenza radice e scrivere l'output nel file specificato. </td> 
  </tr> 
 </tbody> 
</table>
