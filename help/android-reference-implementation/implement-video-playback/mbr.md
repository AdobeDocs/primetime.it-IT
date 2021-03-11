---
description: Il TVSDK può riprodurre video con più profili con bit rate diversi, passando da un livello di qualità a un altro in base alla larghezza di banda disponibile.
title: Bit rate multipli
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 0%

---


# Bit rate multipli {#multiple-bit-rates}

Il TVSDK può riprodurre video con più profili con bit rate diversi, passando da un livello di qualità a un altro in base alla larghezza di banda disponibile.

È possibile impostare i bit rate iniziali, minimi e massimi, nonché i criteri di switch ABR (Adaptive Bit Rate) per un flusso a bit rate multiplo (MBR). Il TVSDK passa automaticamente al bit rate che offre la migliore esperienza di riproduzione nella configurazione specificata.

L&#39;implementazione di riferimento configura i seguenti parametri ABR in [IPlaybackConfig](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html).

| Parametro | Descrizione |
|--- |--- |
| Bit rate iniziale:  getABRInitialBitRate | Il bit rate di riproduzione desiderato (in bit al secondo) per il primo segmento. All’avvio della riproduzione, per il primo segmento viene utilizzato il profilo più vicino (uguale o maggiore del bit rate iniziale).  Se viene definito un bit rate minimo e il bit rate iniziale è inferiore al minimo, il TVSDK seleziona il profilo con il bit rate più basso al di sopra del bit rate minimo. Allo stesso modo, se la frequenza iniziale è superiore alla velocità massima, il TVSDK seleziona la frequenza più alta al di sotto del valore massimo. Se il bit rate iniziale è zero o non definito, il bit rate iniziale è determinato dal criterio ABR.  Restituisce un valore intero che rappresenta il profilo byte per secondo. |
| Bit rate minimo:  getABRMinBitRate | Il bit rate più basso consentito a cui può passare l&#39;ABR. Il passaggio ABR ignora i profili con una velocità di trasmissione inferiore a questa. Restituisce un valore intero che rappresenta i bit per secondo del profilo. |
| Velocità bit massima:  getABRMaxBitRate | Il bit rate più alto consentito a cui può passare l&#39;ABR. Il passaggio ABR ignora i profili con un bit rate più alto di questo. Restituisce un valore intero che rappresenta i bit per secondo del profilo. |
| Criteri di commutazione ABR:  getABRPolicy | Quando possibile, la riproduzione passa gradualmente al profilo a bit rate più alto. È possibile impostare i criteri per il passaggio all’ABR, che determina la velocità con cui il TVSDK passa da un profilo all’altro. Il valore predefinito è Moderato. <ul><li>*Conservatore*: Passa al profilo con il bit rate successivo più alto quando la larghezza di banda è superiore del 50% rispetto al bit rate corrente. </li><li>*Modera*: Passa al successivo profilo di bit rate più alto quando la larghezza di banda è superiore del 20% rispetto al bit rate corrente.</li><li>*Aggressivo*: Passa immediatamente al profilo di bit rate più alto quando la larghezza di banda è superiore al bit rate corrente</li></ul><br/>Se il bit rate iniziale è zero o non specificato e viene specificato un criterio, la riproduzione inizia con il profilo bit-rate più basso per Conservative, il profilo più vicino al bit rate mediano dei profili disponibili per Moderato e il profilo bit-rate più alto per Aggressivo.<br/><br/>Il criterio funziona entro i limiti dei bit rate minimo e massimo, se specificati.  Restituisce l&#39;impostazione corrente dall&#39;enum ABRControlParameters: <ul><li>ABR_CONSERVATIVE</li><li>ABR_MODERATE </li><li>ABR_AGGRESSIVE</li></ul><br>Vedere anche  [ABRPolicy](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/ABRControlParameters.ABRPolicy.html). |

>[!NOTE]
>
>* Il meccanismo di failover TVSDK potrebbe ignorare queste impostazioni, perché TVSDK favorisce un’esperienza di riproduzione continua rispetto al rigoroso rispetto dei parametri di controllo.
>* Quando il bit rate cambia, TVSDK invia gli eventi `onProfileChanged` in `PlaybackEventListener`.


## Abilitazione del controllo ABR personalizzato nell&#39;implementazione di riferimento {#section_72A6E7263E1441DD8D7E0690285515E6}

Il bit rate adattivo (ABR) è abilitato nel TVSDK per impostazione predefinita. Puoi utilizzare l’interfaccia utente Impostazioni Primetime per ignorare il comportamento TVSDK predefinito nell’implementazione di riferimento configurando il controllo ABR personalizzato.

Per abilitare l’ABR personalizzato tramite l’interfaccia utente Impostazioni:

* Apri la finestra di dialogo Impostazioni Primetime .
* Selezionare **[!UICONTROL ABR controls]**.

   ![](assets/abr-configuration.jpg)

* Toccare il controllo [!UICONTROL Enable ON] in modo che visualizzi `OFF`.

Il `PlaybackManager` imposta i parametri ABR solo se [isABRControlEnabled](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html) restituisce true (ON). Se restituisce false (OFF), il `PlaybackManager` utilizza il controllo ABR predefinito in modo che i bit rate iniziale, minimo e massimo siano tutti uguali a 0 e il criterio ABR sia `ABR_MODERATE`.

## Configura i bit rate bassi {#section_5451691CBBD24542AD54A474D222CD39}

Per alcune velocità di riproduzione a bit rate ridotto, il TVSDK, per impostazione predefinita, passa al flusso solo audio e la riproduzione appare bloccata. È possibile configurare il lettore in modo che non si verifichi mai una situazione in cui passa a solo audio.

* Implementa l&#39;interfaccia [IPlaybackConfig](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html) :

* Assicurati che [getABRMinBitRate](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#getABRMinBitRate()) sia superiore al bit rate solo audio (superiore a 64000).
* Assicurati che [isABRControlEnabled](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#isABRControlEnabled()) sia attivato.