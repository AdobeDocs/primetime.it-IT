---
description: La rete CDN multipla consente di impostare una o più posizioni della rete CDN per distribuire annunci transcodificati.
title: Supporto di più reti CDN
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Supporto di più reti CDN {#multi-cdn-support}

La rete CDN multipla consente di impostare una o più posizioni della rete CDN per distribuire annunci transcodificati.

Per impostazione predefinita, tutte le risorse trascodificate sono ospitate sulla rete CDN Akamai di proprietà dell’Adobe. Tuttavia, puoi scegliere zero o più posizioni CDN aggiuntive in cui CRS ospiterà la risorsa transcodificata. In questo caso, le risorse e i contenuti transcodificati possono essere serviti dalla stessa CDN.

Quando il server manifest cerca le richieste transcodificate, utilizza un URL di bootstrap che contiene una serie di parametri di query. Se hai impostato un ambiente con più reti CDN, l’URL di avvio deve contenere anche `ptcdn` parameter.Il server manifesto utilizza questo parametro per identificare il server CDN da cui ottenere la versione transcodificata dell’annuncio.

È inoltre disponibile il supporto per più reti CDN per le seguenti soluzioni Primetime:

1. TVSDK per Android
1. TVSDK per HLS desktop
1. TVSDK per iOS

## Abilita supporto CDN {#section_1BA344F2300B49F291865A7461EDFEAE}

Per impostazione predefinita, CRS è disabilitato per tutti i clienti

Contatta l’account manager tecnico Adobe per configurare l’account CRS in modo che utilizzi altre CDN per ospitare le risorse degli annunci transcodificati. Ti verrà richiesto di fornire le seguenti informazioni, necessarie a CRS per caricare le risorse degli annunci transcodificati nella CDN

1. URL CDN
1. Dettagli autenticazione
1. Formato URL di output

Inoltre, il tuo account manager tecnico Adobe ti fornirà un soprannome per questa rete CDN.Devi passare questo come valore della `ptcdn` parametro nell&#39;URL di Bootstrap.

È possibile configurare più CDN sull’estremità CRS tramite il supporto Adobe. Tuttavia, il CDN utilizzato per scegliere le risorse degli annunci da unire tramite il server manifesto deve essere quello passato come valore del `ptcdn` parametro nell&#39;URL di Bootstrap.
