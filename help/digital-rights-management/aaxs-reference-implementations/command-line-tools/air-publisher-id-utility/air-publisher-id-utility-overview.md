---
title: Panoramica dell'utilità AIR Publisher ID
description: Panoramica dell'utilità AIR Publisher ID
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Panoramica dell&#39;utilità AIR Publisher ID {#air-publisher-id-utility-overview}

Durante la creazione di un file AIR, AIR Developer Tool (ADT) genera un ID di pubblicazione. Questo è un identificatore univoco del certificato utilizzato per generare il file AIR. Se si riutilizza lo stesso certificato per più applicazioni AIR, queste avranno lo stesso ID editore.L&#39;utility AIR Publisher ID viene utilizzata per calcolare l&#39;ID editore per un&#39;applicazione AIR. Le versioni di AIR successive alla 1.5.2 non scrivono l’ID dell’editore generato in un file, pertanto è necessario utilizzare questo strumento per determinare l’ID dell’editore se si utilizza un elenco consentiti di applicazione AIR.

>[!NOTE]
>
>L’ID del server di pubblicazione, utilizzato per l’applicazione dell’elenco consentiti AIR, non è lo stesso dell’ID del server di pubblicazione specificato dal server di pubblicazione dell’applicazione nel file [!DNL application.xml] file.
