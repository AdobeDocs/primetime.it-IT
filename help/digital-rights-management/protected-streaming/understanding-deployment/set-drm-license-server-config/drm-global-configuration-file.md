---
description: Il file di configurazione flashaccess-global.xml include impostazioni valide per tutti i tenant del server licenze.
seo-description: Il file di configurazione flashaccess-global.xml include impostazioni valide per tutti i tenant del server licenze.
seo-title: File di configurazione globale
title: File di configurazione globale
uuid: 294d6cff-be07-4b4b-8aa6-943044a1c56f
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# File di configurazione globale{#global-configuration-file}

Il file di configurazione flashaccess-global.xml include impostazioni valide per tutti i tenant del server licenze.

È necessario inserire il file di configurazione nella [!DNL LicenseServer.ConfigRoot] directory.

Vedere la [!DNL configs] directory per un esempio di file di configurazione globale.

Il file di configurazione globale include:

* Caching Controlla la memorizzazione nella cache dei file di configurazione.

   Consultate *Aggiornamento dei file* di configurazione per informazioni sulle impostazioni di memorizzazione nella cache.
* Registrazione — Specifica il livello di registrazione e la frequenza con cui viene eseguito il rollout dei file di registro.
* password HSM — Obbligatorio solo se viene utilizzato un HSM per memorizzare le credenziali del server.

Vedere i commenti nel file di configurazione globale di esempio che si trova in DRM di [!DNL Primetime <DVD>\Adobe Primetime DRM Server for Protected Streaming\configs] per ulteriori dettagli.
