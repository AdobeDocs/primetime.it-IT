---
description: Le seguenti opzioni di crittografia sono selezionate al momento della creazione del pacchetto e non possono essere modificate durante l'acquisizione della licenza.
title: Rotazione tasti
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---


# Rotazione chiave{#key-rotation}

Le seguenti opzioni di crittografia sono selezionate al momento della creazione del pacchetto e non possono essere modificate durante l&#39;acquisizione della licenza.

Durante la creazione del pacchetto, in genere il contenuto viene crittografato utilizzando la chiave di crittografia dei contenuti (CEK) e il client ottiene una licenza contenente la CEK per utilizzare il contenuto. Quando la rotazione delle chiavi è abilitata, la chiave di rotazione viene utilizzata per cifrare il contenuto e la chiave può essere modificata in modo che ogni chiave di rotazione sia utilizzata solo per cifrare una parte del contenuto. Le chiavi di rotazione sono protette utilizzando la chiave di crittografia del contenuto e il client ottiene ancora una singola licenza contenente la CEK per utilizzare il contenuto. L’implementazione del packager può controllare la chiave di crittografia dei contenuti e le chiavi di rotazione utilizzate, nonché la frequenza con cui i tasti di rotazione cambiano.

Il contenuto compilato utilizzando la rotazione delle chiavi può essere riprodotto solo sui client Adobe Access versione 3.0 e successive. Per riprodurre questo contenuto, è necessario eseguire l’aggiornamento dei client meno recenti.
