---
description: È possibile utilizzare il packager Bento4 di ExpressPlay per preparare i contenuti per qualsiasi soluzione DRM supportata da Primetime Cloud DRM, con tecnologia ExpressPlay.
title: Pacchetto ExpressPlay / Cloud DRM / TVSDK
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---


# Pacchetto ExpressPlay / Cloud DRM / TVSDK {#expressplay-packager-cloud-drm-tvsdk}

È possibile utilizzare il packager Bento4 di ExpressPlay per preparare i contenuti per qualsiasi soluzione DRM supportata da Primetime Cloud DRM, con tecnologia ExpressPlay.

Questa attività descrive come utilizzare uno strumento di terze parti per preparare contenuti protetti, in questo caso *Strumenti ExpressPlay Bento4*, da utilizzare con diverse soluzioni DRM. Per ulteriori informazioni, consulta la documentazione *Bento4 tools* sul sito web [ExpressPlay](https://www.expressplay.com/developer/).
1. Acquisisci un account ExpressPlay e ottieni le informazioni sull’Autenticatore del cliente ExpressPlay.

   Consulta [Avvio rapido di Primetime DRM Cloud.](../../quick-start/quick-overview.md)
1. Se stai crittografando il contenuto per Primetime Access , acquisisci l&#39;SDK di Primetime Adobe Access dall&#39;Adobe, insieme ai certificati richiesti (certificati di licenza, trasporto e pacchetto).
1. Fornire una chiave di crittografia del contenuto (CEK) e un ID di archiviazione della chiave di crittografia del contenuto (CEKSID) per l&#39;utilizzo in tutti i sistemi DRM. (Puoi generarli in modo casuale utilizzando OpenSSL o simili.)

   CEK è la chiave effettiva utilizzata per crittografare i file video. È possibile archiviarlo in modo sicuro sul proprio server nel proprio sistema di gestione delle chiavi, oppure utilizzare la [soluzione di storage principale di ExpressPlay](https://www.expressplay.com/developer/key-storage/).

   Un CEKSID è l&#39;identificatore di un CEK specifico. In genere non trasmetti la chiave di crittografia. Ad esempio, quando richiedi un token di licenza, fornisci il CEKSID.

1. Se stai crittografando i contenuti per Access, utilizza CEK per creare metadati di Primetime Access associati al contenuto.

1. Frammenta il contenuto per prepararlo allo strumento *Bento4 MP4DASH* .

   Per questo passaggio puoi utilizzare lo strumento *MP4FRAGMENT* . È sufficiente frammentare il contenuto una sola volta. Ad esempio:

   ```
   ./mp4fragment Unfragmented.mp4 Fragmented.mp4
   ```

1. Utilizza lo strumento *Bento4 MPDASH* per &quot;DASH-ify&quot; e crittografare il contenuto frammentato.

   Utilizzare questo comando per specificare tutti i sistemi DRM che si utilizzeranno e trasmettere i metadati di accesso Primetime generati dai passaggi precedenti. Ad esempio:

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

1. Crea un &quot;server di vetrina&quot;.

       Questo server deve gestire le seguenti operazioni:
   
   1. Selezione del contenuto da parte del cliente. Questa implementazione deve includere un endpoint per i client per richiedere un token di contenuto per un ID di contenuto specifico.
   1. Adesione del cliente
   1. Richieste di token di licenza (ExpressPlay) dal client ( [richiesta di token di licenza ExpressPlay / riferimento di risposta](../../license-token-req-resp-ref/license-req-resp-overview.md))

1. Crea il tuo client.

   Il client deve includere una chiamata al server di vetrina. L’Adobe consiglia al client di chiamare la vetrina dopo che l’utente ha selezionato del contenuto e dopo che l’utente è autenticato. Quindi, passa il token restituito da ExpressPlay al tuo lettore per utilizzare per le richieste di licenza. Le presentazioni per l&#39;implementazione del componente DRM dei tuoi giocatori sono qui:

   * Browser TVSDK per HTML5
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. Con il token di licenza in mano, il client ora può derivare l’URL della richiesta dal token ed effettuare la richiesta di licenza a ExpressPlay, quindi riprodurre il contenuto protetto selezionato per l’utente.
