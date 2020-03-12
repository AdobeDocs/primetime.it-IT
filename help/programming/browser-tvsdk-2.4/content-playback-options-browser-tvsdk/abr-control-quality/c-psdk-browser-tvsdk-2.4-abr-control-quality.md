---
description: I flussi HLS e DASH forniscono codifiche di bitrate (profili) diverse per lo stesso breve spezzone di video. Browser TVSDK può selezionare il livello di qualità per ogni burst in base alla larghezza di banda disponibile.
seo-description: I flussi HLS e DASH forniscono codifiche di bitrate (profili) diverse per lo stesso breve spezzone di video. Browser TVSDK può selezionare il livello di qualità per ogni burst in base alla larghezza di banda disponibile.
seo-title: Bitrate adattivo (ABR) per la qualità video
title: Bitrate adattivo (ABR) per la qualità video
uuid: 4c34fb7b-1bbd-4fa9-8929-d50e85a17396
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Panoramica {#adaptive-bit-rates-abr-for-video-quality-overview}

I flussi HLS e DASH forniscono codifiche di bitrate (profili) diverse per lo stesso breve spezzone di video. Browser TVSDK può selezionare il livello di qualità per ogni burst in base alla larghezza di banda disponibile.

Browser TVSDK controlla costantemente il bitrate per garantire che il contenuto venga riprodotto al bitrate ottimale per la connessione di rete corrente.

Potete impostare i criteri di commutazione ABR (Bitrate adattivo) e i bitrate iniziali, minimi e massimi per un flusso a bit rate multiplo (MBR). Browser TVSDK passa automaticamente al bitrate che offre la migliore esperienza di riproduzione nella configurazione specificata.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> Bitrate iniziale </td> 
   <td colname="col2">Bitrate di riproduzione desiderato (in bit al secondo) per il primo segmento. All’avvio della riproduzione, per il primo segmento viene utilizzato il profilo più vicino, pari o superiore al bitrate iniziale. <p> Se viene definito un bitrate minimo e il bitrate iniziale è inferiore al bitrate minimo, Browser TVSDK seleziona il profilo con il bitrate più basso al di sopra del bitrate minimo. Se la frequenza iniziale è superiore alla velocità massima, Browser TVSDK seleziona la frequenza massima al di sotto della velocità massima. </p> <p>Se il bitrate iniziale è zero o undefined, il bitrate iniziale è determinato dal criterio ABR. </p> <p><span class="codeph"> initialBitRate</span> restituisce un valore intero che rappresenta il profilo byte per secondo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Bitrate minimo </td> 
   <td colname="col2">Bitrate più basso consentito a cui può passare l'ABR. La commutazione ABR ignora i profili con un bitrate inferiore a tale bitrate. <p><span class="codeph"> minBitRate</span> restituisce un valore intero che rappresenta il profilo bit per secondo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Bitrate massimo </td> 
   <td colname="col2">Bitrate massimo consentito a cui può passare l'ABR. La commutazione ABR ignora i profili con bitrate maggiore di questo valore. <p><span class="codeph"> maxBitRate</span> restituisce un valore intero che rappresenta il profilo bit per secondo. </p> </td> 
  </tr> 
 </tbody> 
</table>

Tenete presenti le seguenti informazioni:

* Quando il bitrate cambia, Browser TVSDK invia `AdobePSDK.ProfileEvent` con il tipo `AdobePSDK.PSDKEventType.PROFILE_CHANGED`.

* È possibile modificare le impostazioni ABR in qualsiasi momento, e il lettore utilizza il profilo che meglio corrisponde alle impostazioni più recenti.

Ad esempio, se un flusso ha i seguenti profili:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

Se specificate un intervallo da 300000 a 2000000, l’SDK per browser considera solo i profili 1, 2 e 3. Questo consente alle applicazioni di adattarsi a varie condizioni di rete, come il passaggio da wi-fi a 3G o a vari dispositivi come un telefono, un tablet o un computer desktop.

Per impostare i parametri di controllo ABR:

* Impostate i parametri sulla `ABRControlParameters` classe.

