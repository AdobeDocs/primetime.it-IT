---
seo-title: Verifica del contenuto del file crittografato
title: Verifica del contenuto del file crittografato
uuid: 1b3318f6-0850-43f2-9127-c72ea81a1bdf
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Verifica del contenuto del file crittografato{#examining-encrypted-file-content}

Potete esaminare il contenuto di un file multimediale crittografato utilizzando l&#39;API Java.

Per esaminare il contenuto del file crittografato:

1. Configurate l&#39;ambiente di sviluppo e includete tutti i file JAR. Consultate *Impostazione dell’SDK* per il progetto.
1. Create un&#39; `MediaEncrypter` istanza.
1. Passare il file crittografato al `MediaEncrypter.examineEncryptedContent` metodo, che restituisce un `KeyMetaData` oggetto.

1. Esaminare le informazioni all&#39;interno dell&#39; `KeyMetaData` oggetto.

Per un esempio di codice che descrive come estrarre i metadati DRM da un file crittografato, vedere `com.adobe.flashaccess.samples.mediapackager.ExamineContent` nella directory Strumenti della riga di comando di implementazione di riferimento [!DNL samples/] .
