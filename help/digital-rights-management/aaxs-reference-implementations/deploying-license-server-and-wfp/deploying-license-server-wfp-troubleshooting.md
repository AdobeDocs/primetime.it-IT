---
title: Risoluzione dei problemi
description: Risoluzione dei problemi
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---


# Risoluzione dei problemi {#troubleshooting}

Di seguito sono elencati i problemi e le soluzioni comuni per la distribuzione:

* Se viene visualizzato il seguente errore:

   ```
       "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
       javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
   ```

   Assicurati che la password sia crittografata utilizzando la classe `ScrambleUtil` fornita.

* Se viene visualizzato il seguente errore:

   ```
       "Unable to load credential from file.pfx -- possibly wrong password."
   ```

   Assicurati di aver specificato la password crittografata corretta per il file PFX.

* Se viene visualizzato il seguente errore:

   ```
       "javax.crypto.BadPaddingException: Given final block not properly padded"
   ```

   Assicurati di aver utilizzato la classe di scrambler password fornita con l&#39;implementazione di riferimento (questa utility di scrambler è diversa da quella fornita con Adobe® Access™ Server for Protected Streaming).

