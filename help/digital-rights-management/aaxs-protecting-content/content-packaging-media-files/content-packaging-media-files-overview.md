---
title: Panoramica
description: Panoramica
copied-description: true
exl-id: 67c3d98f-8c17-4b5a-8abb-00f6f0f1e823
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---

# Panoramica {#overview}

*Imballaggio* si riferisce al processo di crittografia e applicazione di una policy ai file FLV o F4V. Utilizza le API Media Packaging per creare pacchetti di file. L’SDK Java per accesso Adobe può creare pacchetti solo per contenuti AIR e Flash a download progressivo, come FLV, F4V e MP4. Per creare un pacchetto di contenuti con Adobe Access DRM per altri formati di contenuti, come Adobe HTTP Dynamic Streaming (HDS) o Apple HTTP Live Streaming (HLS), è necessario utilizzare altri strumenti, come Adobe Medium Server ( [https://www.adobe.com/products/adobe-media-server-family.html](https://www.adobe.com/products/adobe-media-server-family.html)) o un codificatore che implementa l&#39;SDK di trasmissione Adobe ( [https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf](https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf)). In alternativa, i clienti possono scegliere di utilizzare il set di strumenti di Adobe Java Primetime Packager, che può creare pacchetti di contenuti per diversi formati di destinazione, come HDS, HLS e DASH.

Il pacchetto viene disaccoppiato dal server licenze. Non è necessario che il responsabile del pacchetto si connetta al server licenze per scambiare informazioni sul contenuto. Tutto ciò che il server licenze deve sapere per rilasciare la licenza è incluso nei metadati del contenuto.

Quando un file viene crittografato, il relativo contenuto non può essere analizzato senza la licenza appropriata. Adobe Access consente di selezionare le parti del file da crittografare. Ad Adobe ® Access™ è in grado di analizzare il formato di file del contenuto FLV e F4V e di crittografare in modo intelligente parti selettive del file anziché l&#39;intero file. Dati come metadati e cue point possono rimanere non crittografati in modo che i motori di ricerca possano comunque cercare il file.

È possibile che un dato contenuto abbia più criteri. Ciò potrebbe essere utile, ad esempio, se desideri concedere in licenza i contenuti secondo diversi modelli di business senza dover creare più pacchetti di contenuti. Ad esempio, puoi consentire l’accesso anonimo per un breve periodo di tempo, dopo di che il cliente potrà acquistare il contenuto e avere accesso illimitato. Se il contenuto viene creato utilizzando più criteri, il server licenze deve implementare una logica per selezionare i criteri da utilizzare per il rilascio di una licenza.

>[!NOTE]
>
>L’architettura consente di specificare i criteri di utilizzo e di associarli al contenuto quando viene creato il pacchetto. Prima che un client possa riprodurre il contenuto, deve acquisire una licenza per tale computer. La licenza specifica le regole di utilizzo applicate e fornisce la chiave utilizzata per decrittografare il contenuto. Il criterio è un modello per la generazione della licenza, ma il server licenze può scegliere di ignorare le regole di utilizzo durante il rilascio della licenza. Tieni presente che la licenza potrebbe non essere valida a causa di vincoli quali i tempi di scadenza o le finestre di riproduzione.

Sono disponibili numerose opzioni per la creazione di pacchetti di contenuto. Questi sono specificati nella `DRMParameters` e le classi che implementano tale interfaccia, ovvero `F4VDRMParameters` e `FLVDRMParameters`. Con queste classi è possibile impostare la firma e i parametri chiave, nonché indicare se crittografare il contenuto audio, il contenuto video o i dati di script. Per vedere come questi vengono implementati nell’implementazione di riferimento, consulta le descrizioni delle opzioni della riga di comando di Media Packager discusse in *Utilizzo delle implementazioni di riferimento di accesso Adobe*. Queste opzioni si basano sull’API Java e sono quindi disponibili per l’utilizzo a livello di programmazione.

Le opzioni di packaging includono:

* Opzioni di crittografia (audio, video, crittografia parziale).
* URL del server licenze (il client utilizza questo come URL di base per tutte le richieste inviate al server licenze)
* Certificato trasporto server licenze
* Certificato del server licenze, utilizzato per crittografare il codice di licenza.
* Credenziali Packager per la firma dei metadati

Adobe Access fornisce un’API per il passaggio nel CEK. Se non viene specificato alcun CEK, l’SDK lo genera in modo casuale. In genere è necessario un CEK diverso per ogni elemento di contenuto. Tuttavia, in Dynamic Streaming, è probabile che si utilizzi lo stesso CEK per tutti i file di quel contenuto, quindi l’utente ha bisogno di una sola licenza e può passare facilmente da una velocità bit a un’altra. Per utilizzare la stessa chiave e la stessa licenza per più parti di contenuto, trasmettere la stessa `DRMParameters` oggetto a `MediaEncrypter.encryptContent()`, o passa nel CEK utilizzando `V2KeyParameters.setContentEncryptionKey()`. Per utilizzare una chiave e una licenza diverse per ogni contenuto, crea un nuovo `DRMParameters` per ciascun file.

Quando si crea un pacchetto di contenuto utilizzando la rotazione dei tasti, è possibile controllare i tasti di rotazione utilizzati e la frequenza con cui cambiano i tasti. `F4VDRMParameters` e `FLVDRMParameters` implementare `KeyRotationParameters` di rete. Tramite questa interfaccia, puoi abilitare la rotazione dei tasti. È inoltre necessario specificare un `RotatingContentEncryptionKeyProvider`. Per ogni esempio crittografato, questa classe determina la chiave di rotazione da utilizzare. È possibile implementare un proprio provider o utilizzare `TimeBasedKeyProvider` incluso con l’SDK. Questa implementazione genera in modo casuale una nuova chiave dopo un numero specificato di secondi.

In alcuni casi, potrebbe essere necessario archiviare i metadati del contenuto come file separato e renderli disponibili al client separatamente dal contenuto. A questo scopo, richiama `MediaEncrypter.encryptContent()`, che restituisce un `MediaEncrypterResult` oggetto. Chiamata `MediaEncrypterResult.getKeyInfo()` e assegna il risultato a `V2KeyStatus`. Quindi recupera i metadati del contenuto e memorizzali in un file.

Tutte queste attività possono essere eseguite utilizzando l’API Java. Per informazioni dettagliate sull’API Java descritta in questo capitolo, consulta *Riferimento API per l’accesso agli Adobi*.

Per informazioni sull’implementazione di riferimento di Media Packager, consulta *Utilizzo delle implementazioni di riferimento di accesso Adobe*.
