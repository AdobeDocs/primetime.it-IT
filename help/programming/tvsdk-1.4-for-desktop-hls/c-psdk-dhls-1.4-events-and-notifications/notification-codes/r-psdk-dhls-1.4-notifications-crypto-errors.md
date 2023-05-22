---
description: Il modulo di crittografia del motore video Adobe restituisce queste notifiche nell'oggetto metadati NATIVE_ERROR.
title: Valori di crittografia NATIVE_ERROR
exl-id: c14b35c1-ed91-4a44-b826-fd6a05dbe345
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 8%

---

# NATIVE_ERROR: Crittografia dei valori{#native-error-crypto-values}

Il modulo di crittografia del motore video Adobe restituisce queste notifiche nell&#39;oggetto metadati NATIVE_ERROR.

| Valore per la chiave dei metadati RUNTIME_CODE | Valore per la chiave dei metadati RUNTIME_CODE_MESSAGE | Significato |
|---|---|---|
| 300 | `CRYPTO_ALGORITHM_NOT_SUPPORTED` | L’algoritmo in uso non è supportato. |
| 301 | `CRYPTO_ERROR_CORRUPTED_DATA` | Dati danneggiati. |
| 302 | `CRYPTO_ERROR_BUFFER_TOO_SMALL` | Buffer troppo piccolo. |
| 303 | `CRYPTO_ERROR_BAD_CERTIFICATE` | Certificato non valido. |
| 304 | `CRYPTO_ERROR_DIGEST_UPDATE` | Aggiornamento digest. |
| 305 | `CRYPTO_ERROR_DIGEST_FINISH` | Fine digest. |
| 306 | `CRYPTO_ERROR_BAD_PARAMETER` | Parametro non valido. |
