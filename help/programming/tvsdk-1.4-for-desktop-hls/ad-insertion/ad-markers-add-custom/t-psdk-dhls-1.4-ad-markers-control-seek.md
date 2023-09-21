---
description: Quando utilizzi i marcatori di annunci personalizzati, puoi sovrascrivere il comportamento predefinito per la ricerca di TVSDK sugli annunci.
title: Controlla il comportamento di riproduzione per la ricerca sui marcatori di annunci personalizzati
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# Controlla il comportamento di riproduzione per la ricerca sui marcatori di annunci personalizzati{#control-playback-behavior-for-seeking-over-custom-ad-markers}

Quando utilizzi i marcatori di annunci personalizzati, puoi sovrascrivere il comportamento predefinito per la ricerca di TVSDK sugli annunci.

Per impostazione predefinita, quando un utente cerca in o nelle sezioni di annunci precedenti che derivano dal posizionamento di marcatori di annunci personalizzati, TVSDK salta gli annunci. Questo comportamento potrebbe differire da quello corrente per le interruzioni pubblicitarie standard.

Puoi dire a TVSDK di riposizionare la testina di riproduzione all’inizio dell’annuncio personalizzato saltato più di recente quando l’utente cerca oltre uno o più annunci personalizzati.

1. Configurare un’istanza di metadati con `DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` enumerazione impostata sul valore stringa &quot;true&quot; (non come booleano) `true`).

1. Creare e configurare un `MediaResource` , passando le opzioni di configurazione aggiuntive a `TimeRangeCollection.toMetadata`. Questo metodo riceve opzioni di configurazione aggiuntive tramite un’altra struttura di metadati generica.
