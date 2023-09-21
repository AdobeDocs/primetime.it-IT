---
title: Criticità della politica
description: Criticità della politica
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# Criticità della politica{#policy-criticality}

Se nei criteri vengono utilizzate nuove regole di utilizzo e questi criteri vengono utilizzati in un pacchetto di contenuti per server licenze meno recenti (che non comprendono le nuove regole di utilizzo), è possibile specificare il comportamento dei server licenze meno recenti. Per impostazione predefinita, la criticità della policy è &quot;true&quot;, il che significa che il server licenze deve comprendere tutte le parti della policy per generare una licenza utilizzando la policy. Se la criticità della policy è impostata su &quot;false&quot;, un server licenze precedente può ignorare parti della policy non comprese e le licenze generate dal server non conterranno le nuove regole di utilizzo.

Adobe I server di accesso che utilizzano la versione 2.0.2 dell’SDK e successive rispetteranno l’impostazione di criticità dei criteri.
