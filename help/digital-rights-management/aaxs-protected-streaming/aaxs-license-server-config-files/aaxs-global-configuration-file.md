---
title: File di configurazione globale
description: File di configurazione globale
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---


# File di configurazione globale{#global-configuration-file}

Il file di configurazione flashaccess-global.xml contiene impostazioni che si applicano a tutti gli tenant del server licenze. Questo file deve trovarsi in *LicenseServer.ConfigRoot*. Vedi la directory configs per un esempio di file di configurazione globale. Il file di configurazione globale include quanto segue:

* Memorizzazione in cache — controlla il caching dei file di configurazione nella memoria. Per una spiegazione delle impostazioni di memorizzazione in cache, vedere &quot;Aggiornamento dei file di configurazione&quot;.
* Logging - Specifica il livello di registrazione e la frequenza di scorrimento dei file di registro.
* Password HSM — necessaria solo se viene utilizzato un HSM per memorizzare le credenziali del server.

Per ulteriori informazioni, consulta i commenti nel file di configurazione globale di esempio disponibile in `<AdobeAccessDVD>\Adobe Access Server for Protected Streaming\configs` .
