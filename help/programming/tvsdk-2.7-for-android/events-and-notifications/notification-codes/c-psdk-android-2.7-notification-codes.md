---
description: Il sistema di notifica TVSDK genera vari avvisi di errore, di avvertenza e informativi che forniscono metadati diagnostici.
title: Codici di notifica
exl-id: 7bf016c6-8651-413b-a478-ac2d24f9453c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# Panoramica {#notification-codes-overview}

Il sistema di notifica TVSDK genera vari avvisi di errore, di avvertenza e informativi che forniscono metadati diagnostici.

Gli oggetti di notifica forniscono informazioni relative allo stato del lettore. TVSDK fornisce un elenco cronologico di oggetti di notifica. Ogni notifica contiene i seguenti metadati:

<table frame="all" colsep="1" rowsep="1" id="table_1A32EFFE1834438D8261886EC9D7250D"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Elemento </th> 
   <th colname="2" class="entry"> Descrizione </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> tipo</span> </td> 
   <td colname="2"> <p>Il tipo di notifica. </p> <p>A seconda della piattaforma, questa proprietà è un tipo enumerato con i possibili valori INFO, WARN ed ERROR. Questo è il raggruppamento di primo livello per le notifiche. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> codice</span> </td> 
   <td colname="2"> <p>Alle notifiche vengono assegnate le seguenti rappresentazioni numeriche: 
     <ul id="ul_A86BF89D6B3B410E81FAD718D3C4A9F0"> 
      <li id="li_8180972D704C40098723734DD4B45643">Eventi di notifica degli errori, da 100000 a 199999 </li> 
      <li id="li_0EC29EA5F0034E5EBFEF8E68A6498D39">Eventi di notifica di avviso, da 200000 a 299999 </li> 
      <li id="li_189A53D3D7EF4960A521AB04D00DCF70">Eventi di notifica delle informazioni, da 300000 a 399999 </li> 
     </ul> </p> <p>Ogni intervallo di primo livello, ad esempio gli errori, è diviso in sottointervalli, ad esempio da 101000 a 101999 che rappresentano gli errori di riproduzione. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> nome</span> </td> 
   <td colname="2">Una stringa che contiene una descrizione leggibile dell’evento di notifica, ad esempio <span class="codeph"> SEEK_ERROR</span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> metadati</span> </td> 
   <td colname="2"> <p>Coppie chiave/valore contenenti ulteriori informazioni rilevanti sulla notifica. </p> <p>Ad esempio, una chiave denominata <span class="codeph"> URL</span> fornirebbe un valore che sia un URL correlato alla notifica, ad esempio un URL non valido che ha causato un errore. </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> innerNotification</span> </td> 
   <td colname="2"> <p>Un riferimento a un altro <span class="codeph"> MediaPlayerNotification</span> oggetto che ha avuto un impatto diretto su questa notifica. </p> <p>Un esempio potrebbe essere una notifica relativa a un errore di inserimento di annunci che corrisponde direttamente a un conflitto di inserimento della riga temporale. Non tutte le notifiche sono interne. </p> </td> 
  </tr> 
 </tbody> 
</table>
