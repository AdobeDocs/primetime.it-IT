---
description: Utilizzando gli indicatori di annunci personalizzati, potete contrassegnare sezioni specifiche del contenuto principale come periodi di contenuto correlati agli annunci.
seo-description: Utilizzando gli indicatori di annunci personalizzati, potete contrassegnare sezioni specifiche del contenuto principale come periodi di contenuto correlati agli annunci.
seo-title: Aggiunta di indicatori di annunci personalizzati
title: Aggiunta di indicatori di annunci personalizzati
uuid: 712da406-094a-49b2-b21d-4d5d73fff8cf
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---


# Panoramica {#add-custom-ad-markers-overview}

Utilizzando gli indicatori di annunci personalizzati, potete contrassegnare sezioni specifiche del contenuto principale come periodi di contenuto correlati agli annunci.

Questa funzione è particolarmente utile quando il contenuto viene registrato, ad esempio, da un evento live e il risultato della registrazione è un flusso HLS. La registrazione contiene il contenuto principale e il contenuto relativo alla pubblicità in un flusso video su richiesta (VOD) HLS. Il processo di registrazione non tiene traccia dei segmenti relativi agli annunci, pertanto le informazioni relative al posizionamento degli annunci nel contenuto principale vanno perse.

Potreste essere in grado di ottenere le informazioni relative al posizionamento dei periodi di contenuto pubblicitario da altre sorgenti fuori banda, come i sistemi CMS esterni. Potete definire marcatori personalizzati attraverso i quali queste informazioni fuori banda possono essere trasmesse al sottosistema di gestione della timeline. L&#39;intenzione è di contrassegnare le sezioni di contenuto che corrispondono al contenuto relativo all&#39;annuncio specificato in modo tale che tutti gli eventi di riproduzione specifici per l&#39;annuncio vengano attivati nello stesso modo in cui si verifica se questi periodi di annuncio personalizzati sono stati inseriti esplicitamente nella timeline del lettore.

Il tracciamento degli annunci non è gestito internamente da TVSDK, ad esempio quando gli annunci vengono risolti da  Adobe Primetime. Tuttavia, TVSDK fornisce le seguenti astrazioni che definiscono il modo in cui il contenuto relativo agli annunci viene rappresentato nella timeline:

* L&#39;interruzione dell&#39;annuncio

   Un&#39;interruzione di annuncio è un elenco ordinato di singoli annunci consecutivi.
* Singolo annuncio

Gli eventi di riproduzione vengono attivati separatamente per le interruzioni di annunci e gli annunci al punto iniziale e finale di ogni annuncio.

TVSDK invia eventi di tracciamento annunci alla tua applicazione, in modo da poter implementare una logica di tracciamento personalizzata. Se impostate indicatori di annunci personalizzati, riceverete gli eventi `onAdBreakStart`, `onAdStart`, `onAdProgress`, `onAdComplete` e `onAdBreakComplete`.