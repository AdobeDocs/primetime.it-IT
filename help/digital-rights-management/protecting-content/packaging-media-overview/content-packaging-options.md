---
seo-title: Opzioni pacchetto
title: Opzioni pacchetto
uuid: 04244428-cb42-438a-8f16-91532c70ea60
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---


# Opzioni pacchetto{#packaging-options}

Sono disponibili numerose opzioni per la creazione di pacchetti di contenuto. È possibile specificare le opzioni nell&#39;interfaccia `DRMParameters` e implementare le classi che possono interfacciarsi. Con queste classi è possibile impostare parametri di firma e chiave, nonché indicare se cifrare contenuto audio, contenuto video o dati di script. Per vedere come queste vengono implementate nell&#39;implementazione di riferimento, consultate le descrizioni delle opzioni della riga di comando di Media Packager illustrate in *Utilizzo delle implementazioni di riferimento Adobe Primetime DRM* . Queste opzioni si basano sull&#39;API Java e sono quindi disponibili per l&#39;utilizzo a livello di programmazione.

Le opzioni di package includono:

* Opzioni di cifratura (audio, video, cifratura parziale).
* URL del server delle licenze utilizzato dal client come URL di base per tutte le richieste inviate al server delle licenze
* Certificato di trasporto server licenze
* Certificato del server di licenze, utilizzato per crittografare il CEK
* Credenziali Packager per la firma dei metadati

