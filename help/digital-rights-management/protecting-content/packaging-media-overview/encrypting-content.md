---
title: Crittografia del contenuto
description: Crittografia del contenuto
copied-description: true
exl-id: c6b5d8c7-eda4-40c0-a609-0ebfeba90c04
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# Crittografia del contenuto{#encrypting-content}

I contenuti video vengono crittografati con `MediaEncrypter` oggetto. È possibile crittografare i file multimediali che includono solo tracce audio. È inoltre possibile applicare solo la crittografia parziale, ad esempio per migliorare le prestazioni quando si crittografano i contenuti H.264 per dispositivi di fascia bassa.

Per crittografare i file multimediali utilizzando l’API Java:

1. Configura l’ambiente di sviluppo e includi tutti i file JAR menzionati in *Configurazione dell’ambiente di sviluppo* all’interno del progetto.
1. Creare un `ServerCredential` per caricare le credenziali necessarie per la firma.
1. Creare un `MediaEncrypter` dell&#39;istanza. Utilizza un `MediaEncryperFactory` se non sai che tipo di file hai.

1. Specificare le opzioni di crittografia utilizzando un `DRMParameters` oggetto.
1. Impostare le opzioni di firma utilizzando un `SignatureParameters` e passare il `ServerCredential` istanza al relativo `setServerCredentials` metodo.

1. Impostare la chiave e le informazioni sulla licenza utilizzando un `V2KeyParameters` oggetto. Impostare i criteri DRM utilizzando `setPolicies` metodo. Impostare le informazioni necessarie al client per contattare il server licenze chiamando `setLicenseServerUrl` e `setLicenseServerTransportCertificate` metodi. Impostare le opzioni di crittografia CEK utilizzando `setKeyProtectionOptions` e le relative proprietà personalizzate utilizzando `setCustomProperties` metodo. Infine, a seconda del tipo di crittografia utilizzata, esegui il cast `DRMKeyParameters` oggetto al tipo appropriato ( `VideoDRMParameters`, `AudioDRMParameters`) e impostare le opzioni di crittografia.

1. Crittografa il contenuto passando i file di input e di output e le opzioni di crittografia al `MediaEncrypter.encryptContent` metodo.

Per un codice di esempio che mostra come crittografare il contenuto, consulta `com.adobe.flashaccess.samples.mediapackager.EncryptContent` negli strumenti della riga di comando per l’implementazione di riferimento [!DNL samples/] directory.
