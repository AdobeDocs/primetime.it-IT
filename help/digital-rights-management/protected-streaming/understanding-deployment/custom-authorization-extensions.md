---
description: È possibile richiamare la logica di autorizzazione personalizzata durante l'acquisizione della licenza per decidere se una licenza deve essere rilasciata al client richiedente.
title: Estensioni di autorizzazione personalizzate
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---

# Estensioni di autorizzazione personalizzate{#custom-authorization-extensions}

È possibile richiamare la logica di autorizzazione personalizzata durante l&#39;acquisizione della licenza per decidere se una licenza deve essere rilasciata al client richiedente.

Se desideri implementare una tua estensione di autorizzazione cliente, devi prima esaminare [!DNL SampleAuthorizer.java] codice di esempio che si trova nella directory samples. La versione compilata di questo esempio si trova in [!DNL flashaccess-license-server-ext-sample.jar].

Se desideri creare una tua estensione, devi implementare `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` e assicurati che [!DNL flashaccess-license-server-exts.jar] e [!DNL commons-logging.jar] sono nel percorso di compilazione ( [!DNL adobe-flashaccess-sdk.jar] deve trovarsi anche nel percorso di build se utilizzi alcuni campi in `IMessageFacade`).

Se desideri distribuire l’estensione, devi copiare i file jar o di classe in *LicenseServer.ConfigRoot* [!DNL /flashaccessserver/libs].

Se desideri aggiornare i file jar o di classe, devi riavviare il server prima di poter utilizzare la versione aggiornata. È inoltre necessario aggiungere il nome della classe di authoring al file di configurazione del tenant.
