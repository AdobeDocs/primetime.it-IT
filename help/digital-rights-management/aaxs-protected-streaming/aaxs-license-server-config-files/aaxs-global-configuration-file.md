---
seo-title: File di configurazione globale
title: File di configurazione globale
uuid: 10370bc0-36ab-4e43-9e75-c46a7177874c
translation-type: tm+mt
source-git-commit: ed1430bdcb590a53fa69b324ef340ad636b2fa7c
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---


# File di configurazione globale{#global-configuration-file}

Il file di configurazione flashaccess-global.xml contiene impostazioni valide per tutti i tenant del server licenze. Questo file deve trovarsi in *LicenseServer.ConfigRoot*. Vedere la directory configs per un esempio di file di configurazione globale. Il file di configurazione globale include quanto segue:

* Caching Controlla la memorizzazione nella cache dei file di configurazione. Per una spiegazione delle impostazioni di memorizzazione nella cache, vedere &quot;Aggiornamento dei file di configurazione&quot;.
* Registrazione — Specifica il livello di registrazione e la frequenza con cui viene eseguito il rollout dei file di registro.
* password HSM — Obbligatorio solo se viene utilizzato un HSM per memorizzare le credenziali del server.

Per ulteriori informazioni, vedere i commenti nel file di configurazione globale di esempio in `<AdobeAccessDVD>\Adobe Access Server for Protected Streaming\configs`.
