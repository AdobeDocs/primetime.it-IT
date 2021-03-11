---
title: Durata della memorizzazione in cache delle licenze
description: Durata della memorizzazione in cache delle licenze
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# Durata della memorizzazione in cache della licenza{#license-caching-duration}

La durata del caching delle licenze specifica per quanto tempo una licenza può essere memorizzata nella cache su disco nell&#39;archivio licenze locale del client senza richiedere la riacquisizione dal server licenze. In alternativa, è possibile specificare una data e un’ora assolute dopo le quali una licenza non può più essere memorizzata nella cache.

Una volta passata la data di scadenza della cache, la licenza non è più valida e il client deve richiedere una nuova licenza dal server licenze.

Esempio di utilizzo: Utilizzare la durata del caching delle licenze per specificare un periodo di tempo fisso valido per una determinata licenza, ad esempio in un caso di utilizzo a noleggio. È possibile specificare un noleggio di 30 giorni (con memorizzazione in cache della licenza) per indicare la durata totale della licenza entro cui utilizzare il contenuto.
