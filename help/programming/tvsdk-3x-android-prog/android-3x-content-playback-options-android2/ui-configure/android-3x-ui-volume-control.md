---
description: È possibile impostare un controllo dell'interfaccia utente per regolare il volume del video.
title: Fornire il controllo volume
exl-id: 8b8b0263-9874-4e87-853e-eb394ebef3e3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
