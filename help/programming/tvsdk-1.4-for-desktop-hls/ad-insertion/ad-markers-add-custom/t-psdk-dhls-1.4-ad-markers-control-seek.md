---
description: Potete ignorare il comportamento predefinito per il modo in cui TVSDK cerca sugli annunci quando si utilizzano gli indicatori di annunci personalizzati.
seo-description: Potete ignorare il comportamento predefinito per il modo in cui TVSDK cerca sugli annunci quando si utilizzano gli indicatori di annunci personalizzati.
seo-title: Controllare il comportamento di riproduzione per la ricerca su indicatori di annunci personalizzati
title: Controllare il comportamento di riproduzione per la ricerca su indicatori di annunci personalizzati
uuid: 926299c6-9c23-457d-b836-08432e4e169e
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Controllare il comportamento di riproduzione per la ricerca su indicatori di annunci personalizzati{#control-playback-behavior-for-seeking-over-custom-ad-markers}

Potete ignorare il comportamento predefinito per il modo in cui TVSDK cerca sugli annunci quando si utilizzano gli indicatori di annunci personalizzati.

Per impostazione predefinita, quando un utente cerca o passa sezioni di annunci derivanti dal posizionamento di marcatori di annunci personalizzati, TVSDK salta gli annunci. Questo potrebbe essere diverso dal comportamento di riproduzione corrente per le interruzioni pubblicitarie standard.

Potete indicare a TVSDK di riposizionare l&#39;indicatore di riproduzione all&#39;inizio dell&#39;annuncio personalizzato saltato più di recente quando l&#39;utente cerca oltre uno o più annunci personalizzati.

1. Configurate un’istanza di metadati con l’ `DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` enumerazione impostata sul valore stringa &quot;true&quot; (non come booleano `true`).

1. Create e configurate un&#39; `MediaResource` istanza, passando le opzioni di configurazione aggiuntive a `TimeRangeCollection.toMetadata`. Questo metodo riceve opzioni di configurazione aggiuntive tramite un’altra struttura di metadati generica.

