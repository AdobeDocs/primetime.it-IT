---
seo-title: Cifratura del contenuto
title: Cifratura del contenuto
uuid: 03f33473-bcd4-4e06-a823-e944897cb28e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---


# Cifratura di contenuto{#encrypting-content}

Il contenuto video viene cifrato con l&#39;oggetto `MediaEncrypter`. Potete cifrare i file multimediali che includono solo tracce audio. È inoltre possibile applicare solo la cifratura parziale; ad esempio, per migliorare le prestazioni durante la cifratura del contenuto H.264 per i dispositivi di fascia inferiore.

Per crittografare i file multimediali utilizzando l&#39;API Java:

1. Configurate l&#39;ambiente di sviluppo e includete tutti i file JAR menzionati in *Impostazione dell&#39;ambiente di sviluppo* all&#39;interno del progetto.
1. Creare un&#39;istanza `ServerCredential` per caricare le credenziali necessarie per la firma.
1. Create un&#39;istanza `MediaEncrypter`. Utilizzare un `MediaEncryperFactory` se non si conosce il tipo di file di cui si dispone.

1. Specificare le opzioni di cifratura utilizzando un oggetto `DRMParameters`.
1. Impostare le opzioni di firma utilizzando un oggetto `SignatureParameters` e passare l&#39;istanza `ServerCredential` al relativo metodo `setServerCredentials`.

1. Impostare le informazioni sulla chiave e sulla licenza utilizzando un oggetto `V2KeyParameters`. Impostare i criteri DRM utilizzando il metodo `setPolicies`. Impostate le informazioni necessarie al client per contattare il server licenze chiamando i metodi `setLicenseServerUrl` e `setLicenseServerTransportCertificate`. Impostare le opzioni di cifratura CEK utilizzando il metodo `setKeyProtectionOptions` e le relative proprietà personalizzate utilizzando il metodo `setCustomProperties`. Infine, a seconda del tipo di cifratura utilizzato, inserire l&#39;oggetto `DRMKeyParameters` nel tipo appropriato ( `VideoDRMParameters`, `AudioDRMParameters`) e impostare le opzioni di cifratura.

1. Cifra il contenuto trasmettendo i file di input e output e le opzioni di cifratura al metodo `MediaEncrypter.encryptContent`.

Per un esempio di codice che mostra come cifrare il contenuto, vedere `com.adobe.flashaccess.samples.mediapackager.EncryptContent` nella directory Reference Implementation Command Line Tools [!DNL samples/].
