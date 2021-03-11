---
description: Il riferimento TVSDK Primetime è un’applicazione Android basata sui framework TVSDK e AVE.
title: Creare l’implementazione di riferimento di Primetime
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 1%

---


# Creare l&#39;implementazione di riferimento di Primetime {#build-the-primetime-reference-implementation}

Il riferimento TVSDK Primetime è un’applicazione Android basata sui framework TVSDK e AVE.

Per impostare e creare il progetto di riferimento Primetime in Eclipse:

1. Scarica il file zip TVSDK Android e decomprimi in una directory in una posizione che ricorderai.
1. Avvia Eclipse.
1. Selezionare **[!UICONTROL File]** > **[!UICONTROL Import]**.
1. Selezionare **[!UICONTROL Android]** > **[!UICONTROL Existing Android Code Into Workspace]**.
1. Clic **[!UICONTROL Next]**.
1. Utilizza il pulsante **[!UICONTROL Browse]** per compilare il campo **[!UICONTROL Root Directory]** con la directory in [!DNL samples/PrimetimeReference/src] a cui hai decompresso il file zip TVSDK Android.
1. Seleziona i seguenti progetti da importare: **[!UICONTROL appcompat]**, **[!UICONTROL PrimetimeReference]**.
1. Clic **[!UICONTROL Finish]**.
1. Seleziona **[!UICONTROL Project]** > **[!UICONTROL Build Project]** per creare il progetto.

   Questo passaggio non è necessario se il progetto è configurato per la generazione automatica.
1. Se desideri includere il progetto test nell’area di lavoro, associa il progetto test al progetto PrimetimeReference:
   1. Ripetere i passaggi 3. da 6 a 6.
   1. Seleziona il seguente progetto da importare: `PrimetimeReference\tests`.
   1. Clic **[!UICONTROL Finish]**.

      Il progetto test ha una dipendenza dal progetto CatalogActivity ed è quindi necessario associare il progetto test al progetto CatalogActivity.
   1. Fai clic con il pulsante destro del mouse su **[!UICONTROL tests]** e scegli **[!UICONTROL Properties]**.
   1. Seleziona la scheda **[!UICONTROL Projects]** in Percorso build Java.
   1. Clic **[!UICONTROL Add...]**
   1. Seleziona Attività catalogo.
   1. Fai clic su **[!UICONTROL OK]** per aggiungere il progetto.
   1. Fai clic su **[!UICONTROL OK]** per uscire dalla pagina Proprietà .
   1. Seleziona **[!UICONTROL Project]** > **[!UICONTROL Build Project]** per creare il progetto.

      Questo passaggio non è necessario se il progetto è configurato per la generazione automatica.
