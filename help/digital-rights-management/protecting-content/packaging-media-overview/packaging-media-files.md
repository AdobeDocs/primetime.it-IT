---
seo-title: Panoramica sulla creazione di pacchetti di file multimediali
title: Panoramica sulla creazione di pacchetti di file multimediali
uuid: 9509bcdc-ee4d-4025-9bb6-9b8ac439b926
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 0%

---


# Panoramica {#packaging-media-files-overview}

Per pacchetto si intende il processo di cifratura e applicazione di un criterio DRM al contenuto video. Potete utilizzare le API per la creazione di pacchetti di file multimediali per creare pacchetti di file. L&#39;SDK Java DRM di Primetime può creare pacchetti solo per il download progressivo, ad esempio MP4.

>[!NOTE]
>
>Assicuratevi di contattare il rappresentante DRM di Primetime per sapere come selezionare l&#39;opzione di pacchetto più appropriata per il formato e i casi di utilizzo del supporto.

Il pacchetto viene scollegato dal server licenze. Non è necessario che il packager si connetta al server licenze per scambiare informazioni sul contenuto. Tutto ciò che il server licenze deve sapere per rilasciare una licenza è incluso nei metadati del contenuto.

Quando un file è crittografato, il suo contenuto non può essere analizzato senza la licenza appropriata. È possibile utilizzare Primetime DRM per selezionare le parti del file da cifrare. Poiché DRM di Primetime è in grado di analizzare il formato file del contenuto video, può crittografare in modo intelligente parti selettive di un file invece di un intero file. I dati, come metadati e cue point, possono rimanere non crittografati, in modo che i motori di ricerca possano comunque eseguire ricerche nel file.

Un contenuto specifico può avere più criteri DRM. Ad esempio, potete concedere in licenza il contenuto in diversi modelli aziendali senza dover più creare pacchetti di contenuto. Inoltre, potete consentire l&#39;accesso anonimo per un breve periodo di tempo e consentire al cliente di acquistare il contenuto per avere accesso illimitato. Se il contenuto è incluso in un pacchetto utilizzando più criteri DRM, il server licenze deve implementare la logica per selezionare quale criterio DRM deve essere utilizzato per rilasciare una licenza.

>[!NOTE]
>
>L&#39;architettura consente di specificare i criteri DRM di utilizzo e di associarli al contenuto quando il contenuto viene incluso nel pacchetto. Prima che un client possa riprodurre il contenuto, deve acquisire una licenza per un computer specificato. La licenza specifica le regole di utilizzo applicate e fornisce la chiave da utilizzare per decrittografare il contenuto. Il criterio DRM rappresenta un modello per la generazione di una licenza. Tuttavia, il server licenze potrebbe ignorare le regole di utilizzo quando rilascia una licenza. Il rendering della licenza potrebbe non essere valido da tali vincoli, ad esempio tempi di scadenza o finestre di riproduzione.

Primetime DRM fornisce un&#39;API per il passaggio nella CEK. Se non viene specificato alcun CEK, l’SDK lo genera in modo casuale. In genere è necessario un CEK diverso per ogni sezione di contenuto. Tuttavia, in Dynamic Streaming, è probabile che si utilizzi lo stesso CEK per tutti i file che compongono tale contenuto. Pertanto, un utente necessita solo di una singola licenza per passare senza soluzione di continuità da un bit rate a un altro. Se si desidera utilizzare la stessa chiave e la stessa licenza per più contenuti, è necessario passare lo stesso oggetto `DRMParameters` a `MediaEncrypter.encryptContent()`, oppure passare la CEK utilizzando `V2KeyParameters.setContentEncryptionKey()`. Se desiderate utilizzare una chiave e una licenza diverse per ciascuna sezione di contenuto, dovete creare una nuova istanza `DRMParameters` per ciascun file.

Quando create un pacchetto di contenuto utilizzando la rotazione chiave, potete controllare i tasti di rotazione utilizzati e la frequenza con cui i tasti cambiano. `F4VDRMParameters` e  `FLVDRMParameters` implementare l&#39; `KeyRotationParameters` interfaccia. Tramite questa interfaccia, è possibile abilitare la rotazione delle chiavi. È inoltre necessario specificare un `RotatingContentEncryptionKeyProvider`. Per ciascun esempio crittografato, questa classe determina la chiave di rotazione da utilizzare. Puoi implementare il tuo provider oppure utilizzare la `TimeBasedKeyProvider` inclusa nell&#39;SDK. Questa implementazione genera in modo casuale una nuova chiave dopo un numero specificato di secondi.

In alcuni casi potrebbe essere necessario archiviare i metadati del contenuto come file separato e renderli disponibili al client separatamente dal contenuto. In tal caso, è necessario richiamare `MediaEncrypter.encryptContent()`, che restituisce un oggetto `MediaEncrypterResult`. Chiamare `MediaEncrypterResult.getKeyInfo()` e inserire il risultato in `V2KeyStatus`. Quindi recuperate i metadati del contenuto e archiviatelo in un file.

Tutte queste attività possono essere eseguite con l&#39;API Java.

Per informazioni dettagliate sull&#39;API Java, consultate *Adobe Primetime DRM API Reference*.

Per informazioni sull&#39;implementazione di riferimento di Media Packager, consultate *Utilizzo  Adobe Primetime DRM Reference Implementation*.
