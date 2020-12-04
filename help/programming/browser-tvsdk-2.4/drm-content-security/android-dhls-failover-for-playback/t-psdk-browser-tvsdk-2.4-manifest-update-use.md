---
description: Potete attivare questa funzione e verificare la presenza di eventi correlati.
seo-description: Potete attivare questa funzione e verificare la presenza di eventi correlati.
seo-title: Usa aggiornamento live master-manifest
title: Usa aggiornamento live master-manifest
uuid: 4ec665ab-b7ce-4a45-a251-13a07eb4d789
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---


# Usa aggiornamento master-manifest live{#use-live-master-manifest-update}

Potete attivare questa funzione e verificare la presenza di eventi correlati.

1. Per attivare gli aggiornamenti Live Master-manifest, imposta la frequenza di aggiornamento (in minuti) impostando la proprietà `NetworkConfiguration.masterUpdateInterval`.
1. Facoltativamente, potete tenere traccia degli aggiornamenti del manifesto riusciti ascoltando l&#39;evento `MediaPlayerItemEvent.MASTER_UPDATED`.
