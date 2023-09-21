---
description: Le funzioni di TVSDK sono guidate dalla configurazione e implementate tramite MediaPlayer.
title: Creazione di feature manager mediante la trasmissione delle informazioni di configurazione a MediaPlayer
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# Creazione di feature manager mediante la trasmissione delle informazioni di configurazione a MediaPlayer {#creating-feature-managers-by-passing-configuration-information-to-the-mediaplayer}

Le funzioni di TVSDK sono guidate dalla configurazione e implementate tramite MediaPlayer.

* Configuration è l&#39;elenco di impostazioni specifiche per la funzione, ad esempio il bitrate iniziale del controllo ABR e la visibilità predefinita dei sottotitoli.

  I gestori di feature devono ottenere le configurazioni per determinare il comportamento della feature.

  Nell’implementazione di riferimento di Primetime, la configurazione viene memorizzata nelle preferenze condivise, ma puoi archiviarla in qualsiasi modo utile per il tuo ambiente.

* `MediaPlayer` è l’oggetto lettore multimediale TVSDK che contiene la risorsa video.

  I gestori di funzioni registrano i listener di eventi TVSDK per questo oggetto lettore, recuperano i dati dalla sessione di riproduzione e attivano le funzioni TVSDK per la sessione di riproduzione.

Ogni funzione dispone di un&#39;interfaccia di configurazione corrispondente. Ad esempio: `CCManager` utilizza `ICCConfig` per recuperare la configurazione. `ICCConfig` contiene metodi per ottenere le informazioni di configurazione relative solo ai sottotitoli.

L&#39;esempio seguente mostra [!DNL ICCConfig.java] file, configurato per ricevere informazioni sulla visibilità dei sottotitoli codificati, sullo stile e sul bordo del carattere dal `MediaPlayer`:

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

Un&#39;applicazione che utilizza una funzione TVSDK può creare la gestione delle funzioni con un provider di configurazione e un `MediaPlayer` oggetto. Ad esempio:

```java
// This application needs to use the advertising workflow feature 
AdsManager adsManager = new AdsManagerOn();
```

Documentazione API per la configurazione di Feature Manager: [Javadoc](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/package-summary.html)
