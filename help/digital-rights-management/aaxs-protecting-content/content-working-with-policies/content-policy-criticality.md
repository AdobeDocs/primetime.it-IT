---
title: Criticità politica
description: Criticità politica
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# Criticità dei criteri{#policy-criticality}

Se nei criteri vengono utilizzate nuove regole di utilizzo e questi criteri vengono utilizzati nel contenuto del pacchetto per i server licenze precedenti (che non conoscono le nuove regole di utilizzo), è possibile specificare il comportamento dei server licenze precedenti. Per impostazione predefinita, la criticità dei criteri è &quot;true&quot;, il che significa che il server licenze deve comprendere tutte le parti del criterio al fine di generare una licenza utilizzando il criterio. Se la criticità dei criteri è impostata su &quot;false&quot;, un server licenze precedente potrebbe ignorare parti del criterio che non comprende e le licenze generate dal server non conterranno le nuove regole di utilizzo.

I server di accesso Adobe che utilizzano la versione 2.0.2 dell’SDK e le versioni successive rispettano l’impostazione di importanza critica dei criteri.
