---
description: Per aggiornare un server che supporta la versione 3.0 Reference Implementation License Server o Watched Folder Packager, è necessario sostituire i file .war distribuiti su un Application Server con i file inclusi con Adobe Primetime DRM Reference Implementation Server.
title: Aggiornare le distribuzioni esistenti
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# Panoramica {#upgrade-existing-deployments-overview}

Per aggiornare un server che supporta la versione 3.0 Reference Implementation License Server o Watched Folder Packager, è necessario sostituire i file .war distribuiti su un Application Server con i file inclusi con Adobe Primetime DRM Reference Implementation Server.

Per utilizzare la registrazione del dominio con il server licenze di implementazione di riferimento, sono necessarie diverse nuove tabelle di database. È necessario ricreare l&#39;intero database di implementazione di riferimento ed eseguire `CreateSampleDB.sql`.

Per conservare i record del database e aggiungere nuove tabelle:

1. Aprire `CreateSampleDB.sql` ed eseguire i comandi che creano le tabelle seguenti:

   * `DomainServerInfo`
   * `DomainKeys`
   * `DomainMembership`
   * `UserDomainMembership`
   * `UserDomainRefCount`

1. Aggiungi le seguenti proprietà a [!DNL flashaccess-refimpl.properties] per utilizzare il supporto del dominio:

   * `HandlerConfiguration.DomainCAs.n` o  `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

   * `Domain RegistrationHandler.ServerCredential` e  `DomainRegistrationHandler.ServerCredential.password` o  `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

   * `DomainRegistrationHandler.DomainServerUrl`

1. Aggiungi le seguenti proprietà a [!DNL flashaccess-refimpl.properties] per supportare la consegna di chiavi remote ai client iOS:

   * `HandlerConfiguration.KeyServerCertificate` o  `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`