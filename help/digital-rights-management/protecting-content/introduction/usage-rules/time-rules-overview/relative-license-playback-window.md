---
title: Finestra di riproduzione
description: Finestra di riproduzione
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# Finestra di riproduzione{#playback-window}

La finestra di riproduzione specifica la durata di validità di una licenza dopo il primo utilizzo per la riproduzione di contenuto protetto.

Caso d’uso di esempio: alcuni modelli aziendali consentono un periodo di noleggio di 30 giorni, ma una volta iniziata la riproduzione, questa deve essere completata in 48 ore. In questo caso, la durata di 48 ore della licenza è la finestra di riproduzione.

**Dalla versione 5.3 in poi** - La finestra di riproduzione supporta anche l’opzione di abilitazione o disabilitazione di Hard Stop, che indica se il contesto di decrittografia per la riproduzione deve arrestarsi alla scadenza della finestra di riproduzione (abilitata) o continuare nonostante la scadenza (disabilitata).

>[!NOTE]
>
>L&#39;opzione di arresto rigido non funziona correttamente con la finestra di riproduzione se utilizzata insieme ad essa (la finestra di riproduzione non verrà rispettata). La riproduzione di contenuto con finestra di riproduzione senza interruzione sicura rispetta la restrizione della finestra di riproduzione.

