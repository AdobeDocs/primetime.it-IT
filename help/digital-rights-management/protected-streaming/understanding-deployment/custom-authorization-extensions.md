---
description: È possibile invocare la logica di autorizzazione personalizzata durante l'acquisizione della licenza per decidere se rilasciare una licenza al client richiedente.
seo-description: È possibile invocare la logica di autorizzazione personalizzata durante l'acquisizione della licenza per decidere se rilasciare una licenza al client richiedente.
seo-title: Estensioni di autorizzazione personalizzate
title: Estensioni di autorizzazione personalizzate
uuid: 588b05e5-3402-4586-bbd4-58b7e9a58ee4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Estensioni di autorizzazione personalizzate{#custom-authorization-extensions}

È possibile invocare la logica di autorizzazione personalizzata durante l&#39;acquisizione della licenza per decidere se rilasciare una licenza al client richiedente.

Se desiderate implementare la vostra estensione di autorizzazione del cliente, dovete prima dare un&#39;occhiata al codice di [!DNL SampleAuthorizer.java] esempio che si trova nella directory degli esempi. La versione compilata di questo esempio si trova in [!DNL flashaccess-license-server-ext-sample.jar].

Se si desidera creare una propria estensione, è necessario implementare l&#39; `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` interfaccia e assicurarsi [!DNL flashaccess-license-server-exts.jar] che e [!DNL commons-logging.jar] siano nel percorso di compilazione ( [!DNL adobe-flashaccess-sdk.jar] deve trovarsi anche nel percorso di compilazione se si utilizzano alcuni campi in `IMessageFacade`).

Per distribuire l’estensione, è necessario copiare i file jar o di classe in *LicenseServer.ConfigRoot* [!DNL /flashaccessserver/libs].

Per aggiornare i file jar o di classe, è necessario riavviare il server prima di poter utilizzare la versione aggiornata. È inoltre necessario aggiungere il nome della classe di authorizer al file di configurazione del tenant.
