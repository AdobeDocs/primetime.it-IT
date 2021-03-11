---
description: I flussi HLS e DASH forniscono codifiche del bit rate (profili) diverse per lo stesso breve burst di video. TVSDK può selezionare il livello di qualità per ogni burst in base al livello di buffering corrente e alla larghezza di banda disponibile.
title: Bit rate adattivi (ABR) per la qualità video
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 0%

---


# Panoramica {#adaptive-bit-rates-abr-for-video-quality-overview}

I flussi HLS e DASH forniscono codifiche del bit rate (profili) diverse per lo stesso breve burst di video. TVSDK può selezionare il livello di qualità per ogni burst in base al livello di buffering corrente e alla larghezza di banda disponibile.

TVSDK controlla costantemente il bit rate per garantire che il contenuto venga riprodotto al bit rate ottimale per la connessione di rete corrente. È possibile impostare i criteri di commutazione del bit rate adattivo (ABR) e i bit rate iniziali, minimi e massimi per un flusso a bit rate multiplo (MBR). TVSDK passa automaticamente al bit rate che offre la migliore esperienza di riproduzione nella configurazione specificata.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> Bit rate iniziale </td> 
   <td colname="col2"> <p>Il bit rate di riproduzione desiderato (in bit al secondo) per il primo segmento. </p> <p>All’avvio della riproduzione, per il primo segmento viene utilizzato il profilo più vicino, che è uguale o maggiore del bit rate iniziale. Se viene definito un bit rate minimo e il bit rate iniziale è inferiore al bit rate minimo, TVSDK seleziona il profilo con il bit rate più basso al di sopra del bit rate minimo. Se la velocità iniziale è superiore alla velocità massima, TVSDK seleziona la velocità più elevata al di sotto della velocità massima. Se il bit rate iniziale è zero o non definito, il bit rate iniziale è determinato dal criterio ABR. </p> <p><span class="codeph"> </span> getABRInitialBitRate restituisce un valore intero che rappresenta il profilo byte per secondo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Bit rate minimo </td> 
   <td colname="col2"> <p>Il bit rate più basso consentito a cui può passare l'ABR. </p> <p>La commutazione ABR ignora i profili con un bit rate inferiore a questo bit rate. <span class="codeph"> </span> getABRMinBitRate restituisce un valore intero che rappresenta i bit per secondo del profilo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Bit rate massimo </td> 
   <td colname="col2"> <p>Il bit rate più alto consentito a cui può passare l'ABR. </p> <p>La commutazione ABR ignora i profili con un bit rate più alto di questo bit rate. <span class="codeph"> </span> getABRMaxBitRateretura un valore intero che rappresenta i bit per secondo del profilo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Criteri di commutazione ABR </td> 
   <td colname="col2"> <p>Quando possibile, la riproduzione passa gradualmente al profilo a bit rate più elevato. È possibile impostare i criteri per il passaggio all’ABR, che determina la velocità con cui TVSDK passa da un profilo all’altro. Il valore predefinito è <span class="codeph"> ABR_MODERATE</span>. </p> <p>Quando TVSDK decide di passare a un bit rate più alto, il lettore seleziona il profilo di bit rate ideale a cui passare in base alla politica ABR corrente: 
     <ul id="ul_AC9C99D84A3B4A8DBD1A05CC05DEE771"> 
      <li id="li_B79C0AA2CBFB42FF98A257CEC9C400BA"><span class="codeph"> ABR_CONSERVATIVE</span>: Passa al profilo con il bit rate successivo più alto quando la larghezza di banda è superiore del 50% rispetto al bit rate corrente. </li> 
      <li id="li_38CC3A95D8634F359D0F7C273D0108C0"><span class="codeph"> ABR_MODERATE</span>: Passa al successivo profilo di bit rate più alto quando la larghezza di banda è superiore del 20% rispetto al bit rate corrente. </li> 
      <li id="li_E845C035420D4B3FB2B179F448F8CA85"><span class="codeph"> ABR_AGGRESSIVE</span>: Passa immediatamente al profilo a bit rate più alto quando la larghezza di banda è superiore al bit rate corrente. </li> 
     </ul> </p> <p>Se il bit rate iniziale è pari a zero o non è specificato ma è specificato un criterio, la riproduzione inizia con il profilo di bit rate più basso per un criterio conservativo, il profilo più vicino al bit rate mediano dei profili disponibili per un criterio moderato e il profilo di bit rate più alto per un criterio aggressivo. </p> <p>Il criterio funziona nei vincoli dei bit rate minimo e massimo, se questi tassi sono specificati. </p> <p> <span class="codeph"> </span> getABRPolicyrestituisce l'impostazione corrente da  <span class="codeph"> </span> ABRControlParameterSenum:  <span class="codeph"> ABR_CONSERVATIVE</span>,  <span class="codeph"> ABR_MODERATE</span> o  <span class="codeph"> ABR_AGGRESSIVE</span>. </p> <p>Per ulteriori informazioni, consulta la documentazione API dei parametri di controllo ABR . </p> </td> 
  </tr> 
 </tbody> 
</table>

Considera le seguenti informazioni:

* Il meccanismo di failover TVSDK potrebbe sostituire le impostazioni, perché TVSDK favorisce un’esperienza di riproduzione continua rispetto ai parametri di controllo.
* Quando il bit rate cambia, TVSDK invia eventi `onProfileChanged` in `PlaybackEventListener`.

* È possibile modificare le impostazioni ABR in qualsiasi momento e il lettore passa a utilizzare il profilo che corrisponde maggiormente alle impostazioni più recenti.

Ad esempio, se un flusso ha i seguenti profili:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4. 2400000
* 5: 4000000

Se specifichi un intervallo da 300000 a 2000000, TVSDK considera solo i profili 1, 2 e 3. Questo consente alle applicazioni di adattarsi a varie condizioni di rete, come il passaggio da wi-fi a 3G o a vari dispositivi come un telefono, un tablet o un computer desktop.

Per impostare i parametri di controllo ABR, impostare i parametri nella classe `ABRControlParameter` .