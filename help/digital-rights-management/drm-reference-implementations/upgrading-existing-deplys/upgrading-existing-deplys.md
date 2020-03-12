---
description: Per aggiornare un server che supporta la versione 3.0 Reference Implementation License Server o Watched Folder Packager, è necessario sostituire i file .war distribuiti su un server applicazioni con i file inclusi con Adobe Primetime DRM Reference Implementation Server.
seo-description: Per aggiornare un server che supporta la versione 3.0 Reference Implementation License Server o Watched Folder Packager, è necessario sostituire i file .war distribuiti su un server applicazioni con i file inclusi con Adobe Primetime DRM Reference Implementation Server.
seo-title: Aggiornamento delle distribuzioni esistenti
title: Aggiornamento delle distribuzioni esistenti
uuid: 1a40aae9-f639-41fa-b42d-cf8cdfcde694
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# Panoramica {#upgrade-existing-deployments-overview}

Per aggiornare un server che supporta la versione 3.0 Reference Implementation License Server o Watched Folder Packager, è necessario sostituire i file .war distribuiti su un server applicazioni con i file inclusi con Adobe Primetime DRM Reference Implementation Server.

Per utilizzare la registrazione del dominio con il server delle licenze di implementazione di riferimento, sono necessarie diverse nuove tabelle di database. È necessario ricreare l&#39;intero database di implementazione dei riferimenti ed eseguire `CreateSampleDB.sql`.

Per conservare i record del database e aggiungere nuove tabelle:

1. Aprire `CreateSampleDB.sql` ed eseguire comandi che creano le tabelle seguenti:

   * `DomainServerInfo`
   * `DomainKeys`
   * `DomainMembership`
   * `UserDomainMembership`
   * `UserDomainRefCount`

1. Aggiungete le seguenti proprietà [!DNL flashaccess-refimpl.properties] per utilizzare il supporto del dominio:

   * `HandlerConfiguration.DomainCAs.n` os `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

   * `Domain RegistrationHandler.ServerCredential` e `DomainRegistrationHandler.ServerCredential.password``RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

   * `DomainRegistrationHandler.DomainServerUrl`

1. Aggiungete le seguenti proprietà [!DNL flashaccess-refimpl.properties] per supportare la distribuzione di chiavi remote ai client iOS:

   * `HandlerConfiguration.KeyServerCertificate` os `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`