---
description: Rilasciare un’istanza e risorse di MediaPlayer quando non è più necessario disporre di MediaResource.
seo-description: Rilasciare un’istanza e risorse di MediaPlayer quando non è più necessario disporre di MediaResource.
seo-title: Rilasciare un’istanza e le risorse di MediaPlayer
title: Rilasciare un’istanza e le risorse di MediaPlayer
uuid: e7b2112e-8add-4789-9345-5f829d39d639
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# Rilasciare un&#39;istanza e risorse di MediaPlayer{#release-a-mediaplayer-instance-and-resources}

Rilasciare un’istanza e risorse di MediaPlayer quando non è più necessario disporre di MediaResource.

Quando si rilascia un oggetto `MediaPlayer`, le risorse hardware sottostanti associate a questo oggetto `MediaPlayer` vengono deallocate.

Di seguito sono riportati alcuni motivi per rilasciare un `MediaPlayer`:

* L&#39;utilizzo di risorse non necessarie può influire sulle prestazioni.
* Se più istanze dello stesso codec video non sono supportate su un dispositivo, potrebbe verificarsi un errore di riproduzione per altre applicazioni.

1. Rilasciare la `MediaPlayer`.

   ```
   function release():void;
   ```

Dopo il rilascio dell&#39;istanza `MediaPlayer`, non è più possibile utilizzarla. Se dopo il rilascio viene chiamato un metodo dell&#39;interfaccia `MediaPlayer`, viene restituito un `IllegalStateException`.