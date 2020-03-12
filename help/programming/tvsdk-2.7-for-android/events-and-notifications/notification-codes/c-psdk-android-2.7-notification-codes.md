---
description: Il sistema di notifica TVSDK genera vari errori, avvisi e avvisi informativi che forniscono metadati diagnostici.
seo-description: Il sistema di notifica TVSDK genera vari errori, avvisi e avvisi informativi che forniscono metadati diagnostici.
seo-title: Codici di notifica
title: Codici di notifica
uuid: 24476204-5c35-4ff9-810d-77698ea18b53
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Panoramica {#notification-codes-overview}

Il sistema di notifica TVSDK genera vari errori, avvisi e avvisi informativi che forniscono metadati diagnostici.

Gli oggetti di notifica forniscono informazioni correlate allo stato del lettore. TVSDK fornisce un elenco cronologico degli oggetti di notifica. Ogni notifica contiene i seguenti metadati:

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
   <td colname="2"> <p>Il tipo di notifica. </p> <p>A seconda della piattaforma, questa proprietà è un tipo enumerato con possibili valori INFO, AVVERTENZA ed ERRORE. Questo è il raggruppamento di livello principale per le notifiche. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> code</span> </td> 
   <td colname="2"> <p>Alle notifiche sono assegnate le seguenti rappresentazioni numeriche: 
     <ul id="ul_A86BF89D6B3B410E81FAD718D3C4A9F0"> 
      <li id="li_8180972D704C40098723734DD4B45643">Eventi di notifica di errore, dal 100000 al 19999 </li> 
      <li id="li_0EC29EA5F0034E5EBFEF8E68A6498D39">Eventi di notifica di avviso, dal 20000 al 299999 </li> 
      <li id="li_189A53D3D7EF4960A521AB04D00DCF70">Eventi di notifica delle informazioni, da 300000 a 399999 </li> 
     </ul> </p> <p>Ciascun intervallo di livello principale, ad esempio errori, è suddiviso in sottointervalli, ad esempio da 101000 a 101999 che rappresentano errori di riproduzione. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> name</span> </td> 
   <td colname="2">Una stringa che contiene una descrizione leggibile dell'evento di notifica, ad esempio <span class="codeph"> SEEK_ERROR</span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> metadata</span> </td> 
   <td colname="2"> <p>Coppie chiave/valore che contengono ulteriori informazioni rilevanti sulla notifica. </p> <p>Ad esempio, una chiave denominata <span class="codeph"> URL</span> fornisce un valore che è un URL correlato alla notifica, ad esempio un URL non valido che ha causato un errore. </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> innerNotification</span> </td> 
   <td colname="2"> <p>Un riferimento a un altro oggetto <span class="codeph"> MediaPlayerNotification</span> che ha avuto un impatto diretto su questa notifica. </p> <p>Un esempio potrebbe essere una notifica di un errore di inserimento di annunci che corrisponde direttamente a un conflitto di inserimento della riga temporale. Non tutte le notifiche forniscono una notifica interna. </p> </td> 
  </tr> 
 </tbody> 
</table>

