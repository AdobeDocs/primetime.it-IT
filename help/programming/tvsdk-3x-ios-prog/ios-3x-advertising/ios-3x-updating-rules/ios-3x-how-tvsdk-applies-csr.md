---
keywords: regole di selezione creativa;AdobeTVSDKConfig
title: Applicare regole di selezione creative
description: Applicare regole di selezione creative
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# Applicare regole di selezione creative {#apply-creative-selection-rules}

TVSDK applica le regole di selezione creativa nei seguenti modi:

* TVSDK applica tutto `default` prima le regole, quindi le regole specifiche per la zona.
* TVSDK ignora le regole non definite per l&#39;ID di zona corrente.
* Una volta che TVSDK applica le regole predefinite, le regole specifiche per zona possono modificare ulteriormente le priorità creative in base al `host` (dominio) corrisponde al contenuto creativo selezionato da `default` regole.

* Nel file di regole di esempio incluso con regole di zona aggiuntive, una volta che TVSDK applica `default` regole, se il dominio creativo M3U8 non contiene [!DNL my.domain.com] o [!DNL a.bcd.com] e la zona dell’annuncio è `1234`, i creativi vengono riordinati e la creatività VPAID del Flash viene riprodotta per prima, se disponibile. In caso contrario, viene riprodotto un annuncio MP4 e così via fino a JavaScript.

* Se è selezionato un annuncio creativo che TVSDK non può riprodurre in modalità nativa ( [!DNL .mp4], [!DNL .flv], ecc.), TVSDK invia una richiesta di riconfezionamento.

Tieni presente che i tipi di annunci che possono essere gestiti da TVSDK sono ancora definiti tramite `validMimeTypes` impostazione in `AuditudeSettings`.
