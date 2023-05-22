---
description: Quando crei un pacchetto, puoi selezionare le seguenti opzioni di crittografia. Tuttavia, non è possibile modificare le opzioni di crittografia durante l'acquisizione della licenza
title: Rotazione tasti
exl-id: 1b439b5f-7a63-4fe2-ae15-c18cda0b31cd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---

# Rotazione tasti {#key-rotation}

Quando crei un pacchetto, puoi selezionare le seguenti opzioni di crittografia. Tuttavia, non è possibile modificare le opzioni di crittografia durante l&#39;acquisizione della licenza:

Durante la creazione del pacchetto, il contenuto viene generalmente crittografato utilizzando la chiave di crittografia del contenuto (CEK). Il client ottiene una licenza contenente il codice CEK per utilizzare il contenuto.

Quando abiliti la rotazione delle chiavi, la chiave di rotazione viene utilizzata per crittografare il contenuto e può essere modificata in modo che ogni chiave di rotazione venga utilizzata solo per crittografare una parte del contenuto. I tasti di rotazione sono protetti utilizzando la chiave di crittografia del contenuto e il client ottiene ancora una singola licenza contenente il codice di archiviazione per utilizzare il contenuto.

L’implementazione di Packager può controllare la chiave di crittografia del contenuto e le chiavi di rotazione utilizzate, nonché la frequenza con cui cambiano le chiavi di rotazione.

>[!NOTE]
>
>I contenuti inseriti mediante rotazione chiave possono essere riprodotti solo su client DRM Primetime versione 3.0 o successiva. I client meno recenti potrebbero dover eseguire l’aggiornamento per riprodurre questo contenuto.
