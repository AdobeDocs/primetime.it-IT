---
description: Puoi attivare questa funzione e verificare la presenza di eventi correlati.
title: Usa aggiornamento del manifesto principale live
exl-id: 02cb3116-cc30-4139-841b-8d6297214b8b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 0%

---

# Usa aggiornamento del manifesto principale live{#use-live-master-manifest-update}

Puoi attivare questa funzione e verificare la presenza di eventi correlati.

1. Per attivare gli aggiornamenti live del manifesto principale, impostare la frequenza di aggiornamento (in minuti) impostando `NetworkConfiguration.masterUpdateInterval` proprietà.
1. Facoltativamente, tenere traccia degli aggiornamenti del manifesto riusciti ascoltando `MediaPlayerItemEvent.MASTER_UPDATED` evento.
