---
description: Multi CDN consente di impostare una o più posizioni CDN per distribuire annunci transcodificati.
title: Supporto per più reti CDN
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Supporto per più CDN {#multi-cdn-support}

Multi CDN consente di impostare una o più posizioni CDN per distribuire annunci transcodificati.

Per impostazione predefinita, tutte le risorse transcodificate sono ospitate sulla rete CDN Akamai di proprietà dell’Adobe. Tuttavia, puoi scegliere zero o più posizioni CDN aggiuntive in cui CRS ospiterà la risorsa transcodificata. In questo caso, le risorse e i contenuti transcodificati possono essere serviti dalla stessa CDN.

Quando il server manifest effettua una ricerca per le richieste transcodificate, utilizza un URL di bootstrap che contiene una serie di parametri di query. Se hai impostato un ambiente multi-CDN, anche l&#39;URL di avvio dovrà contenere il parametro `ptcdn`. Il server manifest utilizza questo parametro per identificare il server CDN da cui ottenere la versione transcodificata dell&#39;annuncio.

Il supporto per più reti CDN è disponibile anche per le seguenti soluzioni Primetime:

1. TVSDK per Android
1. TVSDK per HLS desktop
1. TVSDK per iOS

## Abilita il supporto CDN {#section_1BA344F2300B49F291865A7461EDFEAE}

Per impostazione predefinita, CRS è disabilitato per tutti i clienti

Contatta il tuo account manager tecnico Adobe per configurare il tuo account CRS per utilizzare altre CDN per ospitare le risorse degli annunci transcodificati. Ti verrà richiesto di fornire le seguenti informazioni che sono necessarie da CRS per caricare le risorse degli annunci transcodificati nella CDN

1. URL CDN
1. Dettagli di autenticazione
1. Formato URL di output

Inoltre, il tuo Adobe Technical account manager ti fornirà un nickname per questa CDN.Devi passare questo come valore del parametro `ptcdn` nell&#39;URL di Bootstrap.

È possibile configurare più CDN su CRS end tramite Adobe Support. Tuttavia, la rete CDN utilizzata per raccogliere le risorse pubblicitarie da unire tramite il server manifest dovrebbe essere quella passata come valore del parametro `ptcdn` nell&#39;URL di Bootstrap.
