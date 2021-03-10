---
description: Sostituisci una timeline VOD inviando una nuova richiesta di inserimento di annunci al server manifest con un parametro di query pttimeline opportunamente impostato.
title: Sostituire una timeline VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# Sostituire una timeline VOD {#replace-a-vod-timeline}

Sostituisci una timeline VOD inviando una nuova richiesta di inserimento di annunci al server manifest con un parametro di query pttimeline opportunamente impostato.

1. Prepara una richiesta di inserimento annunci nel modo consueto.
1. Imposta il parametro di query `ptcueformat` su DPIScte35.
1. Imposta il parametro di query `enableC3` su true o false come appropriato.
1. Crea un parametro `pttimeline` utilizzando il formato della timeline VOD:
   1. Specifica ogni blocco di contenuto (capitolo) con `duration = 0` e `number_of_lots = 1`.
   1. Specifica ogni blocco di annunci come di consueto, ma imposta `lots = 0` per rimuovere un’interruzione. Imposta `duration = 0` per utilizzare la durata dell&#39;interruzione pubblicitaria (dal file M3U8).

## Esempio: Sostituzione di una timeline VOD

Questo esempio presuppone che il contenuto VOD sia in `Original.m3u8` con una timeline di `C,120,1;B,60,2,m;C,120,1;B,60,2,m;C,120,1;`

La seguente richiesta del server manifest sostituisce le interruzioni in `Original.m3u8` con un pre-roll di 30 secondi, seguite da due interruzioni di durata di due minuti ciascuna.

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,120,4,m;C,0,1;B,120,4,m;C,0,1;
```

La seguente richiesta del server manifest rimuove le interruzioni in `Original.m3u8` e aggiunge un pre-roll di 30 secondi e un post-roll di 30 secondi.

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,0,0,m;C,0,1;B,0,0,m;C,0,1;B,30,2,t;
```
