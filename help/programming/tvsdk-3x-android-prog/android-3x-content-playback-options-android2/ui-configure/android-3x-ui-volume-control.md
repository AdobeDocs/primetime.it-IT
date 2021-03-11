---
description: È possibile impostare un controllo dell'interfaccia utente per regolare il volume del video.
title: Controllo del volume
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 2%

---


# Controllo del volume {#provide-volume-control}

È possibile impostare un controllo dell&#39;interfaccia utente per regolare il volume del video.

1. Nella routine di callback per l&#39;elemento dell&#39;interfaccia di controllo del volume, assicurati che il lettore sia in uno stato valido per questo comando.

   >[!TIP]
   >
   >Qualsiasi stato, ad eccezione di RELEASED, è valido.

1. Chiama `setVolume` per impostare il volume audio.

   Ad esempio:

   ```java
   void setVolume(int volume) throws MediaPlayerException;
   ```

   Il valore per il volume rappresenta il volume richiesto espresso in proporzione al volume massimo, dove `0` è silenzioso e `1` è il volume massimo.