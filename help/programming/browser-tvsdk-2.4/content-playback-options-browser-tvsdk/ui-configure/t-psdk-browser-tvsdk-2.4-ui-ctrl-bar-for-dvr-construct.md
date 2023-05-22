---
description: È possibile implementare una barra di controllo con supporto DVR per VOD e streaming live. Il supporto DVR include il concetto di finestra ricercabile e il punto di attivazione del client.
title: Creare una barra di controllo ottimizzata per DVR
exl-id: e4846f1e-bc57-452b-b393-8f8f55434e7a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# Creare una barra di controllo ottimizzata per DVR{#construct-a-control-bar-enhanced-for-dvr}

È possibile implementare una barra di controllo con supporto DVR per VOD e streaming live. Il supporto DVR include il concetto di finestra ricercabile e il punto di attivazione del client.

* Per VOD, la lunghezza della finestra ricercabile corrisponde alla durata dell’intera risorsa.
* Per lo streaming live, la lunghezza della finestra del DVR (ricercabile) è definita come l’intervallo di tempo che inizia dalla finestra di riproduzione live e termina nel punto live del client.

   Il punto di attivazione del client viene calcolato sottraendo la lunghezza nel buffer dalla fine della finestra attiva. La durata target è un valore maggiore o uguale alla durata massima di un frammento nel manifesto.

   La barra di controllo per la riproduzione dal vivo supporta DVR posizionando prima il pollice in corrispondenza del punto attivo del client all’avvio della riproduzione e visualizzando una regione che contrassegna l’area in cui non è consentita la ricerca.

Per una barra di controllo:

1. Aggiungi una sovrapposizione alla barra di controllo che rappresenta l’intervallo di riproduzione.

1. Quando l’utente inizia a cercare, controlla se la posizione di ricerca desiderata si trova all’interno dell’intervallo ricercabile.
