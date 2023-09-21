---
description: È possibile impostare un controllo dell'interfaccia utente per regolare il volume del video.
title: Fornire il controllo volume
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# Fornire il controllo volume {#provide-volume-control}

È possibile impostare un controllo dell&#39;interfaccia utente per regolare il volume del video.

1. Nella routine di callback per l&#39;elemento dell&#39;interfaccia per il controllo del volume, verificare che il lettore sia in uno stato valido per questo comando.

   >[!TIP]
   >
   >Qualsiasi stato, ad eccezione di RILASCIATO, è valido.

1. Chiamata `setVolume` per impostare il volume audio.

   Ad esempio:

   ```java
   void setVolume(int volume) throws MediaPlayerException;
   ```

   Il valore del volume rappresenta il volume richiesto espresso in percentuale del volume massimo, dove `0` è silenzioso e `1` è il volume massimo
