---
title: Aggiornamento delle distribuzioni esistenti
description: Aggiornamento delle distribuzioni esistenti
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# Aggiornamento delle distribuzioni esistenti {#upgrading-existing-deployments}

Per aggiornare un server che esegue la versione 3.0 Reference Implementation License Server o Watched Folder Packager, sostituire i file [!DNL .war] distribuiti sul server applicazioni con i file inclusi in Adobe Access Reference Implementation Server.

Se si prevede di utilizzare la registrazione del dominio con il server licenze di implementazione di riferimento, sono necessarie diverse nuove tabelle di database. Per ricreare l&#39;intero database di implementazione di riferimento, esegui `CreateSampleDB.sql`. Per conservare i record di database esistenti e aggiungere le nuove tabelle, aprire `CreateSampleDB.sql`ed eseguire solo i comandi per creare le tabelle seguenti:

* `DomainServerInfo`
* `DomainKeys`
* `DomainMembership`
* `UserDomainMembership`
* `UserDomainRefCount`

Per utilizzare il supporto del dominio, è necessario aggiungere le seguenti proprietà a flashaccess-refimpl.properties :

* `HandlerConfiguration.DomainCAs.n` o  `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

* `Domain RegistrationHandler.ServerCredential` e  `DomainRegistrationHandler.ServerCredential.password`, oppure  `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

* `DomainRegistrationHandler.DomainServerUrl`

Per supportare la consegna di chiavi remote ai client iOS, è necessario aggiungere le seguenti proprietà a [!DNL flashaccess-refimpl.properties] :

* `HandlerConfiguration.KeyServerCertificate` o  `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`

