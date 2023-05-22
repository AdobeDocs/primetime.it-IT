---
title: Risoluzione dei problemi
description: Risoluzione dei problemi
copied-description: true
exl-id: 4af7b625-63d3-48b6-98a5-b8894dd0c67f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
