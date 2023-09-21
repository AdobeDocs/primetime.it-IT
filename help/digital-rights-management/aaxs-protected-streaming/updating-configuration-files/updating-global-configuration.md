---
title: Aggiornamento del file di configurazione globale
description: Aggiornamento del file di configurazione globale
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---

# Aggiornamento del file di configurazione globale{#updating-the-global-configuration-file}

La password HSM in [!DNL flashaccess-global.xml] possono essere modificate in qualsiasi momento e le modifiche diventano effettive al successivo ricaricamento del file di configurazione da parte del server. Tuttavia, le modifiche apportate agli elementi &quot;Logging&quot; (Registrazione) e &quot;Caching&quot; (Memorizzazione in cache) non vengono ricaricate; eventuali modifiche apportate a questi elementi richiedono il riavvio del server.
