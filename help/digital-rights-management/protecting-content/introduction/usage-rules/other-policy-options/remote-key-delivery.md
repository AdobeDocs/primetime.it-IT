---
title: Distribuzione remota e locale di chiavi iOS
description: Distribuzione remota e locale di chiavi iOS
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---


# Distribuzione remota e locale di chiavi iOS {#remote-and-local-ios-key-delivery}

Adobe Primetime supporta le seguenti opzioni per la distribuzione delle chiavi ai client iOS:

* **Remote** : esegue come specificato nella specifica HTTP Live Streaming (HLS); il manifesto M3U8 specifica un percorso HTTPS che include una chiave AES che deve essere utilizzata per decrittografare i seguenti segmenti crittografati nel flusso. Quando si specifica `Remote` nel criterio DRM di Primetime, il dispositivo client deve connettersi a un server HTTPS remoto per ottenere una chiave AES.

* **Locale**  - Quando si specifica  `Local` nel DRM di Primetime invece di connettersi a Internet/rete per la chiave AES, un server HTTPS locale viene incorporato nell&#39;applicazione iOS, che gestisce quindi tutte le richieste di chiavi AES. Il server HTTPS incorporato viene configurato e configurato automaticamente nell&#39;applicazione P. Lo sviluppatore dell’applicazione non richiede alcun intervento.

La consegna delle chiavi remote è abilitata tramite i criteri DRM di Primetime utilizzati per creare un pacchetto di contenuti. Se desideri modificare questa impostazione, devi creare un nuovo pacchetto del contenuto. Se abiliti la consegna chiavi remota, devi distribuire un server chiavi DRM Primetime che possa gestire le richieste chiave dei client iOS. Tuttavia, non vi è alcuna modifica al flusso di lavoro per i client su altre piattaforme.

>[!NOTE]
>
>La selezione della consegna chiave interessa solo i client iOS. Tutti gli altri dispositivi che utilizzano contenuti HLS , come Android e Primetime on Desktop (Flash Player), utilizzano sempre la consegna chiavi `Local`, anche se è stato specificato `Remote`.

