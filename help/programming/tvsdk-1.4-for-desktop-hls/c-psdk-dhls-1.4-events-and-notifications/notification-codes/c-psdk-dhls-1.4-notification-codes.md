---
description: Il sistema di notifica TVSDK genera vari avvisi di errore, di avvertenza e informativi che forniscono metadati diagnostici.
title: Codici di notifica
exl-id: 7ea079f1-658d-45ab-891d-044b7b4ff4ec
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# Panoramica {#notification-codes-overview}

Il sistema di notifica TVSDK genera vari avvisi di errore, di avvertenza e informativi che forniscono metadati diagnostici.

Gli oggetti di notifica forniscono informazioni relative allo stato del lettore. TVSDK fornisce un elenco cronologico di oggetti di notifica e ogni notifica contiene i metadati seguenti:

<table frame="all" colsep="1" rowsep="1" id="table_DBA8CACF02DB4AF2B053E560850B49CE"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Elemento </th> 
   <th colname="2" class="entry"> Descrizione </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> tipo </td> 
   <td colname="2"> Il tipo di notifica. A seconda della piattaforma, questa proprietà fa riferimento a un tipo enumerato con valori possibili di INFO, WARN o ERROR. Questo è il raggruppamento di primo livello per le notifiche. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> codice </td> 
   <td colname="2">La rappresentazione numerica assegnata alla notifica: 
    <ul id="ul_31AB497C6FFA452496DD09B0D78687B9"> 
     <li id="li_53E75022C50246E0982E315D04EFD8B3">Eventi di notifica degli errori, da 100000 a 199999 </li> 
     <li id="li_11AE91D1325E4F718228E662C9C55F9A">Eventi di notifica di avviso, da 200000 a 299999 </li> 
     <li id="li_6D3EA03845294DC2BAD1ACF507639E51">Eventi di notifica delle informazioni, da 300000 a 399999 </li> 
    </ul> <p>Ogni intervallo di primo livello, ad esempio gli errori, è diviso in sottointervalli, ad esempio da 101000 a 101999 che rappresentano gli errori di riproduzione. </p>
    <pre>
     Enumerazione 
     <span class="codeph"> mediacore.PSDKErrorCode</span> elenca i valori possibili.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> nome </td> 
   <td colname="2">Una stringa che contiene una descrizione leggibile del codice, ad esempio <span class="codeph"> SEEK_ERROR</span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> metadati </td> 
   <td colname="2">Coppie chiave/valore contenenti ulteriori informazioni rilevanti sulla notifica. Ad esempio, una chiave denominata <span class="codeph"> URL</span> verrebbe associata a un valore che sia un URL correlato alla notifica, ad esempio un URL non valido che ha causato un errore. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> innerNotification </td> 
   <td colname="2">Un riferimento a un altro <span class="codeph"> MediaPlayerNotification</span> oggetto che ha direttamente interessato la notifica. Un esempio potrebbe essere una notifica relativa a un errore di inserimento di annunci che corrisponde direttamente a un conflitto di inserimento della riga temporale. Non tutte le notifiche sono interne. </td> 
  </tr> 
 </tbody> 
</table>
