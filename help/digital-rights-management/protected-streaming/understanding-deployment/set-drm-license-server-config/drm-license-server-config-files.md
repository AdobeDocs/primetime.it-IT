---
title: File di configurazione del server licenze
description: File di configurazione del server licenze
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# File di configurazione del server licenze{#license-server-configuration-files}

Il server DRM di Adobe Primetime per lo streaming protetto richiede i seguenti tipi di file di configurazione:

* File di configurazione globale ( [!DNL flashaccess-global.xml])
* File di configurazione tenant per ciascun tenant ( [!DNL flashaccess-tenant.xml])

Dopo aver completato la modifica dei file di configurazione, Adobe consiglia di utilizzare le utility fornite con Primetime DRM Server for Protected Streaming per verificare che i file siano ben formati.

Vedere *Convalida della configurazione*.

Se si desidera evitare di rendere le password disponibili in testo chiaro nei file di configurazione, è necessario crittografare tutte le password specificate nei file di configurazione globale e tenant utilizzando lo strumento Scrambler fornito da Adobe.

Per ulteriori informazioni su come crittografare le password, consulta *Password Scrambler* .
