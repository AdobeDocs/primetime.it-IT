---
title: Imposta il token XSTS nel lettore
description: Imposta il token XSTS nel lettore
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '64'
ht-degree: 0%

---


# Imposta il token XSTS nel lettore{#set-the-xsts-token-in-your-player}

In Xbox360, il token viene impostato in modo asincrono in risposta al `MediaPlayer.RequestKeyAttribute` evento.

Imposta il token XSTS.

L’app di esempio fornita con il software mostra come impostare il token XSTS nel lettore. Di seguito è riportato lo snippet di codice relativo dal sample player:

```
   MediaPlayer mMediaPlayer;  
 
mMediaPlayer.RequestKeyAttribute += Player_RequestKeyAttribute;  
 
private void Player_RequestKeyAttribute(object sender, RequestKeyAttributeEventArgs args) {  
    string token = "";  
    // XBOX XSTS Token...  
    KeyAttribute keyAttribute = new KeyAttribute(System.Text.Encoding.UTF8.GetBytes(token), null);  
    mMediaPlayer.SetKeyAttribute(args.RequestIdentifier, keyAttribute);  
} 
```

