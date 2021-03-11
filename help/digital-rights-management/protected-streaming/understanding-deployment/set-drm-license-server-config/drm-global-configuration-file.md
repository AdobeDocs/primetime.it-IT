---
description: Il file di configurazione flashaccess-global.xml include impostazioni che si applicano a tutti gli tenant del server licenze.
title: File di configurazione globale
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---


# File di configurazione globale{#global-configuration-file}

Il file di configurazione flashaccess-global.xml include impostazioni che si applicano a tutti gli tenant del server licenze.

È necessario inserire il file di configurazione nella directory [!DNL LicenseServer.ConfigRoot].

Per un esempio di file di configurazione globale, consulta la directory [!DNL configs] .

Il file di configurazione globale include:

* Memorizzazione in cache — controlla il caching dei file di configurazione nella memoria.

   Per informazioni sulle impostazioni di memorizzazione in cache, consulta *Aggiornamento dei file di configurazione* .
* Logging - Specifica il livello di registrazione e la frequenza di scorrimento dei file di registro.
* Password HSM — necessaria solo se viene utilizzato un HSM per memorizzare le credenziali del server.

Per ulteriori informazioni, vedere i commenti nel file di configurazione globale di esempio che si trova in DRM `<DVD>`\Adobe Primetime DRM Server for Protected Streaming\configs.
