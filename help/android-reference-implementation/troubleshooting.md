---
title: Risoluzione dei problemi
description: Risoluzione dei problemi
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '46'
ht-degree: 0%

---


# Risoluzione dei problemi{#troubleshooting}

* Per alcuni dispositivi meno recenti con API di livello 10 o più recente, logcat non è in grado di aprire il dispositivo di registro a causa di un problema di autorizzazioni. Viene visualizzata la seguente eccezione: `java.lang.Exception: logcat returns error: Unable to open log device '/dev/log/main': Permission denied` **Soluzione:**

   1. Apri [!DNL AndroidManifest.xml] nel progetto [!DNL CatalogActivity] nell&#39;area di lavoro.

   1. Aggiungi la seguente autorizzazione al file [!DNL `AndroidManfest.xml`] :

      ```
      android.permission.READ_LOGS
      ```
