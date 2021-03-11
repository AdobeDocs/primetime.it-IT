---
title: Panoramica sui file multimediali di pacchetto
description: Panoramica sui file multimediali di pacchetto
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 0%

---


# Panoramica {#packaging-media-files-overview}

Il termine &quot;pacchetto&quot; si riferisce al processo di crittografia e applicazione di una policy DRM al contenuto video. Puoi utilizzare le API per la creazione di pacchetti multimediali per creare pacchetti di file. L&#39;SDK Java DRM di Primetime può creare un pacchetto solo per il contenuto a download progressivo, ad esempio MP4.

>[!NOTE]
>
>Contatta il tuo rappresentante DRM Primetime per sapere come selezionare l&#39;opzione di packaging più appropriata per il tuo formato multimediale e i casi d&#39;uso.

Il pacchetto viene scollegato dal server licenze. Non è necessario che il packager si connetta al server licenze per scambiare informazioni sul contenuto. Tutto ciò che il server licenze deve sapere per rilasciare una licenza è incluso nei metadati del contenuto.

Quando un file viene crittografato, il suo contenuto non può essere analizzato senza la licenza appropriata. È possibile utilizzare Primetime DRM per selezionare le parti del file che si desidera crittografare. Poiché Primetime DRM può analizzare il formato file del contenuto video, può crittografare in modo intelligente parti selettive di un file invece di un intero file. I dati, come metadati e punti di cue, possono rimanere non crittografati, in modo che i motori di ricerca possano comunque cercare il file.

Un contenuto specifico può avere più criteri DRM. Ad esempio, puoi concedere in licenza il contenuto in diversi modelli aziendali senza dover creare più pacchetti di contenuto. Inoltre, puoi consentire l’accesso anonimo per un breve periodo di tempo e consentire al cliente di acquistare il contenuto in modo che abbia accesso illimitato. Se il contenuto viene compilato utilizzando più criteri DRM, il server licenze deve implementare la logica per selezionare quale criterio DRM deve essere utilizzato per rilasciare una licenza.

>[!NOTE]
>
>L’architettura consente di specificare i criteri DRM di utilizzo e di associarli al contenuto quando il contenuto viene compilato. Prima che un client possa riprodurre contenuto, è necessario acquisire una licenza per un computer specifico. La licenza specifica le regole di utilizzo applicate e fornisce la chiave che deve essere utilizzata per decrittografare il contenuto. Il criterio DRM rappresenta un modello per la generazione di una licenza. Tuttavia, il server licenze può ignorare le regole di utilizzo quando rilascia una licenza. La licenza potrebbe essere resa non valida da tali vincoli, ad esempio i tempi di scadenza o le finestre di riproduzione.

Primetime DRM fornisce un&#39;API per il passaggio nella CEK. Se non viene specificato alcun CEK, l’SDK lo genera in modo casuale. In genere è necessario un CEK diverso per ogni sezione di contenuto. Tuttavia, in Dynamic Streaming, è probabile che si utilizzi lo stesso CEK per tutti i file che compongono tale contenuto. Pertanto, un utente necessita solo di una singola licenza per passare senza soluzione di continuità da un bit rate a un altro. Se desideri utilizzare la stessa chiave e la stessa licenza per più contenuti, devi passare lo stesso oggetto `DRMParameters` a `MediaEncrypter.encryptContent()` oppure passare la CEK utilizzando `V2KeyParameters.setContentEncryptionKey()`. Se desideri utilizzare una chiave e una licenza diverse per ogni sezione di contenuto, devi creare una nuova istanza `DRMParameters` per ogni file.

Quando si crea un pacchetto di contenuti utilizzando la rotazione dei tasti, è possibile controllare i tasti di rotazione utilizzati e la frequenza con cui i tasti cambiano. `F4VDRMParameters` e  `FLVDRMParameters` implementa l&#39; `KeyRotationParameters` interfaccia . Tramite questa interfaccia è possibile abilitare la rotazione delle chiavi. È inoltre necessario specificare un valore `RotatingContentEncryptionKeyProvider`. Per ogni esempio crittografato, questa classe determina la Chiave di rotazione da utilizzare. Puoi implementare il tuo provider oppure utilizzare il `TimeBasedKeyProvider` incluso nell&#39;SDK. Questa implementazione genera in modo casuale una nuova chiave dopo un numero specificato di secondi.

In alcuni casi potrebbe essere necessario archiviare i metadati del contenuto come file separato e renderli disponibili al client separatamente dal contenuto. In tal caso, è necessario richiamare `MediaEncrypter.encryptContent()`, che restituisce un oggetto `MediaEncrypterResult`. Chiama `MediaEncrypterResult.getKeyInfo()` e trascina il risultato su `V2KeyStatus`. Quindi recupera i metadati del contenuto e memorizzalo in un file.

Tutte queste attività possono essere eseguite con l’API Java.

Per informazioni dettagliate sull&#39;API Java, consulta *Riferimento API DRM di Adobe Primetime* .

Per informazioni sull&#39;implementazione di riferimento di Media Packager, consulta *Utilizzo delle implementazioni di riferimento DRM di Adobe Primetime* .
