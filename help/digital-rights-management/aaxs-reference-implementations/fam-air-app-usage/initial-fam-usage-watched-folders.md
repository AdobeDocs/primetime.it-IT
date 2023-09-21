---
title: Cartelle controllate
description: Cartelle controllate
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# Cartelle controllate {#watched-folders}

È possibile utilizzare Cartelle controllate per creare automaticamente pacchetti di contenuto creato in determinate cartelle. Ogni cartella controllata può essere configurata con diverse opzioni di creazione pacchetti. Per verificare le opzioni di creazione dei pacchetti prima di creare una cartella controllata, utilizza la scheda Package Media.

Per creare una cartella controllata, fai clic su **[!UICONTROL Add New Watched Folder]** e compila le opzioni di imballaggio. Consulta la [Creazione di pacchetti di file multimediali](../../aaxs-protecting-content/content-packaging-media-files/content-packaging-media-files-overview.md) per una descrizione di ciascuna opzione. Al termine, fai clic su **[!UICONTROL Save Watched Folder Properties]**.

Quando viene salvata una cartella controllata, le opzioni di creazione pacchetti vengono salvate in *[Cartella di input]* [!DNL \properties\watchfolder.properties]. Tutti i contenuti aggiunti alla cartella di input che soddisfano i criteri di selezione dei file multimediali di input verranno automaticamente inseriti in un pacchetto e inseriti nella cartella di output. Consulta le Preferenze cartella controllata globale nella sezione [Preferenze Packager](../../aaxs-reference-implementations/fam-air-app-usage/initial-fam-setup-set-prefs/initial-fam-setup-pkg-prefs.md) per configurare ulteriori opzioni della cartella controllata.

Per modificare le impostazioni della cartella controllata, seleziona il percorso di input della cartella controllata dall’elenco nella parte superiore dello schermo. Modifica le impostazioni e fai clic su **[!UICONTROL Save Watched Folder Properties]**.

Per eliminare una cartella controllata, seleziona il percorso di input della cartella controllata dall’elenco nella parte superiore dello schermo e fai clic su **[!UICONTROL Delete Watched Folder Properties]**.
