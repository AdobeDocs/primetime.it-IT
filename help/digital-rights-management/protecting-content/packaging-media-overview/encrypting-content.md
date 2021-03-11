---
title: Crittografia del contenuto
description: Crittografia del contenuto
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---


# Cifratura contenuto{#encrypting-content}

Il contenuto video viene crittografato con l’oggetto `MediaEncrypter` . È possibile crittografare i file multimediali che includono solo tracce audio. È inoltre possibile applicare solo la cifratura parziale; ad esempio, per migliorare le prestazioni quando si crittografa il contenuto H.264 per i dispositivi di fascia bassa.

Per crittografare i file multimediali utilizzando l’API Java:

1. Configura l&#39;ambiente di sviluppo e includi tutti i file JAR menzionati in *Impostazione dell&#39;ambiente di sviluppo* all&#39;interno del progetto.
1. Crea un&#39;istanza `ServerCredential` per caricare le credenziali necessarie per la firma.
1. Crea un&#39;istanza `MediaEncrypter`. Utilizza un `MediaEncryperFactory` se non sai che tipo di file hai.

1. Specificare le opzioni di crittografia utilizzando un oggetto `DRMParameters`.
1. Impostare le opzioni di firma utilizzando un oggetto `SignatureParameters` e passare l&#39;istanza `ServerCredential` al relativo metodo `setServerCredentials`.

1. Impostare le informazioni sulla chiave e sulla licenza utilizzando un oggetto `V2KeyParameters`. Imposta i criteri DRM utilizzando il metodo `setPolicies` . Imposta le informazioni necessarie al client per contattare il server licenze richiamando i metodi `setLicenseServerUrl` e `setLicenseServerTransportCertificate` . Impostare le opzioni di crittografia CEK utilizzando il metodo `setKeyProtectionOptions` e le relative proprietà personalizzate utilizzando il metodo `setCustomProperties` . Infine, a seconda del tipo di crittografia utilizzato, eseguire il cast dell&#39;oggetto `DRMKeyParameters` al tipo appropriato ( `VideoDRMParameters`, `AudioDRMParameters`) e impostare le opzioni di crittografia.

1. Cifrare il contenuto passando i file di input e di output e le opzioni di cifratura al metodo `MediaEncrypter.encryptContent` .

Per un esempio di codice che mostra come cifrare il contenuto, consulta `com.adobe.flashaccess.samples.mediapackager.EncryptContent` nella directory Strumenti della riga di comando Implementazione riferimento [!DNL samples/] .
