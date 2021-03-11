---
title: Estensioni di autorizzazione personalizzate
description: La logica di autorizzazione personalizzata può essere invocata durante l'acquisizione della licenza per decidere se rilasciare una licenza al cliente richiedente.
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# Estensioni di autorizzazione personalizzate {#custom-authorization-extensions}

La logica di autorizzazione personalizzata può essere invocata durante l&#39;acquisizione della licenza per decidere se rilasciare una licenza al cliente richiedente.

Per implementare la tua estensione di autorizzazione dei clienti, controlla innanzitutto il codice di esempio [!DNL SampleAuthorizer.java] presente nella directory dei campioni (la versione compilata di questo esempio si trova in flashaccess-license-server-ext-sample.jar).

Per generare la tua estensione, implementa l’ interfaccia `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` e assicurati che `flashaccess-license-server-exts.jar` e `commons-logging.jar` si trovino nel percorso di build `adobe-flashaccess-sdk.jar` anche nel percorso di build se utilizzi alcuni campi in `IMessageFacade`). Per distribuire l&#39;estensione, copia i file jar o class in *LicenseServer.ConfigRoot* `/flashaccessserver/libs`. Se è necessario aggiornare i file jar o class, è necessario riavviare il server prima di utilizzare la versione aggiornata. È inoltre necessario aggiungere il nome della classe dell’autore al file di configurazione del tenant.
