---
title: Gestione degli errori della richiesta di licenza
description: Gestione degli errori della richiesta di licenza
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# Gestione degli errori della richiesta di licenza {#license-request-error-handling}

Se si verifica un errore durante l&#39;analisi della richiesta, si verifica un `HandlerParsingException`. Questa eccezione include informazioni di errore restituite al client. Se devi recuperare le informazioni sull’errore, devi chiamare `HandlerParsingException.getErrorData()`. Se si verifica un errore durante la generazione di una licenza a causa di requisiti di policy DRM non soddisfatti, si verifica un `PolicyEvaluationException`. Questa eccezione include anche `ErrorData` da restituire al client.

Per informazioni dettagliate su come valutare i criteri DRM durante la generazione della licenza, consulta la documentazione API per `LicenseRequestMessage.generateLicense()` .
