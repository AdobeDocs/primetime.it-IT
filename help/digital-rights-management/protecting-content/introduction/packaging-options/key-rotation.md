---
description: 'Quando crei un pacchetto, puoi selezionare le seguenti opzioni di crittografia. Tuttavia, non è possibile modificare le opzioni di crittografia durante l''acquisizione della licenza '
title: Rotazione tasti
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---


# Rotazione chiave {#key-rotation}

Quando crei un pacchetto, puoi selezionare le seguenti opzioni di crittografia. Tuttavia, non è possibile modificare le opzioni di crittografia durante l&#39;acquisizione della licenza:

Durante la creazione del pacchetto, il contenuto viene in genere crittografato utilizzando la chiave di crittografia del contenuto (CEK). Il client ottiene una licenza contenente la CEK per utilizzare il contenuto.

Quando abiliti la rotazione delle chiavi, la chiave di rotazione viene utilizzata per cifrare il contenuto e la chiave può essere modificata in modo che ogni chiave di rotazione sia utilizzata solo per cifrare una parte del contenuto. Le chiavi di rotazione sono protette utilizzando la chiave di crittografia del contenuto e il client ottiene ancora una singola licenza contenente la CEK per utilizzare il contenuto.

L’implementazione del packager può controllare la chiave di crittografia dei contenuti e le chiavi di rotazione utilizzate, nonché la frequenza con cui i tasti di rotazione cambiano.

>[!NOTE]
>
>I contenuti raccolti utilizzando la rotazione delle chiavi possono essere riprodotti solo sui client DRM di Primetime versione 3.0 o successiva. I client meno recenti potrebbero dover eseguire l’aggiornamento per riprodurre questo contenuto.