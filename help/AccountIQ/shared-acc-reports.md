---
title: Rapporti sugli account condivisi
description: Report account condivisi
exl-id: 16c5ded1-2a95-4373-8b90-b445131f333a
source-git-commit: dd1001d94e32a1a8b5346ff97b0f6cb7d244dcf2
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# Report account condivisi {#shared-accounts-reports}

I rapporti Account condivisi suddividono le metriche quali il numero di dispositivi e i tipi di dispositivi in base all&#39;intervallo selezionato di probabilità di condivisione, ad esempio **Probabilità eccessiva** e **Probabilità eccessiva** per il segmento corrente.

Questi intervalli possono quindi fungere da soglie definite dall’utente e i grafici vengono aggiornati in base alle soglie selezionate.

L’account IQ classifica tutti i conti degli abbonati del segmento definito nei conti con le seguenti cinque categorie in base alle loro probabilità di condivisione:

* Molto elevato (80%-100%)
* Elevato (60%-80%)
* Moderato (40%-60%)
* Bassa (20%-40%)
* Molto basso (0%-20%)

## Probabilità di condivisione account {#accounts-sharing-probability}

Il grafico ad anello qui classifica e mostra le percentuali (e i numeri assoluti) dei conti degli abbonati da varie categorie di probabilità.

La linea rossa indica l’intervallo di soglia selezionato dagli utenti in [Conti oltre la soglia del segmento corrente](#threshold-selector) pannello.

![](assets/accounts-sharing-probability-pie.png)

Il grafico a barre traccia il numero di account sull&#39;asse y per varie categorie di probabilità di condivisione (tracciati sull&#39;asse x).

![](assets/accounts-sharing-probability-bar.png)

La linea rossa indica l’intervallo di soglia e può essere regolata nel grafico a barre. La soglia regolata nel grafico a barre si riflette nell&#39;intervallo di soglia nel grafico a tendina.

<!--![](assets/shared-accounts-rep.gif)-->

### Conti oltre la soglia del segmento corrente{#threshold-selector}

Questo pannello consente di selezionare un intervallo tra le seguenti soglie per gli account abbonati (in base alle loro probabilità di condivisione):

* Account **molto basso** condivisione **probabilità**

* Account **più basso** condivisione **probabilità**

* Account **troppo moderato** condivisione **probabilità**

* Account **superiore** condivisione **probabilità**

![](assets/threshold-selector-shared-accounts.png)

Una volta selezionata la soglia, il pannello mostra la percentuale (e il numero) di account su tutti gli account abbonati nel segmento selezionato.

## Segmento - Richieste di riproduzione dal totale {#play-request-out-total}

Il grafico ad anello mostra la percentuale (e il numero) di richieste di riproduzione effettuate dagli abbonati al segmento; e ti consente di confrontare le richieste di riproduzione effettuate dagli abbonati non nel segmento definito.

![](assets/play-req-outof-total.png)

Quando sposti il cursore sul grafico ad anello, mostra anche le percentuali degli abbonati e i numeri da vari intervalli di probabilità.

<!--![](assets/play-request-total.gif)-->

## Numero medio di dispositivi per account{#avg-devices-account}

Il grafico a barre mostra il numero medio di dispositivi di ogni tipo di dispositivo utilizzati dagli abbonati al segmento corrente e dagli abbonati non al segmento corrente.

![](assets/avg-devices-per-acc.png)

## Segmento: codici postali per periodo per conto {#zip-codes-period-account}

Questo grafico ti informa sul numero di abbonati che consumano contenuti da diverse posizioni in un intervallo di tempo.

![](assets/zip-period-account.png)

È possibile ingrandire per restringere e visualizzare le specifiche di una barra nel grafico che traccia una serie di posizioni.

<!--![](assets/zip-code-period.gif)-->

## Segmento: estensione geografica/periodo/account {#geo-span-period-account}

Questo grafico a barre mostra il numero di conti utente con sottoscrizione in relazione a diversi intervalli geografici in miglia. L&#39;intervallo si basa sulla distanza massima tra le posizioni da cui un utente iscritto ha trasmesso lo streaming durante l&#39;intervallo di tempo.

<!--Total number of users ...

How many accounts are within 99 miles of each other.....and how many are apart. 

Based on points on the map.-->

![](assets/geogr-span-account.png)

Quando selezioni una barra che rappresenta un intervallo di distanza geografica, espande l’intervallo per visualizzare ulteriori dettagli.

<!--![](assets/geo-span-period-acc.gif)-->
