---
description: L’implementazione di riferimento illustra come impostare il lettore per gli annunci, che include la configurazione dei metadati video per l’inserimento di annunci e la risoluzione degli annunci pre, mid e post-roll in flussi video VOD o live/lineari. Illustra inoltre come gestire gli annunci cliccabili.
title: Inserimento di annunci
exl-id: 3c2d8fca-2a0e-4577-81f3-7b390f6396e1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Inserimento di annunci {#ad-insertion}

L’implementazione di riferimento illustra come impostare il lettore per gli annunci, che include la configurazione dei metadati video per l’inserimento di annunci e la risoluzione degli annunci pre, mid e post-roll in flussi video VOD o live/lineari. Illustra inoltre come gestire gli annunci cliccabili.

Il processo di configurazione di un lettore per l’inserimento di annunci include:

* **Feed di input:** Compilazione di un feed di input con metadati di annunci. Consulta [Formato catalogo](../set-up-dev-environment/exploring-code/catalog-format.md).
* **Adattatore feed di implementazione di riferimento:** Analisi del feed di input per compilare un oggetto metadati di annunci.
* **Gestione annunci:** Utilizzo di AdsManager per recuperare i metadati dell’annuncio e creare l’AdProvider corrispondente.
