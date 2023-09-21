---
title: File di configurazione del server licenze
description: File di configurazione del server licenze
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# File di configurazione del server licenze{#license-server-configuration-files}

Il server Adobe Primetime DRM per lo streaming protetto richiede i seguenti tipi di file di configurazione:

* File di configurazione globale ( [!DNL flashaccess-global.xml])
* File di configurazione tenant per ogni tenant ( [!DNL flashaccess-tenant.xml])

Dopo aver completato la modifica dei file di configurazione, l&#39;Adobe consiglia di utilizzare le utilità fornite con Primetime DRM Server for Protected Streaming per verificare che i file siano ben formati.

Consulta *Convalida configurazione*.

Se si desidera evitare di rendere disponibili le password in testo non crittografato nei file di configurazione, è necessario crittografare tutte le password specificate nei file di configurazione globale e tenant utilizzando lo strumento Scrambler fornito dall&#39;Adobe.

Consulta *Scrambler password* per ulteriori informazioni su come crittografare le password.
