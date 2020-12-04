---
seo-title: Panoramica dell'utilità ID di AIR Publisher
title: Panoramica dell'utilità ID di AIR Publisher
uuid: 31aecc0e-ad9b-43ad-ba58-77d2c999f4a4
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Panoramica dell&#39;utility ID di AIR Publisher {#air-publisher-id-utility-overview}

Come parte del processo di creazione di un file AIR, ADT (AIR Developer Tool) genera un ID Publisher. Si tratta di un identificatore univoco per il certificato utilizzato per creare il file AIR. Se riutilizzate lo stesso certificato per più applicazioni AIR, queste avranno lo stesso ID editore. L&#39;utilità ID di pubblicazione AIR viene utilizzata per calcolare l&#39;ID di editore per un&#39;applicazione AIR. Le versioni di AIR successive alla 1.5.2 non scrivono l&#39;ID editore generato in un file, pertanto è necessario utilizzare questo strumento per determinare l&#39;ID editore se si utilizza un&#39;applicazione AIR  elenco consentiti.

>[!NOTE]
>
>L&#39;ID editore, utilizzato per l&#39;imposizione di elenchi consentiti di AIR , non è uguale all&#39;ID editore specificato dall&#39;editore dell&#39;applicazione nel file [!DNL application.xml] dell&#39;applicazione.
