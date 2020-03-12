---
description: Il server manifesto supporta le didascalie WebVTT abilitate per l'editore per tutti i formati video HLS. Quando riceve richieste di inserimento di annunci nel contenuto con sottotitoli WebVTT, lo fa correttamente.
seo-description: Il server manifesto supporta le didascalie WebVTT abilitate per l'editore per tutti i formati video HLS. Quando riceve richieste di inserimento di annunci nel contenuto con sottotitoli WebVTT, lo fa correttamente.
seo-title: Supporto per le didascalie WebVTT
title: Supporto per le didascalie WebVTT
uuid: 1dc728b0-5aeb-4c48-8f3b-54ff4b135742
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# Supporto per le didascalie WebVTT {#support-for-webvtt-captions}

Il server manifesto supporta le didascalie WebVTT abilitate per l&#39;editore per tutti i formati video HLS. Quando riceve richieste di inserimento di annunci nel contenuto con sottotitoli WebVTT, lo fa correttamente.

Se l&#39;editore include didascalie WebVTT nel contenuto, il server manifesto invia al client un flusso di contenuto con didascalie. WebVTT deve essere abilitato dall&#39;editore affinché il server del manifesto supporti le didascalie. Quando il client dispone di didascalie WebVTT abilitate e invia una richiesta al server manifest, il server manifest modifica la timeline e la traccia WebVTT e restituisce al client il contenuto con annunci e didascalie uniti.

Il flusso di lavoro per i flussi di contenuti VOD è il seguente:

1. Il client invia un flusso di contenuto con le didascalie WebVTT abilitate al server manifesto.
1. Il server manifesto modifica la timeline per unire gli annunci nel flusso di contenuti.
1. Il server manifesto modifica la traccia WebVTT per aggiungere didascalie al contenuto (inclusi gli annunci).
1. Il server manifesto distribuisce il flusso di contenuto al client, con annunci e didascalie inseriti.

>[!NOTE]
>
>Se un segmento di sottotitoli WebVTT si trova all&#39;interno di un annuncio pubblicitario mid-roll, il visualizzatore vede la riproduzione della didascalia prima e dopo tale interruzione di annuncio mid-roll. Ad esempio, in un segmento di sottotitoli di 10 secondi con un annuncio mid-roll di 30 secondi al punto 5 secondi, il visualizzatore vede quel segmento di sottotitoli per 5 secondi prima del mid-roll e per 5 secondi dopo il mid-roll.

>[!NOTE]
>
>Se un client richiede che un video venga riprodotto in una lingua specifica, ad esempio l&#39;inglese, e successivamente richiede di riprodurre il video in francese, il server manifest non è in grado di rilevare che il client ha richiesto di cambiare la lingua in francese. Poiché il client non comunica con il server manifesto, il server manifesto inserisce la didascalia annuncio nel flusso video utilizzando la prima lingua specificata nel file master M3U8 dell&#39;annuncio.