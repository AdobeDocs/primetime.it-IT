---
description: Sostituisci una timeline VOD inviando una nuova richiesta di inserimento di annunci al server manifest con un parametro di query della cronologia impostato correttamente.
seo-description: Sostituisci una timeline VOD inviando una nuova richiesta di inserimento di annunci al server manifest con un parametro di query della cronologia impostato correttamente.
seo-title: Sostituire una timeline VOD
title: Sostituire una timeline VOD
uuid: 17a6daa3-5ee5-48fb-8981-0d183aed0fe4
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---


# Sostituire una timeline VOD {#replace-a-vod-timeline}

Sostituisci una timeline VOD inviando una nuova richiesta di inserimento di annunci al server manifest con un parametro di query della cronologia impostato correttamente.

1. Prepara una richiesta di inserimento di annunci secondo le modalità usuali.
1. Impostate il parametro di query `ptcueformat` su DPIScte35.
1. Impostate il parametro di query `enableC3` su true o false a seconda dei casi.
1. Create un parametro `pttimeline` utilizzando il formato della timeline VOD:
   1. Specificate ciascun blocco di contenuto (capitolo) con `duration = 0` e `number_of_lots = 1`.
   1. Specificate ogni blocco di annunci come al solito, ma impostate `lots = 0` per rimuovere un&#39;interruzione. Impostate `duration = 0` per utilizzare la durata dell&#39;interruzione dell&#39;annuncio (dal file M3U8).

## Esempio: Sostituzione di una timeline VOD

Questo esempio presuppone che il contenuto VOD sia in `Original.m3u8` con una timeline di `C,120,1;B,60,2,m;C,120,1;B,60,2,m;C,120,1;`

La seguente richiesta del server di manifesto sostituisce le interruzioni in `Original.m3u8` con un pre-roll di 30 secondi, seguita da due interruzioni di durata di due minuti ciascuna.

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,120,4,m;C,0,1;B,120,4,m;C,0,1;
```

La seguente richiesta del server di manifesto rimuove le interruzioni in `Original.m3u8` e aggiunge un pre-roll di 30 secondi e un post-roll di 30 secondi.

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,0,0,m;C,0,1;B,0,0,m;C,0,1;B,30,2,t;
```
