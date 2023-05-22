---
title: Consegna chiavi iOS remota e locale
description: Consegna chiavi iOS remota e locale
copied-description: true
exl-id: de9c7070-46a9-453c-9d98-a9f161282cfa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# Consegna chiavi iOS remota e locale{#remote-and-local-ios-key-delivery}

Adobe Primetime supporta due opzioni per la consegna di chiavi ai client iOS:

* Remoto: esattamente come specificato nella specifica HLS, il manifesto M3U8 specifica un percorso HTTPS contenente una chiave AES che deve essere utilizzata per decrittografare i seguenti segmenti crittografati nel flusso. Se si specifica &quot;Remote&quot;, il dispositivo client si rivolge a un server HTTPS remoto per recuperare la chiave AES.
* Locale: se si specifica &quot;Locale&quot;, invece di connettersi a Internet/rete per la chiave AES, nell’applicazione iOS viene incorporato un server HTTPS locale che gestirà tutte le richieste di chiave AES. Il server HTTPS incorporato viene configurato e configurato automaticamente nell&#39;applicazione Primetime. Non è richiesto alcun intervento da parte dello sviluppatore dell&#39;applicazione.

La distribuzione tramite chiave remota viene abilitata tramite il criterio utilizzato per creare pacchetti di contenuto (la modifica di questa impostazione richiede la creazione di nuovi pacchetti di contenuto). Quando la distribuzione tramite chiave remota è abilitata, è necessario distribuire un Adobe di Access Key Server per gestire le richieste chiave dai client iOS, ma non vi è alcuna modifica al flusso di lavoro per i client su altre piattaforme.

>[!NOTE]
>
>La selezione della consegna Chiave influisce solo sui client iOS. Tutti gli altri dispositivi che utilizzano contenuti HLS utilizzeranno sempre la distribuzione con chiave &quot;Locale&quot;, anche se è stato specificato &quot;Remoto&quot;.

Per informazioni, consulta *Utilizzo del server con chiave di accesso Adobe*.
