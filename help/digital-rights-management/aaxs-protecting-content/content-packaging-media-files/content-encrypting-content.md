---
title: Crittografia del contenuto
description: Crittografia del contenuto
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# Crittografia del contenuto{#encrypting-content}

La crittografia dei contenuti FLV e F4V comporta l&#39;utilizzo di un `MediaEncrypter` oggetto. È inoltre possibile creare pacchetti di file FLV e F4V che contengono solo tracce audio. Quando si crittografano i contenuti H.264 per i dispositivi di fascia bassa, può risultare pratico applicare solo una crittografia parziale per migliorare le prestazioni. In tali casi, un file F4V può essere parzialmente crittografato utilizzando `F4VDRMParameters.setVideoEncryptionLevel`metodo.

Per crittografare un file FLV o F4V utilizzando l&#39;API Java, effettuare le seguenti operazioni:

1. Configura l’ambiente di sviluppo e includi tutti i file JAR menzionati in Configurazione dell’ambiente di sviluppo all’interno del progetto.
1. Creare un `ServerCredential` per caricare le credenziali necessarie per la firma.
1. Creare un `MediaEncrypter` dell&#39;istanza. Utilizza un `MediaEncryperFactory` se non sai che tipo di file hai. Altrimenti puoi creare un’ `FLVEncrypter` o `F4VEncrypter` direttamente.
1. Specificare le opzioni di crittografia utilizzando un `DRMParameters` oggetto.
1. Impostare le opzioni di firma utilizzando un `SignatureParameters` e passare il `ServerCredential` istanza al relativo `setServerCredentials` metodo.
1. Impostare la chiave e le informazioni sulla licenza utilizzando un `V2KeyParameters` oggetto. Impostare i criteri utilizzando `setPolicies` metodo. Impostare le informazioni necessarie al client per contattare il server licenze chiamando `setLicenseServerUrl` e `setLicenseServerTransportCertificate` metodi. Impostare le opzioni di crittografia CEK utilizzando `setKeyProtectionOptions` e le relative proprietà personalizzate utilizzando `setCustomProperties` metodo. Infine, a seconda del tipo di crittografia utilizzata, esegui il cast `DRMKeyParameters` oggetto a uno di `VideoDRMParameters`, `AudioDRMParameters`, `FLVDRMParameters`, o `F4VDRMParameters`e impostare le opzioni di crittografia.
1. Crittografa il contenuto passando i file di input e di output e le opzioni di crittografia al `MediaEncrypter.encryptContent` metodo.

Per un codice di esempio che illustra come crittografare il contenuto, consulta `com.adobe.flashaccess.samples.mediapackager.EncryptContent` nella directory &quot;samples&quot; degli strumenti della riga di comando per l’implementazione di riferimento.
