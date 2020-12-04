---
seo-title: Cifratura del contenuto
title: Cifratura del contenuto
uuid: ea71154e-557b-447e-bc14-208232f00be1
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---


# Cifratura di contenuto{#encrypting-content}

La cifratura dei contenuti FLV e F4V implica l&#39;utilizzo di un oggetto `MediaEncrypter`. Potete anche creare pacchetti di file FLV e F4V contenenti solo tracce audio. Durante la cifratura del contenuto H.264 per i dispositivi di fascia inferiore, può essere pratico applicare solo la cifratura parziale per migliorare le prestazioni. In tali casi, un file F4V può essere cifrato parzialmente utilizzando il metodo `F4VDRMParameters.setVideoEncryptionLevel`.

Per crittografare un file FLV o F4V utilizzando l&#39;API Java, effettuate le seguenti operazioni:

1. Configurate l&#39;ambiente di sviluppo e includete tutti i file JAR citati in Impostazione dell&#39;ambiente di sviluppo all&#39;interno del progetto.
1. Creare un&#39;istanza `ServerCredential` per caricare le credenziali necessarie per la firma.
1. Create un&#39;istanza `MediaEncrypter`. Utilizzare un `MediaEncryperFactory` se non si conosce il tipo di file di cui si dispone. In caso contrario è possibile creare direttamente un `FLVEncrypter` o `F4VEncrypter`.
1. Specificare le opzioni di cifratura utilizzando un oggetto `DRMParameters`.
1. Impostare le opzioni di firma utilizzando un oggetto `SignatureParameters` e passare l&#39;istanza `ServerCredential` al relativo metodo `setServerCredentials`.
1. Impostare le informazioni sulla chiave e sulla licenza utilizzando un oggetto `V2KeyParameters`. Impostare i criteri utilizzando il metodo `setPolicies`. Impostate le informazioni necessarie al client per contattare il server licenze chiamando i metodi `setLicenseServerUrl` e `setLicenseServerTransportCertificate`. Impostare le opzioni di cifratura CEK utilizzando il metodo `setKeyProtectionOptions` e le relative proprietà personalizzate utilizzando il metodo `setCustomProperties`. Infine, a seconda del tipo di cifratura utilizzato, inserire l&#39;oggetto `DRMKeyParameters` in uno dei formati `VideoDRMParameters`, `AudioDRMParameters`, `FLVDRMParameters` o `F4VDRMParameters` e impostare le opzioni di cifratura.
1. Cifra il contenuto trasmettendo i file di input e output e le opzioni di cifratura al metodo `MediaEncrypter.encryptContent`.

Per un esempio di codice che illustra come cifrare il contenuto, vedere `com.adobe.flashaccess.samples.mediapackager.EncryptContent` nella directory &quot;samples&quot; degli strumenti della riga di comando di implementazione di riferimento.
