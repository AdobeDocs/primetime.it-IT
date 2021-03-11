---
description: È possibile implementare una barra di controllo con supporto DVR per VOD e streaming live. Il supporto DVR include il concetto di una finestra ricercabile e il punto live del cliente.
title: Costruire una barra di controllo migliorata per il DVR
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---


# Costruire una barra di controllo migliorata per DVR{#construct-a-control-bar-enhanced-for-dvr}

È possibile implementare una barra di controllo con supporto DVR per VOD e streaming live. Il supporto DVR include il concetto di una finestra ricercabile e il punto live del cliente.

* Per VOD, la lunghezza della finestra ricercabile corrisponde alla durata dell’intera risorsa.
* Per lo streaming dal vivo, la lunghezza della finestra DVR (ricercabile) è definita come l&#39;intervallo di tempo che inizia dalla finestra di riproduzione dal vivo e termina al punto dal vivo del client.

   Il punto live del client viene calcolato sottraendo la lunghezza del buffered dall&#39;estremità della finestra live. La durata di destinazione è un valore maggiore o uguale alla durata massima di un frammento nel manifesto.

   La barra di controllo per la riproduzione in diretta supporta il DVR posizionando prima il pollice nel punto di attivazione del client all&#39;avvio della riproduzione e visualizzando una regione che contrassegna l&#39;area in cui la ricerca non è consentita.

Per una barra di controllo:

1. Aggiungi una sovrapposizione alla barra di controllo che rappresenta l’intervallo di riproduzione.

1. Quando l’utente inizia a cercare, controlla se la posizione di ricerca desiderata si trova nell’intervallo ricercabile.
