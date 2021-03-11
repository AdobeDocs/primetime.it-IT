---
description: I flussi HLS e DASH forniscono codifiche del bit rate (profili) diverse per lo stesso breve burst di video. Browser TVSDK può selezionare il livello di qualità per ogni burst in base alla larghezza di banda disponibile.
title: Bit rate adattivi (ABR) per la qualità video
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 1%

---


# Panoramica {#adaptive-bit-rates-abr-for-video-quality-overview}

I flussi HLS e DASH forniscono codifiche del bit rate (profili) diverse per lo stesso breve burst di video. Browser TVSDK può selezionare il livello di qualità per ogni burst in base alla larghezza di banda disponibile.

Browser TVSDK controlla costantemente il bit rate per garantire che il contenuto venga riprodotto al bit rate ottimale per la connessione di rete corrente.

È possibile impostare i criteri di commutazione del bit rate adattivo (ABR) e i bit rate iniziali, minimi e massimi per un flusso a bit rate multiplo (MBR). Il browser TVSDK passa automaticamente al bit rate che offre la migliore esperienza di riproduzione nella configurazione specificata.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> Bit rate iniziale </td> 
   <td colname="col2">Il bit rate di riproduzione desiderato (in bit al secondo) per il primo segmento. All’avvio della riproduzione, per il primo segmento viene utilizzato il profilo più vicino, che è uguale o maggiore del bit rate iniziale. <p> Se viene definito un bit rate minimo e il bit rate iniziale è inferiore alla velocità minima, il browser TVSDK seleziona il profilo con il bit rate più basso al di sopra del bit rate minimo. Se la velocità iniziale è superiore alla velocità massima, Browser TVSDK seleziona la velocità più alta al di sotto della velocità massima. </p> <p>Se il bit rate iniziale è zero o non definito, il bit rate iniziale è determinato dal criterio ABR. </p> <p><span class="codeph"> </span> initialBitRateretura un valore intero che rappresenta il profilo byte per secondo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Bit rate minimo </td> 
   <td colname="col2">Il bit rate più basso consentito a cui può passare l'ABR. La commutazione ABR ignora i profili con un bit rate inferiore a questo bit rate. <p><span class="codeph"> </span> minBitRateretura un valore intero che rappresenta i bit al secondo del profilo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Bit rate massimo </td> 
   <td colname="col2">Il bit rate più alto consentito a cui può passare l'ABR. La commutazione ABR ignora i profili con un bit rate più alto di questo bit rate. <p><span class="codeph"> </span> maxBitRateretura un valore intero che rappresenta i bit al secondo del profilo. </p> </td> 
  </tr> 
 </tbody> 
</table>

Considera le seguenti informazioni:

* Quando il bit rate cambia, il browser TVSDK invia `AdobePSDK.ProfileEvent` con il tipo `AdobePSDK.PSDKEventType.PROFILE_CHANGED`.

* È possibile modificare le impostazioni ABR in qualsiasi momento e il lettore passa a utilizzare il profilo che corrisponde maggiormente alle impostazioni più recenti.

Ad esempio, se un flusso ha i seguenti profili:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4. 2400000
* 5: 4000000

Se specifichi un intervallo da 300000 a 2000000, il browser TVSDK considera solo i profili 1, 2 e 3. Questo consente alle applicazioni di adattarsi a varie condizioni di rete, come il passaggio da wi-fi a 3G o a vari dispositivi come un telefono, un tablet o un computer desktop.

Per impostare i parametri di controllo ABR:

* Imposta i parametri sulla classe `ABRControlParameters` .

