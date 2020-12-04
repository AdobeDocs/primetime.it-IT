---
description: 'Quando create un pacchetto, potete selezionare le seguenti opzioni di cifratura. Tuttavia, non è possibile modificare le opzioni di cifratura durante l''acquisizione della licenza '
seo-description: 'Quando create un pacchetto, potete selezionare le seguenti opzioni di cifratura. Tuttavia, non è possibile modificare le opzioni di cifratura durante l''acquisizione della licenza '
seo-title: Rotazione chiave
title: Rotazione chiave
uuid: 6ac3b828-2cd1-42df-b9ee-4daa8e553d5e
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Rotazione chiave {#key-rotation}

Quando create un pacchetto, potete selezionare le seguenti opzioni di cifratura. Tuttavia, non è possibile modificare le opzioni di cifratura durante l&#39;acquisizione della licenza:

Durante la creazione del pacchetto, il contenuto viene in genere crittografato mediante la chiave di crittografia dei contenuti (CEK). Il client ottiene una licenza contenente il CEK per utilizzare il contenuto.

Quando abilitate la rotazione delle chiavi, la chiave di rotazione viene utilizzata per cifrare il contenuto e la chiave può essere modificata in modo che ogni chiave di rotazione sia utilizzata solo per cifrare una parte del contenuto. Le chiavi di rotazione sono protette mediante la chiave di crittografia dei contenuti e il client ottiene comunque una singola licenza contenente la CEK per utilizzare i contenuti.

L’implementazione del packager può controllare la chiave di crittografia del contenuto e i tasti di rotazione utilizzati, nonché la frequenza con cui i tasti di rotazione cambiano.

>[!NOTE]
>
>Il contenuto compresso utilizzando la rotazione chiave può essere riprodotto solo sui client DRM di Primetime versione 3.0 o successiva. I client meno recenti potrebbero dover effettuare l&#39;aggiornamento per riprodurre questo contenuto.