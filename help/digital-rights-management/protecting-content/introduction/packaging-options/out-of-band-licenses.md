---
title: Licenze out-of-band
description: Licenze out-of-band
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# Licenze out-of-band {#out-of-band-licenses}

Utilizzando Primetime DRM, è possibile implementare un flusso di lavoro in cui i client ottengono licenze pregenerate fuori banda, eliminando quindi la necessità di distribuire un server licenze. Per supportare questo flusso di lavoro, è necessario specificare un&#39;opzione che indichi che non è disponibile alcun server licenze al momento della creazione del pacchetto. In questo modo si impedisce al client di richiedere una licenza per questo contenuto da un server licenze.

Il contenuto che indica la non disponibilità di un server licenze può essere riprodotto solo su client DRM Primetime versione 3.0 o successiva. I client meno recenti devono effettuare l’aggiornamento per riprodurre questo contenuto.
