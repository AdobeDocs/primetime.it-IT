---
description: Il riferimento Primetime di TVSDK è un’applicazione Android basata sui framework TVSDK e AVE.
title: Creare l’implementazione di riferimento di Primetime
exl-id: d2950f2b-06d7-4fc8-a031-5f058ce47545
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# Creare l’implementazione di riferimento di Primetime {#build-the-primetime-reference-implementation}

Il riferimento Primetime di TVSDK è un’applicazione Android basata sui framework TVSDK e AVE.

Per impostare e generare il progetto Primetime Reference in Eclipse:

1. Scarica il file zip TVSDK Android e decomprimi il file in una directory in una posizione che ricorderai.
1. Avvia Eclipse.
1. Seleziona **[!UICONTROL File]** > **[!UICONTROL Import]**.
1. Seleziona **[!UICONTROL Android]** > **[!UICONTROL Existing Android Code Into Workspace]**.
1. Clic **[!UICONTROL Next]**.
1. Utilizza il **[!UICONTROL Browse]** per popolare il **[!UICONTROL Root Directory]** con la directory in [!DNL samples/PrimetimeReference/src] in cui è stato decompresso il file zip TVSDK Android.
1. Seleziona i seguenti progetti da importare: **[!UICONTROL appcompat]**, **[!UICONTROL PrimetimeReference]**.
1. Clic **[!UICONTROL Finish]**.
1. Seleziona  **[!UICONTROL Project]** > **[!UICONTROL Build Project]** per generare il progetto.

   Questo passaggio non è necessario se il progetto è configurato per la generazione automatica.
1. Se si desidera includere il progetto test nell&#39;area di lavoro, associare il progetto test al progetto PrimetimeReference:
   1. Ripetere i passaggi 3. da 6 a 6.
   1. Seleziona il seguente progetto da importare: `PrimetimeReference\tests`.
   1. Clic **[!UICONTROL Finish]**.

      Il progetto test ha una dipendenza dal progetto CatalogActivity, pertanto è necessario associare il progetto test al progetto CatalogActivity.
   1. Clic con il pulsante destro **[!UICONTROL tests]** e scegli **[!UICONTROL Properties]**.
   1. Seleziona la **[!UICONTROL Projects]** in Percorso build Java.
   1. Clic **[!UICONTROL Add...]**
   1. Seleziona Attività catalogo.
   1. Clic **[!UICONTROL OK]** per aggiungere il progetto.
   1. Clic **[!UICONTROL OK]** per uscire dalla pagina Proprietà.
   1. Seleziona  **[!UICONTROL Project]** > **[!UICONTROL Build Project]** per generare il progetto.

      Questo passaggio non è necessario se il progetto è configurato per la generazione automatica.
