---
seo-title: Aggiornamento delle distribuzioni esistenti
title: Aggiornamento delle distribuzioni esistenti
uuid: 57e62a88-e541-435c-8274-7f1602548601
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Aggiornamento delle distribuzioni esistenti {#upgrading-existing-deployments}

Per aggiornare un server che esegue la versione 3.0 Reference Implementation License Server o Watched Folder Packager, sostituite i [!DNL .war] file distribuiti sul server applicazioni con i file inclusi in Adobe Access Reference Implementation Server.

Se si prevede di utilizzare la registrazione del dominio con il server delle licenze di implementazione di riferimento, sono necessarie diverse nuove tabelle di database. Per ricreare l&#39;intero database di implementazione dei riferimenti, eseguire `CreateSampleDB.sql`. Per conservare i record di database esistenti e aggiungere le nuove tabelle, aprire `CreateSampleDB.sql`ed eseguire solo i comandi per creare le tabelle seguenti:

* `DomainServerInfo`
* `DomainKeys`
* `DomainMembership`
* `UserDomainMembership`
* `UserDomainRefCount`

Per utilizzare il supporto del dominio, è necessario aggiungere le seguenti proprietà a flashaccess-refimpl.properties:

* `HandlerConfiguration.DomainCAs.n` os `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

* `Domain RegistrationHandler.ServerCredential` e `DomainRegistrationHandler.ServerCredential.password`, oppure `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

* `DomainRegistrationHandler.DomainServerUrl`

Per [!DNL flashaccess-refimpl.properties] supportare la distribuzione di chiavi remote ai client iOS, è necessario aggiungere le seguenti proprietà:

* `HandlerConfiguration.KeyServerCertificate` os `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`

