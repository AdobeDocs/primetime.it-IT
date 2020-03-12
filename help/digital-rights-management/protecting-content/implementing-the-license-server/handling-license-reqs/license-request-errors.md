---
seo-title: Gestione degli errori della richiesta di licenza
title: Gestione degli errori della richiesta di licenza
uuid: 4563f546-77fe-4fb9-9ad8-a0689fe6fb4d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Gestione degli errori della richiesta di licenza {#license-request-error-handling}

Se si verifica un errore durante l&#39;analisi della richiesta, `HandlerParsingException` si verifica un errore. Questa eccezione include informazioni di errore restituite al client. Se devi recuperare le informazioni sull&#39;errore, devi chiamare `HandlerParsingException.getErrorData()`. Se si verifica un errore durante la generazione di una licenza a causa di requisiti di criteri DRM non soddisfatti, `PolicyEvaluationException` si verifica un errore. Questa eccezione include anche `ErrorData` la restituzione al client.

Consultate la documentazione API per `LicenseRequestMessage.generateLicense()` informazioni dettagliate sulla valutazione dei criteri DRM durante la generazione della licenza.
