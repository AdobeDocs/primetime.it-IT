---
description: L'implementazione di riferimento illustra come impostare il lettore per gli annunci, che include la configurazione dei metadati video per l'inserimento di annunci e la risoluzione degli annunci pre, mid e post-roll nei flussi video VOD o live/lineari. Illustra inoltre come gestire gli annunci cliccabili.
title: Inserimento di annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Inserimento annuncio {#ad-insertion}

L&#39;implementazione di riferimento illustra come impostare il lettore per gli annunci, che include la configurazione dei metadati video per l&#39;inserimento di annunci e la risoluzione degli annunci pre, mid e post-roll nei flussi video VOD o live/lineari. Illustra inoltre come gestire gli annunci cliccabili.

Il processo di configurazione di un lettore per l&#39;inserimento di annunci include:

* **Feed di input:** popolare un feed di input con metadati di annunci. Vedere [Formato catalogo](../set-up-dev-environment/exploring-code/catalog-format.md).
* **Adattatore di feed di implementazione di riferimento:** analisi del feed di input per compilare un oggetto metadati di un annuncio.
* **AdsManager:** Utilizzo di AdsManager per recuperare i metadati dell&#39;annuncio e creare il corrispondente AdProvider.