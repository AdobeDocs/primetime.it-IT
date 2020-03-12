---
description: 'null'
seo-description: 'null'
seo-title: Impostare il token XSTS nel lettore
title: Impostare il token XSTS nel lettore
uuid: 8995e029-deee-4e23-9cda-a50de8c4f2c0
translation-type: tm+mt
source-git-commit: b7f52b71bde1d7bf59ef51d4f6f90dfaa07e347b

---


# Impostare il token XSTS nel lettore{#set-the-xsts-token-in-your-player}

In Xbox360, il token viene impostato in modo asincrono in risposta all&#39; `MediaPlayer.RequestKeyAttribute` evento.

Impostate il token XSTS.

L&#39;app di esempio fornita con il software mostra come impostare il token XSTS nel lettore. Segue il frammento di codice relativo al lettore di esempio:

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

