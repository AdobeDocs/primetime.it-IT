---
description: È possibile implementare una barra di controllo con supporto DVR per VOD e streaming dal vivo. Il supporto DVR include il concetto di una finestra ricercabile e il punto attivo del cliente.
seo-description: È possibile implementare una barra di controllo con supporto DVR per VOD e streaming dal vivo. Il supporto DVR include il concetto di una finestra ricercabile e il punto attivo del cliente.
seo-title: Costruire una barra di controllo migliorata per il DVR
title: Costruire una barra di controllo migliorata per il DVR
uuid: 83c56def-a454-4f26-bdfc-2ef2497ef9bd
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# Costruire una barra di controllo migliorata per DVR{#construct-a-control-bar-enhanced-for-dvr}

È possibile implementare una barra di controllo con supporto DVR per VOD e streaming dal vivo. Il supporto DVR include il concetto di una finestra ricercabile e il punto attivo del cliente.

* Per VOD, la lunghezza della finestra ricercabile corrisponde alla durata dell’intera risorsa.
* Per lo streaming dal vivo, la lunghezza della finestra DVR (ricercabile) è definita come l&#39;intervallo di tempo che inizia dalla finestra di riproduzione dal vivo e termina al punto attivo del client.

   Il punto attivo del client viene calcolato sottraendo la lunghezza del buffer dall&#39;estremità della finestra dal vivo. La durata di destinazione è un valore maggiore o uguale alla durata massima di un frammento nel manifesto.

   La barra di controllo per la riproduzione dal vivo supporta il DVR posizionando prima il pollice nel punto di vita del client all&#39;avvio della riproduzione e visualizzando un&#39;area che contrassegna l&#39;area in cui non è consentita la ricerca.

Per una barra di controllo:

1. Aggiungete una sovrapposizione alla barra di controllo che rappresenta l’intervallo di riproduzione.

1. Quando l&#39;utente inizia a cercare, controlla se la posizione di ricerca desiderata è compresa nell&#39;intervallo ricercabile.
