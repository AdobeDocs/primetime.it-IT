---
description: Il server manifest supporta i sottotitoli WebVTT abilitati per gli editori per tutti i formati video HLS. Quando riceve richieste di inserimento di annunci nel contenuto con didascalie WebVTT, lo fa correttamente.
title: Supporto per i sottotitoli WebVTT
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---


# Supporto per i sottotitoli WebVTT {#support-for-webvtt-captions}

Il server manifest supporta i sottotitoli WebVTT abilitati per l&#39;autore per i formati video HLS/DASH. Quando riceve richieste di inserimento di annunci nel contenuto con didascalie WebVTT, lo fa correttamente.

Se l&#39;editore include sottotitoli WebVTT nel contenuto, il server manifest invia al client un flusso di contenuto con sottotitoli. WebVTT deve essere abilitato dall&#39;editore affinché il server manifesto supporti i sottotitoli. Quando il client ha abilitato i sottotitoli WebVTT e invia una richiesta al server manifest, quest&#39;ultimo modifica la timeline e la traccia WebVTT e restituisce al client il contenuto con annunci e sottotitoli uniti.

Il flusso di lavoro per i flussi di contenuto VOD è il seguente:

1. Il client invia al server manifesto un flusso di contenuto con sottotitoli WebVTT abilitati.
1. Il server manifest modifica la timeline per unire gli annunci nel flusso di contenuto.
1. Il server manifest modifica il brano WebVTT per aggiungere didascalie al contenuto (inclusi gli annunci).
1. Il server manifest distribuisce il flusso di contenuto al client, con annunci e didascalie inseriti.

>[!NOTE]
>
>Se un segmento di didascalia WebVTT rientra in un annuncio mid-roll, il visualizzatore visualizza la didascalia prima e dopo l’interruzione pubblicitaria mid-roll. Ad esempio, in un segmento di sottotitoli di 10 secondi con un annuncio mid-roll di 30 secondi al punto di 5 secondi, il visualizzatore visualizza tale segmento di sottotitoli per 5 secondi prima dell’interruzione pubblicitaria mid-roll e per 5 secondi dopo il mid-roll.

>[!NOTE]
>
>Se un client richiede che un video venga riprodotto in una lingua specifica, ad esempio l&#39;inglese, e poi richiede di riprodurre il video in francese, il server manifest non è in grado di rilevare che il client ha richiesto di cambiare la lingua in francese. Poiché il client non comunica con il server manifesto, il server manifesto inserisce la didascalia dell&#39;annuncio nel flusso video utilizzando la prima lingua specificata nel file master M3U8 dell&#39;annuncio.
