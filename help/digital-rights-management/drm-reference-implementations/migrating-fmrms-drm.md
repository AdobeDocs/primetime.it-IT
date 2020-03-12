---
description: Per continuare a rilasciare licenze per contenuti che sono stati inclusi in pacchetti con Flash Media Rights Management Server (FMRMS) 1.0 o 1.5, è necessario migrare i dati delle licenze e dei criteri DRM dal server LiveCycle ES al nuovo server del cliente basato su Adobe Primetime DRM SDK.
seo-description: Per continuare a rilasciare licenze per contenuti che sono stati inclusi in pacchetti con Flash Media Rights Management Server (FMRMS) 1.0 o 1.5, è necessario migrare i dati delle licenze e dei criteri DRM dal server LiveCycle ES al nuovo server del cliente basato su Adobe Primetime DRM SDK.
seo-title: Migrazione da FMRMS 1.0 o 1.5 ad Adobe Primetime DRM 2.0 o versione successiva
title: Migrazione da FMRMS 1.0 o 1.5 ad Adobe Primetime DRM 2.0 o versione successiva
uuid: 49ecbbd2-d83b-4bf2-841e-c3f9e5d5e141
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Migrazione da FMRMS 1.0 o 1.5 ad Adobe Primetime DRM 2.0 o versione successiva{#migrate-from-fmrms-or-to-adobe-primetime-drm-or-later}

Per continuare a rilasciare licenze per contenuti che sono stati inclusi in pacchetti con Flash Media Rights Management Server (FMRMS) 1.0 o 1.5, è necessario migrare i dati delle licenze e dei criteri DRM dal server LiveCycle ES al nuovo server del cliente basato su Adobe Primetime DRM SDK.

Per eseguire la migrazione, completare le seguenti attività:

1. Informazioni sulle licenze di importazione:

   1. Per importare le informazioni sulla licenza da LiveCycle ES al server basato su DRM di Primetime, vedere gli script di database di esempio nella [!DNL Reference Implementation\Server\migration\db] cartella.
   1. Eseguire gli script di esempio per esportare i dati rilevanti da un database MySQL, Oracle o SQL Server in un formato di file CSV.
   1. Dopo aver esportato i dati da LiveCycle ES, importarli nel database.

      Le informazioni sulla licenza esportata includono quanto segue:

      * ID licenza
      * Un ID contenuto assegnato al momento della creazione del pacchetto
      * ID del criterio DRM applicato
      * L&#39;ora in cui è stato creato il pacchetto del contenuto
      * La chiave di crittografia del contenuto
      Queste informazioni sono necessarie prima di poter convertire i metadati del contenuto 1.x nel formato di metadati DRM di Primetime. Nell&#39;implementazione di riferimento, questi dati vengono memorizzati nella tabella del database delle licenze e utilizzati da `RefImplMetadataConvReqHandler`. For more information, see `FMRMSv1RequestHandler` and `FMRMSv1MetadataHandler`.


1. Conversione dei criteri FMRMS nel formato DRM di Primetime:

   1. Prima di poter applicare i criteri DRM per convertire i metadati e rilasciare licenze per i contenuti della versione 1.0 o 1.5, convertite i criteri DRM esistenti nel formato DRM di Primetime.

      La `Reference Implementation\Server\migration` cartella include il codice di esempio per creare un criterio DRM Primetime basato su criteri DRM meno recenti. Per effettuare la migrazione da FMRMS 1.0 a DRM di Primetime, vedere il `V1_0PolicyConverter.java` campione.
   1. Compilate il codice di esempio eseguendo `ant-f build-migration.xml build-1.0-converter` lo script, che cerca le librerie DRM 1.0 e Primetime nelle [!DNL libs/1.0] directory e [!DNL libs/flashaccess] .

   1. Modificare il [!DNL converter.properties] file in modo che punti al server LiveCycle ES.
   1. Eseguire `ant -f build-migration.xml migrate-all-1.0-policies` per convertire tutti i criteri DRM FMRMS 1.0 in formato DRM Primetime.

      Per effettuare la migrazione da FMRMS 1.5 a Primetime DRM, vedere il `V1_5PolicyConverter.java` campione.

   1. Compilate il codice di esempio eseguendo `ant-f build-migration.xml build-1.5-converter` lo script, che prevede che le librerie 1.5 e 3.0 si trovino nelle [!DNL libs/1.5] directory e [!DNL libs/flashaccess] .

   1. Modificare il [!DNL converter.properties] file in modo che punti al server LiveCycle ES.
   1. Eseguire `ant -f build-migration.xml migrate-all-1.5-policies` per convertire tutti i criteri DRM FMRMS 1.5 in formato DRM Primetime.

      I criteri DRM convertiti vengono salvati come set di file. Viene `DRM PolicyConverter` generato un file in formato CSV che include la mappatura degli ID dei criteri DRM obsoleti ai nuovi ID dei criteri DRM. Potete importare questo file nella [!DNL PolicyConversion] tabella del database di implementazione di riferimento, dove viene utilizzato da `RefImplMetadataConvReqHandler`.

1. Supportate le richieste di compatibilità 1.x con le `FMRMSv1RequestHandler` proprietà e `FMRMSv1MetadataHandler` :

   1. Dopo la migrazione dei dati rilevanti a un server basato su DRM di Primetime, implementa il supporto per le richieste di compatibilità 1.x.

      Per esempi su come elaborare questi tipi di richieste, vedete `RefImplUpgradeV1ClientHandler` e `RefImplMetadataConvReqHandler` nell&#39;implementazione di riferimento.

