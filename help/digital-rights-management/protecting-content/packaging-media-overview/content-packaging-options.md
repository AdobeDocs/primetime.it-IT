---
title: Opzioni di packaging
description: Opzioni di packaging
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---

# Opzioni di packaging{#packaging-options}

Sono disponibili numerose opzioni per la creazione di pacchetti di contenuti. È possibile specificare le opzioni in `DRMParameters` e implementare le classi che possono interfacciarsi. Con queste classi è possibile impostare la firma e i parametri chiave, nonché indicare se crittografare il contenuto audio, il contenuto video o i dati script. Per vedere come questi vengono implementati nell’implementazione di riferimento, consulta le descrizioni delle opzioni della riga di comando di Media Packager discusse in *Utilizzo delle implementazioni di riferimento Adobe Primetime DRM*. Queste opzioni si basano sull’API Java e sono quindi disponibili per l’utilizzo a livello di programmazione.

Le opzioni di packaging includono:

* Opzioni di crittografia (audio, video, crittografia parziale).
* URL del server licenze utilizzato dal client come URL di base per tutte le richieste inviate al server licenze
* Certificato trasporto server licenze
* Certificato del server licenze, utilizzato per crittografare il codice di licenza
* Credenziali Packager per la firma dei metadati
