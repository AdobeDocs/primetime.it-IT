---
seo-title: Domande frequenti
title: Domande frequenti
uuid: 7e7409b5-9b3f-4dc3-96b6-42a06d9b1265
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Domande frequenti {#faq}

* Con quale frequenza si verificano modifiche ECI?
   * Ogni volta che viene rilasciato un nuovo client Adobe DRM, viene aggiunto un record del dispositivo ECI.

* Quanto sono grandi i file ECI?
   * Sono generalmente inferiori a 1 kilobyte per record dispositivo.

* Cosa succede se al server manca un record dispositivo ECI?
   * Questa particolare classe di client non sarà in grado di individualizzarsi rispetto al server di Individualizzazione dei locali e gli errori verranno registrati nei file di registro.

* Cosa succede se i CRL di un server sono scaduti?
   * Il server smetterà di funzionare correttamente e gli errori verranno registrati nei file di registro.