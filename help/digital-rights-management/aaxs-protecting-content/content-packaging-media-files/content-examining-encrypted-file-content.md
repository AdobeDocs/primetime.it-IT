---
seo-title: Verifica del contenuto del file crittografato
title: Verifica del contenuto del file crittografato
uuid: 2132fac7-5f11-4308-b511-ed4f216527a6
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Verifica del contenuto del file crittografato {#examining-encrypted-file-content}

Per esaminare il contenuto di un file FLV o F4V utilizzando l&#39;API Java, effettuate le seguenti operazioni:

1. Configurate l&#39;ambiente di sviluppo e includete tutti i file JAR menzionati in [Impostazione dell&#39;ambiente](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) di sviluppo all&#39;interno del progetto.
1. Create un&#39; `MediaEncrypter` istanza.
1. Passare il file crittografato al `MediaEncrypter.examineEncryptedContent` metodo, che restituisce un `KeyMetaData` oggetto.
1. Esaminare le informazioni all&#39;interno dell&#39; `KeyMetaData` oggetto.

Per un esempio di codice che illustra come estrarre i metadati DRM da un file crittografato, vedere `com.adobe.flashaccess.samples.mediapackager.ExamineContent` nella directory &quot;samples&quot; degli strumenti della riga di comando di implementazione di riferimento.
