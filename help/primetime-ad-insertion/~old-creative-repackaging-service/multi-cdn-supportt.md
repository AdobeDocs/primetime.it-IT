---
description: Multi CDN consente di impostare una o più posizioni CDN per distribuire annunci transcodificati.
seo-description: Multi CDN consente di impostare una o più posizioni CDN per distribuire annunci transcodificati.
seo-title: Supporto per più CDN
title: Supporto per più CDN
uuid: 2b6d71f0-61c8-486b-a35a-f7ef3a9519d2
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---


# Supporto per più CDN {#multi-cdn-support}

Multi CDN consente di impostare una o più posizioni CDN per distribuire annunci transcodificati.

Per impostazione predefinita, tutte le risorse transcodificate sono ospitate nella rete CDN di  di proprietà del Adobe Akamai. Tuttavia, potete scegliere zero o più posizioni CDN aggiuntive in cui il CRS ospiterà la risorsa transcodificata. In questo caso, le risorse e i contenuti transcodificati possono essere serviti dalla stessa CDN.

Quando il server manifesto effettua una ricerca per le richieste transcodificate, utilizza un URL di avvio che contiene una serie di parametri di query. Se avete impostato un ambiente CDN multi-CDN, anche l&#39;URL di avvio dovrà contenere il parametro `ptcdn`. Il server manifesto utilizza questo parametro per identificare il server CDN da cui ottenere la versione transcodificata dell&#39;annuncio.

Il supporto per più CDN è disponibile anche per le seguenti soluzioni Primetime:

1. TVSDK per Android
1. TVSDK per desktop HLS
1. TVSDK per iOS

## Abilita supporto CDN {#section_1BA344F2300B49F291865A7461EDFEAE}

Per impostazione predefinita, CRS è disabilitato per tutti i clienti

Contatta il tuo account manager tecnico  Adobe per configurare il tuo account CRS in modo che utilizzi altri CDN per ospitare le risorse degli annunci transcodificati. Ti verrà richiesto di fornire le seguenti informazioni necessarie a CRS per caricare le risorse degli annunci transcodificati nella CDN

1. URL CDN
1. Dettagli autenticazione
1. Formato URL di output

Inoltre, il vostro  account manager tecnico di Adobe vi fornirà un nickname per questa CDN. Dovete trasmettere questo come il valore del parametro `ptcdn` nell&#39;URL di Bootstrap.

È possibile configurare più CDN su CRS end tramite  supporto Adobe. Tuttavia, la rete CDN utilizzata per raccogliere le risorse pubblicitarie da unire tramite il server manifesto dovrebbe essere quella passata come valore del parametro `ptcdn` nell&#39;URL di Bootstrap.
