---
title: File di configurazione globale
description: File di configurazione globale
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# File di configurazione globale{#global-configuration-file}

Il file di configurazione flashaccess-global.xml contiene impostazioni applicabili a tutti i tenant del server licenze. Questo file deve trovarsi in *LicenseServer.ConfigRoot*. Consulta la directory configs per un esempio di file di configurazione globale. Il file di configurazione globale include quanto segue:

* Memorizzazione in cache — controlla la memorizzazione nella cache dei file di configurazione in memoria. Per una spiegazione delle impostazioni di memorizzazione nella cache, vedere &quot;Aggiornamento dei file di configurazione&quot;.
* Registrazione — specifica il livello di registrazione e la frequenza con cui viene eseguito il rollback dei file di registro.
* Password HSM — Obbligatoria solo se viene utilizzato un HSM per memorizzare le credenziali del server.

Vedi i commenti nell’esempio di file di configurazione globale che si trova in `<AdobeAccessDVD>\Adobe Access Server for Protected Streaming\configs` per ulteriori dettagli.
