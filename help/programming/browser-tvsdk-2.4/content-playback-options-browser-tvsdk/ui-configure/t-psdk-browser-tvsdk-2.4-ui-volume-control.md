---
description: È possibile impostare un controllo dell'interfaccia utente per il volume del suono.
seo-description: È possibile impostare un controllo dell'interfaccia utente per il volume del suono.
seo-title: Controllo del volume
title: Controllo del volume
uuid: 5f2f69cc-3969-4ca2-8ab9-5713fdf5cdb8
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Controllo del volume{#provide-volume-control}

È possibile impostare un controllo dell&#39;interfaccia utente per il volume del suono.

1. Attendete che lo stato dell&#39; `MediaPlayer` istanza sia valido per questo comando.

   Qualsiasi stato tranne RELEASE o ERROR è valido.
1. Impostate l&#39;attributo volume sull&#39; `MediaPlayer` istanza per impostare il volume audio.

   ```js
   player.volume = ...
   ```

   Il valore per il volume rappresenta il volume richiesto espresso in proporzione al volume massimo, dove 0 è invisibile ed è il volume massimo.

