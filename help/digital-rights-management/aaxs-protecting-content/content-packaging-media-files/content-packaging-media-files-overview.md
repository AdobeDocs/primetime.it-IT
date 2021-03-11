---
title: Panoramica
description: Panoramica
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---


# Panoramica {#overview}

** Il termine &quot;pacchetto&quot; si riferisce al processo di cifratura e applicazione di un criterio ai file FLV o F4V. Utilizza le API per la creazione di pacchetti multimediali per creare pacchetti di file. L’SDK Java per Adobe Access può includere solo contenuti AIR e Flash a download progressivo, come FLV, F4V e MP4. Per creare pacchetti di contenuti utilizzando DRM di accesso Adobe per altri formati di contenuti, come Adobe HTTP Dynamic Streaming (HDS) o Apple HTTP Live Streaming (HLS), dovrai utilizzare altri strumenti, ad esempio Adobe Medium Server ( [https://www.adobe.com/products/adobe-media-server-family.html](https://www.adobe.com/products/adobe-media-server-family.html)) o un codificatore che implementa l’SDK di trasmissione di Adobe ( [https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf](https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf)). In alternativa, i clienti possono scegliere di utilizzare il set di strumenti Java Primetime Packager di Adobe, che può creare pacchetti di contenuti per diversi formati di destinazione, come HDS, HLS e DASH.

Il pacchetto viene scollegato dal server licenze. Non è necessario che il packager si connetta al server licenze per scambiare informazioni sul contenuto. Tutto ciò che il server licenze deve sapere per rilasciare la licenza è incluso nei metadati del contenuto.

Quando un file viene crittografato, il suo contenuto non può essere analizzato senza la licenza appropriata. Adobe Access consente di selezionare le parti del file da crittografare. Poiché Adobe® Access™ può analizzare il formato di file dei contenuti FLV e F4V, può crittografare in modo intelligente parti selettive del file invece che l&#39;intero file nel suo complesso. I dati come metadati e punti di cue possono rimanere non crittografati, in modo che i motori di ricerca possano comunque cercare il file.

È possibile che un dato contenuto abbia più criteri. Ciò potrebbe essere utile, ad esempio, se desideri concedere in licenza il contenuto in diversi modelli di business senza dover creare più pacchetti di contenuto. Ad esempio, puoi consentire l’accesso anonimo per un breve periodo di tempo e successivamente consentire al cliente di acquistare il contenuto e avere accesso illimitato. Se il contenuto viene compilato utilizzando più criteri, il server licenze deve implementare la logica necessaria per selezionare i criteri da utilizzare per rilasciare una licenza.

>[!NOTE]
>
>L’architettura consente di specificare i criteri di utilizzo e di associarli al contenuto quando il contenuto viene assemblato. Prima che un client possa riprodurre contenuto, è necessario che il client acquisisca una licenza per quel computer. La licenza specifica le regole di utilizzo applicate e fornisce la chiave utilizzata per decrittografare il contenuto. Il criterio è un modello per la generazione della licenza, ma il server licenze può scegliere di ignorare le regole di utilizzo al momento del rilascio della licenza. Tieni presente che la licenza potrebbe essere resa non valida da vincoli quali tempi di scadenza o finestre di riproduzione.

Sono disponibili numerose opzioni per la creazione di pacchetti di contenuti. Questi sono specificati nell&#39;interfaccia `DRMParameters` e nelle classi che implementano tale interfaccia, ovvero `F4VDRMParameters` e `FLVDRMParameters`. Con queste classi è possibile impostare la firma e i parametri chiave, nonché indicare se cifrare il contenuto audio, il contenuto video o i dati di script. Per vedere come vengono implementate nell&#39;implementazione di riferimento, consulta le descrizioni delle opzioni della riga di comando Media Packager descritte in *Utilizzo delle implementazioni di riferimento di accesso Adobe*. Queste opzioni si basano sull’API Java e sono quindi disponibili per l’utilizzo programmatico.

Le opzioni di imballaggio includono:

* Opzioni di crittografia (audio, video, crittografia parziale).
* URL del server licenze (il client utilizza questo come URL di base per tutte le richieste inviate al server licenze)
* Certificato di trasporto del server licenze
* Certificato del server licenze, utilizzato per crittografare la CEK.
* Credenziali del pacchetto per la firma dei metadati

Adobe Access fornisce un&#39;API per il passaggio nella CEK. Se non viene specificato alcun CEK, l’SDK lo genera in modo casuale. In genere è necessario un CEK diverso per ogni elemento di contenuto. Tuttavia, in Dynamic Streaming, è probabile che si utilizzi lo stesso CEK per tutti i file per quel contenuto, in modo che l&#39;utente abbia solo bisogno di una licenza singola e possa passare facilmente da un bit rate a un altro. Per utilizzare la stessa chiave e la stessa licenza per più contenuti, passare lo stesso oggetto `DRMParameters` a `MediaEncrypter.encryptContent()` oppure passare la CEK utilizzando `V2KeyParameters.setContentEncryptionKey()`. Per utilizzare una chiave e una licenza diverse per ogni contenuto, crea una nuova istanza `DRMParameters` per ogni file.

Quando si crea un pacchetto di contenuti utilizzando la rotazione dei tasti, è possibile controllare i tasti di rotazione utilizzati e la frequenza con cui i tasti cambiano. `F4VDRMParameters` e  `FLVDRMParameters` implementa l&#39; `KeyRotationParameters` interfaccia . Tramite questa interfaccia è possibile abilitare la rotazione delle chiavi. È inoltre necessario specificare un valore `RotatingContentEncryptionKeyProvider`. Per ogni esempio crittografato, questa classe determina la Chiave di rotazione da utilizzare. Puoi implementare il tuo provider oppure utilizzare il `TimeBasedKeyProvider` incluso nell&#39;SDK. Questa implementazione genera in modo casuale una nuova chiave dopo un numero specificato di secondi.

In alcuni casi potrebbe essere necessario archiviare i metadati del contenuto come file separato e renderli disponibili al client separatamente dal contenuto. A questo scopo, richiamare `MediaEncrypter.encryptContent()`, che restituisce un oggetto `MediaEncrypterResult`. Chiama `MediaEncrypterResult.getKeyInfo()` e trascina il risultato su `V2KeyStatus`. Quindi recupera i metadati del contenuto e memorizzalo in un file.

Tutte queste attività possono essere eseguite utilizzando l’API Java. Per informazioni dettagliate sull&#39;API Java discussa in questo capitolo, consulta *Riferimento API di accesso agli Adobi*.

Per informazioni sull&#39;implementazione di riferimento di Media Packager, consulta *Utilizzo delle implementazioni di riferimento di accesso Adobe*.
