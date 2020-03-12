---
description: Puoi scegliere di utilizzare i comportamenti annunci predefiniti.
seo-description: Puoi scegliere di utilizzare i comportamenti annunci predefiniti.
seo-title: Utilizzare il comportamento di riproduzione predefinito
title: Utilizzare il comportamento di riproduzione predefinito
uuid: 7139384c-167a-4cab-816a-c02fb723a5cb
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Utilizzare il comportamento di riproduzione predefinito{#use-the-default-playback-behavior}

Puoi scegliere di utilizzare i comportamenti annunci predefiniti.

Per utilizzare i comportamenti predefiniti:

    * Se implementate la vostra classe &#39;ContentFactory`, restituite una nuova istanza di `DefaultAdPolicySelector` nell&#39;implementazione di `doRetrieveAdPolicySelector`.
    
    &quot;Classe
    pubblica CustomContentFactory estende ContentFactory {
    
    //...
    // il codice personalizzato per le classi
    pubblicitarie//...
    
    /**
    * @inheritDoc
    */
    override della
    funzione protetta doRetrieveAdPolicySelector(item:MediaPlayerItem):AdPolicySelector {
    return new DefaultAdPolicySelector(item);
    }
    &quot;
    
    
    * Se non hai un&#39;implementazione personalizzata per la classe ‘ContentFactory’, TVSDK utilizza `DefaultAdSelector PolicySelector`.