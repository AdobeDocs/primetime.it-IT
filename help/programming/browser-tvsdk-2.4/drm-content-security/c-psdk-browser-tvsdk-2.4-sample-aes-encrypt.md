---
description: Mentre il metodo di crittografia AES-128 crittografa l'intero contenitore di flussi di trasporto (TS), comprese le intestazioni, la crittografia SAMPLE-AES crittografa solo l'audio e una parte dei dati video.
title: Flussi HLS crittografati AES di esempio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---


# Campione di flussi HLS crittografati AES{#sample-aes-encrypted-hls-streams}

Mentre il metodo di crittografia AES-128 crittografa l&#39;intero contenitore di flussi di trasporto (TS), comprese le intestazioni, la crittografia SAMPLE-AES crittografa solo l&#39;audio e una parte dei dati video.

Nei flussi criptati, viene identificato un blocco protetto su cui viene completato il processo di protezione. I blocchi video protetti H.264 sono il corpo dei tipi 1 e 5 di unità di livello di adattamento della rete (NAL). Un blocco audio protetto è un frame audio e l&#39;audio deve essere in formato AAC.

>[!IMPORTANT]
>
>È necessario disporre della chiave e del vettore di inizializzazione (IV). Il browser TVSDK utilizza la chiave e IV per decrittografare il flusso prima di riprodurlo.

Ogni blocco protetto contiene un numero intero di blocchi a 16 byte crittografati utilizzando la modalità CBC (cifratura blocco-concatenamento) AES-128 senza spaziatura interna. CBC si trova in ciascun blocco protetto e all&#39;inizio di ogni nuovo blocco protetto, il IV deve essere reimpostato sul suo valore originale.

Sono supportati i seguenti codec:

* Per i video, è supportato il formato H.264.
* Per l&#39;audio, sample-AES è supportato solo per AAC.

