---
description: È possibile impostare un controllo dell'interfaccia utente per il volume audio.
title: Fornire il controllo volume
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
