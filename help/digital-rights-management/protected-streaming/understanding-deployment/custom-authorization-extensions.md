---
description: È possibile invocare la logica di autorizzazione personalizzata durante l'acquisizione della licenza per decidere se rilasciare una licenza al client richiedente.
title: Estensioni di autorizzazione personalizzate
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---


# Estensioni di autorizzazione personalizzate{#custom-authorization-extensions}

È possibile invocare la logica di autorizzazione personalizzata durante l&#39;acquisizione della licenza per decidere se rilasciare una licenza al client richiedente.

Se desideri implementare una tua estensione di autorizzazione dei clienti, devi prima dare un&#39;occhiata al codice di esempio [!DNL SampleAuthorizer.java] presente nella directory amples. La versione compilata di questo esempio si trova in [!DNL flashaccess-license-server-ext-sample.jar].

Se desideri generare la tua estensione, devi implementare l’interfaccia `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` e accertarti che [!DNL flashaccess-license-server-exts.jar] e [!DNL commons-logging.jar] siano nel percorso di build ( [!DNL adobe-flashaccess-sdk.jar] deve trovarsi anche nel percorso di build se utilizzi determinati campi in `IMessageFacade`).

Se desideri distribuire l&#39;estensione, devi copiare i file jar o class in *LicenseServer.ConfigRoot* [!DNL /flashaccessserver/libs].

Per aggiornare i file jar o class, è necessario riavviare il server prima di poter utilizzare la versione aggiornata. È inoltre necessario aggiungere il nome della classe dell’autore al file di configurazione del tenant.
