---
description: È possibile impostare un controllo dell'interfaccia utente per il volume audio.
title: Fornire il controllo volume
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---

# Fornire il controllo volume{#provide-volume-control}

È possibile impostare un controllo dell&#39;interfaccia utente per il volume audio.

1. Attendere che l&#39;istanza MediaPlayer sia in uno stato valido per questo comando, che è qualsiasi tranne RILASCIATO o ERRORE.
1. Chiamata `setVolume` il `MediaPlayer` per impostare il volume audio.

   ```java
   void setVolume(int volume) throws IllegalStateException;
   ```

   Il valore per il volume rappresenta il volume richiesto espresso come proporzione del volume massimo, dove 0 indica il volume invisibile all&#39;utente e 100 indica il volume massimo.
