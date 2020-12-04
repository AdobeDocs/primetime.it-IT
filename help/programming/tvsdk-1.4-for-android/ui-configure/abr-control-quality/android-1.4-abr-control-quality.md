---
description: I flussi HLS e DASH forniscono codifiche di bitrate (profili) diverse per lo stesso breve spezzone di video. TVSDK può selezionare il livello di qualità per ogni burst in base alla larghezza di banda disponibile.
seo-description: I flussi HLS e DASH forniscono codifiche di bitrate (profili) diverse per lo stesso breve spezzone di video. TVSDK può selezionare il livello di qualità per ogni burst in base alla larghezza di banda disponibile.
seo-title: Bitrate adattivo (ABR) per la qualità video
title: Bitrate adattivo (ABR) per la qualità video
uuid: 1de26f34-4eac-4c9c-8f59-8c34d69a2d01
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

---


# Panoramica {#adaptive-bit-rates-abr-for-video-quality-overview}

I flussi HLS e DASH forniscono codifiche di bitrate (profili) diverse per lo stesso breve spezzone di video. TVSDK può selezionare il livello di qualità per ogni burst in base alla larghezza di banda disponibile.

TVSDK controlla costantemente il bitrate per garantire che il contenuto venga riprodotto al bitrate ottimale per la connessione di rete corrente.

Potete impostare i criteri di commutazione ABR (Bitrate adattivo) e i bitrate iniziali, minimi e massimi per un flusso a bit rate multiplo (MBR). TVSDK passa automaticamente al bitrate che offre la migliore esperienza di riproduzione nella configurazione specificata.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> Bitrate iniziale </td> 
   <td colname="col2"> <p>Bitrate di riproduzione desiderato (in bit al secondo) per il primo segmento. All’avvio della riproduzione, per il primo segmento viene utilizzato il profilo più vicino, pari o superiore al bitrate iniziale. </p> <p> Se viene definito un bitrate minimo e il bitrate iniziale è inferiore al bitrate minimo, TVSDK seleziona il profilo con il bitrate più basso al di sopra del bitrate minimo. Se la frequenza iniziale è superiore alla velocità massima, TVSDK seleziona la frequenza massima al di sotto della velocità massima. </p> <p>Se il bitrate iniziale è zero o undefined, il bitrate iniziale è determinato dal criterio ABR. </p> <p><span class="codeph"> </span> getABRIninitialBitRateretela un valore intero che rappresenta il profilo byte per secondo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Bitrate minimo </td> 
   <td colname="col2"> <p>Bitrate più basso consentito a cui può passare l'ABR. La commutazione ABR ignora i profili con un bitrate inferiore a tale bitrate. </p> <p><span class="codeph"> </span> getABRMinBitRateretra un valore intero che rappresenta il profilo bit per secondo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Bitrate massimo </td> 
   <td colname="col2"> <p>Bitrate massimo consentito a cui può passare l'ABR. La commutazione ABR ignora i profili con bitrate maggiore di questo valore. </p> <p><span class="codeph"> </span> getABRMaxBitRateretra un valore intero che rappresenta il profilo bit per secondo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Criteri di commutazione ABR </td> 
   <td colname="col2"> Quando possibile, la riproduzione passa gradualmente al profilo con bitrate più elevato. Puoi impostare il criterio per il passaggio ABR, che determina la velocità con cui TVSDK passa da un profilo all'altro. Il valore predefinito è <span class="codeph"> ABR_MODERATE</span>. <p>Quando TVSDK decide di passare a un bitrate più alto, il lettore seleziona il profilo di bitrate ideale a cui passare in base al criterio ABR corrente: 
     <ul id="ul_AC9C99D84A3B4A8DBD1A05CC05DEE771"> 
      <li id="li_B79C0AA2CBFB42FF98A257CEC9C400BA"><span class="codeph"> ABR_CONSERVATIVE</span>: Passa al profilo con bitrate successivo più elevato quando la larghezza di banda è superiore del 50% rispetto al bitrate corrente. </li> 
      <li id="li_38CC3A95D8634F359D0F7C273D0108C0"><span class="codeph"> ABR_MODERATE</span>: Passa al successivo profilo di bitrate più elevato quando la larghezza di banda è superiore del 20% rispetto al bitrate corrente. </li> 
      <li id="li_E845C035420D4B3FB2B179F448F8CA85"><span class="codeph"> ABR_AGGRESSIVE</span>: Passa immediatamente al profilo bitrate più alto quando la larghezza di banda è superiore al bitrate corrente. </li> 
     </ul> </p> <p>Se il bitrate iniziale è pari a zero o non è specificato, ma viene specificato un criterio, la riproduzione inizia con il profilo di bitrate più basso per gli utenti meno esperti, il profilo più vicino al bitrate medio dei profili disponibili per gli utenti meno esperti e il profilo di bitrate più alto per gli utenti meno esperti. </p> <p>Il criterio funziona nei limiti dei bitrate minimo e massimo, se questi valori vengono specificati. </p> <p><span class="codeph"> </span> getABRPolicyrestituisce l'impostazione corrente da  <span class="codeph"> </span> ABRControlParametersenum: 
     <ul id="ul_bd4_5kb_cz"> 
      <li id="li_E7C118AF48994454B7B3C016913DE545"><span class="codeph"> ABR_CONSERVATIVE</span> </li> 
      <li id="li_0A90BB42786449629CE7DD3364B385EE"><span class="codeph"> ABR_MODERATE</span> </li> 
      <li id="li_AFEB9B2862F24A369CA90596184A2883"><span class="codeph"> ABR_AGGRESSIVE</span> </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

Tenete presenti le seguenti informazioni:

* Il meccanismo di failover TVSDK potrebbe sovrascrivere le impostazioni, perché TVSDK favorisce un’esperienza di riproduzione continua in modo da rispettare rigorosamente i parametri di controllo.
* Quando il bitrate cambia, TVSDK invia eventi `onProfileChanged` in `PlaybackEventListener`.

* È possibile modificare le impostazioni ABR in qualsiasi momento, e il lettore utilizza il profilo che meglio corrisponde alle impostazioni più recenti.

Ad esempio, se un flusso ha i seguenti profili:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

Se specificate un intervallo da 300000 a 2000000, TVSDK considera solo i profili 1, 2 e 3. Questo consente alle applicazioni di adattarsi a varie condizioni di rete, come il passaggio da wi-fi a 3G o a vari dispositivi come un telefono, un tablet o un computer desktop.

Per impostare i parametri di controllo ABR, impostare i parametri sulla classe `ABRControlParameter`.
