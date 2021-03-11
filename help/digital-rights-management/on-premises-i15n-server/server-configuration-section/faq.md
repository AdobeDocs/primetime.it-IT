---
title: Domande frequenti
description: Domande frequenti
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# Domande frequenti {#faq}

* Con quale frequenza si verificano i cambiamenti ECI?
   * Ogni volta che viene rilasciato un nuovo client DRM di Adobe, viene aggiunto un record dispositivo ECI.

* Quanto sono grandi i file ECI?
   * In genere sono meno di 1 Kilobyte per record dispositivo.

* Cosa succede se al server manca un record dispositivo ECI?
   * Questa particolare classe di client non sarà in grado di individualizzarsi rispetto al server di Individualizzazione On Premises e gli errori verranno registrati nei file di log.

* Cosa succede se i CRL di un server sono scaduti?
   * Il server smetterà di funzionare correttamente e gli errori verranno registrati nei file di registro.