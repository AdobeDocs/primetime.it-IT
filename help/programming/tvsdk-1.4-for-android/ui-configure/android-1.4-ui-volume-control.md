---
description: È possibile impostare un controllo dell'interfaccia utente per il volume sonoro.
title: Controllo del volume
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---


# Fornire il controllo del volume{#provide-volume-control}

È possibile impostare un controllo dell&#39;interfaccia utente per il volume sonoro.

1. Attendere che lo stato dell&#39;istanza MediaPlayer sia valido per questo comando, che è qualsiasi tranne RELEASED o ERROR.
1. Chiama `setVolume` sull&#39;istanza `MediaPlayer` per impostare il volume audio.

   ```java
   void setVolume(int volume) throws IllegalStateException;
   ```

   Il valore per il volume rappresenta il volume richiesto espresso in proporzione al volume massimo, dove 0 è silenzioso e 100 è il volume massimo.

