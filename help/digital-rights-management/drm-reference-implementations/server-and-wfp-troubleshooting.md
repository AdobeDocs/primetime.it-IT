---
title: Risoluzione dei problemi
description: Risoluzione dei problemi
copied-description: true
exl-id: 6c4f15b6-507e-496e-ad1c-702ce77dd069
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# Risoluzione dei problemi{#troubleshooting}

Di seguito sono riportati alcuni problemi e soluzioni che possono verificarsi durante la distribuzione.

* Se viene visualizzato il seguente messaggio di errore:

   ```
   "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
       javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
   ```

   Verificare che la password sia stata crittografata con `ScrambleUtil` classe.

* Se viene visualizzato il seguente messaggio di errore:

   ```
   "Unable to load credential from file.pfx -- possibly wrong password."
   ```

   Verificare di aver specificato la password crittografata corretta nel file PFX.

* Se viene visualizzato il seguente messaggio di errore:

   ```
   "javax.crypto.BadPaddingException: Given final block not properly padded"
   ```

   Assicurati di utilizzare la classe di scrambler delle password *che è stato fornito con l’implementazione di riferimento*. Questa utility di scrambler è diversa da quella fornita con Adobe Primetime DRM Server for Protected Streaming.
