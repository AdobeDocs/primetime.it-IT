---
description: 'null'
keywords: creative selection rules;AdobeTVSDKConfig
seo-description: 'null'
seo-title: Applica regole di selezione creative
title: Applica regole di selezione creative
uuid: 75109483-ea60-43a8-92e7-4bcba48986bc
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Applica regole di selezione creative {#apply-creative-selection-rules}

TVSDK applica le regole di selezione creativa nei seguenti modi:

* TVSDK applica prima tutte `default` le regole, seguite da quelle specifiche per la zona.
* TVSDK ignora eventuali regole non definite per l&#39;ID di zona corrente.
* Una volta che TVSDK applica le regole predefinite, le regole specifiche per la zona possono cambiare ulteriormente le priorità creative in base alle corrispondenze `host` (dominio) in base alla creatività selezionata dalle `default` regole.

* Nel file delle regole di area di esempio incluso con regole di area aggiuntive, una volta che TVSDK applica le `default` regole, se il dominio creativo M3U8 non contiene [!DNL my.domain.com] o [!DNL a.bcd.com] e l&#39;area degli annunci è `1234`, le creatività vengono riordinate e il creativo Flash VPAID viene riprodotto per primo, se disponibile. In caso contrario viene riprodotto un annuncio MP4 e così via fino a JavaScript.

* Se viene selezionato un annuncio creativo per il quale TVSDK non può essere riprodotto in modo nativo ( [!DNL .mp4], [!DNL .flv]ecc.), TVSDK invia una richiesta di ricompilazione.

I tipi di annunci che possono essere gestiti da TVSDK sono ancora definiti tramite l&#39; `validMimeTypes` impostazione in `AuditudeSettings`.

<!-- 

In Android 2.5 API docs, I see a 
<span class="codeph"> setValidMimeTypes</span> but not a 
<span class="codeph"> getValidMimeTypes</span>.

 -->

