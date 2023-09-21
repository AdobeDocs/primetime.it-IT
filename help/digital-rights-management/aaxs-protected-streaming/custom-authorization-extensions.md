---
title: Estensioni di autorizzazione personalizzate
description: Durante l'acquisizione della licenza è possibile richiamare la logica di autorizzazione personalizzata per decidere se è necessario rilasciare una licenza al client richiedente.
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# Estensioni di autorizzazione personalizzate {#custom-authorization-extensions}

Durante l&#39;acquisizione della licenza è possibile richiamare la logica di autorizzazione personalizzata per decidere se è necessario rilasciare una licenza al client richiedente.

Per implementare una tua estensione di autorizzazione del cliente, controlla [!DNL SampleAuthorizer.java] codice di esempio che si trova nella directory samples (la versione compilata di questo esempio si trova in flashaccess-license-server-ext-sample.jar).

Per creare una tua estensione, implementa la `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` e assicurati che `flashaccess-license-server-exts.jar` e `commons-logging.jar` si trovano nel percorso di compilazione `adobe-flashaccess-sdk.jar` deve trovarsi anche nel percorso di build se utilizzi alcuni campi in `IMessageFacade`). Per distribuire l’estensione, copia i file jar o di classe in *LicenseServer.ConfigRoot* `/flashaccessserver/libs`. Se devi aggiornare i file jar o di classe, il server deve essere riavviato prima di utilizzare la versione aggiornata. È inoltre necessario aggiungere il nome della classe di authoring al file di configurazione del tenant.
