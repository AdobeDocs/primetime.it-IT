---
seo-title: Durata della cache delle licenze
title: Durata della cache delle licenze
uuid: 378940a2-f072-478d-bee1-05ccba888b5c
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# Durata della cache delle licenze{#license-caching-duration}

Specifica la durata per la quale una licenza può essere memorizzata nella cache su disco nell&#39;archivio licenze locale del client senza che sia necessario riacquisire dal server licenze. In alternativa, potete specificare una data/ora assoluta dopo la quale una licenza non può più essere memorizzata nella cache.

Una volta trascorsa la data di scadenza della cache, la licenza non è più valida e il client deve richiedere una nuova licenza al server licenze.

Esempio di utilizzo: Utilizzare la durata del caching delle licenze per specificare un periodo di tempo fisso valido per una licenza particolare, ad esempio in un caso di utilizzo in affitto. È possibile specificare un noleggio di 30 giorni (con memorizzazione nella cache delle licenze) per indicare la durata totale della licenza entro la quale consumare il contenuto.
