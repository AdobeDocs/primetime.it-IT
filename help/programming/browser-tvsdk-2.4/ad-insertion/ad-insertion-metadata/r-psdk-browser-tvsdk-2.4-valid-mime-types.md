---
description: Un annuncio potrebbe avere più contenuti creativi, di cui uno selezionato per la riproduzione.
title: Tipi mime validi
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# Tipi di mime validi{#valid-mime-types}

Un annuncio potrebbe avere più contenuti creativi, di cui uno selezionato per la riproduzione.

Con i tipi mime, puoi specificare quali tipi creativi gli utenti possono assegnare la priorità. I tipi mime specificati dagli utenti e i tipi mime supportati dall&#39;SDK del browser vengono utilizzati per determinare quale creativo avrà la priorità.

Per impostare i tipi di mime validi in Browser TVSDK:

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var mimeTypes = [“video/mp4”, “application/x-mpegURL”]; 
auditudeSettings.validMimeTypes = mimeTypes; 
```

dove `mimeTypes` è una matrice di stringhe e ogni stringa rappresenta un tipo mime.

Nel caso in cui vengano restituiti più file multimediali per un annuncio, la selezione dipende dall’ordine in cui i file multimediali vengono visualizzati nella matrice `validMimeTypes`. Ai tipi mime con indice inferiore viene data una preferenza rispetto a quelli con indice più alto.
