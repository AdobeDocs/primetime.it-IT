---
seo-title: Cifratura del contenuto
title: Cifratura del contenuto
uuid: ea71154e-557b-447e-bc14-208232f00be1
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Cifratura del contenuto{#encrypting-content}

La cifratura dei contenuti FLV e F4V implica l&#39;utilizzo di un `MediaEncrypter` oggetto. Potete anche creare pacchetti di file FLV e F4V contenenti solo tracce audio. Durante la cifratura del contenuto H.264 per i dispositivi di fascia inferiore, può essere pratico applicare solo la cifratura parziale per migliorare le prestazioni. In tali casi, un file F4V può essere cifrato parzialmente utilizzando il `F4VDRMParameters.setVideoEncryptionLevel`metodo .

Per crittografare un file FLV o F4V utilizzando l&#39;API Java, effettuate le seguenti operazioni:

1. Configurate l&#39;ambiente di sviluppo e includete tutti i file JAR citati in Impostazione dell&#39;ambiente di sviluppo all&#39;interno del progetto.
1. Creare un&#39; `ServerCredential` istanza per caricare le credenziali necessarie per la firma.
1. Create un&#39; `MediaEncrypter` istanza. Utilizzate un file `MediaEncryperFactory` se non sapete che tipo di file avete. In caso contrario, potete creare un oggetto `FLVEncrypter` o `F4VEncrypter` direttamente.
1. Specificare le opzioni di cifratura utilizzando un `DRMParameters` oggetto.
1. Impostare le opzioni di firma utilizzando un `SignatureParameters` oggetto e passare l&#39; `ServerCredential` istanza al relativo `setServerCredentials` metodo.
1. Impostare le informazioni sulla chiave e sulla licenza utilizzando un `V2KeyParameters` oggetto. Impostare i criteri utilizzando il `setPolicies` metodo . Impostate le informazioni necessarie al client per contattare il server licenze chiamando i `setLicenseServerUrl` metodi e `setLicenseServerTransportCertificate` . Impostare le opzioni di cifratura CEK utilizzando il `setKeyProtectionOptions` metodo e le relative proprietà personalizzate utilizzando il `setCustomProperties` metodo . Infine, a seconda del tipo di cifratura utilizzato, inserire l&#39; `DRMKeyParameters` oggetto in uno dei `VideoDRMParameters`, `AudioDRMParameters`, `FLVDRMParameters`o `F4VDRMParameters`e impostare le opzioni di cifratura.
1. Cifra il contenuto passando al `MediaEncrypter.encryptContent` metodo i file di input e output e le opzioni di cifratura.

Per un esempio di codice che illustra come cifrare il contenuto, vedere `com.adobe.flashaccess.samples.mediapackager.EncryptContent` nella directory &quot;samples&quot; degli strumenti della riga di comando per l’implementazione di riferimento.
