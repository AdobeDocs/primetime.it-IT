---
title: Distribuzione remota e locale delle chiavi iOS
description: Distribuzione remota e locale delle chiavi iOS
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---


# Consegna chiavi iOS remota e locale{#remote-and-local-ios-key-delivery}

Adobe Primetime supporta due opzioni per la consegna delle chiavi ai client iOS:

* Remoto - Esattamente come specificato nella specifica HLS, il manifesto M3U8 specifica un percorso HTTPS contenente una chiave AES che deve essere utilizzata per decrittografare i seguenti segmenti crittografati nel flusso. Quando si specifica &quot;Remote&quot;, il dispositivo client si rivolgerà a un server HTTPS remoto per recuperare la chiave AES.
* Locale: quando si specifica &quot;Locale&quot;, invece di connettersi a Internet/rete per la chiave AES, nell’applicazione iOS viene incorporato un server HTTPS locale che gestirà tutte le richieste di chiavi AES. Il server HTTPS incorporato viene configurato e configurato automaticamente nell&#39;applicazione Primetime . Lo sviluppatore dell’applicazione non richiede alcun intervento.

La consegna delle chiavi remote è abilitata tramite il criterio utilizzato per creare pacchetti di contenuto (la modifica di questa impostazione richiede il ricompilamento del contenuto). Quando la consegna delle chiavi remote è abilitata, è necessario distribuire un server chiavi di accesso Adobe per gestire le richieste chiave dei client iOS, ma non vi è alcuna modifica al flusso di lavoro per i client su altre piattaforme.

>[!NOTE]
>
>La selezione della consegna chiave interessa solo i client iOS. Tutti gli altri dispositivi che utilizzano contenuti HLS utilizzeranno sempre la consegna chiavi &quot;Local&quot;, anche se è stato specificato &quot;Remote&quot;.

Per informazioni, vedere *Uso del server chiavi di accesso Adobe*.
