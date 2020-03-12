---
description: Rilasciare un’istanza e risorse di MediaPlayer quando non è più necessario disporre di MediaResource.
seo-description: Rilasciare un’istanza e risorse di MediaPlayer quando non è più necessario disporre di MediaResource.
seo-title: Rilasciare un’istanza e le risorse di MediaPlayer
title: Rilasciare un’istanza e le risorse di MediaPlayer
uuid: e7b2112e-8add-4789-9345-5f829d39d639
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Rilasciare un’istanza e le risorse di MediaPlayer{#release-a-mediaplayer-instance-and-resources}

Rilasciare un’istanza e risorse di MediaPlayer quando non è più necessario disporre di MediaResource.

Quando si rilascia un `MediaPlayer` oggetto, le risorse hardware sottostanti associate a tale `MediaPlayer` oggetto vengono deallocate.

Di seguito sono riportati alcuni motivi per rilasciare un `MediaPlayer`:

* L&#39;utilizzo di risorse non necessarie può influire sulle prestazioni.
* Se più istanze dello stesso codec video non sono supportate su un dispositivo, potrebbe verificarsi un errore di riproduzione per altre applicazioni.

1. Rilasciate il `MediaPlayer`.

   ```
   function release():void;
   ```

Una volta rilasciata l&#39; `MediaPlayer` istanza, non sarà più possibile utilizzarla. Se dopo il rilascio viene chiamato un metodo dell’ `MediaPlayer` interfaccia, viene `IllegalStateException` generato un messaggio.