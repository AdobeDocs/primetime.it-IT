---
description: I flussi HLS e DASH forniscono codifiche del bit rate (profili) diverse per lo stesso breve burst di video. TVSDK può selezionare il livello di qualità per ogni burst in base alla larghezza di banda disponibile.
title: Bit rate adattivi (ABR) per la qualità video
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 0%

---


# Bit rate adattivi (ABR) per qualità video{#adaptive-bit-rates-abr-for-video-quality}

I flussi HLS e DASH forniscono codifiche del bit rate (profili) diverse per lo stesso breve burst di video. TVSDK può selezionare il livello di qualità per ogni burst in base alla larghezza di banda disponibile.

TVSDK controlla costantemente il bit rate per garantire che il contenuto venga riprodotto al bit rate ottimale per la connessione di rete corrente.

È possibile impostare i criteri di commutazione del bit rate adattivo (ABR) e i bit rate iniziali, minimi e massimi per un flusso a bit rate multiplo (MBR). TVSDK passa automaticamente al bit rate che offre la migliore esperienza di riproduzione nella configurazione specificata.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> Bit rate iniziale </td> 
   <td colname="col2"> <p>Il bit rate di riproduzione desiderato (in bit al secondo) per il primo segmento. All’avvio della riproduzione, per il primo segmento viene utilizzato il profilo più vicino, che è uguale o maggiore del bit rate iniziale. </p> <p> Se viene definito un bit rate minimo e il bit rate iniziale è inferiore al bit rate minimo, TVSDK seleziona il profilo con il bit rate più basso al di sopra del bit rate minimo. Se la velocità iniziale è superiore alla velocità massima, TVSDK seleziona la velocità più elevata al di sotto della velocità massima. </p> <p>Se il bit rate iniziale è zero o non definito, il bit rate iniziale è determinato dal criterio ABR. </p> <p> <span class="apiname"> ABRInitialBitRate  </span> restituisce un valore intero che rappresenta il profilo byte per secondo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Bit rate minimo </td> 
   <td colname="col2"> <p>Il bit rate più basso consentito a cui può passare l'ABR. La commutazione ABR ignora i profili con un bit rate inferiore a questo bit rate. </p> <p> <span class="apiname"> ABRMinBitRate  </span> restituisce un valore intero che rappresenta i bit al secondo del profilo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Bit rate massimo </td> 
   <td colname="col2"> <p>Il bit rate più alto consentito a cui può passare l'ABR. La commutazione ABR ignora i profili con un bit rate più alto di questo bit rate. </p> <p> <span class="apiname"> ABRMaxBitRate  </span> restituisce un valore intero che rappresenta i bit al secondo del profilo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Criteri di commutazione ABR </td> 
   <td colname="col2"> Quando possibile, la riproduzione passa gradualmente al profilo a bit rate più elevato. È possibile impostare i criteri per il passaggio all’ABR, che determina la velocità con cui TVSDK passa da un profilo all’altro. Il valore predefinito è <span class="codeph"> MODERATE_POLICY </span>. <p>Quando TVSDK decide di passare a un bit rate più alto, il lettore seleziona il profilo di bit rate ideale a cui passare in base alla politica ABR corrente: 
     <ul id="ul_058D0FFC944C476A83BB9E756B95DEBD"> 
      <li id="li_C690A12DC34C4754B01C2D0616FB6A0A"> <span class="codeph"> CONSERVATIVE_POLICY  </span>: Passa al profilo con il bit rate successivo più alto quando la larghezza di banda è superiore del 50% rispetto al bit rate corrente. </li> 
      <li id="li_FF5BDB099B554940AC296938C7A12B81"> <span class="codeph"> MODERATE_POLICY  </span>: Passa al successivo profilo di bit rate più alto quando la larghezza di banda è superiore del 20% rispetto al bit rate corrente. </li> 
      <li id="li_E602508429864C279BF78360E95718A6"> <span class="codeph"> AGGRESSIVE_POLICY  </span>: Passa immediatamente al profilo a bit rate più alto quando la larghezza di banda è superiore al bit rate corrente. </li> 
     </ul> </p> <p>Se il bit rate iniziale è zero o non è specificato, ma è specificato un criterio, la riproduzione inizia con il profilo di bit rate più basso per conservatore, il profilo più vicino al bit rate mediano dei profili disponibili per moderato e il profilo di bit rate più alto per aggressivo. </p> <p>Il criterio funziona nei vincoli dei bit rate minimo e massimo, se questi tassi sono specificati. </p> <p> <span class="codeph"> ABRPolicy  </span> restituisce l'impostazione corrente dall' <span class="codeph"> ABRControlParameters  </span> enum: CONSERVATIVE_POLICY, MODERATE_POLICY o AGGRESSIVE_POLICY. </p> </td> 
  </tr> 
 </tbody> 
</table>

Considera le seguenti informazioni:

* Il meccanismo di failover TVSDK potrebbe sostituire le impostazioni, perché TVSDK favorisce un’esperienza di riproduzione continua rispetto ai parametri di controllo.
* Quando cambia il bit rate, TVSDK invia `ProfileEvent.PROFILE_CHANGED`.
* È possibile modificare le impostazioni ABR in qualsiasi momento e il lettore passa a utilizzare il profilo che corrisponde maggiormente alle impostazioni più recenti.

Ad esempio, se un flusso ha i seguenti profili:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4. 2400000
* 5: 4000000

Se specifichi un intervallo da 300000 a 2000000, TVSDK considera solo i profili 1, 2 e 3. Questo consente alle applicazioni di adattarsi a varie condizioni di rete, come il passaggio da wi-fi a 3G o a vari dispositivi come un telefono, un tablet o un computer desktop.

Per impostare i parametri di controllo ABR, effettuare una delle seguenti operazioni:

* Utilizza la classe di supporto `ABRControlParameterBuilder` per impostare qualsiasi sottoinsieme di parametri (funziona su `ABRControlParameter` dietro le quinte)

* Imposta i parametri sulla classe `ABRControlParameter` .

## Configura i bit rate adattivi utilizzando ABRControlParametersBuilder {#section_3DDE397A7CE445E1832EBAA46CE5C069}

L&#39;utilizzo della classe di supporto `ABRControlParametersBuilder` è il modo più semplice ed efficiente per impostare i parametri ABR.

* Il costruttore `ABRControlParametersBuilder` imposta tutti i parametri ABR sui valori predefiniti dell&#39;oggetto `ABRControlParameters` sottostante.

* È possibile reimpostare i singoli parametri ABR durante l&#39;esecuzione, purché si mantenga un riferimento alla stessa istanza `ABRControlParametersBuilder`.

Questa classe include anche il metodo helper `toABRControlParameters()`. Utilizzare questo metodo per ottenere un&#39;istanza di `ABRControlParameters` e impostarla sulla proprietà `mediaPlayer.ABRControlParameters` . In questo modo le impostazioni diventano effettive nel lettore.

1. Creare un&#39;istanza della classe helper `ABRControlParametersBuilder` e impostare i parametri su Media Player.

   >[!NOTE]
   >
   >Ad esempio, l’esempio seguente inizializza tutti i parametri alle impostazioni predefinite, quindi imposta solo il criterio su conservativo e limita il bit rate massimo a 100000:
   >
   >
   ```
   >var abrBuilder:ABRControlParametersBuilder =  
   >   new ABRControlParametersBuilder(); 
   >abrBuilder.policy = ABRControlParameters.CONSERVATIVE_POLICY; 
   >abrBuilder.maxBitRate = 1000000; 
   >mediaPlayer.abrControlParameters =  
   >   abrBuilder.toABRControlParameters();
   >```

1. Modifica i singoli parametri ABR in fase di esecuzione.

   Per modificare i singoli parametri lasciando gli altri come fossero:

   ```
   // If later you want to reset the max bit rate to 2000000 
   abrBuilder.maxBitRate = 2000000; 
   mediaPlayer.abrControlParameters =  
     abrBuilder.toABRControlParameters();
   ```

   Per mantenere le impostazioni precedenti, è necessario mantenere un riferimento alla stessa istanza `ABRControlParametersBuilder` creata nel passaggio 1.

## Configura i bit rate adattivi utilizzando ABRControlParameters {#section_02161FD0A73F40ED9CAE17F9AF850483}

È possibile impostare valori di controllo ABR solo con `ABRControlParameters`, ma è possibile crearne uno nuovo in qualsiasi momento.

Questa capacità di impostare parametri ABR è stata supportata prima dell&#39;esistenza della classe `ABRControlParametersBuilder`, ma questa capacità è ancora efficace per l&#39;impostazione di parametri ABR in fase di costruzione. Tuttavia, per modificare i singoli parametri dopo la costruzione, è necessario utilizzare la classe `ABRControlParametersBuilder` .

Le seguenti condizioni si applicano a `ABRControlParameters`:

* È necessario fornire valori per tutti i parametri in fase di costruzione.
* Non è possibile modificare singoli valori dopo il tempo di costruzione.
* Se i parametri specificati sono al di fuori dell’intervallo consentito, viene lanciato un `ArgumentError`.

1. Decidere i bit rate iniziali, minimi e massimi.
1. Determina il criterio ABR:

   * `CONSERVATIVE_POLICY`
   * `MODERATE_POLICY`
   * `AGGRESSIVE_POLICY`

1. Imposta i valori dei parametri ABR nel costruttore `ABRControlParameters` e assegnali a Media Player.

   ```
   mediaPlayer.abrControlParameters = new ABRControlParameters( 
       ABRControlParameters.CONSERVATIVE_POLICY, 
       0, // Initial bit rate 
       0, // Minimum bit rate 
       1000000 // Maximum bit rate 
   );
   ```

