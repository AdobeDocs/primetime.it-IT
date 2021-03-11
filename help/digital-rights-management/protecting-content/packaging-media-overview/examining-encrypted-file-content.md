---
title: Analisi del contenuto del file crittografato
description: Analisi del contenuto del file crittografato
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# Esame del contenuto del file crittografato{#examining-encrypted-file-content}

Puoi esaminare il contenuto di un file multimediale crittografato utilizzando l’API Java.

Per esaminare il contenuto del file crittografato:

1. Imposta l&#39;ambiente di sviluppo e includi tutti i file JAR. Consulta *Configurazione dell&#39;SDK* per il progetto.
1. Crea un&#39;istanza `MediaEncrypter`.
1. Passa il file crittografato al metodo `MediaEncrypter.examineEncryptedContent` che restituisce un oggetto `KeyMetaData`.

1. Inspect le informazioni all&#39;interno dell&#39;oggetto `KeyMetaData` .

Per un esempio di codice che descrive come estrarre i metadati DRM da un file crittografato, consulta `com.adobe.flashaccess.samples.mediapackager.ExamineContent` nella directory Strumenti della riga di comando di implementazione di riferimento [!DNL samples/] .
