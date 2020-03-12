---
description: Mentre il metodo di cifratura AES-128 codifica l'intero contenitore del flusso di trasporto (TS), comprese le intestazioni, la cifratura SAMPLE-AES codifica solo l'audio e parte dei dati video.
seo-description: Mentre il metodo di cifratura AES-128 codifica l'intero contenitore del flusso di trasporto (TS), comprese le intestazioni, la cifratura SAMPLE-AES codifica solo l'audio e parte dei dati video.
seo-title: Flussi HLS crittografati AES di esempio
title: Flussi HLS crittografati AES di esempio
uuid: 32c1f87b-eb81-4e1c-92ea-ec37260a7ecb
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Flussi HLS crittografati AES di esempio{#sample-aes-encrypted-hls-streams}

Mentre il metodo di cifratura AES-128 codifica l&#39;intero contenitore del flusso di trasporto (TS), comprese le intestazioni, la cifratura SAMPLE-AES codifica solo l&#39;audio e parte dei dati video.

Nei flussi crittografati, viene identificato un blocco protetto su cui viene completato il processo di protezione. I blocchi protetti per video H.264 sono il corpo dei tipi 1 e 5 di unità di livello di adattamento della rete (NAL). Un blocco audio protetto è un fotogramma audio e l&#39;audio deve essere in formato AAC.

>[!IMPORTANT]
>
>È necessario disporre della chiave e del vettore di inizializzazione (IV). Browser TVSDK utilizza la chiave e IV per decrittografare il flusso prima di riprodurlo.

Ogni blocco protetto contiene un numero intero di blocchi a 16 byte cifrati utilizzando la modalità CBC (cifratura a blocchi AES-128) senza riempimento. CBC si verifica in ciascun blocco protetto, e all&#39;inizio di ogni nuovo blocco protetto, il IV deve essere reimpostato sul valore originale.

Sono supportati i seguenti codec:

* Per i video, è supportato H.264.
* Per l&#39;audio, sample-AES è supportato solo per AAC.

