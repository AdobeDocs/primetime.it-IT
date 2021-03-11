---
description: Il server manifest supporta le didascalie WebVTT abilitate all'editore per tutti i formati video HLS. Quando riceve richieste di inserimento di annunci nel contenuto con sottotitoli WebVTT, lo fa correttamente.
title: Supporto per le didascalie WebVTT
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---


# Supporto per le didascalie WebVTT {#support-for-webvtt-captions}

Il server manifest supporta i sottotitoli WebVTT abilitati per l&#39;editore per i formati video HLS/DASH. Quando riceve richieste di inserimento di annunci nel contenuto con sottotitoli WebVTT, lo fa correttamente.

Se l’editore include didascalie WebVTT nel contenuto, il server manifest invia al client un flusso di contenuto con didascalie. WebVTT deve essere abilitato dall&#39;editore affinché il server manifest supporti le didascalie. Quando il client dispone di didascalie WebVTT abilitate e invia una richiesta al server manifest, il server manifest manipola la timeline e la traccia WebVTT e restituisce al client il contenuto con annunci e didascalie uniti.

Il flusso di lavoro per i flussi di contenuto VOD è il seguente:

1. Il client invia un flusso di contenuto con le didascalie WebVTT abilitate al server manifest.
1. Il server manifest manipola la timeline per unire gli annunci nel flusso di contenuto.
1. Il server manifest manipola la traccia WebVTT per aggiungere didascalie al contenuto (inclusi gli annunci).
1. Il server manifest consegna il flusso di contenuto al client, con annunci e didascalie inseriti.

>[!NOTE]
>
>Se un segmento di didascalia WebVTT si trova all’interno di un annuncio a scorrimento medio, il visualizzatore visualizza la didascalia prima e dopo l’interruzione dell’annuncio a scorrimento medio. Ad esempio, in un segmento di sottotitoli di 10 secondi con un annuncio mid-roll di 30 secondi a 5 secondi, il visualizzatore vede quel segmento di sottotitoli per 5 secondi prima dell’interruzione pubblicitaria mid-roll e per 5 secondi dopo il mid-roll.

>[!NOTE]
>
>Se un client richiede che un video venga riprodotto in una lingua specifica come l&#39;inglese e poi richiede di riprodurre il video in francese, il server manifest non è in grado di rilevare che il client ha richiesto di cambiare la lingua in francese. Poiché il client non comunica con il server manifest, il server manifest inserisce la didascalia dell&#39;annuncio nel flusso video utilizzando la prima lingua specificata nel file master M3U8 dell&#39;annuncio.
