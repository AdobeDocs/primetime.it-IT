---
description: I flussi HLS e DASH forniscono codifiche di bitrate (profili) diverse per lo stesso breve spezzone di video. TVSDK può selezionare il livello di qualità per ogni burst in base alla larghezza di banda disponibile.
seo-description: I flussi HLS e DASH forniscono codifiche di bitrate (profili) diverse per lo stesso breve spezzone di video. TVSDK può selezionare il livello di qualità per ogni burst in base alla larghezza di banda disponibile.
seo-title: Bitrate adattivo (ABR) per la qualità video
title: Bitrate adattivo (ABR) per la qualità video
uuid: e3d5ef90-067d-48e0-a025-081de931d842
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '1011'
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
   <td colname="col2"> <p>Bitrate di riproduzione desiderato (in bit al secondo) per il primo segmento. All’avvio della riproduzione, per il primo segmento viene utilizzato il profilo più vicino, pari o superiore al bitrate iniziale. </p> <p> Se viene definito un bitrate minimo e il bitrate iniziale è inferiore al bitrate minimo, TVSDK seleziona il profilo con il bitrate più basso al di sopra del bitrate minimo. Se la frequenza iniziale è superiore alla velocità massima, TVSDK seleziona la frequenza massima al di sotto della velocità massima. </p> <p>Se il bitrate iniziale è zero o undefined, il bitrate iniziale è determinato dal criterio ABR. </p> <p> <span class="apiname"> ABRIninitialBitRate  </span> restituisce un valore intero che rappresenta il profilo byte per secondo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Bitrate minimo </td> 
   <td colname="col2"> <p>Bitrate più basso consentito a cui può passare l'ABR. La commutazione ABR ignora i profili con un bitrate inferiore a tale bitrate. </p> <p> <span class="apiname"> ABRMinBitRate  </span> restituisce un valore intero che rappresenta il profilo bit per secondo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Bitrate massimo </td> 
   <td colname="col2"> <p>Bitrate massimo consentito a cui può passare l'ABR. La commutazione ABR ignora i profili con bitrate maggiore di questo valore. </p> <p> <span class="apiname"> ABRMaxBitRate  </span> restituisce un valore intero che rappresenta il profilo bit per secondo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Criteri di commutazione ABR </td> 
   <td colname="col2"> Quando possibile, la riproduzione passa gradualmente al profilo con bitrate più elevato. Puoi impostare il criterio per il passaggio ABR, che determina la velocità con cui TVSDK passa da un profilo all'altro. Il valore predefinito è <span class="codeph"> MODERATE_POLICY </span>. <p>Quando TVSDK decide di passare a un bitrate più alto, il lettore seleziona il profilo di bitrate ideale a cui passare in base al criterio ABR corrente: 
     <ul id="ul_058D0FFC944C476A83BB9E756B95DEBD"> 
      <li id="li_C690A12DC34C4754B01C2D0616FB6A0A"> <span class="codeph"> CONSERVATIVE_POLICY  </span>: Passa al profilo con bitrate successivo più elevato quando la larghezza di banda è superiore del 50% rispetto al bitrate corrente. </li> 
      <li id="li_FF5BDB099B554940AC296938C7A12B81"> <span class="codeph"> MODERATE_POLICY  </span>: Passa al successivo profilo di bitrate più elevato quando la larghezza di banda è superiore del 20% rispetto al bitrate corrente. </li> 
      <li id="li_E602508429864C279BF78360E95718A6"> <span class="codeph"> AGGRESSIVE_POLICY  </span>: Passa immediatamente al profilo bitrate più alto quando la larghezza di banda è superiore al bitrate corrente. </li> 
     </ul> </p> <p>Se il bitrate iniziale è pari a zero o non è specificato, ma viene specificato un criterio, la riproduzione inizia con il profilo di bitrate più basso per gli utenti meno esperti, il profilo più vicino al bitrate medio dei profili disponibili per gli utenti meno esperti e il profilo di bitrate più alto per gli utenti meno esperti. </p> <p>Il criterio funziona nei limiti dei bitrate minimo e massimo, se questi valori vengono specificati. </p> <p> <span class="codeph"> ABRPolicy  </span> restituisce l'impostazione corrente dall' <span class="codeph"> ABRControlParameters  </span> enum: CONSERVATIVE_POLICY, MODERATE_POLICY o AGGRESSIVE_POLICY. </p> </td> 
  </tr> 
 </tbody> 
</table>

Tenete presenti le seguenti informazioni:

* Il meccanismo di failover TVSDK potrebbe sovrascrivere le impostazioni, perché TVSDK favorisce un’esperienza di riproduzione continua in modo da rispettare rigorosamente i parametri di controllo.
* Quando il bitrate cambia, TVSDK invia `ProfileEvent.PROFILE_CHANGED`.
* È possibile modificare le impostazioni ABR in qualsiasi momento, e il lettore utilizza il profilo che meglio corrisponde alle impostazioni più recenti.

Ad esempio, se un flusso ha i seguenti profili:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

Se specificate un intervallo da 300000 a 2000000, TVSDK considera solo i profili 1, 2 e 3. Questo consente alle applicazioni di adattarsi a varie condizioni di rete, come il passaggio da wi-fi a 3G o a vari dispositivi come un telefono, un tablet o un computer desktop.

Per impostare i parametri di controllo ABR, effettuate una delle seguenti operazioni:

* Utilizzate la classe helper `ABRControlParameterBuilder` per impostare qualsiasi sottoinsieme di parametri (opera su `ABRControlParameter` dietro le quinte)

* Impostate i parametri sulla classe `ABRControlParameter`.

## Configurare i bitrate adattivi mediante ABRControlParametersBuilder {#section_3DDE397A7CE445E1832EBAA46CE5C069}

L&#39;utilizzo della classe helper `ABRControlParametersBuilder` è il modo più semplice ed efficiente per impostare i parametri ABR.

* Il costruttore `ABRControlParametersBuilder` imposta tutti i parametri ABR sui valori predefiniti per l&#39;oggetto `ABRControlParameters` sottostante.

* È possibile ripristinare i singoli parametri ABR durante il runtime, purché si mantenga un riferimento alla stessa istanza `ABRControlParametersBuilder`.

Questa classe include anche il metodo helper `toABRControlParameters()`. Utilizzare questo metodo per ottenere un&#39;istanza di `ABRControlParameters` e impostarla sulla proprietà `mediaPlayer.ABRControlParameters`. In questo modo le impostazioni diventano effettive nel lettore.

1. Create un&#39;istanza della classe helper `ABRControlParametersBuilder` e impostate i parametri su Media Player.

   >[!NOTE]
   >
   >Ad esempio, l’esempio seguente inizializza tutti i parametri in base alle impostazioni predefinite, imposta solo il criterio su conservativo e limita il bitrate massimo a 1000000:
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

1. Modificare i singoli parametri ABR in fase di esecuzione.

   Per modificare i singoli parametri lasciando gli altri così come erano:

   ```
   // If later you want to reset the max bit rate to 2000000 
   abrBuilder.maxBitRate = 2000000; 
   mediaPlayer.abrControlParameters =  
     abrBuilder.toABRControlParameters();
   ```

   Per mantenere le impostazioni precedenti, è necessario mantenere un riferimento alla stessa istanza `ABRControlParametersBuilder` creata nel passaggio 1.

## Configurare i bitrate adattivi utilizzando ABRControlParameters {#section_02161FD0A73F40ED9CAE17F9AF850483}

È possibile impostare i valori di controllo ABR solo con `ABRControlParameters`, ma è possibile crearne uno nuovo in qualsiasi momento.

Questa capacità di impostare i parametri ABR era supportata prima dell&#39;esistenza della classe `ABRControlParametersBuilder`, ma questa capacità è ancora efficace per impostare i parametri ABR in fase di costruzione. Tuttavia, per modificare i singoli parametri dopo la costruzione, è necessario utilizzare la classe `ABRControlParametersBuilder`.

Le seguenti condizioni si applicano a `ABRControlParameters`:

* È necessario specificare i valori per tutti i parametri al momento della costruzione.
* Non è possibile modificare singoli valori dopo il tempo di costruzione.
* Se i parametri specificati non rientrano nell&#39;intervallo consentito, viene restituito un `ArgumentError`.

1. Decidete i bitrate iniziali, minimi e massimi.
1. Determinare il criterio ABR:

   * `CONSERVATIVE_POLICY`
   * `MODERATE_POLICY`
   * `AGGRESSIVE_POLICY`

1. Impostate i valori dei parametri ABR nel costruttore `ABRControlParameters` e assegnateli a Media Player.

   ```
   mediaPlayer.abrControlParameters = new ABRControlParameters( 
       ABRControlParameters.CONSERVATIVE_POLICY, 
       0, // Initial bit rate 
       0, // Minimum bit rate 
       1000000 // Maximum bit rate 
   );
   ```

