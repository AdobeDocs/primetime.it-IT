---
description: Potete impostare un controllo dell’interfaccia utente per regolare il volume del video.
seo-description: Potete impostare un controllo dell’interfaccia utente per regolare il volume del video.
seo-title: Controllo del volume
title: Controllo del volume
uuid: f1e959e0-1817-4ccb-8adc-3eba09c91887
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Controllo del volume {#provide-volume-control}

Potete impostare un controllo dell’interfaccia utente per regolare il volume del video.

1. Nella routine di callback per l&#39;elemento dell&#39;interfaccia di controllo del volume, assicurarsi che il lettore sia in uno stato valido per questo comando.

   >[!TIP]
   >
   >Qualsiasi stato, tranne RELEASED, è valido.

1. Chiamata `setVolume` per impostare il volume audio.

   Ad esempio:

   ```java
   void setVolume(int volume) throws MediaPlayerException;
   ```

   Il valore per il volume rappresenta il volume richiesto espresso in proporzione al volume massimo, dove `0` è silenzioso e `1` corrisponde al volume massimo.

