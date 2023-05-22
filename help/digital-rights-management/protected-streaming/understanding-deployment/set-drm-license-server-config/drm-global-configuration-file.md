---
description: Il file di configurazione flashaccess-global.xml include impostazioni applicabili a tutti i tenant del server licenze.
title: File di configurazione globale
exl-id: 3e74bce6-1634-469f-9d02-1121e9d50687
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# File di configurazione globale{#global-configuration-file}

Il file di configurazione flashaccess-global.xml include impostazioni applicabili a tutti i tenant del server licenze.

È necessario inserire il file di configurazione nel [!DNL LicenseServer.ConfigRoot] directory.

Consulta la [!DNL configs] per un esempio di file di configurazione globale.

Il file di configurazione globale include:

* Memorizzazione in cache — controlla la memorizzazione nella cache dei file di configurazione in memoria.

   Consulta *Aggiornamento dei file di configurazione* per informazioni sulle impostazioni di memorizzazione in cache.
* Registrazione — specifica il livello di registrazione e la frequenza con cui viene eseguito il rollback dei file di registro.
* Password HSM — Obbligatoria solo se viene utilizzato un HSM per memorizzare le credenziali del server.

Vedere i commenti nell&#39;esempio di file di configurazione globale che si trova in DRM Primetime `<DVD>`\Adobe Primetime DRM Server for Protected Streaming\configs per ulteriori dettagli.
