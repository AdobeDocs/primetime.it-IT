---
description: Le funzioni TVSDK sono guidate dalla configurazione e implementate tramite MediaPlayer.
seo-description: Le funzioni TVSDK sono guidate dalla configurazione e implementate tramite MediaPlayer.
seo-title: Creazione di feature manager trasmettendo le informazioni di configurazione a MediaPlayer
title: Creazione di feature manager trasmettendo le informazioni di configurazione a MediaPlayer
uuid: 106ececd-a670-4360-b000-a31fec65233c
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# Creazione di feature manager trasmettendo le informazioni di configurazione a MediaPlayer {#creating-feature-managers-by-passing-configuration-information-to-the-mediaplayer}

Le funzioni TVSDK sono guidate dalla configurazione e implementate tramite MediaPlayer.

* La configurazione è l’elenco di impostazioni specifiche per la funzione, come il bit rate iniziale del controllo ABR e la visibilità predefinita dei sottotitoli.

   Per determinare il comportamento delle funzioni, i manager delle funzioni devono ottenere le configurazioni necessarie.

   Nell&#39;implementazione di riferimento di Primetime, la configurazione è memorizzata nelle preferenze condivise, ma puoi memorizzarla in qualsiasi modo per il tuo ambiente.

* `MediaPlayer` è l’oggetto lettore multimediale TVSDK che contiene la risorsa video.

   I manager delle funzioni registrano i listener di eventi TVSDK a questo oggetto del lettore, recuperano i dati dalla sessione di riproduzione e attivano le funzioni TVSDK per la sessione di riproduzione.

Ciascuna funzione dispone di un&#39;interfaccia di configurazione corrispondente. Ad esempio, `CCManager` utilizza `ICCConfig` per recuperare la configurazione. `ICCConfig` contiene metodi per ottenere le informazioni di configurazione relative solo ai sottotitoli codificati.

L&#39;esempio seguente mostra il file [!DNL ICCConfig.java] configurato per ricevere informazioni sulla visibilità delle didascalie, lo stile del font e il bordo del font dal percorso `MediaPlayer`:

```java
// Constructor of CCManager 
 
<b>public CCManager(ICCConfig ccConfig, MediaPlayer mediaPlayer) {...}</b> 
  
// ICCConfig methods 
 
<b>public interface ICCConfig {</b> 
  
    /** 
     * Get the closed captioning visibility config 
     * 
     * @return true if visibility is set to true, false otherwise 
     */ 
    
<b> public boolean getCCVisibility();</b> 
  
    /** 
     * Get the closed captioning font style 
     * 
     * @return TextFormat.Font object represents font style 
     */ 
     
<b>public TextFormat.Font getCCFont();</b>

    /** 
     * Get the closed captioning font edge 
     * 
     * @return TextFormat.FontEdge represents of font edge 
     */ 
     
<b>public TextFormat.FontEdge getCCFontEdge();</b> 
... 
}
```

Un&#39;applicazione che utilizza una funzione TVSDK può creare il proprio feature manager con un provider di configurazione e un oggetto `MediaPlayer`. Ad esempio:

```java
// This application needs to use the advertising workflow feature 
AdsManager adsManager = new AdsManagerOn();
```

Documenti API di configurazione di Feature Manager: [Javadoc](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/package-summary.html)