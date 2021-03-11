---
description: È possibile ignorare il comportamento predefinito per la ricerca degli annunci da parte di TVSDK quando si utilizzano gli ad markers personalizzati.
title: Controllare il comportamento di riproduzione per la ricerca di indicatori di annunci personalizzati
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# Controllare il comportamento di riproduzione per la ricerca di marcatori di annunci personalizzati{#control-playback-behavior-for-seeking-over-custom-ad-markers}

È possibile ignorare il comportamento predefinito per la ricerca degli annunci da parte di TVSDK quando si utilizzano gli ad markers personalizzati.

Per impostazione predefinita, quando un utente cerca nelle sezioni o nelle sezioni precedenti degli annunci risultanti dal posizionamento di marcatori pubblicitari personalizzati, TVSDK salta gli annunci. Questo potrebbe differire dal comportamento di riproduzione corrente per le interruzioni pubblicitarie standard.

Puoi dire a TVSDK di riposizionare il playhead all&#39;inizio dell&#39;annuncio personalizzato saltato più di recente quando l&#39;utente cerca oltre uno o più annunci personalizzati.

1. Configura un&#39;istanza di metadati con l&#39;enumerazione `DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` impostata sul valore stringa &quot;true&quot; (non come booleano `true`).

1. Crea e configura un&#39;istanza `MediaResource`, passando le opzioni di configurazione aggiuntive a `TimeRangeCollection.toMetadata`. Questo metodo riceve opzioni di configurazione aggiuntive tramite un’altra struttura di metadati generica.

