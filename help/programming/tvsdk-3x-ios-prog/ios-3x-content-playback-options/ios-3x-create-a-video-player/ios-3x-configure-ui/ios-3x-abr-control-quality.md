---
description: I flussi HLS e DASH forniscono codifiche del bit rate (profili) diverse per lo stesso breve burst di video. TVSDK può selezionare il livello di qualità per ogni burst in base alla larghezza di banda disponibile.
title: Bit rate adattivi (ABR) per la qualità video
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---


# Bit rate adattivi (ABR) per qualità video {#adaptive-bit-rates-abr-for-video-quality}

I flussi HLS e DASH forniscono codifiche del bit rate (profili) diverse per lo stesso breve burst di video. TVSDK può selezionare il livello di qualità per ogni burst in base alla larghezza di banda disponibile.

TVSDK controlla costantemente il bit rate per garantire che il contenuto venga riprodotto al bit rate ottimale per la connessione di rete corrente.

È possibile impostare i criteri di commutazione del bit rate adattivo (ABR) e i bit rate iniziali, minimi e massimi per un flusso a bit rate multiplo (MBR). TVSDK passa automaticamente al bit rate che offre la migliore esperienza di riproduzione nella configurazione specificata.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> Bit rate iniziale </td> 
   <td colname="col2"> <p>Il bit rate di riproduzione desiderato (in bit al secondo) per il primo segmento. All’avvio della riproduzione, per il primo segmento viene utilizzato il profilo più vicino, che è uguale o maggiore del bit rate iniziale. </p> <p> Se viene definito un bit rate minimo e il bit rate iniziale è inferiore al bit rate minimo, TVSDK seleziona il profilo con il bit rate più basso al di sopra del bit rate minimo. Se la velocità iniziale è superiore alla velocità massima, TVSDK seleziona la velocità più elevata al di sotto della velocità massima. </p> <p>Se il bit rate iniziale è zero o non definito, il bit rate iniziale è determinato dal criterio ABR. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Bit rate minimo </td> 
   <td colname="col2"> <p>Il bit rate più basso consentito a cui può passare l'ABR. La commutazione ABR ignora i profili con un bit rate inferiore a questo bit rate. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Bit rate massimo </td> 
   <td colname="col2"> <p>Il bit rate più alto consentito a cui può passare l'ABR. La commutazione ABR ignora i profili con un bit rate più alto di questo bit rate. </p> </td> 
  </tr> 
 </tbody> 
</table>

Considera le seguenti informazioni:

* TVSDK non invia eventi dal passaggio a bit rate.
* È possibile modificare le impostazioni ABR in qualsiasi momento e il lettore passa a utilizzare il profilo che corrisponde maggiormente alle impostazioni più recenti.

Ad esempio, se un flusso ha i seguenti profili:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4. 2400000
* 5: 4000000

Se specifichi un intervallo da 300000 a 2000000, TVSDK considera solo i profili 1, 2 e 3. Questo consente alle applicazioni di adattarsi a varie condizioni di rete, come il passaggio da WiFi a 3G o a vari dispositivi come un telefono, un tablet o un computer desktop.

## Configurare i bit rate adattivi {#section_572FCE4CC28D4DF8BD9C461F00B3CA17}

Per configurare i parametri del bit rate adattivo TVSDK:

1. Configura un&#39;istanza di `PTABRControlParameters` per impostare le impostazioni del bit rate iniziale, minimo e massimo.

   I valori predefiniti vengono visualizzati nel seguente frammento di codice, ma l&#39;applicazione può impostare qualsiasi valore intero per ciascuno di questi parametri.

   >[!IMPORTANT]
   >
   >Specificare le impostazioni del bit rate in bit al secondo (bps).

   ```
   // ARC (add autorelease for non-ARC) 
   PTABRControlParameters *abrMetaData =  
       [[PTABRControlParameters alloc] init];  
   
   abrMetaData.initialBitRate = -1; 
   abrMetaData.minBitRate = 0; 
   abrMetaData.maxBitRate = INT_MAX;
   ```

1. Aggiorna l&#39;istanza `PTMediaPlayer` con l&#39;istanza `PTABRControlParameters` configurata.

   ```
   // assuming self.player is the PTMediaPlayer instance 
   self.player.abrControlParameters = abrMetaData;
   ```

Ricorda quanto segue:

* L&#39;applicazione deve impostare la proprietà `abrControlParameters` su `PTMediaPlayer` prima di configurare un&#39;istanza `PTMediaPlayerItem` affinché le impostazioni del bitrate iniziale e minima abbiano effetto.

   Dopo l’avvio della riproduzione del contenuto, l’impostazione di una nuova istanza influisce solo sull’impostazione del bitrate massimo.

* Per aggiornare l&#39;impostazione del bitrate massimo durante la riproduzione, crea una nuova istanza `PTABRControlParameters` e impostala sull&#39;istanza del lettore.
* È possibile aggiornare l&#39;impostazione del bitrate massimo durante la riproduzione solo su iOS 8.0 e versioni successive. Per le versioni precedenti, viene utilizzato il valore `maxBitrate` impostato prima dell’avvio della riproduzione del contenuto.