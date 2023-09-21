---
title: Gestione degli errori nelle richieste di licenza
description: Gestione degli errori nelle richieste di licenza
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# Gestione degli errori nelle richieste di licenza {#license-request-error-handling}

Se si verifica un errore durante l’analisi della richiesta, viene `HandlerParsingException` si verifica. Questa eccezione include informazioni sull&#39;errore restituite al client. Se devi recuperare le informazioni di errore, devi chiamare `HandlerParsingException.getErrorData()`. Se durante la generazione di una licenza si verifica un errore a causa di requisiti delle regole DRM non soddisfatti, `PolicyEvaluationException` si verifica. Questa eccezione include anche `ErrorData` da restituire al client.

Consulta la documentazione API per `LicenseRequestMessage.generateLicense()` per informazioni dettagliate sulla valutazione dei criteri DRM durante la generazione della licenza.
