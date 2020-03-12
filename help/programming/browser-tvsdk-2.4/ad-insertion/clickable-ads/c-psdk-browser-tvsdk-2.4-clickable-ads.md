---
description: Browser TVSDK fornisce all'app video le informazioni necessarie per rispondere al clic di un utente su un annuncio cliccabile.
seo-description: Browser TVSDK fornisce all'app video le informazioni necessarie per rispondere al clic di un utente su un annuncio cliccabile.
seo-title: Annunci cliccabili
title: Annunci cliccabili
uuid: 493c3199-b5ba-4809-86eb-e80f10eb957b
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Panoramica {#clickable-ads-overview}

Browser TVSDK fornisce all&#39;app video le informazioni necessarie per rispondere al clic di un utente su un annuncio cliccabile.

Quando un utente fa clic su un annuncio selezionabile, una tipica risposta da un&#39;app video consiste nell&#39;aprire una nuova finestra del browser e passare all&#39;URL associato all&#39;annuncio. Per facilitare questa fase, Browser TVSDK avvia e invia notifiche che la tua app può utilizzare per gestire il processo di click-through.

Nell&#39;app, puoi fornire all&#39;utente un controllo su cui fare clic (ad esempio, un pulsante) durante la riproduzione dell&#39;annuncio cliccabile. È necessario creare gestori per gli eventi attivati da Browser TVSDK associati all&#39;annuncio (ad esempio, inizio dell&#39;annuncio, clic dell&#39;annuncio e completamento). Infine, devi implementare i comportamenti specifici che la tua app seguirà dopo un clic dell&#39;utente (ad esempio, se mettere in pausa o meno l&#39;annuncio, visualizzare l&#39;URL di click-through e così via).

>[!NOTE]
>
>Il lettore di riferimento incluso con Browser TVSDK include una possibile soluzione di lavoro per l&#39;elaborazione di annunci click-through.