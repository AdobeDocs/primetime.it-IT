---
description: Per l'inserimento di annunci in streaming dal vivo, potrebbe essere necessario uscire da un'interruzione di annuncio prima che tutti gli annunci nell'interruzione siano riprodotti al completamento.
seo-description: Per l'inserimento di annunci in streaming dal vivo, potrebbe essere necessario uscire da un'interruzione di annuncio prima che tutti gli annunci nell'interruzione siano riprodotti al completamento.
seo-title: Implementazione di un ritorno rapido all'interruzione dell'annuncio
title: Implementazione di un ritorno rapido all'interruzione dell'annuncio
uuid: 984b6ed0-c929-49a3-9553-e30d1a7758ed
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---


# Implementazione di un ritorno iniziale all&#39;interruzione dell&#39;annuncio{#implementing-an-early-ad-break-return}

Per l&#39;inserimento di annunci in streaming dal vivo, potrebbe essere necessario uscire da un&#39;interruzione di annuncio prima che tutti gli annunci nell&#39;interruzione siano riprodotti al completamento.

>[!NOTE]
>
>È necessario abbonarsi ai marcatori di annunci in uscita/in di giunzione ( `#EXT-X-CUE-OUT`, `#EXT-X-CUE-IN` e `#EXT-X-CUE`).

Di seguito sono riportati alcuni requisiti da tenere in considerazione:

* Parse marker come `EXT-X-CUE-IN` (o tag marker equivalente) che appaiono nei flussi lineari o FER.

   Registra i marcatori come marcatore per un punto di ritorno iniziale. Riproduci solo `adBreaks` fino alla posizione del marcatore durante la riproduzione, che supera la durata del `adBreak` contrassegnato dal marcatore `EXE-X-CUE-OUT` iniziale.

* Se esistono due `EXT-X-CUE-IN` marcatori per lo stesso marcatore `EXT-X-CUE-OUT`, il primo marcatore `EXT-X-CUE-IN` visualizzato è quello che conta.

* Se il marcatore `EXE-X-CUE-IN` viene visualizzato nella timeline senza un marcatore `EXT-X-CUE-OUT` iniziale, il marcatore `EXE-X-CUE-IN` viene eliminato.

   In uno streaming live, se il marcatore `EXT-X-CUE-OUT` iniziale è appena stato spostato fuori dalla finestra, TVSDK non risponderà.

* Quando si verifica un ritorno anticipato da un&#39;interruzione pubblicitaria, la riproduzione `adBreak` viene riprodotta fino al ritorno dell&#39;indicatore di riproduzione nella posizione originale quando l&#39;interruzione dell&#39;annuncio doveva terminare e riprendere la riproduzione del contenuto principale da tale posizione.

## SpliceOut e SpliceIn {#section_36DD55BA58084E21BD3DC039BB245C82}

`SpliceOut` e  `SpliceIn` i marcatori indicano l’inizio e la fine dell’interruzione dell’annuncio. La durata del tipo `SpliceOut` del marcatore `EXE-X-CUE` potrebbe essere zero e il tipo `SpliceIn` del marcatore `EXE-X-CUE` indica la fine dell&#39;interruzione dell&#39;annuncio. Vengono visualizzati in un tag e differiscono per tipo.

**Un marcatore con diversi tipi**

Ad esempio, di seguito è riportato un marcatore con diversi tipi:

```
#EXTM3U#EXT-X-TARGETDURATION:10
#EXT-X-VERSION:3
#EXT-X-MEDIA-SEQUENCE:44
  
#EXTINF:9.9,
https://server-host/path/file44.ts
#EXTINF:4.2,
https://server-host/path/file45.ts
  
#EXT-X-CUE:TYPE="SpliceOut",ID="1",DURATION="0",TIME="266.198",PROGRAM-ID="138",AVAIL-NUM="1",AVAILS-EXPECTED="10"
#EXTINF:5.8,
https://server-host/path/file46.ts
#EXTINF:9.9,
https://server-host/path/file47.ts
...
#EXTINF:9.9,
https://server-host/path/file56.ts
#EXTINF:4.2,
https://server-host/path/file57.ts
#EXT-X-CUE:TYPE="SpliceIn",ID="1",DURATION="0",TIME="266.198",PROGRAM-ID="138"
#EXTINF:9.9,
https://server-host/path/file58.ts
```

In un unico marcatore con tipi diversi, ad esempio, se la durata del tipo `SpliceOut` è zero, `SpliceOut` e `SpliceIn` devono funzionare insieme per ogni interruzione di annuncio. Attualmente, un marcatore `SpliceOut` con una durata diversa da zero e non richiede l&#39;associazione di marcatori `SpliceIn` è più tipico.

**Due marcatori separati**

Lo scenario più tipico è un marcatore `SpliceOut` con una durata diversa da zero e che non necessita dei marcatori di accoppiamento `SpliceIn`. In questo caso, un indicatore di associazione `SpliceIn` indica la fine dell&#39;interruzione dell&#39;annuncio durante la riproduzione dell&#39;interruzione dell&#39;annuncio, ma l&#39;interruzione dell&#39;annuncio viene ridotta in corrispondenza della posizione del marcatore `SpliceIn` e il contenuto principale inizia a essere riprodotto in questa posizione.

Ad esempio, di seguito sono riportati due marcatori separati:

```
#EXT-X-CUE-OUT:ID=105,DURATION=30.0,TIME=1081.08
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589090425811,format=m3u8-aapl-v4)
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589150485811,format=m3u8-aapl-v4)
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589210545811,format=m3u8-aapl-v4)
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589270605811,format=m3u8-aapl-v4)
#EXT-X-CUE-IN:ID=105,TIME=1105.104
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589330665811,format=m3u8-aapl-v4)
```

