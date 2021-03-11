---
description: Il sistema di notifica TVSDK genera vari errori, avvisi e avvisi informativi che forniscono metadati diagnostici.
title: Sistema di notifica TVSDK
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---


# Sistema di notifica TVSDK {#tvsdk-notification-system}

Il sistema di notifica TVSDK genera vari errori, avvisi e avvisi informativi che forniscono metadati diagnostici.

Gli oggetti di notifica forniscono informazioni relative allo stato del lettore. TVSDK fornisce un elenco ordinato cronologicamente degli oggetti di notifica e ogni notifica contiene i seguenti metadati:

<table frame="all" colsep="1" rowsep="1" id="table_DBA8CACF02DB4AF2B053E560850B49CE"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Elemento </th> 
   <th colname="2" class="entry"> Descrizione </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> type</span> </td> 
   <td colname="2"> Tipo di notifica. A seconda della piattaforma, questa proprietà fa riferimento a un tipo enumerato con possibili valori INFO, WARN o ERROR. Questo è il raggruppamento di livello principale per le notifiche. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> codice</span> </td> 
   <td colname="2">La rappresentazione numerica assegnata alla notifica. 
    <ul id="ul_31AB497C6FFA452496DD09B0D78687B9"> 
     <li id="li_53E75022C50246E0982E315D04EFD8B3">Eventi di notifica di errore, dal 10000 al 199999 </li> 
     <li id="li_11AE91D1325E4F718228E662C9C55F9A">Eventi di notifica di avviso, dal 20000 al 299999 </li> 
     <li id="li_6D3EA03845294DC2BAD1ACF507639E51">Eventi di notifica delle informazioni, da 30000 a 399999 </li> 
    </ul> <p>Ciascun intervallo di livello superiore, ad esempio gli errori, è suddiviso in sottointervalli, ad esempio da 101000 a 101999, che rappresentano gli errori di riproduzione. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> name</span> </td> 
   <td colname="2">Una stringa contenente una descrizione leggibile del codice, ad esempio <span class="codeph"> SEEK_ERROR</span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> metadati</span> </td> 
   <td colname="2">Coppie chiave/valore che contengono ulteriori informazioni rilevanti sulla notifica. Ad esempio, una chiave denominata <span class="codeph"> URL</span> verrebbe associata a un valore che è un URL correlato alla notifica, ad esempio un URL non valido che ha causato un errore. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> innerNotification</span> </td> 
   <td colname="2">Riferimento a un altro oggetto <span class="codeph"> PTNotification</span> che ha interessato direttamente questa notifica. Un esempio potrebbe essere una notifica di un errore di inserimento di annunci che corrisponde direttamente a un conflitto di inserimento della riga temporale. Non tutte le notifiche forniscono una notifica interna. </td> 
  </tr> 
 </tbody> 
</table>