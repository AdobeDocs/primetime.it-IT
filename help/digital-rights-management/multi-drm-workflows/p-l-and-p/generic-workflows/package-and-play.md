---
description: Potete utilizzare il packager Bento4 di ExpressPlay per preparare i contenuti per qualsiasi soluzione DRM supportata da Primetime Cloud DRM, basata su ExpressPlay.
seo-description: Potete utilizzare il packager Bento4 di ExpressPlay per preparare i contenuti per qualsiasi soluzione DRM supportata da Primetime Cloud DRM, basata su ExpressPlay.
seo-title: ExpressPlay Packager / Cloud DRM / TVSDK
title: ExpressPlay Packager / Cloud DRM / TVSDK
uuid: 0d2f5a8d-15c4-42ba-acb8-1dc8d5bc62de
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---


# ExpressPlay Packager / Cloud DRM / TVSDK {#expressplay-packager-cloud-drm-tvsdk}

Potete utilizzare il packager Bento4 di ExpressPlay per preparare i contenuti per qualsiasi soluzione DRM supportata da Primetime Cloud DRM, basata su ExpressPlay.

Questa attività descrive come utilizzare uno strumento di terze parti per preparare i contenuti protetti, in questo caso *ExpressPlay Bento4 Tools*, da utilizzare con diverse soluzioni DRM. Per ulteriori informazioni, consultare la documentazione *Bento4 tools* sul sito Web [ExpressPlay](https://www.expressplay.com/developer/).
1. Acquisisci un account ExpressPlay e ottieni le informazioni sull&#39;autenticazione del cliente ExpressPlay.

   Consultate [Primetime DRM Cloud Quick start.](../../quick-start/quick-overview.md)
1. Se state crittografando il contenuto per Primetime Access, acquisite l&#39;SDK Primetime  Adobe Access dal Adobe  insieme ai certificati richiesti (certificati di licenza, trasporto e creazione di pacchetti).
1. Fornite una chiave di crittografia dei contenuti (CEK) e un ID di memorizzazione della chiave di crittografia dei contenuti (CEKSID) da utilizzare nei sistemi DRM. (Potete generarli in modo casuale utilizzando OpenSSL o simili.)

   CEK è la chiave che utilizzate per cifrare i file video. È possibile archiviarlo in modo sicuro sul proprio server nel proprio sistema di gestione delle chiavi, oppure utilizzare la [soluzione di storage ](https://www.expressplay.com/developer/key-storage/) di ExpressPlay.

   Un CEKSID è l’identificatore di un CEK specifico. In genere non trasmettete la chiave di crittografia. Ad esempio, quando si richiede un token di licenza, è necessario fornire il CEKSID.

1. Se state codificando il contenuto per Access, utilizzate CEK per creare metadati Primetime Access associati al contenuto.

1. Frammenti il contenuto per prepararlo allo strumento *Bento4 MP4DASH*.

   Per questo passaggio è possibile utilizzare lo strumento *MP4FRAGMENT*. È necessario frammentare il contenuto una sola volta. Ad esempio:

   ```
   ./mp4fragment Unfragmented.mp4 Fragmented.mp4
   ```

1. Utilizzare lo strumento *Bento4 MPDASH* per &quot;DASH-ify&quot; e cifrare il contenuto frammentato.

   Utilizzate questo comando per specificare tutti i sistemi DRM che utilizzerete e per trasmettere i metadati di accesso Primetime generati dai passaggi precedenti. Ad esempio:

   ```
   /mp4dash -f  
   --use-segment-list  
   --use-segment-timeline  
   --encryption-key=<CEKSID>:<CEK>  
   --playready  
   --Widevine  
   --Widevine-header=provider:intertrust#content_id:2a  
   --primetime  
   --primetime-metadata=@AAXS.metadata 
    Fragmented.mp4 -o DASH_OUTPUT
   ```

1. Creare un &quot;server storefront&quot;.

       Il server deve gestire le seguenti operazioni:
   
   1. Selezione del contenuto da parte del cliente. Questa implementazione deve includere un endpoint per i client per richiedere un token contenuto per un ID contenuto specifico.
   1. Adesione cliente
   1. Richieste di token di licenza (ExpressPlay) dal client ( [Richiesta token di licenza ExpressPlay / riferimento risposta](../../license-token-req-resp-ref/license-req-resp-overview.md))

1. Crea il tuo client.

   Il client deve includere una chiamata al server di storefront.  Adobe consiglia al client di chiamare lo storefront dopo che l&#39;utente ha selezionato del contenuto e dopo che l&#39;utente è stato autenticato. Quindi, passare il token restituito da ExpressPlay al lettore per utilizzarlo per le richieste di licenza. Presentazioni per l&#39;implementazione del componente DRM dei lettori sono:

   * Browser TVSDK per HTML5
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. Con il token di licenza in mano, il client ora può derivare l&#39;URL della richiesta dal token, effettuare la richiesta di licenza per ExpressPlay, quindi riprodurre il contenuto protetto selezionato per l&#39;utente.
