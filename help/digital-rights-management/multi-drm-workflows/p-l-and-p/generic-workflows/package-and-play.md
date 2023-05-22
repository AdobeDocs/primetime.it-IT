---
description: È possibile utilizzare il packager Bento4 di ExpressPlay per preparare i contenuti per qualsiasi soluzione DRM supportata da Primetime Cloud DRM, con tecnologia ExpressPlay.
title: ExpressPlay Packager/Cloud DRM/TVSDK
exl-id: ff937279-3866-4d0a-9a19-cf61726299e1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# ExpressPlay Packager/Cloud DRM/TVSDK {#expressplay-packager-cloud-drm-tvsdk}

È possibile utilizzare il packager Bento4 di ExpressPlay per preparare i contenuti per qualsiasi soluzione DRM supportata da Primetime Cloud DRM, con tecnologia ExpressPlay.

Questa attività descrive come utilizzare uno strumento di terze parti per preparare contenuti protetti, in questo caso *Strumenti ExpressPlay Bento4*, per l&#39;utilizzo con diverse soluzioni DRM. Per ulteriori informazioni, vedere *Strumenti Bento4* documentazione sulla [ExpressPlay](https://www.expressplay.com/developer/) sito Web.
1. Acquisire un account ExpressPlay e ottenere le informazioni sull&#39;autenticatore del cliente ExpressPlay.

   Consulta [Guida introduttiva di Primetime DRM Cloud.](../../quick-start/quick-overview.md)
1. Se stai crittografando il contenuto per l’accesso Primetime , acquisisci l’SDK per l’accesso agli Adobi Primetime da Adobe, insieme ai certificati richiesti (certificati di licenza, trasporto e creazione pacchetti).
1. Fornire una chiave di crittografia del contenuto (CEK) e un ID di archiviazione della chiave di crittografia del contenuto (CEKSID) da utilizzare nei sistemi DRM. Puoi generarli in modo casuale utilizzando OpenSSL o simile.

   Il codice CEK è la chiave utilizzata per crittografare i file video. È possibile archiviarlo in modo sicuro sul proprio server nel proprio sistema di gestione delle chiavi oppure utilizzare ExpressPlay [soluzione di storage chiave](https://www.expressplay.com/developer/key-storage/).

   Un CEKSID è l’identificatore di un CEK specifico. In genere la chiave di crittografia non viene passata. Ad esempio, quando richiedi un token di licenza, fornisci il CEKSID.

1. Se si crittografa il contenuto per Access, utilizzare il codice CEK per creare i metadati di Primetime Access associati al contenuto.

1. Frammentare il contenuto per prepararlo per il *Bento4 MP4DASH* strumento.

   Per questo passaggio puoi utilizzare *MP4FRAGMENT* strumento. È sufficiente frammentare il contenuto una sola volta. Ad esempio:

   ```
   ./mp4fragment Unfragmented.mp4 Fragmented.mp4
   ```

1. Utilizza il *MPDASH Bento4* per &quot;DASH-ify&quot; e crittografare i contenuti frammentati.

   Utilizzare questo comando per specificare tutti i sistemi DRM che verranno utilizzati e passare i metadati di Primetime Access generati dai passaggi precedenti. Ad esempio:

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

       Il server deve gestire le operazioni seguenti:
   
   1. Selezione di contenuti da parte del cliente. Questa implementazione deve includere un endpoint per consentire ai client di richiedere un token di contenuto per un ID di contenuto specifico.
   1. Adesione cliente
   1. Richieste di token di licenza (ExpressPlay) dal client ( [Richiesta token di licenza ExpressPlay/riferimento di risposta](../../license-token-req-resp-ref/license-req-resp-overview.md))

1. Crea il client.

   Il client deve includere una chiamata al server storefront. L’Adobe consiglia al client di chiamare la vetrina dopo che l’utente ha selezionato alcuni contenuti e dopo che è stato autenticato. Quindi, passa il token restituito da ExpressPlay al lettore per utilizzarlo per le richieste di licenza. Le presentazioni per l’implementazione del componente DRM dei lettori sono disponibili qui:

   * Browser TVSDK per HTML5
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. Con il token di licenza a disposizione, il client può ora derivare l’URL della richiesta dal token, effettuare la richiesta di licenza a ExpressPlay e quindi riprodurre il contenuto protetto selezionato per l’utente.
