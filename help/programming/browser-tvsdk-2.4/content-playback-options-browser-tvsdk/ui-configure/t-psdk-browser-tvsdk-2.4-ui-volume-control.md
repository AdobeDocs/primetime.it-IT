---
description: È possibile impostare un controllo dell'interfaccia utente per il volume audio.
title: Fornire il controllo volume
exl-id: 5c446081-5491-46b6-9259-293131af80cb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '87'
ht-degree: 0%

---

# Fornire il controllo volume{#provide-volume-control}

È possibile impostare un controllo dell&#39;interfaccia utente per il volume audio.

1. Attendi `MediaPlayer` l&#39;istanza deve trovarsi in uno stato valido per questo comando.

   Qualsiasi stato ad eccezione di RILASCIATO o ERRORE è valido.
1. Impostare l&#39;attributo volume su `MediaPlayer` per impostare il volume audio.

   ```js
   player.volume = ...
   ```

   Il valore per il volume rappresenta il volume richiesto espresso come proporzione del volume massimo, dove 0 indica il volume invisibile all&#39;utente e rappresenta il volume massimo.
