---
description: TVSDK inserisce nella timeline il contenuto alternativo (annunci) che corrisponde al contenuto principale.
seo-description: TVSDK inserisce nella timeline il contenuto alternativo (annunci) che corrisponde al contenuto principale.
seo-title: Fase di inserimento annunci
title: Fase di inserimento annunci
uuid: 4a8e9578-6e95-44c0-b045-ae3c20da75e9
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---


# Fase di inserimento annunci{#ad-insertion-phase}

TVSDK inserisce nella timeline il contenuto alternativo (annunci) che corrisponde al contenuto principale.

Al termine della fase di risoluzione degli annunci, TVSDK dispone di un elenco ordinato di risorse pubblicitarie raggruppate in interruzioni di annunci. Ogni interruzione di annuncio viene posizionata sulla timeline del contenuto principale utilizzando un valore di ora iniziale espresso in millisecondi (ms). Ogni annuncio in un&#39;interruzione annuncio ha una proprietà di durata che è anche espressa in ms. Gli annunci in un&#39;interruzione di pubblicità vengono concatenati uno dopo l&#39;altro. Di conseguenza, la durata di un&#39;interruzione di annuncio è uguale alla somma delle durate dei singoli annunci compositi.

Il failover può verificarsi in questa fase con conflitti che potrebbero verificarsi sulla timeline durante l&#39;inserimento di annunci. Per combinazioni specifiche di valori di inizio/durata dell&#39;interruzione di annunci, i segmenti di annunci potrebbero sovrapporsi. La sovrapposizione si verifica quando l&#39;ultima parte di un&#39;interruzione di annuncio interseca l&#39;inizio del primo annuncio nell&#39;interruzione di annuncio successiva. In queste situazioni, TVSDK elimina l’interruzione annuncio successiva e continua il processo di inserimento annunci con la voce successiva nell’elenco fino a quando tutte le interruzioni di annuncio non vengono inserite o eliminate.

TVSDK invia una notifica di avviso relativa all&#39;errore e continua l&#39;elaborazione.
