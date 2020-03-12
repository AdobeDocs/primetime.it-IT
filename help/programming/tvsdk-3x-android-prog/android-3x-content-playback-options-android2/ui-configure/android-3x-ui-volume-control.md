---
description: Potete impostare un controllo dell’interfaccia utente per regolare il volume del video.
seo-description: Potete impostare un controllo dell’interfaccia utente per regolare il volume del video.
seo-title: Controllo del volume
title: Controllo del volume
uuid: c87fe656-0329-4c9c-b65b-43be48c77062
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

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