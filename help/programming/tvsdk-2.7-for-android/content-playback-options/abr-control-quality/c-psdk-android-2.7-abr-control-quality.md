---
description: I flussi HLS e DASH forniscono codifiche di bitrate (profili) diverse per lo stesso breve spezzone di video. TVSDK può selezionare il livello di qualità per ogni burst in base al livello di buffer corrente e alla larghezza di banda disponibile.
seo-description: I flussi HLS e DASH forniscono codifiche di bitrate (profili) diverse per lo stesso breve spezzone di video. TVSDK può selezionare il livello di qualità per ogni burst in base al livello di buffer corrente e alla larghezza di banda disponibile.
seo-title: Bitrate adattivo (ABR) per la qualità video
title: Bitrate adattivo (ABR) per la qualità video
uuid: d41c3edf-33c7-4616-820f-22303d578df0
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Panoramica {#adaptive-bit-rates-abr-for-video-quality-overview}

I flussi HLS e DASH forniscono codifiche di bitrate (profili) diverse per lo stesso breve spezzone di video. TVSDK può selezionare il livello di qualità per ogni burst in base al livello di buffer corrente e alla larghezza di banda disponibile.

TVSDK controlla costantemente il bitrate per garantire che il contenuto venga riprodotto al bitrate ottimale per la connessione di rete corrente. Potete impostare i criteri di commutazione ABR (Adaptive Bitrate) e i bitrate iniziali, minimi e massimi per un flusso a più bit rate (MBR). TVSDK passa automaticamente al bitrate che offre la migliore esperienza di riproduzione nella configurazione specificata.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> Bitrate iniziale </td> 
   <td colname="col2"> <p>Bitrate di riproduzione desiderato (in bit al secondo) per il primo segmento. </p> <p>All’avvio della riproduzione, per il primo segmento viene utilizzato il profilo più vicino, pari o superiore al bitrate iniziale. Se viene definito un bitrate minimo e il bitrate iniziale è inferiore al bitrate minimo, TVSDK seleziona il profilo con il bitrate più basso al di sopra del bitrate minimo. Se la frequenza iniziale è superiore alla velocità massima, TVSDK seleziona la frequenza massima al di sotto della velocità massima. Se il bitrate iniziale è zero o undefined, il bitrate iniziale è determinato dal criterio ABR. </p> <p><span class="codeph"> getABRIninitialBitRate</span> restituisce un valore intero che rappresenta il profilo byte per secondo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Bitrate minimo </td> 
   <td colname="col2"> <p>Bitrate più basso consentito a cui può passare l'ABR. </p> <p>La commutazione ABR ignora i profili con un bitrate inferiore a tale bitrate. <span class="codeph"> getABRMinBitRate</span> restituisce un valore intero che rappresenta il profilo bit per secondo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Bitrate massimo </td> 
   <td colname="col2"> <p>Bitrate massimo consentito a cui può passare l'ABR. </p> <p>La commutazione ABR ignora i profili con bitrate maggiore di questo valore. <span class="codeph"> getABRMaxBitRate</span> restituisce un valore intero che rappresenta il profilo bit per secondo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Criteri di commutazione ABR </td> 
   <td colname="col2"> <p>Quando possibile, la riproduzione passa gradualmente al profilo con bitrate più elevato. Puoi impostare il criterio per il passaggio ABR, che determina la velocità con cui TVSDK passa da un profilo all'altro. Il valore predefinito è <span class="codeph"> ABR_MODERATE</span>. </p> <p>Quando TVSDK decide di passare a un bitrate più elevato, il lettore seleziona il profilo di bitrate ideale a cui passare in base al criterio ABR corrente: 
     <ul id="ul_AC9C99D84A3B4A8DBD1A05CC05DEE771"> 
      <li id="li_B79C0AA2CBFB42FF98A257CEC9C400BA"><span class="codeph"> ABR_CONSERVATIVE</span>: Passa al profilo con bitrate successivo più elevato quando la larghezza di banda è superiore del 50% rispetto al bitrate corrente. </li> 
      <li id="li_38CC3A95D8634F359D0F7C273D0108C0"><span class="codeph"> ABR_MODERATE</span>: Passa al successivo profilo di bitrate più elevato quando la larghezza di banda è superiore del 20% rispetto al bitrate corrente. </li> 
      <li id="li_E845C035420D4B3FB2B179F448F8CA85"><span class="codeph"> ABR_AGGRESSIVE</span>: Passa immediatamente al profilo bitrate più alto quando la larghezza di banda è superiore al bitrate corrente. </li> 
     </ul> </p> <p>Se il bitrate iniziale è zero o non è specificato ma viene specificato un criterio, la riproduzione inizia con il profilo di bitrate più basso per un criterio conservativo, il profilo più vicino al bitrate medio dei profili disponibili per un criterio moderato e il profilo di bitrate più alto per un criterio aggressivo. </p> <p>Il criterio funziona nei limiti dei bitrate minimo e massimo, se questi valori vengono specificati. </p> <p> <span class="codeph"> getABRPolicy</span> restituisce l’impostazione corrente dall’enum <span class="codeph"> ABRControlParameters</span> : <span class="codeph"> ABR_CONSERVATIVE</span>, <span class="codeph"> ABR_MODERATE</span>o <span class="codeph"> ABR_AGGRESSIVE</span>. </p> <p>Per ulteriori informazioni, consultate il documento API ABRControlParameters.</p> </td> 
  </tr> 
 </tbody> 
</table>

Tenete presenti le seguenti informazioni:

* Il meccanismo di failover TVSDK potrebbe sovrascrivere le impostazioni, perché TVSDK favorisce un’esperienza di riproduzione continua in modo da rispettare rigorosamente i parametri di controllo.
* Quando il bitrate cambia, TVSDK invia `onProfileChanged` eventi in `PlaybackEventListener`.

* È possibile modificare le impostazioni ABR in qualsiasi momento, e il lettore utilizza il profilo che meglio corrisponde alle impostazioni più recenti.

Ad esempio, se un flusso ha i seguenti profili:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

Se specificate un intervallo da 300000 a 2000000, TVSDK considera solo i profili 1, 2 e 3. Questo consente alle applicazioni di adattarsi a varie condizioni di rete, come il passaggio da wi-fi a 3G o a vari dispositivi come un telefono, un tablet o un computer desktop.

Per impostare i parametri di controllo ABR, impostate i parametri sulla `ABRControlParameter` classe.
