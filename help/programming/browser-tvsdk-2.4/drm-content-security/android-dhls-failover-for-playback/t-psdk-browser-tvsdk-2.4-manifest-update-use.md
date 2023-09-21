---
description: Puoi attivare questa funzione e verificare la presenza di eventi correlati.
title: Usa aggiornamento del manifesto principale live
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 0%

---

# Usa aggiornamento del manifesto principale live{#use-live-master-manifest-update}

Puoi attivare questa funzione e verificare la presenza di eventi correlati.

1. Per attivare gli aggiornamenti live del manifesto principale, impostare la frequenza di aggiornamento (in minuti) impostando `NetworkConfiguration.masterUpdateInterval` proprietà.
1. Facoltativamente, tenere traccia degli aggiornamenti del manifesto riusciti ascoltando `MediaPlayerItemEvent.MASTER_UPDATED` evento.
