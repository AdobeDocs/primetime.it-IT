---
title: Opzioni di pacchetto
description: Opzioni di pacchetto
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---


# Opzioni di pacchetto{#packaging-options}

Ci sono numerose opzioni disponibili per il contenuto di imballaggio. È possibile specificare le opzioni nell&#39;interfaccia `DRMParameters` e implementare le classi che possono interagire. Con queste classi è possibile impostare la firma e i parametri chiave, nonché indicare se cifrare il contenuto audio, il contenuto video o i dati di script. Per vedere come vengono implementate nell&#39;implementazione di riferimento, consulta le descrizioni delle opzioni della riga di comando Media Packager descritte in *Utilizzo delle implementazioni di riferimento Adobe Primetime DRM*. Queste opzioni si basano sull’API Java e sono quindi disponibili per l’utilizzo programmatico.

Le opzioni di imballaggio includono:

* Opzioni di crittografia (audio, video, crittografia parziale).
* URL del server licenze utilizzato dal client come URL di base per tutte le richieste inviate al server licenze
* Certificato di trasporto del server licenze
* Certificato del server licenze, utilizzato per crittografare la CEK
* Credenziali del pacchetto per la firma dei metadati

