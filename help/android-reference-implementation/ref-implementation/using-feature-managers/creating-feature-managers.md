---
description: Le funzioni TVSDK sono guidate dalla configurazione e implementate tramite MediaPlayer.
title: Creazione di gestori di funzioni trasmettendo le informazioni di configurazione a MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---


# Creazione di gestori di funzioni trasmettendo le informazioni di configurazione a MediaPlayer {#creating-feature-managers-by-passing-configuration-information-to-the-mediaplayer}

Le funzioni TVSDK sono guidate dalla configurazione e implementate tramite MediaPlayer.

* La configurazione è l’elenco di impostazioni specifiche per la funzione, ad esempio il bit rate iniziale del controllo ABR e la visibilità predefinita dei sottotitoli.

   I gestori di funzioni devono ottenere le configurazioni per determinare il comportamento della funzione.

   Nell’implementazione di riferimento di Primetime, la configurazione viene memorizzata nelle preferenze condivise, ma puoi memorizzarla in qualsiasi modo abbia senso per il tuo ambiente.

* `MediaPlayer` è l’oggetto Media Player TVSDK che contiene la risorsa video.

   I gestori di funzioni registrano gli ascoltatori di eventi TVSDK a questo oggetto del lettore, recuperano i dati dalla sessione di riproduzione e attivano le funzioni TVSDK nella sessione di riproduzione.

Ciascuna funzione dispone di un’interfaccia di configurazione corrispondente. Ad esempio, `CCManager` utilizza `ICCConfig` per recuperare la configurazione. `ICCConfig` contiene metodi per ottenere le informazioni di configurazione relative solo ai sottotitoli codificati.

L&#39;esempio seguente mostra il file [!DNL ICCConfig.java] configurato per ricevere informazioni sulla visibilità delle didascalie chiuse, lo stile del font e il bordo del font dal `MediaPlayer`:

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