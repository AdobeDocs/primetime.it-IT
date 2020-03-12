---
seo-title: Risoluzione dei problemi
title: Risoluzione dei problemi
uuid: b7a41ea7-86c5-442c-b751-86a9055c5e35
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Risoluzione dei problemi{#troubleshooting}

* Per alcuni dispositivi meno recenti con API di livello 10 o precedente, logcat non è in grado di aprire il dispositivo di registro a causa di un problema di autorizzazioni. Viene visualizzata la seguente eccezione: `java.lang.Exception: logcat returns error: Unable to open log device '/dev/log/main': Permission denied` Soluzione **alternativa:**

   1. Aprite [!DNL AndroidManifest.xml] il progetto nell’ [!DNL CatalogActivity] area di lavoro.

   1. Aggiungete la seguente autorizzazione al [!DNL `AndroidManfest.xml`] file:

      ```
      android.permission.READ_LOGS
      ```
