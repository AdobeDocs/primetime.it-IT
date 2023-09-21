---
description: I flussi HLS e DASH forniscono codifiche (profili) di bitrate diverse per lo stesso breve burst di video. Il browser TVSDK può selezionare il livello di qualità per ogni burst in base alla larghezza di banda disponibile.
title: Velocità bit adattive (ABR) per la qualità video
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 1%

---

# Panoramica {#adaptive-bit-rates-abr-for-video-quality-overview}

I flussi HLS e DASH forniscono codifiche (profili) di bitrate diverse per lo stesso breve burst di video. Il browser TVSDK può selezionare il livello di qualità per ogni burst in base alla larghezza di banda disponibile.

Browser TVSDK controlla costantemente il bit rate per garantire che il contenuto venga riprodotto al bit rate ottimale per la connessione di rete corrente.

È possibile impostare il criterio di commutazione ABR (Adaptive Bit Rate) e i bit rate iniziale, minimo e massimo per un flusso MBR (Multiple Bit Rate). Il browser TVSDK passa automaticamente al bitrate che offre la migliore esperienza di riproduzione nella configurazione specificata.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> Bitrate iniziale </td> 
   <td colname="col2">Velocità in bit di riproduzione desiderata (in bit al secondo) per il primo segmento. All’avvio della riproduzione, per il primo segmento viene utilizzato il profilo più vicino, corrispondente o superiore alla velocità in bit iniziale. <p> Se viene definita una velocità in bit minima e la velocità in bit iniziale è inferiore alla velocità in bit minima, il browser TVSDK seleziona il profilo con la velocità in bit più bassa al di sopra della velocità in bit minima. Se la frequenza iniziale è superiore alla frequenza massima, il TVSDK del browser seleziona la frequenza più alta al di sotto della frequenza massima. </p> <p>Se il bit rate iniziale è zero o non definito, il bit rate iniziale è determinato dalla policy ABR. </p> <p><span class="codeph"> initialBitRate</span> restituisce un valore intero che rappresenta il profilo byte al secondo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Velocità bit minima </td> 
   <td colname="col2">La velocità bit minima consentita alla quale l'ABR può passare. La commutazione ABR ignora i profili con una velocità di trasmissione inferiore a questa. <p><span class="codeph"> minBitRate</span> restituisce un valore intero che rappresenta il profilo bit al secondo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Velocità bit massima </td> 
   <td colname="col2">La velocità bit massima consentita alla quale l'ABR può passare. Quando si cambia ABR, vengono ignorati i profili con una velocità di trasmissione superiore a questa. <p><span class="codeph"> maxBitRate</span> restituisce un valore intero che rappresenta il profilo bit al secondo. </p> </td> 
  </tr> 
 </tbody> 
</table>

Considera le seguenti informazioni:

* Quando la velocità di trasmissione cambia, il browser TVSDK invia `AdobePSDK.ProfileEvent` con il tipo come `AdobePSDK.PSDKEventType.PROFILE_CHANGED`.

* È possibile modificare le impostazioni ABR in qualsiasi momento e il lettore passa all&#39;uso del profilo che corrisponde maggiormente alle impostazioni più recenti.

Ad esempio, se un flusso ha i seguenti profili:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

Se specifichi un intervallo di 300000 da 2000000, TVSDK per browser considera solo i profili 1, 2 e 3. Questo consente alle applicazioni di adattarsi a varie condizioni di rete, ad esempio passare dal wi-fi al 3G o a vari dispositivi, come un telefono, un tablet o un computer desktop.

Per impostare i parametri di controllo ABR:

* Impostare i parametri su `ABRControlParameters` classe.
