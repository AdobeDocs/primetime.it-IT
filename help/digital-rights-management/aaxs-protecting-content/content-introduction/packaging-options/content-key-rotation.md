---
description: Le seguenti opzioni di cifratura sono selezionate al momento della creazione del pacchetto e non possono essere modificate durante l'acquisizione della licenza.
seo-description: Le seguenti opzioni di cifratura sono selezionate al momento della creazione del pacchetto e non possono essere modificate durante l'acquisizione della licenza.
seo-title: Rotazione chiave
title: Rotazione chiave
uuid: 6ee47c06-9981-4281-b10b-343f8b1e55b7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# Rotazione chiave{#key-rotation}

Le seguenti opzioni di cifratura sono selezionate al momento della creazione del pacchetto e non possono essere modificate durante l&#39;acquisizione della licenza.

Durante la creazione del pacchetto, in genere il contenuto viene crittografato utilizzando la chiave di crittografia dei contenuti (CEK) e il client ottiene una licenza contenente la CEK per utilizzare il contenuto. Quando la rotazione delle chiavi è abilitata, per cifrare il contenuto viene utilizzato il tasto di rotazione, che può essere modificato in modo che ogni chiave di rotazione sia utilizzata solo per cifrare una parte del contenuto. Le chiavi di rotazione sono protette mediante la chiave di crittografia dei contenuti e il client ottiene comunque una singola licenza contenente la CEK per utilizzare il contenuto. L’implementazione del packager può controllare la chiave di crittografia del contenuto e i tasti di rotazione utilizzati, nonché la frequenza con cui i tasti di rotazione cambiano.

Il contenuto compresso utilizzando la rotazione chiave può essere riprodotto solo  client di accesso Adobe versione 3.0 e successive. Per riprodurre questo contenuto, è necessario aggiornare i client meno recenti.
