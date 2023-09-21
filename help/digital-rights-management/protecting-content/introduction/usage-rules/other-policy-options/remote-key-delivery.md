---
title: Recapito chiavi iOS remoto e locale
description: Recapito chiavi iOS remoto e locale
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Recapito chiavi iOS remoto e locale {#remote-and-local-ios-key-delivery}

Adobe Primetime supporta le seguenti opzioni per la consegna di chiavi ai client iOS:

* **Remoto** - Esegue come specificato nella specifica HTTP Live Streaming (HLS); il manifesto M3U8 specifica un percorso HTTPS che include una chiave AES che deve essere utilizzata per decrittografare i seguenti segmenti crittografati nel flusso. Quando si specifica `Remote` nel criterio DRM di Primetime, il dispositivo client deve connettersi a un server HTTPS remoto per ottenere una chiave AES.

* **Locale** - Quando si specifica `Local` in DRM di Primetime invece di connettersi a Internet/rete per la chiave AES, nell’applicazione iOS è incorporato un server HTTPS locale che gestisce tutte le richieste chiave AES. Il server HTTPS incorporato viene configurato e configurato automaticamente nell’applicazione P. Non è richiesto alcun intervento da parte dello sviluppatore dell&#39;applicazione.

La consegna della chiave remota viene abilitata tramite il criterio DRM di Primetime utilizzato per creare pacchetti di contenuto. Se desideri modificare questa impostazione, devi ricompilare il contenuto. Se si abilita la distribuzione di chiavi remote, è necessario distribuire un server chiavi DRM Primetime in grado di gestire le richieste di chiavi provenienti dai client iOS. Tuttavia, non vi è alcuna modifica al flusso di lavoro per i client su altre piattaforme.

>[!NOTE]
>
>La selezione della consegna Chiave influisce solo sui client iOS. Tutti gli altri dispositivi che utilizzano contenuti HLS, come Android e Primetime su desktop (Flash Player), utilizzano sempre `Local` consegna chiave, anche se `Remote` specificato.
