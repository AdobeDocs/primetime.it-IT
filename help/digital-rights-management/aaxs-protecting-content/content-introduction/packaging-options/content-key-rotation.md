---
description: Le seguenti opzioni di crittografia vengono selezionate al momento del packaging e non possono essere modificate durante l'acquisizione della licenza.
title: Rotazione tasti
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# Rotazione tasti{#key-rotation}

Le seguenti opzioni di crittografia vengono selezionate al momento del packaging e non possono essere modificate durante l&#39;acquisizione della licenza.

Durante la creazione del pacchetto, in genere il contenuto viene crittografato utilizzando la chiave di crittografia del contenuto (CEK) e il client ottiene una licenza contenente il CEK per utilizzare il contenuto. Quando è abilitata la rotazione delle chiavi, la chiave di rotazione viene utilizzata per crittografare il contenuto e può essere modificata in modo che ogni chiave di rotazione venga utilizzata solo per crittografare una parte del contenuto. I tasti di rotazione sono protetti utilizzando la chiave di crittografia del contenuto e il client ottiene ancora una singola licenza contenente il codice CEK per utilizzare il contenuto. L’implementazione di Packager può controllare la chiave di crittografia del contenuto e le chiavi di rotazione utilizzate, nonché la frequenza con cui cambiano le chiavi di rotazione.

I contenuti inseriti mediante rotazione chiave possono essere riprodotti solo su client Adobe Access versione 3.0 e successive. I client meno recenti dovrebbero effettuare l’aggiornamento per riprodurre questo contenuto.
