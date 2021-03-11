---
description: È possibile attivare questa funzione e verificare la presenza di eventi correlati.
title: Usa aggiornamento del manifesto del master in tempo reale
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 0%

---


# Usa aggiornamento del manifesto master live{#use-live-master-manifest-update}

È possibile attivare questa funzione e verificare la presenza di eventi correlati.

1. Per attivare gli aggiornamenti del manifest live, imposta la frequenza di aggiornamento (in minuti) impostando la proprietà `NetworkConfiguration.masterUpdateInterval` .
1. Facoltativamente, tieni traccia degli aggiornamenti del manifesto riusciti ascoltando l&#39;evento `MediaPlayerItemEvent.MASTER_UPDATED` .
