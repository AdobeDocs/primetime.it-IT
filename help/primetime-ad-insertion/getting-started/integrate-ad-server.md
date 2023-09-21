---
title: Integrare il server di annunci
description: Integrazione del server di annunci
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# Integrare il server di annunci {#integrate-ad-server}

Per iniziare, riceverai un login per accedere alla console Ad Insertion di Primetime, dove puoi impostare le regole che Primetime Ad Insertion utilizza per inoltrare le richieste di annunci al server di annunci desiderato. Primetime Ad Insertion supporta la maggior parte dei server di annunci VAST o VMAP compatibili.

>[!NOTE]
>
>[Pagina IAB VAST](https://www.iab.com/guidelines/digital-video-ad-serving-template-vast)

## Supporto macro {#macro-support}

Primetime Ad Insertion abilita le seguenti macro di ad server per tutti i flussi:

* Cache-busting
* Contesto dell’applicazione o URL della pagina
* Durata disponibile
* Risorsa video corrente

Se sono necessarie ulteriori macro, contatta il rappresentante del supporto Adobe Primetime.

## Funzioni avanzate {#advanced-features}

Primetime Ad Insertion dispone anche di decisioning basato su regole che abilita funzioni avanzate. Questo può essere importante se desideri indirizzare gli annunci a server di annunci diversi in base ai diritti di inventario o abilitare la limitazione della frequenza per i singoli annunci. Per ulteriori informazioni, consulta [Funzioni avanzate](/help/primetime-ad-insertion/advanced-features/route-ads-based-on-rules.md).
