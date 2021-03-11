---
title: Panoramica dell'utilità ID di AIR Publisher
description: Panoramica dell'utilità ID di AIR Publisher
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Panoramica dell&#39;utilità ID di AIR Publisher {#air-publisher-id-utility-overview}

Come parte del processo di creazione di un file AIR, l’AIR Developer Tool (ADT) genera un ID editore. Si tratta di un identificatore univoco per il certificato utilizzato per creare il file AIR. Se riutilizzi lo stesso certificato per più applicazioni AIR, queste avranno lo stesso ID editore. L&#39;utility AIR Publisher ID viene utilizzata per calcolare l&#39;ID editore per un&#39;applicazione AIR. Le versioni di AIR successive alla versione 1.5.2 non scrivono l&#39;ID editore generato in un file, pertanto è necessario utilizzare questo strumento per determinare l&#39;ID editore se si utilizza un elenco consentiti di applicazione AIR.

>[!NOTE]
>
>L&#39;ID editore, utilizzato per l&#39;applicazione dell&#39;elenco consentiti AIR, non è lo stesso ID editore specificato dall&#39;editore dell&#39;applicazione nel file [!DNL application.xml] dell&#39;applicazione.
