---
title: Risoluzione dei problemi
description: Risoluzione dei problemi
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# Risoluzione dei problemi{#troubleshooting}

Di seguito sono riportati alcuni problemi e soluzioni che potresti riscontrare durante l&#39;implementazione.

* Se viene visualizzato il seguente messaggio di errore:

   ```
   "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
       javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
   ```

   Assicurati che la password sia stata crittografata con la classe `ScrambleUtil` .

* Se viene visualizzato il seguente messaggio di errore:

   ```
   "Unable to load credential from file.pfx -- possibly wrong password."
   ```

   Assicurati di aver specificato la password crittografata corretta nel file PFX.

* Se viene visualizzato il seguente messaggio di errore:

   ```
   "javax.crypto.BadPaddingException: Given final block not properly padded"
   ```

   Assicurati di utilizzare la classe di scrambler della password *fornita con l&#39;implementazione di riferimento*. Questa utility Srambler è diversa da quella fornita con Adobe Primetime DRM Server per lo streaming protetto.

