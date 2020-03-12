---
seo-title: Estensioni di autorizzazione personalizzate
title: Estensioni di autorizzazione personalizzate
description: La logica di autorizzazione personalizzata può essere invocata durante l'acquisizione della licenza per decidere se rilasciare una licenza al cliente richiedente.
seo-description: La logica di autorizzazione personalizzata può essere invocata durante l'acquisizione della licenza per decidere se rilasciare una licenza al cliente richiedente.
uuid: fb40db6f-30aa-46e3-9eeb-faff3cfedab1
translation-type: tm+mt
source-git-commit: fe9493d610bc6fb97d30351c707b73cda92c67a0

---


# Estensioni di autorizzazione personalizzate {#custom-authorization-extensions}

La logica di autorizzazione personalizzata può essere invocata durante l&#39;acquisizione della licenza per decidere se rilasciare una licenza al cliente richiedente.

Per implementare la propria estensione di autorizzazione del cliente, consultare innanzitutto il codice di [!DNL SampleAuthorizer.java] esempio presente nella directory degli esempi (la versione compilata di questo esempio si trova in flashaccess-license-server-ext-sample.jar).

Per creare una propria estensione, implementate l&#39; `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` interfaccia e assicuratevi che `flashaccess-license-server-exts.jar` e `commons-logging.jar` siano sul percorso di compilazione `adobe-flashaccess-sdk.jar` sia anche sul percorso di compilazione, se utilizzate alcuni campi in `IMessageFacade`). Per distribuire l’estensione, copiate i file jar o di classe in *LicenseServer.ConfigRoot*`/flashaccessserver/libs`. Se è necessario aggiornare i file jar o di classe, il server deve essere riavviato prima di utilizzare la versione aggiornata. È inoltre necessario aggiungere il nome della classe di authorizer al file di configurazione del tenant.
