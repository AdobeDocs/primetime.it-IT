---
description: TVSDK inserisce il contenuto alternativo (annunci) nella timeline che corrisponde al contenuto principale.
title: Fase di inserimento dell’annuncio
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# Fase di inserimento dell’annuncio{#ad-insertion-phase}

TVSDK inserisce il contenuto alternativo (annunci) nella timeline che corrisponde al contenuto principale.

Al termine della fase di risoluzione degli annunci, TVSDK dispone di un elenco ordinato di risorse pubblicitarie raggruppate in interruzioni pubblicitarie. Ogni interruzione pubblicitaria è posizionata sulla timeline del contenuto principale utilizzando un valore di ora di inizio espresso in millisecondi (ms). Ogni annuncio in un’interruzione pubblicitaria ha una proprietà duration espressa anche in ms. Gli annunci in un’interruzione pubblicitaria sono concatenati uno dopo l’altro. Di conseguenza, la durata di un’interruzione pubblicitaria è uguale alla somma delle durate dei singoli annunci di composizione.

In questa fase può verificarsi il failover con conflitti che potrebbero verificarsi sulla timeline durante l’inserimento di annunci. Per combinazioni specifiche di valori di ora di inizio/durata dell’interruzione pubblicitaria, i segmenti dell’annuncio potrebbero sovrapporsi. La sovrapposizione si verifica quando l’ultima parte di un’interruzione pubblicitaria interseca l’inizio del primo annuncio nell’interruzione pubblicitaria successiva. In queste situazioni, TVSDK elimina l’interruzione pubblicitaria successiva e continua il processo di inserimento dell’annuncio con la voce successiva nell’elenco fino a quando tutte le interruzioni pubblicitarie non vengono inserite o eliminate.

TVSDK invia una notifica di avviso relativa all’errore e continua l’elaborazione.
