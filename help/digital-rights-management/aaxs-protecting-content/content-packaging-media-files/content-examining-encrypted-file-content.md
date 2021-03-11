---
title: Analisi del contenuto del file crittografato
description: Analisi del contenuto del file crittografato
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# Esame del contenuto del file crittografato {#examining-encrypted-file-content}

Per esaminare il contenuto di un file FLV o F4V utilizzando l’API Java, esegui le seguenti operazioni:

1. Configura l&#39;ambiente di sviluppo e includi tutti i file JAR menzionati in [Impostazione dell&#39;ambiente di sviluppo](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) all&#39;interno del progetto.
1. Crea un&#39;istanza `MediaEncrypter`.
1. Passa il file crittografato al metodo `MediaEncrypter.examineEncryptedContent` che restituisce un oggetto `KeyMetaData`.
1. Inspect le informazioni all&#39;interno dell&#39;oggetto `KeyMetaData` .

Per un esempio di codice che illustra come estrarre i metadati DRM da un file crittografato, consulta `com.adobe.flashaccess.samples.mediapackager.ExamineContent` nella directory &quot;amples&quot; degli strumenti della riga di comando per l’implementazione di riferimento.
