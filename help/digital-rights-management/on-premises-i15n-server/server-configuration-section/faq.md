---
title: Domande frequenti
description: Domande frequenti
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# Domande frequenti {#faq}

* Con quale frequenza si verificano le modifiche ECI?
   * Ogni volta che viene rilasciato un nuovo client DRM di Adobe, viene aggiunto un record dispositivo ECI.

* Quanto sono grandi i file ECI?
   * Sono in genere meno di 1 kilobyte per record di dispositivo.

* Cosa succede se nel server manca un record dispositivo ECI?
   * Questa particolare classe di client non sarà in grado di individualizzarsi rispetto al server di personalizzazione locale e gli errori verranno registrati nei file di registro.

* Cosa succede se i CRL di un server sono scaduti?
   * Il server smetterà di funzionare correttamente e gli errori verranno registrati nei file di registro.
