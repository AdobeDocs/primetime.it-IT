---
title: Esame del contenuto di file crittografati
description: Esame del contenuto di file crittografati
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# Esame del contenuto di file crittografati {#examining-encrypted-file-content}

Per esaminare il contenuto di un file FLV o F4V utilizzando l&#39;API Java, effettuare le seguenti operazioni:

1. Configura l’ambiente di sviluppo e includi tutti i file JAR menzionati in [Configurazione dell’ambiente di sviluppo](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) all’interno del progetto.
1. Creare un `MediaEncrypter` dell&#39;istanza.
1. Passa il file crittografato a `MediaEncrypter.examineEncryptedContent` , che restituisce un `KeyMetaData` oggetto.
1. Inspect le informazioni all’interno di `KeyMetaData` oggetto.

Per un codice di esempio che illustra come estrarre i metadati DRM da un file crittografato, vedere `com.adobe.flashaccess.samples.mediapackager.ExamineContent` nella directory &quot;samples&quot; degli strumenti della riga di comando per l’implementazione di riferimento.
