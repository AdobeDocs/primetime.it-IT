---
title: Aggiornamento delle implementazioni esistenti
description: Aggiornamento delle implementazioni esistenti
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# Aggiornamento delle implementazioni esistenti {#upgrading-existing-deployments}

Per aggiornare un server che esegue la versione 3.0 di Reference Implementation License Server o Watched Folder Packager, sostituire la [!DNL .war] file distribuiti sul server applicazioni con i file inclusi nel server di implementazione di riferimento per l&#39;accesso agli Adobi.

Se si prevede di utilizzare la registrazione del dominio con il server licenze di implementazione di riferimento, sono necessarie diverse nuove tabelle di database. Per ricreare l&#39;intero database di implementazione di riferimento, eseguire `CreateSampleDB.sql`. Per conservare i record del database esistenti e aggiungere le nuove tabelle, aprire `CreateSampleDB.sql`ed esegui solo i comandi per creare le tabelle seguenti:

* `DomainServerInfo`
* `DomainKeys`
* `DomainMembership`
* `UserDomainMembership`
* `UserDomainRefCount`

Per utilizzare il supporto del dominio, è necessario aggiungere le seguenti proprietà a flashaccess-refimpl.properties:

* `HandlerConfiguration.DomainCAs.n` o `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

* `Domain RegistrationHandler.ServerCredential` e `DomainRegistrationHandler.ServerCredential.password`, o `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

* `DomainRegistrationHandler.DomainServerUrl`

Le seguenti proprietà devono essere aggiunte a [!DNL flashaccess-refimpl.properties] per supportare la consegna di chiavi remote ai client iOS:

* `HandlerConfiguration.KeyServerCertificate` o `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`
