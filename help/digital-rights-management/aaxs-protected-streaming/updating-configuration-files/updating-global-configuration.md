---
title: Aggiornamento del file di configurazione globale
description: Aggiornamento del file di configurazione globale
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---


# Aggiornamento del file di configurazione globale{#updating-the-global-configuration-file}

La password HSM in [!DNL flashaccess-global.xml] può essere modificata in qualsiasi momento e le modifiche hanno effetto alla successiva ricarica del file di configurazione da parte del server. Tuttavia, le modifiche agli elementi &quot;Logging&quot; e &quot;Caching&quot; non vengono ricaricate; qualsiasi modifica in questi elementi richiede un riavvio del server.
