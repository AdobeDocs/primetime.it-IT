---
description: I flussi HLS e DASH forniscono codifiche di bitrate (profili) diverse per lo stesso breve spezzone di video. TVSDK può selezionare il livello di qualità per ogni burst in base alla larghezza di banda disponibile.
seo-description: I flussi HLS e DASH forniscono codifiche di bitrate (profili) diverse per lo stesso breve spezzone di video. TVSDK può selezionare il livello di qualità per ogni burst in base alla larghezza di banda disponibile.
seo-title: Bitrate adattivo (ABR) per la qualità video
title: Bitrate adattivo (ABR) per la qualità video
uuid: e5752d7e-fa7d-407c-96df-c3830a35c66e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---


# Bitrate adattivo (ABR) per qualità video{#adaptive-bit-rates-abr-for-video-quality}

I flussi HLS e DASH forniscono codifiche di bitrate (profili) diverse per lo stesso breve spezzone di video. TVSDK può selezionare il livello di qualità per ogni burst in base alla larghezza di banda disponibile.

TVSDK controlla costantemente il bitrate per garantire che il contenuto venga riprodotto al bitrate ottimale per la connessione di rete corrente.

Potete impostare i criteri di commutazione ABR (Bitrate adattivo) e i bitrate iniziali, minimi e massimi per un flusso a bit rate multiplo (MBR). TVSDK passa automaticamente al bitrate che offre la migliore esperienza di riproduzione nella configurazione specificata.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> Bitrate iniziale </td> 
   <td colname="col2"> <p>Bitrate di riproduzione desiderato (in bit al secondo) per il primo segmento. All’avvio della riproduzione, per il primo segmento viene utilizzato il profilo più vicino, pari o superiore al bitrate iniziale. </p> <p> Se viene definito un bitrate minimo e il bitrate iniziale è inferiore al bitrate minimo, TVSDK seleziona il profilo con il bitrate più basso al di sopra del bitrate minimo. Se la frequenza iniziale è superiore alla velocità massima, TVSDK seleziona la frequenza massima al di sotto della velocità massima. </p> <p>Se il bitrate iniziale è zero o undefined, il bitrate iniziale è determinato dal criterio ABR. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Bitrate minimo </td> 
   <td colname="col2"> <p>Bitrate più basso consentito a cui può passare l'ABR. La commutazione ABR ignora i profili con un bitrate inferiore a tale bitrate. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Bitrate massimo </td> 
   <td colname="col2"> <p>Bitrate massimo consentito a cui può passare l'ABR. La commutazione ABR ignora i profili con bitrate maggiore di questo valore. </p> </td> 
  </tr> 
 </tbody> 
</table>

Tenete presenti le seguenti informazioni:

* TVSDK non invia eventi dal cambio di bitrate.
* È possibile modificare le impostazioni ABR in qualsiasi momento, e il lettore utilizza il profilo che meglio corrisponde alle impostazioni più recenti.

Ad esempio, se un flusso ha i seguenti profili:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

Se specificate un intervallo da 300000 a 2000000, TVSDK considera solo i profili 1, 2 e 3. Questo consente alle applicazioni di adattarsi a varie condizioni di rete, come il passaggio dal WiFi al 3G o a vari dispositivi come un telefono, un tablet o un computer desktop.

## Configurare i bitrate adattivi {#section_572FCE4CC28D4DF8BD9C461F00B3CA17}

Per configurare i parametri di bitrate adattivo TVSDK:

1. Configurate un&#39;istanza di `PTABRControlParameters` per impostare il bitrate iniziale, minimo e massimo.

   I valori predefiniti sono visualizzati nello snippet di codice seguente, ma l&#39;applicazione può impostare qualsiasi valore intero per ciascuno di questi parametri.

   >[!IMPORTANT]
   >
   >Specificate le impostazioni del bitrate in bit al secondo (bps).

   ```
   // ARC (add autorelease for non-ARC) 
   PTABRControlParameters *abrMetaData =  
       [[PTABRControlParameters alloc] init];  
   
   abrMetaData.initialBitRate = -1; 
   abrMetaData.minBitRate = 0; 
   abrMetaData.maxBitRate = INT_MAX;
   ```

1. Aggiornate l&#39;istanza `PTMediaPlayer` con l&#39;istanza `PTABRControlParameters` configurata.

   ```
   // assuming self.player is the PTMediaPlayer instance 
   self.player.abrControlParameters = abrMetaData;
   ```

Ricorda quanto segue:

* L&#39;applicazione deve impostare la proprietà `abrControlParameters` su `PTMediaPlayer` prima di configurare un&#39;istanza `PTMediaPlayerItem` affinché le impostazioni del bitrate iniziale e minima abbiano effetto.

   Dopo l’avvio della riproduzione del contenuto, l’impostazione di una nuova istanza influisce solo sull’impostazione del bitrate massimo.

* Per aggiornare l&#39;impostazione del bitrate massimo durante la riproduzione, create una nuova istanza `PTABRControlParameters` e impostatela sull&#39;istanza del lettore.
* Potete aggiornare l&#39;impostazione del bitrate massimo durante la riproduzione solo su iOS 8.0 e versioni successive. Per le versioni precedenti, viene utilizzato il valore `maxBitrate` impostato prima dell&#39;avvio della riproduzione del contenuto.

