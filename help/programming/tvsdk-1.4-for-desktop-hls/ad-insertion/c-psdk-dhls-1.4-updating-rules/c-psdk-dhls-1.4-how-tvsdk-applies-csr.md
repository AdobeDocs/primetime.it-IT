---
title: Applicazione delle regole di selezione creativa
description: Applicazione delle regole di selezione creativa
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---


# Applicazione delle regole di selezione creativa{#applying-creative-selection-rules}

TVSDK applica le regole di selezione creativa nei seguenti modi:

* TVSDK applica prima tutte le regole `default` , seguite dalle regole specifiche per la zona.
* TVSDK ignora eventuali regole non definite per l’ID di zona corrente.
* Una volta che TVSDK applica le regole predefinite, le regole specifiche per la zona possono modificare ulteriormente le priorità creative in base alle corrispondenze `host` (dominio) in base alla creatività selezionata dalle regole `default` .

* Nel file di regole di esempio incluso con regole di zona aggiuntive, una volta che TVSDK applica le regole `default`, se il dominio creativo M3U8 non contiene [!DNL my.domain.com] o [!DNL a.bcd.com] e la zona annunci è `1234`, le creatività vengono riordinate e il creativo VPAID Flash viene riprodotto per primo, se disponibile. Altrimenti viene riprodotto un annuncio MP4 e così via fino a JavaScript.

* Se è selezionata una creativa pubblicitaria che non può essere riprodotta in modo nativo da TVSDK ( [!DNL .mp4], [!DNL .flv], ecc.), TVSDK invia una richiesta di riconfezionamento.

I tipi di annunci che possono essere gestiti da TVSDK sono ancora definiti tramite l&#39;impostazione `validMimeTypes` in `AuditudeSettings`.
