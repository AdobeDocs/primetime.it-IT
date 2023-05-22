---
description: Per l’inserimento di annunci in streaming live, potrebbe essere necessario uscire da un’interruzione pubblicitaria prima che tutti gli annunci dell’interruzione vengano riprodotti fino al completamento.
title: Implementazione di un ritorno a inizio annuncio
exl-id: 584e870e-1408-41a9-bb6f-e82b921fe99e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# Implementazione di un ritorno a inizio annuncio{#implementing-an-early-ad-break-return}

Per l’inserimento di annunci in streaming live, potrebbe essere necessario uscire da un’interruzione pubblicitaria prima che tutti gli annunci dell’interruzione vengano riprodotti fino al completamento.

>[!NOTE]
>
>Devi iscriverti ai marcatori degli annunci out/in del giunto ( `#EXT-X-CUE-OUT`, `#EXT-X-CUE-IN`, e `#EXT-X-CUE`).

Di seguito sono riportati alcuni requisiti da considerare:

* Analizzare marcatori quali `EXT-X-CUE-IN` (o tag di marker equivalente) che appaiono nei flussi lineari o FER.

   Registrate i marcatori come marcatori per il punto di ritorno iniziale dell&#39;annuncio. Solo riproduzione `adBreaks` fino a questa posizione del marcatore durante la riproduzione, che sostituisce la durata del `adBreak` contrassegnato dall&#39;interlinea `EXE-X-CUE-OUT` marcatore.

* Se due `EXT-X-CUE-IN` esistono marcatori per lo stesso `EXT-X-CUE-OUT` marcatore, il primo `EXT-X-CUE-IN` l&#39;indicatore visualizzato è quello che conta.

* Se il `EXE-X-CUE-IN` il marcatore viene visualizzato nella timeline senza interlinea `EXT-X-CUE-OUT` marcatore, il `EXE-X-CUE-IN` il marcatore viene eliminato.

   In un flusso live, se l&#39;interlinea `EXT-X-CUE-OUT` il marcatore è appena stato spostato fuori dalla finestra, il TVSDK non risponderà.

* Quando si verifica un ritorno anticipato da un’interruzione pubblicitaria, il `adBreak` viene riprodotto finché l’indicatore di riproduzione non ritorna nella posizione originale quando l’interruzione pubblicitaria doveva terminare e riprende la riproduzione del contenuto principale da tale posizione.

## Splice Out e SpliceIn {#section_36DD55BA58084E21BD3DC039BB245C82}

`SpliceOut` e `SpliceIn` i marcatori contrassegnano l’inizio e la fine dell’interruzione pubblicitaria. La durata del `SpliceOut` tipo di `EXE-X-CUE` il marcatore potrebbe essere zero e il `SpliceIn` tipo di `EXE-X-CUE` marcatore indica la fine dell’interruzione pubblicitaria. Vengono visualizzate in un tag e si differenziano per tipo.

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

Nell&#39;esempio di un marcatore con tipi diversi, se la durata del `SpliceOut` il tipo è zero, il `SpliceOut` e `SpliceIn` deve lavorare insieme per ogni interruzione pubblicitaria. Attualmente, un `SpliceOut` marcatore con durata diversa da zero e non richiede accoppiamento `SpliceIn` i marcatori sono più tipici.

**Due marcatori separati**

Lo scenario più tipico è un `SpliceOut` marcatore con durata diversa da zero e che non necessita dell&#39;associazione `SpliceIn` marcatori. Qui, un accoppiamento `SpliceIn` contrassegna la fine dell’interruzione pubblicitaria durante la riproduzione dell’interruzione pubblicitaria, ma l’interruzione pubblicitaria viene interrotta in corrispondenza del `SpliceIn` posizione del marcatore e il contenuto principale inizia la riproduzione da questa posizione.

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
