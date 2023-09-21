---
title: Risoluzione dei problemi
description: Risoluzione dei problemi
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# Risoluzione dei problemi {#troubleshooting}

Di seguito sono elencati i problemi comuni e le soluzioni per la distribuzione:

* Se viene visualizzato il seguente errore:

  ```
      "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
      javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
  ```

  Assicurati che la password sia crittografata utilizzando il fornito `ScrambleUtil` classe.

* Se viene visualizzato il seguente errore:

  ```
      "Unable to load credential from file.pfx -- possibly wrong password."
  ```

  Assicurarsi di aver specificato la password crittografata corretta per il file PFX.

* Se viene visualizzato il seguente errore:

  ```
      "javax.crypto.BadPaddingException: Given final block not properly padded"
  ```

  Assicurarsi di aver utilizzato la classe scrambler password fornita con l&#39;implementazione di riferimento (questa utility scrambler è diversa da quella fornita con l&#39;Adobe ® Access™ Server for Protected Streaming).
