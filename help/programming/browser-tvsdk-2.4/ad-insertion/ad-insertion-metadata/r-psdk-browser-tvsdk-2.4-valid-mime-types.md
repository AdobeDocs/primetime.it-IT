---
description: Un annuncio potrebbe avere più contenuti creativi, di cui uno selezionato per essere riprodotto.
title: Tipi mime validi
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# Tipi mime validi{#valid-mime-types}

Un annuncio potrebbe avere più contenuti creativi, di cui uno selezionato per essere riprodotto.

Con i tipi mime, puoi specificare il tipo creativo che gli utenti possono dare priorità. I tipi mime specificati dagli utenti e i tipi mime supportati da Browser TVSDK vengono utilizzati per determinare quale creatività avrà priorità.

Per impostare i tipi mime validi nel TVSDK del browser:

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var mimeTypes = [“video/mp4”, “application/x-mpegURL”]; 
auditudeSettings.validMimeTypes = mimeTypes; 
```

dove `mimeTypes` è una matrice di stringhe e ogni stringa rappresenta un tipo mime.

Se vengono restituiti più file multimediali per un annuncio, la selezione dipende dall’ordine in cui i file multimediali vengono visualizzati in `validMimeTypes` array. Ai tipi mime con indice più basso viene data una preferenza rispetto a quelli con indice più alto.
