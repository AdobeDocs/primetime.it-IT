---
description: Il sistema di notifica TVSDK genera vari errori, avvisi e avvisi informativi che forniscono metadati diagnostici.
title: Codici di notifica
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---


# Panoramica {#notification-codes-overview}

Il sistema di notifica TVSDK genera vari errori, avvisi e avvisi informativi che forniscono metadati diagnostici.

Gli oggetti di notifica forniscono informazioni correlate allo stato del lettore. TVSDK fornisce un elenco ordinato cronologicamente degli oggetti di notifica. Ogni notifica contiene i seguenti metadati:

<table frame="all" colsep="1" rowsep="1" id="table_1A32EFFE1834438D8261886EC9D7250D"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Elemento </th> 
   <th colname="2" class="entry"> Descrizione </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> type</span> </td> 
   <td colname="2"> <p>Tipo di notifica. </p> <p>A seconda della piattaforma, questa proprietà è un tipo enumerato con i possibili valori INFO, WARN e ERROR. Questo è il raggruppamento di livello principale per le notifiche. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> codice</span> </td> 
   <td colname="2"> <p>Alle notifiche sono assegnate le seguenti rappresentazioni numeriche: 
     <ul id="ul_A86BF89D6B3B410E81FAD718D3C4A9F0"> 
      <li id="li_8180972D704C40098723734DD4B45643">Eventi di notifica di errore, dal 10000 al 199999 </li> 
      <li id="li_0EC29EA5F0034E5EBFEF8E68A6498D39">Eventi di notifica di avviso, dal 20000 al 299999 </li> 
      <li id="li_189A53D3D7EF4960A521AB04D00DCF70">Eventi di notifica delle informazioni, da 30000 a 399999 </li> 
     </ul> </p> <p>Ciascun intervallo di livello superiore, ad esempio gli errori, è suddiviso in sottointervalli, ad esempio da 101000 a 101999, che rappresentano gli errori di riproduzione. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> name</span> </td> 
   <td colname="2">Una stringa che contiene una descrizione leggibile dall'utente dell'evento di notifica, ad esempio <span class="codeph"> SEEK_ERROR</span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> metadati</span> </td> 
   <td colname="2"> <p>Coppie chiave/valore che contengono ulteriori informazioni rilevanti sulla notifica. </p> <p>Ad esempio, una chiave denominata <span class="codeph"> URL</span> fornirà un valore corrispondente a un URL correlato alla notifica, ad esempio un URL non valido che ha causato un errore. </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> innerNotification</span> </td> 
   <td colname="2"> <p>Un riferimento a un altro oggetto <span class="codeph"> MediaPlayerNotification</span> che ha avuto un impatto diretto su questa notifica. </p> <p>Un esempio potrebbe essere una notifica di un errore di inserimento di annunci che corrisponde direttamente a un conflitto di inserimento della riga temporale. Non tutte le notifiche forniscono una notifica interna. </p> </td> 
  </tr> 
 </tbody> 
</table>

