---
description: Dopo aver caricato correttamente l’oggetto MediaResource, TVSDK crea un’istanza della classe MediaPlayerItem per fornire l’accesso a tale risorsa.
title: Informazioni sulla classe MediaPlayerItem
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---


# Informazioni sulla classe MediaPlayerItem {#about-the-mediaplayeritem-class}

L&#39;oggetto MediaPlayer rappresenta il lettore multimediale. Un MediaPlayerItem rappresenta audio o video sul lettore.

Dopo aver caricato correttamente l’oggetto MediaResource, TVSDK crea un’istanza della classe MediaPlayerItem per fornire l’accesso a tale risorsa.

Il `MediaResource` rappresenta una richiesta emessa dal livello dell&#39;applicazione all&#39;istanza `MediaPlayer` per caricare il contenuto.

Il `MediaPlayer` risolve la risorsa multimediale, carica il file manifesto associato e analizza il manifesto. Questa è la parte asincrona del processo di caricamento delle risorse. L’istanza `MediaPlayerItem` viene prodotta dopo la risoluzione della risorsa, e questa istanza è una versione risolta di un `MediaResource`. TVSDK fornisce l&#39;accesso all&#39;istanza `MediaPlayerItem` appena creata tramite `MediaPlayer.CurrentItem`.

>[!TIP]
>
>È necessario attendere che la risorsa venga caricata correttamente prima di accedere all’elemento del lettore multimediale.