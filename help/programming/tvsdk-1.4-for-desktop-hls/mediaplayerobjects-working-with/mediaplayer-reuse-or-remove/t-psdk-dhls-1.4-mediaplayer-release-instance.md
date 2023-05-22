---
description: È necessario rilasciare un'istanza MediaPlayer e le relative risorse quando non è più necessario MediaResource.
title: Rilasciare un’istanza MediaPlayer e le relative risorse
exl-id: 2a802754-5c51-4e5f-8c36-843074b487b5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
