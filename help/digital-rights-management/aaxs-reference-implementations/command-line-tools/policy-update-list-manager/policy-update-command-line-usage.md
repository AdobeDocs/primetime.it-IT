---
title: Utilizzo della riga di comando
description: Utilizzo della riga di comando
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Utilizzo della riga di comando {#command-line-usage}

Policy Update List Manager si trova nella directory \Reference Implementation\Command Line Tools sul DVD. Per creare un elenco di aggiornamenti dei criteri, utilizzare la sintassi seguente:

```
    java -jar AdobePolicyUpdateListManager.jar  
<i class="+ topic ph hi-d="" i "="">
  destfile [ 
 <i class="+ topic ph hi-d="" i "="">
   options]  
 </i class="+ topic> 
</i class="+ topic>
```

* `destfile` indica dove verrà scritto l&#39;elenco di aggiornamento dei criteri.

Per visualizzare un elenco di aggiornamenti dei criteri esistente, utilizzare la sintassi seguente:

```
    java -jar AdobePolicyUpdateListManager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  filename 
</i class="+ topic>
```

La tabella seguente contiene le descrizioni delle opzioni della riga di comando mostrate nella sintassi precedente:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_ghb_jqy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opzione della riga di comando </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrizione </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c file di configurazione </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica la posizione del file di configurazione. Se questa opzione non viene utilizzata, Gestione elenchi aggiornamenti criteri cercherà <span class="filepath"> flashaccesstools.properties </span> nella directory di lavoro. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -d nomefile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Visualizza informazioni sull'elenco di aggiornamento dei criteri. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e data </span> </td> 
   <td colname="2" class="- topic/entry "> (Facoltativo) La data di scadenza dell’elenco di aggiornamento dei criteri. Utilizza il formato <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-gg </span> o <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-gg-h24:min:sec </span> (ad esempio, 2009-01-31-14:30:00 rappresenta il 31 gennaio alle 14:30). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -f nomefile [certfile] </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Aggiunge tutte le voci dall'elenco di aggiornamento dei criteri esistente. È possibile specificare un solo file esistente. </p> <p class="- topic/p ">Se l'elenco esistente è stato firmato con una credenziale diversa da quella utilizzata per firmare il nuovo elenco, specificarne il file di certificato, in modo che la firma possa essere verificata. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Non chiedere se il file di destinazione deve essere sovrascritto. Se il file di destinazione esiste già e <span class="codeph"> -o </span> non è impostato, verrà restituito un errore. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se il file di destinazione esiste già, sovrascriverlo senza chiedere conferma. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r policyID </span> <span class="+ topic/ph pr-d/codeph codeph"> data </span> " <span class="+ topic/ph pr-d/codeph codeph"> reasonCode </span>"" <span class="+ topic/ph pr-d/codeph codeph"> reasonText </span>"" <span class="+ topic/ph pr-d/codeph codeph"> reasonURL </span>" </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(Facoltativo) Revoca l’ID del criterio alla data specificata. È inoltre possibile fornire un codice motivo facoltativo, un testo motivo e un URL motivo. Specifica una stringa vuota "" per indicare che non viene fornito alcun valore per i parametri facoltativi. Specifica la data come <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-gg </span> o <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-gg-h24:min:sec </span> (ad esempio 2008-12-1 o 2008-12-1-00:00:00 per mezzanotte del 1 dicembre 2008). Se non viene specificata una data, viene utilizzata la data corrente. Il codice motivo deve essere maggiore o uguale a 0. È possibile specificare più opzioni -r. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-rf <span class="+ topic/ph pr-d/codeph codeph"> policyFilename </span> <span class="+ topic/ph pr-d/codeph codeph"> data </span> " <span class="+ topic/ph pr-d/codeph codeph"> reasonCode </span>"" <span class="+ topic/ph pr-d/codeph codeph"> reasonText </span>"" <span class="+ topic/ph pr-d/codeph codeph"> reasonURL </span>" </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Esegue la stessa azione del flag -r, ma estrae l’identificatore della policy dal file specificato. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -u policyFilename " reasonCode" " reasonText" " reasonURL" </span> </td> 
   <td colname="2" class="- topic/entry "> <p>Sostituisce qualsiasi criterio corrispondente in una richiesta di licenza con questo criterio utilizzando il codice motivo specificato (facoltativo), il testo del motivo (facoltativo) e l’URL del motivo (facoltativo). </p> <p>Specifica una stringa vuota "" per indicare che non viene fornito alcun valore per i parametri facoltativi. </p> <p>Il codice motivo deve essere maggiore o uguale a <span class="codeph"> 0 </span>. Più <span class="codeph"> -u </span> è possibile specificare le opzioni. </p> </td> 
  </tr> 
 </tbody> 
</table>
