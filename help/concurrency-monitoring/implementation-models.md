---
title: Modelli di implementazione
description: Modelli di implementazione
source-git-commit: ac0c15b951f305e29bb8fa0bd45aa2c53de6ad15
workflow-type: tm+mt
source-wordcount: '62'
ht-degree: 0%

---


# Modelli di implementazione {#imp-models}

## Criteri lato server {#ss-policies}

Questo modello utilizzerà il CM come punto decisionale politico, delegando in tal modo la decisione di accesso al servizio.

Poiché il client non deve fare alcuna supposizione riguardo ai criteri applicati, l’implementazione deve verificare la decisione sull’inizializzazione della sessione e a intervalli regolari, durante la riproduzione dalla risposta heartbeat.
