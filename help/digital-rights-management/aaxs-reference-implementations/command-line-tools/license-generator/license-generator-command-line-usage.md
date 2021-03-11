---
title: Uso della riga di comando
description: Uso della riga di comando
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---


# Uso della riga di comando {#command-line-usage}

Per generare una licenza, utilizza la sintassi seguente:

```
    java -jar AdobeLicenseGenerator.jar -m 
<i class="+ topic ph hi-d="" i "="">
 metadata 
 <i class="+ topic ph hi-d="" i "="">
   [options]
 </i class="+ topic>
</i class="+ topic>
```

`metadata` è un file .metadata contenente i metadati DRM di accesso Adobe. Questo file può essere ottenuto da contenuti protetti utilizzando l&#39;opzione `-d -m` di Media Packager.

Per visualizzare una licenza generata in precedenza, utilizza la sintassi seguente:

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
   <td colname="2" class="- topic/entry "> Specifica il percorso del file di configurazione. Se questa opzione non viene utilizzata, il Generatore licenze cercherà flashaccesstools.properties nella directory di lavoro. Le opzioni specificate nella riga di comando hanno la precedenza su quelle presenti nel file di configurazione. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <i class="+ topic/ph hi-d/i "><span class="+ topic/ph pr-d/codeph codeph"> file di licenza</span></i> </p> </td> 
   <td colname="2" class="- topic/entry "> Mostra informazioni su una licenza già generata. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-nomefile foglia</span> </td> 
   <td colname="2" class="- topic/entry "> Generare una licenza foglia e scrivere l'output in un file specifico. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-m metadata-nomefile</span> </td> 
   <td colname="2" class="- topic/entry "> Specifica i metadati del contenuto per i quali generare una licenza. (Necessario per generare la licenza) </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry ">Non chiedere se il file di destinazione deve essere sovrascritto. Se il file di destinazione esiste già e <span class="codeph"> -o</span> non è impostato, verrà restituito un errore. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> Se il file di destinazione esiste già, sovrascriverlo senza richiedere conferma. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-policy-num</span> </td> 
   <td colname="2" class="- topic/entry "> Se i metadati contengono più criteri, specifica il numero del criterio da utilizzare (a partire da 1) per generare la licenza. Se non viene specificato, viene utilizzato il primo criterio. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-r Certificato del destinatario</span> </td> 
   <td colname="2" class="- topic/entry ">Genera una licenza per il destinatario specificato. È possibile utilizzare un certificato di dominio o dispositivo. È possibile specificare più opzioni <span class="+ topic/ph pr-d/codeph codeph"> -r </span>per creare una licenza per più destinatari. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-root-nomefile</span> </td> 
   <td colname="2" class="- topic/entry "> Genera una licenza root e scrivi l'output nel file specificato. </td> 
  </tr> 
 </tbody> 
</table>

