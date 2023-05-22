---
description: Utilizzando i marcatori di annunci personalizzati, puoi contrassegnare sezioni specifiche del contenuto principale come periodi di contenuto relativi agli annunci.
title: Aggiungere marcatori annuncio personalizzati
exl-id: f60d3b1e-42e8-40ca-a35c-300d1a580ece
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# Panoramica {#add-custom-ad-markers-overview}

Utilizzando i marcatori di annunci personalizzati, puoi contrassegnare sezioni specifiche del contenuto principale come periodi di contenuto relativi agli annunci.

Questa funzione è particolarmente utile quando il contenuto viene registrato, ad esempio, da un evento live, e il risultato della registrazione è un flusso HLS. La registrazione contiene il contenuto principale e i contenuti relativi alla pubblicità in un unico flusso video-on-demand (VOD) HLS. Il processo di registrazione non tiene traccia dei segmenti relativi agli annunci, pertanto le informazioni relative al posizionamento degli annunci nel contenuto principale andranno perse.

Potresti essere in grado di ottenere le informazioni relative al posizionamento dei periodi di contenuto degli annunci da altre origini fuori banda, ad esempio sistemi CMS esterni. È possibile definire marcatori personalizzati, attraverso i quali queste informazioni fuori banda possono essere trasmesse al sottosistema di gestione della timeline. L’intenzione è quella di contrassegnare le sezioni di contenuto che corrispondono al contenuto specifico dell’annuncio in modo che tutti gli eventi di riproduzione specifici dell’annuncio vengano attivati nello stesso modo in cui si attivano se questi periodi di annuncio personalizzati sono stati esplicitamente posizionati sulla timeline del lettore.

Il tracciamento degli annunci non viene gestito internamente da TVSDK, ad esempio quando gli annunci vengono risolti da Adobe Primetime ad decisioning. Tuttavia, TVSDK fornisce le seguenti astrazioni che definiscono il modo in cui il contenuto relativo agli annunci viene rappresentato nella timeline:

* L’interruzione pubblicitaria

   Un’interruzione pubblicitaria è un elenco ordinato di singoli annunci consecutivi.
* Un singolo annuncio

Gli eventi di riproduzione vengono attivati separatamente per le interruzioni e gli annunci all’inizio e alla fine di ogni annuncio.

TVSDK invia eventi di tracciamento e-mail all’applicazione per consentirti di implementare una logica di tracciamento personalizzata. Se imposti marcatori annuncio personalizzati, riceverai `onAdBreakStart`, `onAdStart`, `onAdProgress`, `onAdComplete`, e `onAdBreakComplete` eventi.
