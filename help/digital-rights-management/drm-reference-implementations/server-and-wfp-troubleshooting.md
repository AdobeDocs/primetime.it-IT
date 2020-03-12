---
description: 'null'
seo-description: 'null'
seo-title: Risoluzione dei problemi
title: Risoluzione dei problemi
uuid: 06b86067-1ff6-4b4e-922f-7f968260ba19
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Risoluzione dei problemi{#troubleshooting}

Di seguito sono riportati alcuni problemi e soluzioni che potrebbero verificarsi durante l&#39;implementazione.

* Se viene visualizzato il seguente messaggio di errore:

   ```
   "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
       javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
   ```

   Verificate che la password sia stata crittografata con la `ScrambleUtil` classe.

* Se viene visualizzato il seguente messaggio di errore:

   ```
   "Unable to load credential from file.pfx -- possibly wrong password."
   ```

   Assicurarsi di aver specificato la password crittografata corretta nel file PFX.

* Se viene visualizzato il seguente messaggio di errore:

   ```
   "javax.crypto.BadPaddingException: Given final block not properly padded"
   ```

   Accertatevi di utilizzare la classe di scorrimento password *fornita con l&#39;implementazione* di riferimento. Questa utility è diversa da quella fornita con Adobe Primetime DRM Server for Protected Streaming.

