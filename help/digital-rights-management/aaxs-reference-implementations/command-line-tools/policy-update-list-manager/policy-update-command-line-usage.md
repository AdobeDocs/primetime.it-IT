---
title: Uso della riga di comando
description: Uso della riga di comando
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---


# Uso della riga di comando {#command-line-usage}

Gestione elenchi aggiornamenti criteri si trova nella directory \Reference Implementation\Command Line Tools del DVD. Per creare un elenco di aggiornamento dei criteri, utilizzare la sintassi seguente:

```
    java -jar AdobePolicyUpdateListManager.jar  
<i class="+ topic ph hi-d="" i "="">
  destfile [ 
 <i class="+ topic ph hi-d="" i "="">
   options]  
 </i class="+ topic> 
</i class="+ topic>
```

* `destfile` indica dove verrà scritto l&#39;elenco degli aggiornamenti dei criteri.

Per visualizzare un elenco di aggiornamento dei criteri esistente, utilizzare la sintassi seguente:

```
    java -jar AdobePolicyUpdateListManager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  filename 
</i class="+ topic>
```

La tabella seguente contiene le descrizioni delle opzioni della riga di comando visualizzate nella sintassi precedente:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_ghb_jqy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opzione della riga di comando </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrizione </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c file di configurazione  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica il percorso del file di configurazione. Se questa opzione non viene utilizzata, Gestione elenchi aggiornamenti criteri cercherà <span class="filepath"> flashaccesstools.properties </span> nella directory di lavoro. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -d nome del file  </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Visualizza informazioni sull'elenco degli aggiornamenti dei criteri. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e data  </span> </td> 
   <td colname="2" class="- topic/entry "> (Facoltativo) La data di scadenza dell'elenco di aggiornamento dei criteri. Utilizzare il formato <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-gg </span> o <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-gg-h24:min:sec </span> (ad esempio, 2009-01-31-14:30:00 rappresenta il 31 gennaio alle 2:30 PM). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -f nomefile [certfile]  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Aggiunge tutte le voci dall'elenco di aggiornamento dei criteri esistente. È possibile specificare un solo file esistente. </p> <p class="- topic/p ">Se l’elenco esistente è stato firmato con una credenziale diversa da quella utilizzata per firmare il nuovo elenco, specificare il file del certificato corrispondente, in modo da verificarne la firma. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -noprompt  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Non chiedere se il file di destinazione deve essere sovrascritto. Se il file di destinazione esiste già e <span class="codeph"> -o </span> non è impostato, viene restituito un errore. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se il file di destinazione esiste già, sovrascriverlo senza richiedere conferma. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r  </span> <span class="+ topic/ph pr-d/codeph codeph"> data policyID  </span> "  <span class="+ topic/ph pr-d/codeph codeph"> motivoCodice  </span>" "  <span class="+ topic/ph pr-d/codeph codeph"> motivoTesto  </span>" "  <span class="+ topic/ph pr-d/codeph codeph"> motivoURL  </span>" </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(Facoltativo) Revoca l'ID del criterio alla data specificata. È inoltre possibile fornire un codice motivo, un testo del motivo e un URL del motivo facoltativo. Specifica una stringa vuota "" per indicare che non viene fornito alcun valore per i parametri facoltativi. Specificare la data come <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-gg </span> o <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-gg-h24:min:sec </span> (ad esempio 2008-12-1 o 2008-12-1-00:00:00 per mezzanotte del 1 dicembre 20 08). Se non viene specificata una data, viene utilizzata la data corrente. Il codice del motivo deve essere maggiore o uguale a 0. È possibile specificare più opzioni -r. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-rf <span class="+ topic/ph pr-d/codeph codeph"> policyFilename </span> <span class="+ topic/ph pr-d/codeph codeph"> data </span> " <span class="+ topic/ph pr-d/codeph codeph"> reasonCode </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonText </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonURL </span>" </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Esegue la stessa azione del flag -r, ma estrae l’identificatore del criterio dal file specificato. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -u policyFilename " reasonCode" " reasonText" " reasonURL"  </span> </td> 
   <td colname="2" class="- topic/entry "> <p>Sostituisce qualsiasi criterio di corrispondenza in una richiesta di licenza con questo criterio utilizzando il codice del motivo specificato (facoltativo), il testo del motivo (facoltativo) e l’URL del motivo (facoltativo). </p> <p>Specifica una stringa vuota "" per indicare che non viene fornito alcun valore per i parametri facoltativi. </p> <p>Il codice del motivo deve essere maggiore o uguale a <span class="codeph"> 0 </span>. È possibile specificare più opzioni <span class="codeph"> -u </span>. </p> </td> 
  </tr> 
 </tbody> 
</table>

