---
description: È possibile impostare un controllo dell'interfaccia utente per il volume del suono.
seo-description: È possibile impostare un controllo dell'interfaccia utente per il volume del suono.
seo-title: Controllo del volume
title: Controllo del volume
uuid: 63e96424-54d0-4c16-bd94-2366722f752a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Controllo del volume{#provide-volume-control}

È possibile impostare un controllo dell&#39;interfaccia utente per il volume del suono.

1. Attendete che lo stato dell’istanza di MediaPlayer sia valido per questo comando, che è una qualsiasi tranne RELEASE o ERROR.
1. Chiamate `setVolume` l’ `MediaPlayer` istanza per impostare il volume audio.

   ```java
   void setVolume(int volume) throws IllegalStateException;
   ```

   Il valore per il volume rappresenta il volume richiesto espresso in proporzione al volume massimo, dove 0 è invisibile e 100 è il volume massimo.

