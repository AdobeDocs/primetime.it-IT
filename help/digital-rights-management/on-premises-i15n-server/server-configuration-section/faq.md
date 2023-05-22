---
title: Domande frequenti
description: Domande frequenti
copied-description: true
exl-id: 9058604e-dbab-4df5-89fd-1219c85c7643
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
