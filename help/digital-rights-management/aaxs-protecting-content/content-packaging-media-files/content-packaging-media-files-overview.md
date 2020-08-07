---
seo-title: Panoramica
title: Panoramica
uuid: 11cf1f1f-a4b2-4ac2-aae7-e925d96729d2
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---


# Panoramica {#overview}

*Per pacchetto* si intende il processo di cifratura e applicazione di un criterio ai file FLV o F4V. Utilizzate le API per la creazione di pacchetti di file multimediali per creare pacchetti di file. L’SDK Java per l’accesso al Adobe  può creare pacchetti solo di Flash con download progressivo e contenuti AIR quali FLV, F4V e MP4. Per creare pacchetti di contenuto utilizzando  DRM di accesso al Adobe per altri formati di contenuto, come  Adobe HTTP Dynamic Streaming (HDS) o Apple HTTP Live Streaming (HLS), dovrete utilizzare altri strumenti, ad esempio  Adobe Media Server ( [https://www.adobe.com/products/adobe-media-server-family.html](https://www.adobe.com/products/adobe-media-server-family.html)) o un codificatore che implementa  Adobe Broadcast SDK ( [https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf](https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf)). In alternativa, i clienti possono scegliere di utilizzare  Adobe  set di strumenti Java Primetime Packager, in grado di creare pacchetti di contenuto per diversi formati di destinazione, come HDS, HLS e DASH.

Il pacchetto viene scollegato dal server licenze. Non è necessario che il packager si connetta al server licenze per scambiare informazioni sul contenuto. Tutto ciò che il server licenze deve sapere per rilasciare la licenza è incluso nei metadati del contenuto.

Quando un file è crittografato, il suo contenuto non può essere analizzato senza la licenza appropriata.  Accesso Adobe consente di selezionare quali parti del file cifrare. Poiché  Adobe® Access™ è in grado di analizzare il formato file dei contenuti FLV e F4V, è possibile crittografare in modo intelligente parti selettive del file invece che l&#39;intero file nel suo insieme. I dati come metadati e cue point possono rimanere non crittografati, in modo che i motori di ricerca possano comunque eseguire ricerche nel file.

È possibile che una determinata parte del contenuto disponga di più criteri. Questo potrebbe essere utile, ad esempio, se desiderate ottenere una licenza per il contenuto in diversi modelli aziendali senza dover creare più pacchetti per il contenuto. Ad esempio, potete consentire l&#39;accesso anonimo per un breve periodo di tempo e, successivamente, consentire al cliente di acquistare il contenuto e avere accesso illimitato. Se il contenuto è incluso in un pacchetto utilizzando più criteri, il server licenze deve implementare la logica per selezionare quale criterio utilizzare per rilasciare una licenza.

>[!NOTE]
>
>L&#39;architettura consente di specificare i criteri di utilizzo e di associarli al contenuto quando il contenuto viene incluso nel pacchetto. Prima che un client possa riprodurre il contenuto, deve acquisire una licenza per quel computer. La licenza specifica le regole di utilizzo applicate e fornisce la chiave utilizzata per decifrare il contenuto. Il criterio è un modello per la generazione della licenza, ma il server licenze può scegliere di ignorare le regole di utilizzo al momento dell&#39;emissione della licenza. Il rendering della licenza potrebbe non essere valido per vincoli quali tempi di scadenza o finestre di riproduzione.

Quando si crea il pacchetto, sono disponibili numerose opzioni. Questi sono specificati nell&#39; `DRMParameters` interfaccia e nelle classi che implementano tale interfaccia, che sono il `F4VDRMParameters` e `FLVDRMParameters`. Con queste classi è possibile impostare parametri di firma e chiave, nonché indicare se cifrare contenuto audio, contenuto video o dati di script. Per vedere in che modo queste vengono implementate nell&#39;implementazione di riferimento, consultate le descrizioni delle opzioni della riga di comando di Media Packager illustrate in *Utilizzo delle implementazioni* di riferimento per l&#39;accesso al Adobe . Queste opzioni sono basate sull&#39;API Java e sono pertanto disponibili per l&#39;utilizzo a livello di programmazione.

Le opzioni di package includono:

* Opzioni di cifratura (audio, video, cifratura parziale).
* URL del server delle licenze (il client utilizza questo come URL di base per tutte le richieste inviate al server delle licenze)
* Certificato di trasporto server licenze
* Certificato del server di licenze, utilizzato per crittografare il CEK.
* Credenziali Packager per la firma dei metadati

 Accesso Adobe fornisce un&#39;API per il passaggio nel CEK. Se non viene specificato alcun CEK, l’SDK lo genera in modo casuale. In genere è necessario un CEK diverso per ogni contenuto. Tuttavia, in Dynamic Streaming, è probabile che per tutti i file per tale contenuto venga utilizzato lo stesso CEK, pertanto l&#39;utente ha bisogno solo di una licenza singola e può passare senza problemi da un bitrate all&#39;altro. Per utilizzare la stessa chiave e la stessa licenza per più contenuti, passare lo stesso `DRMParameters` oggetto a `MediaEncrypter.encryptContent()`CEK o passarlo utilizzando `V2KeyParameters.setContentEncryptionKey()`. Per utilizzare una chiave e una licenza diverse per ogni contenuto, create una nuova `DRMParameters` istanza per ciascun file.

Quando create il pacchetto con la rotazione chiave, potete controllare i tasti di rotazione utilizzati e la frequenza con cui i tasti cambiano. `F4VDRMParameters` e `FLVDRMParameters` implementare l&#39; `KeyRotationParameters` interfaccia. Tramite questa interfaccia, è possibile abilitare la rotazione delle chiavi. È inoltre necessario specificare un `RotatingContentEncryptionKeyProvider`. Per ciascun esempio crittografato, questa classe determina la chiave di rotazione da utilizzare. Puoi implementare il tuo provider o usare il `TimeBasedKeyProvider` file incluso nell’SDK. Questa implementazione genera in modo casuale una nuova chiave dopo un numero specificato di secondi.

In alcuni casi potrebbe essere necessario archiviare i metadati del contenuto come file separato e renderli disponibili al client separatamente dal contenuto. Per eseguire questa operazione, richiamare `MediaEncrypter.encryptContent()`, che restituisce un `MediaEncrypterResult` oggetto. Chiama `MediaEncrypterResult.getKeyInfo()` e scegli il risultato a `V2KeyStatus`. Quindi recuperate i metadati del contenuto e archiviatelo in un file.

Tutte queste attività possono essere eseguite utilizzando l&#39;API Java. Per informazioni dettagliate sulle API Java discusse in questo capitolo, consultate *Riferimento* API di accesso agli Adobi.

Per informazioni sull&#39;implementazione di riferimento di Media Packager, consultate *Utilizzo delle implementazioni* di riferimento per l&#39;accesso al Adobe .
