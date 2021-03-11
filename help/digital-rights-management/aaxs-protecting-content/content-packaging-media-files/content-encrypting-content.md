---
title: Crittografia del contenuto
description: Crittografia del contenuto
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---


# Cifratura contenuto{#encrypting-content}

La crittografia dei contenuti FLV e F4V comporta l’utilizzo di un oggetto `MediaEncrypter`. È inoltre possibile creare pacchetti di file FLV e F4V che contengono solo tracce audio. Quando si crittografano i contenuti H.264 per i dispositivi di fascia bassa, può essere pratico applicare solo la crittografia parziale per migliorare le prestazioni. In questi casi, un file F4V può essere parzialmente crittografato utilizzando il metodo `F4VDRMParameters.setVideoEncryptionLevel`.

Per crittografare un file FLV o F4V utilizzando l’API Java, esegui i seguenti passaggi:

1. Imposta l’ambiente di sviluppo e includi tutti i file JAR menzionati in Impostazione dell’ambiente di sviluppo all’interno del progetto.
1. Crea un&#39;istanza `ServerCredential` per caricare le credenziali necessarie per la firma.
1. Crea un&#39;istanza `MediaEncrypter`. Utilizza un `MediaEncryperFactory` se non sai che tipo di file hai. In caso contrario è possibile creare direttamente un `FLVEncrypter` o `F4VEncrypter`.
1. Specificare le opzioni di crittografia utilizzando un oggetto `DRMParameters`.
1. Impostare le opzioni di firma utilizzando un oggetto `SignatureParameters` e passare l&#39;istanza `ServerCredential` al relativo metodo `setServerCredentials`.
1. Impostare le informazioni sulla chiave e sulla licenza utilizzando un oggetto `V2KeyParameters`. Impostare i criteri utilizzando il metodo `setPolicies` . Imposta le informazioni necessarie al client per contattare il server licenze richiamando i metodi `setLicenseServerUrl` e `setLicenseServerTransportCertificate` . Impostare le opzioni di crittografia CEK utilizzando il metodo `setKeyProtectionOptions` e le relative proprietà personalizzate utilizzando il metodo `setCustomProperties` . Infine, a seconda del tipo di crittografia utilizzato, eseguire il cast dell&#39;oggetto `DRMKeyParameters` su uno dei valori `VideoDRMParameters`, `AudioDRMParameters`, `FLVDRMParameters` o `F4VDRMParameters` e impostare le opzioni di crittografia.
1. Cifrare il contenuto passando i file di input e di output e le opzioni di cifratura al metodo `MediaEncrypter.encryptContent` .

Per un esempio di codice che illustra come cifrare il contenuto, consulta `com.adobe.flashaccess.samples.mediapackager.EncryptContent` nella directory &quot;amples&quot; degli strumenti della riga di comando per l’implementazione di riferimento.
