---
description: Il browser TVSDK fornisce alla tua app video le informazioni necessarie per rispondere al clic di un utente su un annuncio cliccabile.
title: Annunci cliccabili
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# Panoramica {#clickable-ads-overview}

Il browser TVSDK fornisce alla tua app video le informazioni necessarie per rispondere al clic di un utente su un annuncio cliccabile.

Quando un utente fa clic su un annuncio cliccabile, una risposta tipica da un’app video consiste nell’aprire una nuova finestra del browser e passare all’URL associato all’annuncio. Per facilitare questa fase, il TVSDK del browser attiva notifiche e notifiche che l’app può utilizzare per gestire il processo di click-through.

Nell’app, puoi fornire all’utente un controllo su cui fare clic (ad esempio un pulsante) durante la riproduzione dell’annuncio cliccabile. È necessario creare gestori per gli eventi generati dal TVSDK del browser associati all’annuncio (ad esempio, avvio, clic e completamento dell’annuncio). Infine, devi implementare i comportamenti specifici che l’app seguirà al clic dell’annuncio di un utente (ad esempio, se mettere in pausa o meno l’annuncio, visualizzare l’URL di click-through e così via).

>[!NOTE]
>
>Il lettore di riferimento incluso in Browser TVSDK include una possibile soluzione di lavoro per l’elaborazione di annunci click-through.
