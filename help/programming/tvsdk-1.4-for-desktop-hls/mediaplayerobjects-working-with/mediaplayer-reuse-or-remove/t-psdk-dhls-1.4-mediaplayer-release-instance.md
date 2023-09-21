---
description: È necessario rilasciare un'istanza MediaPlayer e le relative risorse quando non è più necessario MediaResource.
title: Rilasciare un’istanza MediaPlayer e le relative risorse
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# Rilasciare un’istanza MediaPlayer e le relative risorse{#release-a-mediaplayer-instance-and-resources}

È necessario rilasciare un&#39;istanza MediaPlayer e le relative risorse quando non è più necessario MediaResource.

Quando si rilascia una `MediaPlayer` oggetto, le risorse hardware sottostanti associate a questo `MediaPlayer` oggetto deallocato.

Di seguito sono riportati alcuni motivi per cui è necessario rilasciare una `MediaPlayer`:

* L&#39;utilizzo di risorse non necessarie può influire sulle prestazioni.
* Se più istanze dello stesso codec video non sono supportate su un dispositivo, potrebbe verificarsi un errore di riproduzione per altre applicazioni.

1. Rilasciare `MediaPlayer`.

   ```
   function release():void;
   ```

Dopo il `MediaPlayer` è stata rilasciata, non è più possibile utilizzarla. Se è stato utilizzato un metodo `MediaPlayer` viene richiamata dopo il rilascio, e `IllegalStateException` viene lanciato.
