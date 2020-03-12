---
seo-title: Cifratura del contenuto
title: Cifratura del contenuto
uuid: 03f33473-bcd4-4e06-a823-e944897cb28e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Cifratura del contenuto{#encrypting-content}

È possibile cifrare il contenuto video con l&#39; `MediaEncrypter` oggetto. Potete cifrare i file multimediali che includono solo tracce audio. È inoltre possibile applicare solo la cifratura parziale; ad esempio, per migliorare le prestazioni durante la cifratura del contenuto H.264 per i dispositivi di fascia inferiore.

Per crittografare i file multimediali utilizzando l&#39;API Java:

1. Configurate l&#39;ambiente di sviluppo e includete tutti i file JAR menzionati in *Impostazione dell&#39;ambiente* di sviluppo all&#39;interno del progetto.
1. Creare un&#39; `ServerCredential` istanza per caricare le credenziali necessarie per la firma.
1. Create un&#39; `MediaEncrypter` istanza. Utilizzate un file `MediaEncryperFactory` se non sapete che tipo di file avete.

1. Specificare le opzioni di cifratura utilizzando un `DRMParameters` oggetto.
1. Impostare le opzioni di firma utilizzando un `SignatureParameters` oggetto e passare l&#39; `ServerCredential` istanza al relativo `setServerCredentials` metodo.

1. Impostare le informazioni sulla chiave e sulla licenza utilizzando un `V2KeyParameters` oggetto. Impostare i criteri DRM utilizzando il `setPolicies` metodo . Impostate le informazioni necessarie al client per contattare il server licenze chiamando i `setLicenseServerUrl` metodi e `setLicenseServerTransportCertificate` . Impostare le opzioni di cifratura CEK utilizzando il `setKeyProtectionOptions` metodo e le relative proprietà personalizzate utilizzando il `setCustomProperties` metodo . Infine, a seconda del tipo di cifratura utilizzato, inserire l&#39; `DRMKeyParameters` oggetto nel tipo appropriato ( `VideoDRMParameters`, `AudioDRMParameters`) e impostare le opzioni di cifratura.

1. Crittografare il contenuto passando al `MediaEncrypter.encryptContent` metodo i file di input e output e le opzioni di cifratura.

Per un esempio di codice che mostra come cifrare il contenuto, vedere `com.adobe.flashaccess.samples.mediapackager.EncryptContent` nella directory Strumenti della riga di comando Implementazione riferimento [!DNL samples/] .
