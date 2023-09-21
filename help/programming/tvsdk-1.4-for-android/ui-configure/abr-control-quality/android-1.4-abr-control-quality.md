---
description: I flussi HLS e DASH forniscono codifiche (profili) di bitrate diverse per lo stesso breve burst di video. TVSDK può selezionare il livello di qualità per ogni burst in base alla larghezza di banda disponibile.
title: Velocità bit adattive (ABR) per la qualità video
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# Panoramica {#adaptive-bit-rates-abr-for-video-quality-overview}

I flussi HLS e DASH forniscono codifiche (profili) di bitrate diverse per lo stesso breve burst di video. TVSDK può selezionare il livello di qualità per ogni burst in base alla larghezza di banda disponibile.

TVSDK controlla costantemente il bit rate per garantire che il contenuto venga riprodotto al bit rate ottimale per la connessione di rete corrente.

È possibile impostare il criterio di commutazione ABR (Adaptive Bit Rate) e i bit rate iniziale, minimo e massimo per un flusso MBR (Multiple Bit Rate). TVSDK passa automaticamente al bitrate che offre la migliore esperienza di riproduzione nella configurazione specificata.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> Bitrate iniziale </td> 
   <td colname="col2"> <p>Velocità in bit di riproduzione desiderata (in bit al secondo) per il primo segmento. All’avvio della riproduzione, per il primo segmento viene utilizzato il profilo più vicino, corrispondente o superiore alla velocità in bit iniziale. </p> <p> Se viene definita una velocità in bit minima e la velocità in bit iniziale è inferiore alla velocità in bit minima, TVSDK seleziona il profilo con la velocità in bit più bassa al di sopra della velocità in bit minima. Se il tasso iniziale è superiore al tasso massimo, TVSDK seleziona il tasso più alto al di sotto del tasso massimo. </p> <p>Se il bit rate iniziale è zero o non definito, il bit rate iniziale è determinato dalla policy ABR. </p> <p><span class="codeph"> getABRInitialBitRate</span> restituisce un valore intero che rappresenta il profilo byte al secondo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Velocità bit minima </td> 
   <td colname="col2"> <p>La velocità bit minima consentita alla quale l'ABR può passare. La commutazione ABR ignora i profili con una velocità di trasmissione inferiore a questa. </p> <p><span class="codeph"> getABRMinBitRate</span> restituisce un valore intero che rappresenta il profilo bit al secondo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Velocità bit massima </td> 
   <td colname="col2"> <p>La velocità bit massima consentita alla quale l'ABR può passare. Quando si cambia ABR, vengono ignorati i profili con una velocità di trasmissione superiore a questa. </p> <p><span class="codeph"> getABRMaxBitRate</span> restituisce un valore intero che rappresenta il profilo bit al secondo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Criteri di cambio ABR </td> 
   <td colname="col2"> Quando possibile, la riproduzione passa gradualmente al profilo con il bit rate più alto. È possibile impostare il criterio per il passaggio ABR, che determina la velocità con cui TVSDK passa da un profilo all’altro. Il valore predefinito è <span class="codeph"> ABR_MODERATE</span>. <p>Quando TVSDK decide di passare a una velocità bit più alta, il lettore seleziona il profilo della velocità bit ideale su cui passare in base alla policy ABR corrente: 
     <ul id="ul_AC9C99D84A3B4A8DBD1A05CC05DEE771"> 
      <li id="li_B79C0AA2CBFB42FF98A257CEC9C400BA"><span class="codeph"> ABR_CONSERVATIVE</span>: passa al profilo con la velocità in bit successiva più elevata quando la larghezza di banda è del 50% superiore alla velocità in bit corrente. </li> 
      <li id="li_38CC3A95D8634F359D0F7C273D0108C0"><span class="codeph"> ABR_MODERATE</span>: passa al profilo con velocità in bit successiva più elevata quando la larghezza di banda è del 20% superiore alla velocità in bit corrente. </li> 
      <li id="li_E845C035420D4B3FB2B179F448F8CA85"><span class="codeph"> ABR_AGGRESSIVO</span>: passa immediatamente al profilo del bit rate più alto quando la larghezza di banda è superiore al bit rate corrente. </li> 
     </ul> </p> <p>Se il bitrate iniziale è zero o non è specificato, ma è specificato un criterio, la riproduzione inizia con il profilo di bitrate più basso per conservativo, il profilo più vicino al bitrate mediano dei profili disponibili per moderato e il profilo di bitrate più alto per aggressivo. </p> <p>Se specificate, le velocità bit minima e massima funzionano in modo limitato. </p> <p><span class="codeph"> getABRPolicy</span> restituisce l'impostazione corrente dalla <span class="codeph"> ABRControlParameters</span> enum: 
     <ul id="ul_bd4_5kb_cz"> 
      <li id="li_E7C118AF48994454B7B3C016913DE545"><span class="codeph"> ABR_CONSERVATIVE</span> </li> 
      <li id="li_0A90BB42786449629CE7DD3364B385EE"><span class="codeph"> ABR_MODERATE</span> </li> 
      <li id="li_AFEB9B2862F24A369CA90596184A2883"><span class="codeph"> ABR_AGGRESSIVO</span> </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

Considera le seguenti informazioni:

* Il meccanismo di failover di TVSDK potrebbe ignorare le impostazioni, perché TVSDK favorisce un’esperienza di riproduzione continua rispetto all’aderenza rigorosa ai parametri di controllo.
* Quando la velocità di trasmissione cambia, TVSDK invia `onProfileChanged` eventi in `PlaybackEventListener`.

* È possibile modificare le impostazioni ABR in qualsiasi momento e il lettore passa all&#39;uso del profilo che corrisponde maggiormente alle impostazioni più recenti.

Ad esempio, se un flusso ha i seguenti profili:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

Se specifichi un intervallo di 300000 da 2000000, TVSDK considera solo i profili 1, 2 e 3. Questo consente alle applicazioni di adattarsi a varie condizioni di rete, ad esempio passare dal wi-fi al 3G o a vari dispositivi, come un telefono, un tablet o un computer desktop.

Per impostare i parametri di controllo ABR, impostate i parametri su `ABRControlParameter` classe.
