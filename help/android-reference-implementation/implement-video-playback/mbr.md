---
description: TVSDK può riprodurre video con più profili con bitrate diversi, passando da un livello di qualità all’altro in base alla larghezza di banda disponibile.
seo-description: TVSDK può riprodurre video con più profili con bitrate diversi, passando da un livello di qualità all’altro in base alla larghezza di banda disponibile.
seo-title: Bitrate multipli
title: Bitrate multipli
uuid: 46eac41e-0b2a-42e3-8a88-54ad9fe34212
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 0%

---


# Bitrate multipli {#multiple-bit-rates}

TVSDK può riprodurre video con più profili con bitrate diversi, passando da un livello di qualità all’altro in base alla larghezza di banda disponibile.

Potete impostare i bitrate iniziali, minimi e massimi, nonché il criterio ABR (Adaptive Bit Rate) per un flusso a bit rate multiplo (MBR). Il TVSDK passa automaticamente al bitrate che offre la migliore esperienza di riproduzione all&#39;interno della configurazione specificata.

L&#39;implementazione di riferimento configura i seguenti parametri ABR in [IPlaybackConfig](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html).

| Parametro | Descrizione |
|--- |--- |
| Bitrate iniziale:  getABRIninitialBitRate | Bitrate di riproduzione desiderato (in bit al secondo) per il primo segmento. All’avvio della riproduzione, per il primo segmento viene utilizzato il profilo più vicino (uguale o maggiore del bitrate iniziale).  Se viene definito un bitrate minimo e il bitrate iniziale è inferiore al minimo, TVSDK seleziona il profilo con il bitrate più basso al di sopra del bitrate minimo. Allo stesso modo, se la frequenza iniziale è superiore alla velocità massima, TVSDK seleziona la frequenza massima al di sotto del valore massimo. Se il bitrate iniziale è zero o undefined, il bitrate iniziale è determinato dal criterio ABR.  Restituisce un valore intero che rappresenta il profilo byte per secondo. |
| Bitrate minimo:  getABRMinBitRate | Bitrate più basso consentito a cui può passare l&#39;ABR. La commutazione ABR ignora i profili con bitrate inferiore a questo. Restituisce un valore intero che rappresenta il profilo bit per secondo. |
| Bitrate massimo:  getABRMaxBitRate | Bitrate massimo consentito a cui può passare l&#39;ABR. La commutazione ABR ignora i profili con un bitrate maggiore di questo. Restituisce un valore intero che rappresenta il profilo bit per secondo. |
| Criteri di commutazione ABR:  getABRPolicy | Quando possibile, la riproduzione passa gradualmente al profilo con bitrate più elevato. Potete impostare il criterio per il passaggio ABR, che determina la velocità con cui l&#39;SDK TVSDK passa da un profilo all&#39;altro. Il valore predefinito è Moderato. <ul><li>*Conservatore*: Passa al profilo con bitrate successivo più elevato quando la larghezza di banda è superiore del 50% rispetto al bitrate corrente. </li><li>*Moderate*: Passa al successivo profilo di bitrate più elevato quando la larghezza di banda è superiore del 20% rispetto al bitrate corrente.</li><li>*Aggressivo*: Passa immediatamente al profilo bitrate più alto quando la larghezza di banda è superiore al bitrate corrente</li></ul><br/>Se il bitrate iniziale è zero o non è specificato e viene specificato un criterio, la riproduzione inizia con il profilo di bitrate più basso per Conservative, il profilo più vicino al bitrate medio dei profili disponibili per Moderate e il profilo di bitrate più alto per Aggressivo.<br/><br/>Il criterio funziona entro i limiti dei bitrate minimo e massimo, se specificati.  Restituisce l’impostazione corrente dall’enum ABRControlParameters: <ul><li>ABR_CONSERVATIVE</li><li>ABR_MODERATE </li><li>ABR_AGGRESSIVE</li></ul><br>Vedere anche  [ABRPolicy](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/ABRControlParameters.ABRPolicy.html). |

>[!NOTE]
>
>* Il meccanismo di failover TVSDK potrebbe sovrascrivere queste impostazioni, perché TVSDK favorisce un&#39;esperienza di riproduzione continua nel rispetto rigoroso dei parametri di controllo.
>* Quando il bitrate cambia, TVSDK invia eventi `onProfileChanged` in `PlaybackEventListener`.


## Abilitazione del controllo ABR personalizzato nell&#39;implementazione di riferimento {#section_72A6E7263E1441DD8D7E0690285515E6}

Il bitrate adattivo (ABR) è attivato in TVSDK per impostazione predefinita. Potete utilizzare l&#39;interfaccia utente Impostazioni Primetime per ignorare il comportamento TVSDK predefinito nell&#39;implementazione di riferimento configurando il controllo ABR personalizzato.

Per abilitare ABR personalizzato tramite l&#39;interfaccia utente Impostazioni:

* Aprite la finestra di dialogo Impostazioni Primetime.
* Selezionare **[!UICONTROL ABR controls]**.

   ![](assets/abr-configuration.jpg)

* Toccate il controllo [!UICONTROL Enable ON] in modo che venga visualizzato `OFF`.

L&#39; `PlaybackManager` imposta i parametri ABR solo se [isABRControlEnabled](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html) restituisce true (ON). Se restituisce false (OFF), il `PlaybackManager` utilizza il controllo ABR predefinito, pertanto i valori bitrate iniziali, minimi e massimi saranno tutti pari a 0 e il criterio ABR sarà `ABR_MODERATE`.

## Configurare per bitrate ridotti {#section_5451691CBBD24542AD54A474D222CD39}

Per alcuni bitrate di riproduzione ridotti, per impostazione predefinita TVSDK passa al flusso solo audio e la riproduzione appare bloccata. È possibile configurare il lettore in modo che non si verifichi mai una situazione in cui passa solo all&#39;audio.

* Implementa l&#39;interfaccia [IPlaybackConfig](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html):

* Assicurarsi che [getABRMinBitRate](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#getABRMinBitRate()) sia maggiore del bitrate solo audio (maggiore di 64000).
* Assicurarsi che [isABRControlEnabled](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#isABRControlEnabled()) sia attivato.