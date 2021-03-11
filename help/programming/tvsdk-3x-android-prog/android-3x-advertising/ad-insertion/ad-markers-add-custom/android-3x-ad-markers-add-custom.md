---
description: Utilizzando marcatori di annunci personalizzati, puoi contrassegnare sezioni specifiche del contenuto principale come periodi di contenuto relativi agli annunci.
title: Aggiungi marcatori di annunci personalizzati
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# Panoramica {#add-custom-ad-markers-overview}

Utilizzando marcatori di annunci personalizzati, puoi contrassegnare sezioni specifiche del contenuto principale come periodi di contenuto relativi agli annunci.

Questa funzione è particolarmente utile quando il contenuto viene registrato, ad esempio, da un evento live e il risultato della registrazione è un flusso HLS. La registrazione contiene il contenuto principale e il contenuto relativo alla pubblicità in un flusso video-on-demand HLS (VOD). Il processo di registrazione non tiene traccia dei segmenti correlati agli annunci, pertanto le informazioni relative al posizionamento degli annunci nel contenuto principale vengono perse.

Potresti essere in grado di ottenere le informazioni relative al posizionamento dei periodi di contenuto pubblicitario da altre sorgenti fuori banda, come i sistemi CMS esterni. È possibile definire marcatori personalizzati attraverso i quali queste informazioni fuori banda possono essere passate al sottosistema di gestione della timeline. L’intenzione è quella di contrassegnare le sezioni di contenuto che corrispondono al contenuto specifico relativo all’annuncio in modo tale che tutti gli eventi di riproduzione specifici dell’annuncio vengano attivati nello stesso modo in cui se questi periodi di annunci personalizzati fossero posizionati esplicitamente sulla timeline del lettore.

Il tracciamento degli annunci non viene gestito internamente da TVSDK, ad esempio quando gli annunci vengono risolti da Adobe Primetime ad Decioning. Tuttavia, TVSDK fornisce le seguenti astrazioni che definiscono il modo in cui il contenuto relativo agli annunci viene rappresentato nella timeline:

* L&#39;interruzione pubblicitaria

   Un’interruzione pubblicitaria è un elenco ordinato di singoli annunci consecutivi.
* Un annuncio individuale

Gli eventi di riproduzione vengono attivati separatamente per le interruzioni di annunci e gli annunci al punto iniziale e finale per ogni annuncio.

TVSDK invia eventi di tracciamento degli annunci all’applicazione in modo da poter implementare una logica di tracciamento personalizzata. Se imposti marcatori di annunci personalizzati, riceverai gli eventi `onAdBreakStart`, `onAdStart`, `onAdProgress`, `onAdComplete` e `onAdBreakComplete`.