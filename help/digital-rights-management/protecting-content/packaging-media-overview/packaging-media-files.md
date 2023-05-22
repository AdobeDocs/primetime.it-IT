---
title: Panoramica sulla creazione di pacchetti di file multimediali
description: Panoramica sulla creazione di pacchetti di file multimediali
copied-description: true
exl-id: 88c593a7-33b5-4773-b283-2ab16f9e8c3a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 0%

---

# Panoramica {#packaging-media-files-overview}

Il packaging si riferisce al processo di crittografia e applicazione di una policy DRM ai contenuti video. Per creare pacchetti di file puoi utilizzare le API Media Packaging. L’SDK Java di Primetime DRM può creare pacchetti solo per contenuti a download progressivo, come MP4.

>[!NOTE]
>
>Contatta il rappresentante DRM di Primetime per informazioni su come selezionare l’opzione di imballaggio più appropriata per il formato multimediale e i casi d’uso.

Il pacchetto viene disaccoppiato dal server licenze. Non è necessario che il responsabile del pacchetto si connetta al server licenze per scambiare informazioni sul contenuto. Tutto ciò che il server licenze deve sapere per rilasciare una licenza è incluso nei metadati del contenuto.

Quando un file viene crittografato, il relativo contenuto non può essere analizzato senza la licenza appropriata. È possibile utilizzare DRM di Primetime per selezionare le parti del file che si desidera crittografare. Poiché Primetime DRM è in grado di analizzare il formato di file del contenuto video, è in grado di crittografare in modo intelligente parti selettive di un file invece che l&#39;intero file. I dati, ad esempio metadati e cue point, possono rimanere non crittografati in modo che i motori di ricerca possano continuare a cercare il file.

Un contenuto specifico può avere più criteri DRM. Ad esempio, è possibile concedere in licenza i contenuti secondo diversi modelli aziendali senza dover creare più pacchetti di contenuti. Inoltre, puoi consentire l’accesso anonimo per un breve periodo di tempo e quindi consentire al cliente di acquistare il contenuto per avere accesso illimitato. Se il contenuto viene creato utilizzando più criteri DRM, il server licenze deve implementare una logica per selezionare i criteri DRM da utilizzare per rilasciare una licenza.

>[!NOTE]
>
>L’architettura consente di specificare i criteri DRM di utilizzo e di associarli al contenuto quando viene creato il pacchetto. Prima che un client possa riprodurre il contenuto, deve acquisire una licenza per un computer specifico. La licenza specifica le regole di utilizzo applicate e fornisce la chiave da utilizzare per decrittografare il contenuto. Il criterio DRM rappresenta un modello per la generazione di una licenza. Tuttavia, il server licenze può ignorare le regole di utilizzo quando rilascia una licenza. La licenza potrebbe non essere valida a causa di tali vincoli, ad esempio i tempi di scadenza o le finestre di riproduzione.

Primetime DRM fornisce un’API per il passaggio nel CEK. Se non viene specificato alcun CEK, l’SDK lo genera in modo casuale. In genere è necessario un CEK diverso per ogni sezione di contenuto. Tuttavia, in Dynamic Streaming, è probabile che si utilizzi lo stesso CEK per tutti i file che compongono tale contenuto. Pertanto, un utente ha bisogno di una sola licenza per passare facilmente da una velocità bit a un’altra. Se desideri utilizzare la stessa chiave e la stessa licenza per più parti di contenuto, è necessario trasmettere lo stesso `DRMParameters` oggetto a `MediaEncrypter.encryptContent()`, o passa nel CEK utilizzando `V2KeyParameters.setContentEncryptionKey()`. Se desideri utilizzare una chiave e una licenza diverse per ogni sezione di contenuto, devi creare una nuova `DRMParameters` per ciascun file.

Quando si crea un pacchetto del contenuto utilizzando la rotazione dei tasti, è possibile controllare i tasti di rotazione utilizzati e la frequenza con cui cambiano i tasti. `F4VDRMParameters` e `FLVDRMParameters` implementare `KeyRotationParameters` di rete. Tramite questa interfaccia, puoi abilitare la rotazione dei tasti. È inoltre necessario specificare un `RotatingContentEncryptionKeyProvider`. Per ogni esempio crittografato, questa classe determina la chiave di rotazione da utilizzare. È possibile implementare un proprio provider o utilizzare `TimeBasedKeyProvider` incluso con l’SDK. Questa implementazione genera in modo casuale una nuova chiave dopo un numero specificato di secondi.

In alcuni casi, potrebbe essere necessario archiviare i metadati del contenuto come file separato e renderli disponibili al client separatamente dal contenuto. In tal caso, devi invocare `MediaEncrypter.encryptContent()`, che restituisce un `MediaEncrypterResult` oggetto. Chiamata `MediaEncrypterResult.getKeyInfo()` e assegna il risultato a `V2KeyStatus`. Quindi recupera i metadati del contenuto e memorizzali in un file.

Tutte queste attività possono essere eseguite con l’API Java.

Consulta *Riferimento API di Adobe Primetime DRM* per informazioni dettagliate sull’API Java.

Consulta *Utilizzo delle implementazioni di riferimento Adobe Primetime DRM* per informazioni sull’implementazione di riferimento di Media Packager.
