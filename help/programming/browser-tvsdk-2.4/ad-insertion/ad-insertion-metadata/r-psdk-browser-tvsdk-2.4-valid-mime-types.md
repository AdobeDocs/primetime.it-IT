---
description: Un annuncio potrebbe avere più elementi creativi, di cui uno selezionato per la riproduzione.
seo-description: Un annuncio potrebbe avere più elementi creativi, di cui uno selezionato per la riproduzione.
seo-title: Tipi mime validi
title: Tipi mime validi
uuid: ab2baac9-a9ef-44f1-83a1-2e6e471e3231
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Tipi mime validi{#valid-mime-types}

Un annuncio potrebbe avere più elementi creativi, di cui uno selezionato per la riproduzione.

Con i tipi mime, potete specificare quali tipi creativi gli utenti possono assegnare priorità. I tipi mime specificati dagli utenti e i tipi mime supportati da Browser TVSDK vengono utilizzati per determinare quali creativi verranno assegnati priorità.

Per impostare i tipi mime validi in Browser TVSDK:

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var mimeTypes = [“video/mp4”, “application/x-mpegURL”]; 
auditudeSettings.validMimeTypes = mimeTypes; 
```

dove `mimeTypes` è un array di stringhe e ogni stringa rappresenta un tipo mime.

Se per un annuncio vengono restituiti più file multimediali, la selezione dipende dall&#39;ordine in cui i file multimediali vengono visualizzati nell&#39; `validMimeTypes` array. Ai tipi mime con indice inferiore viene assegnata una preferenza rispetto a quelli con indice più alto.
