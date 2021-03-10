---
description: È necessario rilasciare un'istanza e risorse MediaPlayer quando non è più necessario MediaResource.
title: Rilasciare un'istanza e risorse MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---


# Rilascia un&#39;istanza e risorse MediaPlayer{#release-a-mediaplayer-instance-and-resources}

È necessario rilasciare un&#39;istanza e risorse MediaPlayer quando non è più necessario MediaResource.

Quando si rilascia un oggetto `MediaPlayer`, le risorse hardware sottostanti associate a questo oggetto `MediaPlayer` vengono deallocate.

Di seguito sono riportati alcuni motivi per rilasciare un `MediaPlayer`:

* L&#39;utilizzo di risorse non necessarie può influire sulle prestazioni.
* Se più istanze dello stesso codec video non sono supportate su un dispositivo, potrebbe verificarsi un errore di riproduzione per altre applicazioni.

1. Rilascia il `MediaPlayer`.

   ```
   function release():void;
   ```

Una volta rilasciata l’istanza `MediaPlayer`, non puoi più utilizzarla. Se dopo il rilascio viene chiamato un metodo dell&#39;interfaccia `MediaPlayer` , viene lanciato un `IllegalStateException` .