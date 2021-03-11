---
description: Il browser TVSDK fornisce all’app video le informazioni necessarie per rispondere al clic di un utente su un annuncio cliccabile.
title: Annunci cliccabili
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# Panoramica {#clickable-ads-overview}

Il browser TVSDK fornisce all’app video le informazioni necessarie per rispondere al clic di un utente su un annuncio cliccabile.

Quando un utente fa clic su un annuncio selezionabile, una risposta tipica da un&#39;app video consiste nell&#39;aprire una nuova finestra del browser e passare all&#39;URL associato all&#39;annuncio. Per facilitare questa fase, il browser TVSDK attiva e invia notifiche che la tua app può utilizzare per gestire il processo di click-through.

Nell’app, puoi fornire all’utente un controllo su cui fare clic (ad esempio, un pulsante) durante la riproduzione dell’annuncio su cui è possibile fare clic. È necessario creare gestori per gli eventi attivati dal browser TVSDK associati all’annuncio (ad esempio, inizio dell’annuncio, clic dell’annuncio e completamento dell’annuncio). Infine, devi implementare i comportamenti specifici che la tua app seguirà al clic dell’annuncio (ad esempio, se mettere in pausa o meno l’annuncio, visualizzare l’URL di click-through e così via).

>[!NOTE]
>
>Il lettore di riferimento incluso nel browser TVSDK include una possibile soluzione di lavoro per l&#39;elaborazione degli annunci click-through.