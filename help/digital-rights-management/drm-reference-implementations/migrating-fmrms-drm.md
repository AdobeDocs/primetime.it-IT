---
description: Per continuare a rilasciare licenze per i contenuti che sono stati inclusi nel pacchetto con Flash Media Rights Management Server (FMRMS) 1.0 o 1.5, è necessario migrare i dati relativi alle licenze e ai criteri DRM dal server ES di LiveCycle al nuovo server del cliente basato sull'SDK Adobe Primetime DRM.
title: Migrazione da FMRMS 1.0 o 1.5 a Adobe Primetime DRM 2.0 o versione successiva
exl-id: 6490f2ad-4863-4b41-9ebd-1de47da4250b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# Migrazione da FMRMS 1.0 o 1.5 a Adobe Primetime DRM 2.0 o versione successiva{#migrate-from-fmrms-or-to-adobe-primetime-drm-or-later}

Per continuare a rilasciare licenze per i contenuti che sono stati inclusi nel pacchetto con Flash Media Rights Management Server (FMRMS) 1.0 o 1.5, è necessario migrare i dati relativi alle licenze e ai criteri DRM dal server ES di LiveCycle al nuovo server del cliente basato sull&#39;SDK Adobe Primetime DRM.

Per eseguire la migrazione, completa le seguenti attività:

1. Informazioni sulla licenza di importazione:

   1. Per importare le informazioni sulla licenza dal LiveCycle ES al server basato su DRM Primetime, vedere gli script di database di esempio in [!DNL Reference Implementation\Server\migration\db] cartella.
   1. Eseguire gli script di esempio per esportare i dati rilevanti da un database MySQL, Oracle o SQL Server in un formato CSV.
   1. Dopo aver esportato i dati dal LiveCycle ES, importarli nel database.

      Le informazioni sulla licenza esportata includono quanto segue:

      * Un ID licenza
      * Un ID contenuto assegnato al momento della creazione del pacchetto
      * ID del criterio DRM applicato
      * Ora di creazione del pacchetto del contenuto
      * Chiave di crittografia del contenuto

      Queste informazioni sono necessarie prima di poter convertire i metadati di contenuto 1.x nel formato di metadati DRM di Primetime. Nell’implementazione di riferimento, questi dati vengono memorizzati nella tabella del database delle licenze e utilizzati da `RefImplMetadataConvReqHandler`. Per ulteriori informazioni, consulta `FMRMSv1RequestHandler` e `FMRMSv1MetadataHandler`.


1. Converti i criteri FMRMS nel formato DRM di Primetime:

   1. Prima di poter applicare i criteri DRM per convertire i metadati e rilasciare le licenze per il contenuto della versione 1.0 o 1.5, convertire i criteri DRM esistenti nel formato DRM di Primetime.

      Il `Reference Implementation\Server\migration` La cartella include un codice di esempio per creare un criterio DRM di Primetime basato su criteri DRM precedenti. Per migrare da FMRMS 1.0 a Primetime DRM, vedere `V1_0PolicyConverter.java` esempio.
   1. Compila il codice di esempio eseguendo `ant-f build-migration.xml build-1.0-converter` , che cerca le librerie DRM 1.0 e Primetime in [!DNL libs/1.0] e [!DNL libs/flashaccess] directory.

   1. Modifica il [!DNL converter.properties] per puntare al server ES del LiveCycle.
   1. Esegui `ant -f build-migration.xml migrate-all-1.0-policies` per convertire tutti i criteri FMRMS 1.0 DRM nel formato DRM Primetime.

      Per migrare da FMRMS 1.5 a Primetime DRM, vedere `V1_5PolicyConverter.java` esempio.

   1. Compila il codice di esempio eseguendo `ant-f build-migration.xml build-1.5-converter` script, che prevede che le librerie 1.5 e 3.0 siano nel [!DNL libs/1.5] e [!DNL libs/flashaccess] directory.

   1. Modifica il [!DNL converter.properties] per puntare al server ES del LiveCycle.
   1. Esegui `ant -f build-migration.xml migrate-all-1.5-policies` per convertire tutti i criteri FMRMS 1.5 DRM nel formato DRM Primetime.

      I criteri DRM convertiti vengono salvati come un set di file. Il `DRM PolicyConverter` genera un file in formato CSV che include la mappatura degli ID dei criteri DRM precedenti ai nuovi ID dei criteri DRM. Puoi importare questo file in [!DNL PolicyConversion] nel database di implementazione di riferimento, dove viene utilizzato da `RefImplMetadataConvReqHandler`.

1. Supporta le richieste di compatibilità 1.x con `FMRMSv1RequestHandler` e `FMRMSv1MetadataHandler` proprietà:

   1. Dopo la migrazione dei dati rilevanti a un server basato su DRM di Primetime, implementare il supporto per le richieste di compatibilità 1.x.

      Per esempi su come elaborare questi tipi di richieste, consulta `RefImplUpgradeV1ClientHandler` e `RefImplMetadataConvReqHandler` nell’implementazione di riferimento.
