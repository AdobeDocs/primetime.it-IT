---
description: Per l'inserimento di annunci in streaming live, potrebbe essere necessario uscire da un'interruzione pubblicitaria prima che tutti gli annunci nell'interruzione siano riprodotti al completamento.
title: Implementazione di un ritorno a capo rapido dell’annuncio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---


# Implementazione di un ritorno a capo rapido dell&#39;annuncio{#implementing-an-early-ad-break-return}

Per l&#39;inserimento di annunci in streaming live, potrebbe essere necessario uscire da un&#39;interruzione pubblicitaria prima che tutti gli annunci nell&#39;interruzione siano riprodotti al completamento.

>[!NOTE]
>
>Devi abbonarti ai marcatori di annunci in uscita/in di congiunzione ( `#EXT-X-CUE-OUT`, `#EXT-X-CUE-IN` e `#EXT-X-CUE`).

Di seguito sono riportati alcuni requisiti da considerare:

* Marcatori di parse, come `EXT-X-CUE-IN` (o tag marker equivalente), che appaiono nei flussi lineari o FER.

   Registra i marcatori come marker per ad early return point. Riproduci solo `adBreaks` fino alla posizione del marcatore durante la riproduzione, che supera la durata del `adBreak` contrassegnato dal marcatore `EXE-X-CUE-OUT` iniziale.

* Se esistono due marcatori `EXT-X-CUE-IN` per lo stesso marcatore `EXT-X-CUE-OUT`, il primo marcatore `EXT-X-CUE-IN` visualizzato è quello che conta.

* Se il marcatore `EXE-X-CUE-IN` viene visualizzato nella timeline senza un marcatore iniziale `EXT-X-CUE-OUT`, il marcatore `EXE-X-CUE-IN` viene scartato.

   In uno streaming live, se il marcatore `EXT-X-CUE-OUT` iniziale è appena stato spostato fuori dalla finestra, il TVSDK non risponderà ad esso.

* Quando si verifica un ritorno anticipato da un&#39;interruzione pubblicitaria, il `adBreak` viene riprodotto fino a quando l&#39;indicatore di riproduzione ritorna nella posizione originale quando l&#39;interruzione pubblicitaria doveva terminare e riprendere a riprodurre il contenuto principale da quella posizione.

## SpliceOut e SpliceIn {#section_36DD55BA58084E21BD3DC039BB245C82}

`SpliceOut` e  `SpliceIn` i marcatori contrassegnano l’inizio e la fine dell’interruzione pubblicitaria. La durata del tipo `SpliceOut` del marcatore `EXE-X-CUE` potrebbe essere zero e il tipo `SpliceIn` del marcatore `EXE-X-CUE` indica la fine dell’interruzione pubblicitaria. Vengono visualizzate in un tag e differiscono per tipo.

**Un marcatore con tipi diversi**

Ad esempio, ecco un marcatore con tipi diversi:

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

In un marcatore con tipi diversi, ad esempio, se la durata del tipo `SpliceOut` è zero, i valori `SpliceOut` e `SpliceIn` devono funzionare insieme per ogni interruzione di annuncio. Al momento, un marcatore `SpliceOut` con una durata diversa da zero e senza la necessità di associare i marcatori `SpliceIn` è più tipico.

**Due marcatori separati**

Lo scenario più tipico è un marcatore `SpliceOut` con una durata diversa da zero e che non necessita dei marcatori di associazione `SpliceIn`. In questo caso, un marcatore di associazione `SpliceIn` indica la fine dell’interruzione pubblicitaria durante la riproduzione dell’interruzione pubblicitaria, ma l’interruzione pubblicitaria viene ridotta alla posizione del marcatore `SpliceIn` e il contenuto principale inizia a essere riprodotto in questa posizione.

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

