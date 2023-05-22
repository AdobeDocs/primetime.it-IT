---
title: File di configurazione del server licenze
description: File di configurazione del server licenze
copied-description: true
exl-id: d48e88a4-caae-4f4e-b870-38da4f3a715e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
