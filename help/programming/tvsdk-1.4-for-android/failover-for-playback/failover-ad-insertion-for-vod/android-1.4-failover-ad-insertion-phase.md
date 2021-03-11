---
description: TVSDK inserisce il contenuto alternativo (annunci) nella timeline che corrisponde al contenuto principale.
title: Fase di inserimento annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# Fase di inserimento annunci{#ad-insertion-phase}

TVSDK inserisce il contenuto alternativo (annunci) nella timeline che corrisponde al contenuto principale.

Al termine della fase di risoluzione degli annunci, TVSDK dispone di un elenco ordinato di risorse di annunci raggruppate in interruzioni di annunci. Ogni interruzione pubblicitaria viene posizionata nella timeline del contenuto principale utilizzando un valore di tempo iniziale espresso in millisecondi (ms). Ogni annuncio in un&#39;interruzione pubblicitaria ha una proprietà di durata che è espressa anche in ms. Gli annunci in una pausa pubblicitaria vengono incatenati uno dopo l&#39;altro. Di conseguenza, la durata di un’interruzione pubblicitaria è uguale alla somma delle durate dei singoli annunci compositi.

Il failover può verificarsi in questa fase con conflitti che potrebbero verificarsi nella timeline durante l&#39;inserimento di annunci. Per combinazioni specifiche di valori di inizio/durata di un’interruzione pubblicitaria, i segmenti di annunci potrebbero sovrapporsi. La sovrapposizione si verifica quando l’ultima parte di un’interruzione pubblicitaria interseca l’inizio del primo annuncio nell’interruzione pubblicitaria successiva. In queste situazioni, TVSDK elimina l’interruzione pubblicitaria successiva e continua il processo di inserimento degli annunci con la voce successiva nell’elenco fino a quando tutte le interruzioni di annunci non vengono inserite o scartate.

TVSDK invia una notifica di avviso relativa all’errore e continua l’elaborazione.
