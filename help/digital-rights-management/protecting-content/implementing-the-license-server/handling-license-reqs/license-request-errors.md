---
seo-title: Gestione degli errori della richiesta di licenza
title: Gestione degli errori della richiesta di licenza
uuid: 4563f546-77fe-4fb9-9ad8-a0689fe6fb4d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# Gestione degli errori della richiesta di licenza {#license-request-error-handling}

Se si verifica un errore durante l&#39;analisi della richiesta, si verifica un `HandlerParsingException`. Questa eccezione include informazioni di errore restituite al client. Per recuperare le informazioni sull&#39;errore, è necessario chiamare `HandlerParsingException.getErrorData()`. Se si verifica un errore durante la generazione di una licenza a causa di requisiti di criteri DRM non soddisfatti, si verifica un `PolicyEvaluationException`. Questa eccezione include anche `ErrorData` da restituire al client.

Consultate la documentazione API per `LicenseRequestMessage.generateLicense()` per informazioni dettagliate sulla valutazione dei criteri DRM durante la generazione della licenza.
