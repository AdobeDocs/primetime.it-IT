---
title: Parte iniziale del contenuto nella cancellazione
description: Parte iniziale del contenuto nella cancellazione
copied-description: true
exl-id: f291e0f5-ce26-41c4-b468-36b111cb7a1c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# Parte iniziale del contenuto nella cancellazione{#initial-portion-of-content-in-the-clear}

Questo parametro opzionale specifica un periodo di tempo (in secondi) dall’inizio del contenuto che non verrà crittografato.

Caso d’uso di esempio: consente un tempo di avvio della riproduzione più rapido mentre il client DRM di Primetime scarica la licenza in background. La parte non crittografata del video inizia la riproduzione immediatamente mentre l’inizializzazione e l’acquisizione della licenza avvengono in background. Quando questa funzione è disattivata, gli utenti potrebbero notare un ritardo nell’esperienza di riproduzione, perché il computer client esegue tutti i passaggi della licenza prima che si possa verificare qualsiasi riproduzione video.
