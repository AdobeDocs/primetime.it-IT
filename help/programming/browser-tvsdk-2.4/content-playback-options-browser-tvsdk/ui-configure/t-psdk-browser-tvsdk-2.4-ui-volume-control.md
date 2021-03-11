---
description: È possibile impostare un controllo dell'interfaccia utente per il volume sonoro.
title: Controllo del volume
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '87'
ht-degree: 0%

---


# Fornire il controllo del volume{#provide-volume-control}

È possibile impostare un controllo dell&#39;interfaccia utente per il volume sonoro.

1. Attendi che l&#39;istanza `MediaPlayer` sia in uno stato valido per questo comando.

   Qualsiasi stato tranne RELEASED o ERROR è valido.
1. Imposta l&#39;attributo del volume sull&#39;istanza `MediaPlayer` per impostare il volume audio.

   ```js
   player.volume = ...
   ```

   Il valore per il volume rappresenta il volume richiesto espresso in proporzione al volume massimo, dove 0 è silenzioso ed è il volume massimo.

