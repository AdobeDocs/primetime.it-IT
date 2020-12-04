---
description: Per continuare a rilasciare licenze per contenuti che sono stati inclusi in pacchetti con Flash Media Rights Management Server (FMRMS) 1.0 o 1.5, è necessario migrare i dati delle licenze e dei criteri DRM dal server LiveCycle ES al nuovo server del cliente basato sull'SDK Adobe Primetime DRM.
seo-description: Per continuare a rilasciare licenze per contenuti che sono stati inclusi in pacchetti con Flash Media Rights Management Server (FMRMS) 1.0 o 1.5, è necessario migrare i dati delle licenze e dei criteri DRM dal server LiveCycle ES al nuovo server del cliente basato sull'SDK Adobe Primetime DRM.
seo-title: Migrazione da FMRMS 1.0 o 1.5 a  Adobe Primetime DRM 2.0 o versione successiva
title: Migrazione da FMRMS 1.0 o 1.5 a  Adobe Primetime DRM 2.0 o versione successiva
uuid: 49ecbbd2-d83b-4bf2-841e-c3f9e5d5e141
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---


# Migrazione da FMRMS 1.0 o 1.5 a  Adobe Primetime DRM 2.0 o versione successiva{#migrate-from-fmrms-or-to-adobe-primetime-drm-or-later}

Per continuare a rilasciare licenze per contenuti che sono stati inclusi in pacchetti con Flash Media Rights Management Server (FMRMS) 1.0 o 1.5, è necessario migrare i dati delle licenze e dei criteri DRM dal server LiveCycle ES al nuovo server del cliente basato sull&#39;SDK Adobe Primetime DRM.

Per eseguire la migrazione, completare le seguenti attività:

1. Informazioni sulle licenze di importazione:

   1. Per importare informazioni sulla licenza dal LiveCycle ES al server basato su DRM di Primetime, vedere gli script di database di esempio nella cartella [!DNL Reference Implementation\Server\migration\db].
   1. Eseguite gli script di esempio per esportare i dati rilevanti da un database MySQL,  Oracle o SQL Server in un formato di file CSV.
   1. Dopo aver esportato i dati dal LiveCycle ES, importateli nel database.

      Le informazioni sulla licenza esportata includono quanto segue:

      * ID licenza
      * Un ID contenuto assegnato al momento della creazione del pacchetto
      * ID del criterio DRM applicato
      * L&#39;ora in cui è stato creato il pacchetto del contenuto
      * La chiave di crittografia del contenuto

      Queste informazioni sono necessarie prima di poter convertire i metadati del contenuto 1.x nel formato di metadati DRM di Primetime. Nell&#39;implementazione di riferimento, questi dati vengono memorizzati nella tabella del database delle licenze e utilizzati da `RefImplMetadataConvReqHandler`. Per ulteriori informazioni, vedere `FMRMSv1RequestHandler` e `FMRMSv1MetadataHandler`.


1. Conversione dei criteri FMRMS nel formato DRM di Primetime:

   1. Prima di poter applicare i criteri DRM per convertire i metadati e rilasciare licenze per i contenuti della versione 1.0 o 1.5, convertite i criteri DRM esistenti nel formato DRM di Primetime.

      La cartella `Reference Implementation\Server\migration` include il codice di esempio per creare un criterio DRM Primetime basato su criteri DRM meno recenti. Per effettuare la migrazione da FMRMS 1.0 a DRM di Primetime, vedere l&#39;esempio `V1_0PolicyConverter.java`.
   1. Compilare il codice di esempio eseguendo lo script `ant-f build-migration.xml build-1.0-converter`, che cerca le librerie DRM 1.0 e Primetime nelle directory [!DNL libs/1.0] e [!DNL libs/flashaccess].

   1. Modificate il file [!DNL converter.properties] in modo che punti al server ES del LiveCycle.
   1. Eseguire `ant -f build-migration.xml migrate-all-1.0-policies` per convertire tutti i criteri DRM FMRMS 1.0 in formato DRM Primetime.

      Per effettuare la migrazione da FMRMS 1.5 a Primetime DRM, vedere l&#39;esempio `V1_5PolicyConverter.java`.

   1. Compilare il codice di esempio eseguendo lo script `ant-f build-migration.xml build-1.5-converter`, che prevede che le librerie 1.5 e 3.0 si trovino nelle directory [!DNL libs/1.5] e [!DNL libs/flashaccess].

   1. Modificate il file [!DNL converter.properties] in modo che punti al server ES del LiveCycle.
   1. Eseguire `ant -f build-migration.xml migrate-all-1.5-policies` per convertire tutti i criteri DRM FMRMS 1.5 in formato DRM Primetime.

      I criteri DRM convertiti vengono salvati come set di file. Il file `DRM PolicyConverter` genera un file in formato CSV che include la mappatura dei vecchi ID dei criteri DRM ai nuovi ID dei criteri DRM. Potete importare questo file nella tabella [!DNL PolicyConversion] del database di implementazione di riferimento, dove viene utilizzato da `RefImplMetadataConvReqHandler`.

1. Supportare le richieste di compatibilità 1.x con le proprietà `FMRMSv1RequestHandler` e `FMRMSv1MetadataHandler`:

   1. Dopo la migrazione dei dati rilevanti a un server basato su DRM di Primetime, implementa il supporto per le richieste di compatibilità 1.x.

      Per esempi su come elaborare questi tipi di richieste, vedere `RefImplUpgradeV1ClientHandler` e `RefImplMetadataConvReqHandler` nell&#39;implementazione di riferimento.

