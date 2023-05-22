---
title: Risoluzione dei problemi
description: Risoluzione dei problemi
copied-description: true
exl-id: 618b1e19-d25d-435d-b118-b43455bde974
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '46'
ht-degree: 0%

---

# Risoluzione dei problemi{#troubleshooting}

* Per alcuni dispositivi meno recenti che eseguono API di livello 10 o superiore, logcat non è in grado di aprire il dispositivo di registro a causa di un problema di autorizzazioni. Viene visualizzata la seguente eccezione: `java.lang.Exception: logcat returns error: Unable to open log device '/dev/log/main': Permission denied` **Soluzione alternativa:**

   1. Apri [!DNL AndroidManifest.xml] sotto [!DNL CatalogActivity] progetto nell&#39;area di lavoro.

   1. Aggiungi la seguente autorizzazione alla [!DNL `AndroidManfest.xml`] file:

      ```
      android.permission.READ_LOGS
      ```
