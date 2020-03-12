---
description: TVSDK Primetime Reference è un’applicazione Android basata sui framework TVSDK e AVE.
seo-description: TVSDK Primetime Reference è un’applicazione Android basata sui framework TVSDK e AVE.
seo-title: Creare l'implementazione di riferimento Primetime
title: Creare l'implementazione di riferimento Primetime
uuid: ab12660a-1563-49a4-82d9-1ab13f8a92be
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Creare l&#39;implementazione di riferimento Primetime {#build-the-primetime-reference-implementation}

TVSDK Primetime Reference è un’applicazione Android basata sui framework TVSDK e AVE.

Per impostare e creare il progetto Primetime Reference in Eclipse:

1. Scaricate il file zip TVSDK Android e decomprimetelo in una directory in una posizione che ricorderete.
1. Avvia Eclipse.
1. Selezionare **[!UICONTROL File]** > **[!UICONTROL Import]**.
1. Selezionare **[!UICONTROL Android]** > **[!UICONTROL Existing Android Code Into Workspace]**.
1. Clic **[!UICONTROL Next]**.
1. Utilizzate il **[!UICONTROL Browse]** pulsante per compilare il **[!UICONTROL Root Directory]** campo con la directory in cui avete decompresso il file zip TVSDK Android [!DNL samples/PrimetimeReference/src] .
1. Selezionate i seguenti progetti da importare: **[!UICONTROL appcompat]**, **[!UICONTROL PrimetimeReference]**..
1. Clic **[!UICONTROL Finish]**.
1. Selezionate **[!UICONTROL Project]** > **[!UICONTROL Build Project]** per creare il progetto.

   Questo passaggio non è necessario se il progetto è impostato per la creazione automatica.
1. Se desiderate includere il progetto test nell&#39;area di lavoro, associatelo al progetto PrimetimeReference:
   1. Ripetere i passaggi 3. fino a 6.
   1. Selezionate il progetto seguente da importare: `PrimetimeReference\tests`.
   1. Clic **[!UICONTROL Finish]**.

      Il progetto test ha una dipendenza dal progetto CatalogActivity, pertanto devi associare il progetto test al progetto CatalogActivity.
   1. Fate clic con il pulsante destro del mouse **[!UICONTROL tests]** e scegliete **[!UICONTROL Properties]**.
   1. Selezionate la **[!UICONTROL Projects]** scheda in Percorso build Java.
   1. Clic **[!UICONTROL Add...]**
   1. Selezionate CatalogActivity.
   1. Fate clic **[!UICONTROL OK]** per aggiungere il progetto.
   1. Fare clic **[!UICONTROL OK]** per uscire dalla pagina Proprietà.
   1. Selezionate **[!UICONTROL Project]** > **[!UICONTROL Build Project]** per creare il progetto.

      Questo passaggio non è necessario se il progetto è impostato per la creazione automatica.
