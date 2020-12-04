---
description: L'implementazione di riferimento illustra come impostare il lettore per gli annunci, che include l'impostazione di metadati video per l'inserimento di annunci e la risoluzione degli annunci pre, mid e post-roll nei flussi video VOD o live/lineari. Inoltre illustra come gestire gli annunci cliccabili.
seo-description: L'implementazione di riferimento illustra come impostare il lettore per gli annunci, che include l'impostazione di metadati video per l'inserimento di annunci e la risoluzione degli annunci pre, mid e post-roll nei flussi video VOD o live/lineari. Inoltre illustra come gestire gli annunci cliccabili.
seo-title: Inserimento annunci
title: Inserimento annunci
uuid: 75c1d77a-a7ff-4cb6-ad7f-7c83a950b7cb
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# Inserimento annunci {#ad-insertion}

L&#39;implementazione di riferimento illustra come impostare il lettore per gli annunci, che include l&#39;impostazione di metadati video per l&#39;inserimento di annunci e la risoluzione degli annunci pre, mid e post-roll nei flussi video VOD o live/lineari. Inoltre illustra come gestire gli annunci cliccabili.

Il processo di configurazione di un lettore per l&#39;inserimento di annunci include:

* **Feed di input:** Compilazione di un feed di input con metadati annuncio. Vedere [Formato catalogo](../set-up-dev-environment/exploring-code/catalog-format.md).
* **Scheda di feed implementazione di riferimento:** analisi del feed di input per compilare un oggetto di metadati annuncio.
* **AdsManager:** Utilizzo di AdsManager per recuperare i metadati dell&#39;annuncio e creare il corrispondente AdProvider.