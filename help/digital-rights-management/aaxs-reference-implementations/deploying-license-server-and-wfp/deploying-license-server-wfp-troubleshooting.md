---
seo-title: Risoluzione dei problemi
title: Risoluzione dei problemi
uuid: db76d6a4-c285-4d86-95a1-4f1a85ed3743
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
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

   Verificate che la password sia crittografata utilizzando la classe `ScrambleUtil` fornita.

* Se viene visualizzato il seguente errore:

   ```
       "Unable to load credential from file.pfx -- possibly wrong password."
   ```

   Assicurarsi di aver specificato la password crittografata corretta per il file PFX.

* Se viene visualizzato il seguente errore:

   ```
       "javax.crypto.BadPaddingException: Given final block not properly padded"
   ```

   Accertatevi di aver utilizzato la classe per lo scorrimento password fornita con l&#39;implementazione di riferimento (questa utility è diversa da quella fornita con il  Adobe® Access™ Server for Protected Streaming).

