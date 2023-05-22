---
title: Durata caching licenze
description: Durata caching licenze
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# Durata caching licenze{#license-caching-duration}

Specifica la durata per la quale una licenza può essere memorizzata nella cache del disco nell&#39;archivio licenze locale del client senza richiedere la riacquisizione dal server licenze. In alternativa, è possibile specificare una data/ora assoluta dopo la quale una licenza non può più essere memorizzata nella cache.

Una volta superata la data di scadenza della cache, la licenza non è più valida e il client deve richiedere una nuova licenza al server licenze.

Caso d’uso di esempio: utilizza la durata di memorizzazione nella cache delle licenze per specificare un periodo di tempo fisso valido per una determinata licenza, ad esempio in un caso d’uso di noleggio. È possibile specificare un noleggio di 30 giorni (con inserimento delle licenze nella cache) per indicare la durata totale della licenza entro la quale utilizzare il contenuto.
