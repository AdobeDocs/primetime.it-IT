---
description: Mentre il metodo di crittografia AES-128 crittografa l’intero contenitore del flusso di trasporto (TS), incluse le intestazioni, la crittografia SAMPLE-AES crittografa solo l’audio e parte dei dati video.
title: Esempio di flussi HLS crittografati AES
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# Esempio di flussi HLS crittografati AES{#sample-aes-encrypted-hls-streams}

Mentre il metodo di crittografia AES-128 crittografa l’intero contenitore del flusso di trasporto (TS), incluse le intestazioni, la crittografia SAMPLE-AES crittografa solo l’audio e parte dei dati video.

Nei flussi crittografati, viene identificato un blocco protetto su cui viene completato il processo di protezione. I blocchi video protetti da H.264 sono costituiti dal corpo dei tipi 1 e 5 di unità NAL (Network Adapter Layer). Un blocco protetto di audio è un frame audio e l&#39;audio deve essere in formato AAC.

>[!IMPORTANT]
>
>È necessario disporre della chiave e del vettore di inizializzazione (IV). Il browser TVSDK utilizza la chiave e IV per decrittografare il flusso prima di riprodurlo.

Ogni blocco protetto contiene un numero intero di blocchi a 16 byte crittografati utilizzando la modalità CBC (cipher block-chaining) di AES-128 senza spaziatura interna. CBC si verifica in ogni blocco protetto e all&#39;inizio di ogni nuovo blocco protetto, il IV deve essere reimpostato al suo valore originale.

Sono supportati i seguenti codec:

* Per i video, è supportato il formato H.264.
* Per l&#39;audio, sample-AES è supportato solo per AAC.
