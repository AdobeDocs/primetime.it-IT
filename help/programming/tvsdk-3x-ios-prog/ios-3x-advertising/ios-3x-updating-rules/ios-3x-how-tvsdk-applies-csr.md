---
description: 'null'
keywords: creative selection rules;AdobeTVSDKConfig
seo-description: 'null'
seo-title: Applica regole di selezione creative
title: Applica regole di selezione creative
uuid: 2f009776-201c-418e-aa8f-cb409d0046d8
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# Applica regole di selezione creativa {#apply-creative-selection-rules}

TVSDK applica le regole di selezione creativa nei seguenti modi:

* TVSDK applica prima tutte le regole `default`, seguite dalle regole specifiche per la zona.
* TVSDK ignora eventuali regole non definite per l&#39;ID di zona corrente.
* Una volta che TVSDK applica le regole predefinite, le regole specifiche per la zona possono cambiare ulteriormente le priorità creative in base alle corrispondenze `host` (dominio) sulla creatività selezionata dalle regole `default`.

* Nel file di regole di area di esempio incluso con regole di area aggiuntive, una volta che TVSDK applica le regole `default`, se il dominio creativo M3U8 non contiene [!DNL my.domain.com] o [!DNL a.bcd.com] e l&#39;area annunci è `1234`, le creatività vengono riordinate e il creativo VPAID Flash viene riprodotto per primo, se disponibile. In caso contrario viene riprodotto un annuncio MP4 e così via fino a JavaScript.

* Se è selezionato un annuncio creativo per il quale TVSDK non può essere riprodotto in modo nativo ( [!DNL .mp4], [!DNL .flv], ecc.), TVSDK invia una richiesta di ricompilazione.

I tipi di annunci che possono essere gestiti da TVSDK sono ancora definiti tramite l&#39;impostazione `validMimeTypes` in `AuditudeSettings`.