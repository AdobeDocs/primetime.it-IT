---
description: I flussi HLS e DASH forniscono codifiche (profili) di bitrate diverse per lo stesso breve burst di video. TVSDK può selezionare il livello di qualità per ogni burst in base alla larghezza di banda disponibile.
title: Velocità bit adattive (ABR) per la qualità video
exl-id: dd6d091a-58c9-4825-8c2c-a1257ef37f22
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# Velocità bit adattive (ABR) per la qualità video{#adaptive-bit-rates-abr-for-video-quality}

I flussi HLS e DASH forniscono codifiche (profili) di bitrate diverse per lo stesso breve burst di video. TVSDK può selezionare il livello di qualità per ogni burst in base alla larghezza di banda disponibile.

TVSDK controlla costantemente il bit rate per garantire che il contenuto venga riprodotto al bit rate ottimale per la connessione di rete corrente.

È possibile impostare il criterio di commutazione ABR (Adaptive Bit Rate) e i bit rate iniziale, minimo e massimo per un flusso MBR (Multiple Bit Rate). TVSDK passa automaticamente al bitrate che offre la migliore esperienza di riproduzione nella configurazione specificata.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> Bitrate iniziale </td> 
   <td colname="col2"> <p>Velocità in bit di riproduzione desiderata (in bit al secondo) per il primo segmento. All’avvio della riproduzione, per il primo segmento viene utilizzato il profilo più vicino, corrispondente o superiore alla velocità in bit iniziale. </p> <p> Se viene definita una velocità in bit minima e la velocità in bit iniziale è inferiore alla velocità in bit minima, TVSDK seleziona il profilo con la velocità in bit più bassa al di sopra della velocità in bit minima. Se il tasso iniziale è superiore al tasso massimo, TVSDK seleziona il tasso più alto al di sotto del tasso massimo. </p> <p>Se il bit rate iniziale è zero o non definito, il bit rate iniziale è determinato dalla policy ABR. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Velocità bit minima </td> 
   <td colname="col2"> <p>La velocità bit minima consentita alla quale l'ABR può passare. La commutazione ABR ignora i profili con una velocità di trasmissione inferiore a questa. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Velocità bit massima </td> 
   <td colname="col2"> <p>La velocità bit massima consentita alla quale l'ABR può passare. Quando si cambia ABR, vengono ignorati i profili con una velocità di trasmissione superiore a questa. </p> </td> 
  </tr> 
 </tbody> 
</table>

Considera le seguenti informazioni:

* TVSDK non invia eventi dalla commutazione del bit-rate.
* È possibile modificare le impostazioni ABR in qualsiasi momento e il lettore passa all&#39;uso del profilo che corrisponde maggiormente alle impostazioni più recenti.

Ad esempio, se un flusso ha i seguenti profili:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

Se specifichi un intervallo di 300000 da 2000000, TVSDK considera solo i profili 1, 2 e 3. Ciò consente alle applicazioni di adattarsi a varie condizioni di rete, ad esempio passare da WiFi a 3G o a vari dispositivi come un telefono, un tablet o un computer desktop.

## Configurare velocità bit adattive {#section_572FCE4CC28D4DF8BD9C461F00B3CA17}

Per configurare i parametri del bitrate adattivo TVSDK:

1. Configurare un’istanza di `PTABRControlParameters` per impostare la velocità di trasmissione iniziale, minima e massima.

   I valori predefiniti vengono visualizzati nel seguente frammento di codice, ma l&#39;applicazione può impostare qualsiasi valore intero per ciascuno di questi parametri.

   >[!IMPORTANT]
   >
   >Specificare le impostazioni della velocità in bit al secondo (bps).

   ```
   // ARC (add autorelease for non-ARC) 
   PTABRControlParameters *abrMetaData =  
       [[PTABRControlParameters alloc] init];  
   
   abrMetaData.initialBitRate = -1; 
   abrMetaData.minBitRate = 0; 
   abrMetaData.maxBitRate = INT_MAX;
   ```

1. Aggiorna il tuo `PTMediaPlayer` con configurato `PTABRControlParameters` dell&#39;istanza.

   ```
   // assuming self.player is the PTMediaPlayer instance 
   self.player.abrControlParameters = abrMetaData;
   ```

Tenere presente quanto segue:

* L&#39;applicazione deve impostare `abrControlParameters` proprietà su `PTMediaPlayer` prima di configurare un `PTMediaPlayerItem` per rendere effettive le impostazioni iniziali e minime del bitrate.

   Dopo l’avvio della riproduzione del contenuto, l’impostazione di una nuova istanza influisce solo sull’impostazione del bitrate massimo.

* Per aggiornare l&#39;impostazione del bitrate massimo durante la riproduzione, creare un nuovo `PTABRControlParameters` e impostarla sull’istanza del lettore.
* È possibile aggiornare l’impostazione del bitrate massimo durante la riproduzione solo su iOS 8.0 e versioni successive. Per le versioni precedenti, il `maxBitrate` valore impostato prima dell’avvio della riproduzione del contenuto.
