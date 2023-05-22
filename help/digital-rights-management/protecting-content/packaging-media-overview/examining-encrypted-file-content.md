---
title: Esame del contenuto di file crittografati
description: Esame del contenuto di file crittografati
copied-description: true
exl-id: df1fd04d-016e-4770-bcb9-97bfe2d39260
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# Esame del contenuto di file crittografati{#examining-encrypted-file-content}

Puoi esaminare il contenuto di un file multimediale crittografato utilizzando l’API Java.

Per esaminare il contenuto di un file crittografato:

1. Configura l’ambiente di sviluppo e includi tutti i file JAR. Consulta *Configurazione dell’SDK* per il tuo progetto.
1. Creare un `MediaEncrypter` dell&#39;istanza.
1. Passa il file crittografato a `MediaEncrypter.examineEncryptedContent` , che restituisce un `KeyMetaData` oggetto.

1. Inspect le informazioni all’interno di `KeyMetaData` oggetto.

Per un codice di esempio che descrive come estrarre i metadati DRM da un file crittografato, vedere `com.adobe.flashaccess.samples.mediapackager.ExamineContent` negli strumenti della riga di comando per l’implementazione di riferimento [!DNL samples/] directory.
