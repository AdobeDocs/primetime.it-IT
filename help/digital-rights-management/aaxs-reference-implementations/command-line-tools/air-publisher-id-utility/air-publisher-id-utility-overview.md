---
seo-title: Panoramica dell'utilità ID di AIR Publisher
title: Panoramica dell'utilità ID di AIR Publisher
uuid: 31aecc0e-ad9b-43ad-ba58-77d2c999f4a4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Panoramica dell&#39;utilità ID di AIR Publisher {#air-publisher-id-utility-overview}

Come parte del processo di creazione di un file AIR, ADT (AIR Developer Tool) genera un ID Publisher. Si tratta di un identificatore univoco per il certificato utilizzato per creare il file AIR. Se riutilizzate lo stesso certificato per più applicazioni AIR, queste avranno lo stesso ID editore. L&#39;utilità ID di pubblicazione AIR viene utilizzata per calcolare l&#39;ID di editore per un&#39;applicazione AIR. Le versioni di AIR successive alla 1.5.2 non scrivono l&#39;ID editore generato in un file, pertanto è necessario utilizzare questo strumento per determinare l&#39;ID editore se si utilizza una whitelist di applicazioni AIR.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>L&#39;ID editore, utilizzato per l&#39;imposizione della whitelist AIR, non è lo stesso ID editore specificato dall&#39;editore dell&#39;applicazione nel [!DNL application.xml] file dell&#39;applicazione.

