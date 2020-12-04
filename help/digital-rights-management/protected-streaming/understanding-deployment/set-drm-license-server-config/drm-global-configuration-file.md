---
description: Il file di configurazione flashaccess-global.xml include impostazioni valide per tutti i tenant del server licenze.
seo-description: Il file di configurazione flashaccess-global.xml include impostazioni valide per tutti i tenant del server licenze.
seo-title: File di configurazione globale
title: File di configurazione globale
uuid: 294d6cff-be07-4b4b-8aa6-943044a1c56f
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---


# File di configurazione globale{#global-configuration-file}

Il file di configurazione flashaccess-global.xml include impostazioni valide per tutti i tenant del server licenze.

È necessario inserire il file di configurazione nella directory [!DNL LicenseServer.ConfigRoot].

Vedere la directory [!DNL configs] per un esempio di file di configurazione globale.

Il file di configurazione globale include:

* Caching Controlla la memorizzazione nella cache dei file di configurazione.

   Per informazioni sulle impostazioni di memorizzazione nella cache, vedere *Aggiornamento dei file di configurazione*.
* Registrazione — Specifica il livello di registrazione e la frequenza con cui viene eseguito il rollout dei file di registro.
* password HSM — Obbligatorio solo se viene utilizzato un HSM per memorizzare le credenziali del server.

Per ulteriori informazioni, vedere i commenti nel file di configurazione globale di esempio che si trova in DRM `<DVD>`\ Adobe Primetime DRM Server for Protected Streaming\configs.
