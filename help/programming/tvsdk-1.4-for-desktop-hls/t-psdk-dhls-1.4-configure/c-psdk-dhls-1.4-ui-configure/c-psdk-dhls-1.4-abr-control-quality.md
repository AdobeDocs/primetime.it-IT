---
description: I flussi HLS e DASH forniscono codifiche (profili) di bitrate diverse per lo stesso breve burst di video. TVSDK può selezionare il livello di qualità per ogni burst in base alla larghezza di banda disponibile.
title: Velocità bit adattive (ABR) per la qualità video
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '973'
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
   <td colname="col2"> <p>Velocità in bit di riproduzione desiderata (in bit al secondo) per il primo segmento. All’avvio della riproduzione, per il primo segmento viene utilizzato il profilo più vicino, corrispondente o superiore alla velocità in bit iniziale. </p> <p> Se viene definita una velocità in bit minima e la velocità in bit iniziale è inferiore alla velocità in bit minima, TVSDK seleziona il profilo con la velocità in bit più bassa al di sopra della velocità in bit minima. Se il tasso iniziale è superiore al tasso massimo, TVSDK seleziona il tasso più alto al di sotto del tasso massimo. </p> <p>Se il bit rate iniziale è zero o non definito, il bit rate iniziale è determinato dalla policy ABR. </p> <p> <span class="apiname"> ABRInitialBitRate </span> restituisce un valore intero che rappresenta il profilo byte al secondo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Velocità bit minima </td> 
   <td colname="col2"> <p>La velocità bit minima consentita alla quale l'ABR può passare. La commutazione ABR ignora i profili con una velocità di trasmissione inferiore a questa. </p> <p> <span class="apiname"> ABRMinBitRate </span> restituisce un valore intero che rappresenta il profilo bit al secondo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Velocità bit massima </td> 
   <td colname="col2"> <p>La velocità bit massima consentita alla quale l'ABR può passare. Quando si cambia ABR, vengono ignorati i profili con una velocità di trasmissione superiore a questa. </p> <p> <span class="apiname"> ABRMaxBitRate </span> restituisce un valore intero che rappresenta il profilo bit al secondo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Criteri di cambio ABR </td> 
   <td colname="col2"> Quando possibile, la riproduzione passa gradualmente al profilo con il bit rate più alto. È possibile impostare il criterio per il passaggio ABR, che determina la velocità con cui TVSDK passa da un profilo all’altro. Il valore predefinito è <span class="codeph"> MODERATE_POLICY </span>. <p>Quando TVSDK decide di passare a una velocità bit più alta, il lettore seleziona il profilo della velocità bit ideale su cui passare in base alla policy ABR corrente: 
     <ul id="ul_058D0FFC944C476A83BB9E756B95DEBD"> 
      <li id="li_C690A12DC34C4754B01C2D0616FB6A0A"> <span class="codeph"> CONSERVATIVE_POLICY </span>: passa al profilo con la velocità in bit successiva più elevata quando la larghezza di banda è del 50% superiore alla velocità in bit corrente. </li> 
      <li id="li_FF5BDB099B554940AC296938C7A12B81"> <span class="codeph"> MODERATE_POLICY </span>: passa al profilo con velocità in bit successiva più elevata quando la larghezza di banda è del 20% superiore alla velocità in bit corrente. </li> 
      <li id="li_E602508429864C279BF78360E95718A6"> <span class="codeph"> AGGRESSIVE_POLICY </span>: passa immediatamente al profilo del bit rate più alto quando la larghezza di banda è superiore al bit rate corrente. </li> 
     </ul> </p> <p>Se il bitrate iniziale è zero o non è specificato, ma è specificato un criterio, la riproduzione inizia con il profilo di bitrate più basso per conservativo, il profilo più vicino al bitrate mediano dei profili disponibili per moderato e il profilo di bitrate più alto per aggressivo. </p> <p>Se specificate, le velocità bit minima e massima funzionano in modo limitato. </p> <p> <span class="codeph"> ABRPolicy </span> restituisce l'impostazione corrente dalla <span class="codeph"> ABRControlParameters </span> enum: CONSERVATIVE_POLICY, MODERATE_POLICY o AGGRESSIVE_POLICY. </p> </td> 
  </tr> 
 </tbody> 
</table>

Considera le seguenti informazioni:

* Il meccanismo di failover di TVSDK potrebbe ignorare le impostazioni, perché TVSDK favorisce un’esperienza di riproduzione continua rispetto all’aderenza rigorosa ai parametri di controllo.
* Quando la velocità di trasmissione cambia, TVSDK invia `ProfileEvent.PROFILE_CHANGED`.
* È possibile modificare le impostazioni ABR in qualsiasi momento e il lettore passa all&#39;uso del profilo che corrisponde maggiormente alle impostazioni più recenti.

Ad esempio, se un flusso ha i seguenti profili:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

Se specifichi un intervallo di 300000 da 2000000, TVSDK considera solo i profili 1, 2 e 3. Questo consente alle applicazioni di adattarsi a varie condizioni di rete, ad esempio passare dal wi-fi al 3G o a vari dispositivi, come un telefono, un tablet o un computer desktop.

Per impostare i parametri di controllo ABR, effettuate una delle seguenti operazioni:

* Utilizza il `ABRControlParameterBuilder` classe helper per impostare qualsiasi sottoinsieme dei parametri (funziona su `ABRControlParameter` dietro le quinte)

* Impostare i parametri su `ABRControlParameter` classe.

## Configurare le velocità di trasmissione adattive utilizzando ABRControlParametersBuilder {#section_3DDE397A7CE445E1832EBAA46CE5C069}

Utilizzo di `ABRControlParametersBuilder` helper class è il modo più semplice ed efficiente per impostare i parametri ABR.

* Il `ABRControlParametersBuilder` costruttore imposta tutti i parametri ABR sui valori predefiniti nel sottostante `ABRControlParameters` oggetto.

* È possibile reimpostare singoli parametri ABR durante il runtime, purché venga mantenuto un riferimento allo stesso `ABRControlParametersBuilder` dell&#39;istanza.

Questa classe include anche `toABRControlParameters()` metodo helper. Utilizzare questo metodo per ottenere un&#39;istanza di `ABRControlParameters` e impostarlo su `mediaPlayer.ABRControlParameters` proprietà. In questo modo le impostazioni diventano effettive nel lettore.

1. Crea un&#39;istanza di `ABRControlParametersBuilder` e impostare i parametri su Media Player.

   >[!NOTE]
   >
   >Ad esempio, nell&#39;esempio seguente tutti i parametri vengono inizializzati in base ai valori predefiniti, quindi viene impostato solo il criterio su conservativo e la velocità in bit massima viene limitata a 1000000:
   >
   >```
   >var abrBuilder:ABRControlParametersBuilder =  
   >   new ABRControlParametersBuilder(); 
   >abrBuilder.policy = ABRControlParameters.CONSERVATIVE_POLICY; 
   >abrBuilder.maxBitRate = 1000000; 
   >mediaPlayer.abrControlParameters =  
   >   abrBuilder.toABRControlParameters();
   >```
   >

1. Modificare i singoli parametri ABR in fase di runtime.

   Per modificare singoli parametri lasciando invariati gli altri parametri:

   ```
   // If later you want to reset the max bit rate to 2000000 
   abrBuilder.maxBitRate = 2000000; 
   mediaPlayer.abrControlParameters =  
     abrBuilder.toABRControlParameters();
   ```

   Per mantenere le impostazioni precedenti, è necessario mantenere un riferimento allo stesso `ABRControlParametersBuilder` istanza creata al passaggio 1.

## Configurare velocità bit adattivi utilizzando ABRControlParameters {#section_02161FD0A73F40ED9CAE17F9AF850483}

È possibile impostare i valori di controllo ABR solo con `ABRControlParameters`, ma puoi crearne una nuova in qualsiasi momento.

Questa capacità di impostare i parametri ABR era supportata prima dell&#39;esistenza del `ABRControlParametersBuilder` ma questa capacità è ancora efficace per impostare i parametri ABR al momento della costruzione. Tuttavia, per modificare i singoli parametri dopo la costruzione, è necessario utilizzare `ABRControlParametersBuilder` classe.

Le seguenti condizioni si applicano a `ABRControlParameters`:

* È necessario fornire i valori per tutti i parametri al momento della costruzione.
* Non è possibile modificare i singoli valori dopo il tempo di costruzione.
* Se i parametri specificati non rientrano nell&#39;intervallo consentito, `ArgumentError` viene lanciato.

1. Decidi la velocità di trasmissione iniziale, minima e massima.
1. Determinare il criterio ABR:

   * `CONSERVATIVE_POLICY`
   * `MODERATE_POLICY`
   * `AGGRESSIVE_POLICY`

1. Impostare i valori dei parametri ABR in `ABRControlParameters` e assegnarli a Media Player.

   ```
   mediaPlayer.abrControlParameters = new ABRControlParameters( 
       ABRControlParameters.CONSERVATIVE_POLICY, 
       0, // Initial bit rate 
       0, // Minimum bit rate 
       1000000 // Maximum bit rate 
   );
   ```
