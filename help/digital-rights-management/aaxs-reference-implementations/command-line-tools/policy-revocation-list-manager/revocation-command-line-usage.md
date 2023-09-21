---
title: Utilizzo della riga di comando
description: Utilizzo della riga di comando
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# Utilizzo della riga di comando {#command-line-usage}

Revocation List Manager si trova nella directory \Reference Implementation\Command Line Tools del DVD. Per eseguire lo strumento, utilizzare una delle sintassi seguenti:

```
    java -jar AdobeRevocationListManager.jar 
<i class="+ topic ph hi-d="" i "="">
 destfile 
 <i class="+ topic ph hi-d="" i "="">
  crlNumber [
  <i class="+ topic ph hi-d="" i "="">
   options] 
       java -jar AdobeRevocationListManager.jar -d 
   <i class="+ topic ph hi-d="" i "="">
     filename
   </i class="+ topic>
  </i class="+ topic>
 </i class="+ topic>
</i class="+ topic>
```

* `destfile` indica dove verrà scritto l&#39;elenco di revoche.
* `crlNumber` è un numero di versione non negativo dell’elenco di revoche di certificati (CRL, Certificate Revocation List). Questo numero deve essere incrementato ogni volta che il CRL viene aggiornato.

La tabella seguente contiene le descrizioni delle opzioni della riga di comando mostrate nella sintassi precedente:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_a3y_wqy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Opzione della riga di comando </th> 
   <th colname="2" class="- topic/entry entry"> Descrizione </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-c file di configurazione</span> </td> 
   <td colname="2" class="- topic/entry ">Specifica la posizione del file di configurazione. Se questa opzione non viene utilizzata, il gestore elenchi di revoche cercherà <span class="filepath"> flashaccesstools.properties</span> nella directory di lavoro. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-d nomefile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Visualizza informazioni sull'elenco di revoche. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-e data</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(Facoltativo) La data di scadenza dell'elenco di revoche. Utilizza il formato <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-gg</span> o <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-gg-h24:min:sec</span> (ad esempio, 2009-01-31-14:30:00 rappresenta il 31 gennaio alle 14:30). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-f nomefile[certfile]</span> </td> 
   <td colname="2" class="- topic/entry ">Aggiunge tutte le voci dall'elenco di revoche esistente. È possibile specificare un solo file esistente. <p class="- topic/p ">Se l'elenco esistente è stato firmato con una credenziale diversa da quella utilizzata per firmare il nuovo elenco, specificare il file di certificato, in modo da verificarne la firma. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Non chiedere se il file di destinazione deve essere sovrascritto. Se il file di destinazione esiste già e -o non è impostato, verrà restituito un errore. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> Se il file di destinazione esiste già, sovrascriverlo senza chiedere conferma. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-r issuerName serialNumber revoationDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Revoca il certificato identificato da <span class="codeph"> issuerName</span> e <span class="codeph"> serialNumber</span> alla data specificata. Il <span class="codeph"> issuerName</span> deve seguire il formato 509 (ad esempio, <span class="codeph"> CN=12345,O=Adobe Systems Incorporated,C=US</span>). Specificare i numeri di serie in formato esadecimale. Specifica la data di revoca come <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-gg</span> o <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-gg-h24:min:sec</span>, ad esempio 2008-12-1 o 2008-12-1-00:00:00 per mezzanotte del 1 dicembre 2008. Se la data di revoca non è specificata, viene utilizzata la data corrente. </p> </td> 
  </tr> 
 </tbody> 
</table>
