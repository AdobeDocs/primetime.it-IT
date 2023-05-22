---
title: Opzioni di packaging
description: Opzioni di packaging
copied-description: true
exl-id: 64c5c22d-0041-4fb9-80d0-72e11cb775f3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---

# Opzioni di packaging{#packaging-options}

Sono disponibili numerose opzioni per la creazione di pacchetti di contenuti. È possibile specificare le opzioni in `DRMParameters` e implementare le classi che possono interfacciarsi. Con queste classi è possibile impostare la firma e i parametri chiave, nonché indicare se crittografare il contenuto audio, il contenuto video o i dati di script. Per vedere come questi vengono implementati nell’implementazione di riferimento, consulta le descrizioni delle opzioni della riga di comando di Media Packager discusse in *Utilizzo delle implementazioni di riferimento Adobe Primetime DRM*. Queste opzioni si basano sull’API Java e sono quindi disponibili per l’utilizzo a livello di programmazione.

Le opzioni di packaging includono:

* Opzioni di crittografia (audio, video, crittografia parziale).
* URL del server licenze utilizzato dal client come URL di base per tutte le richieste inviate al server licenze
* Certificato trasporto server licenze
* Certificato del server licenze, utilizzato per crittografare il codice di licenza
* Credenziali Packager per la firma dei metadati
