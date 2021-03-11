---
description: Per continuare a rilasciare licenze per contenuti che sono stati assemblati con Flash Media Rights Management Server (FMRMS) 1.0 o 1.5, è necessario migrare i dati delle licenze e dei criteri DRM dal server ES di LiveCycle al nuovo server del cliente basato sull'SDK Adobe Primetime DRM.
title: Migrare da FMRMS 1.0 o 1.5 a Adobe Primetime DRM 2.0 o versione successiva
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---


# Migrare da FMRMS 1.0 o 1.5 a Adobe Primetime DRM 2.0 o successivo{#migrate-from-fmrms-or-to-adobe-primetime-drm-or-later}

Per continuare a rilasciare licenze per contenuti che sono stati assemblati con Flash Media Rights Management Server (FMRMS) 1.0 o 1.5, è necessario migrare i dati delle licenze e dei criteri DRM dal server ES di LiveCycle al nuovo server del cliente basato sull&#39;SDK Adobe Primetime DRM.

Per eseguire la migrazione, completa le seguenti attività:

1. Informazioni sulla licenza di importazione:

   1. Per importare le informazioni sulla licenza dal LiveCycle ES al server basato su DRM di Primetime, vedere gli script di database di esempio nella cartella [!DNL Reference Implementation\Server\migration\db].
   1. Eseguire gli script di esempio per esportare i dati rilevanti da un database MySQL, Oracle o SQL Server in un formato di file CSV.
   1. Dopo aver esportato i dati dal LiveCycle ES, importali nel database.

      Le informazioni sulla licenza esportata comprendono:

      * ID licenza
      * Un ID contenuto assegnato al momento della creazione del pacchetto
      * ID del criterio DRM applicato
      * L&#39;ora in cui il contenuto è stato compilato
      * Chiave di crittografia del contenuto

      Queste informazioni sono necessarie prima di poter convertire i metadati del contenuto 1.x nel formato di metadati DRM di Primetime. Nell’implementazione di riferimento, questi dati vengono memorizzati nella tabella del database delle Licenze e vengono utilizzati da `RefImplMetadataConvReqHandler`. Per ulteriori informazioni, vedere `FMRMSv1RequestHandler` e `FMRMSv1MetadataHandler`.


1. Convertire i criteri FMRMS nel formato DRM di Primetime:

   1. Prima di poter applicare i criteri DRM per convertire i metadati e rilasciare licenze per i contenuti versione 1.0 o 1.5, convertire i criteri DRM esistenti in formato Primetime DRM.

      La cartella `Reference Implementation\Server\migration` include un codice di esempio per creare un criterio DRM di Primetime basato su vecchi criteri DRM. Per migrare da FMRMS 1.0 a DRM di Primetime , vedi il campione `V1_0PolicyConverter.java` .
   1. Compila il codice di esempio eseguendo lo script `ant-f build-migration.xml build-1.0-converter` che cerca le librerie DRM 1.0 e Primetime nelle directory [!DNL libs/1.0] e [!DNL libs/flashaccess].

   1. Modifica il file [!DNL converter.properties] in modo che indirizzi al server ES del tuo LiveCycle.
   1. Esegui `ant -f build-migration.xml migrate-all-1.0-policies` per convertire tutti i criteri DRM FMRMS 1.0 in formato DRM Primetime.

      Per eseguire la migrazione da FMRMS 1.5 a Primetime DRM , vedi il campione `V1_5PolicyConverter.java` .

   1. Compila il codice di esempio eseguendo lo script `ant-f build-migration.xml build-1.5-converter` , che prevede che le librerie 1.5 e 3.0 si trovino nelle directory [!DNL libs/1.5] e [!DNL libs/flashaccess].

   1. Modifica il file [!DNL converter.properties] in modo che indirizzi al server ES del tuo LiveCycle.
   1. Esegui `ant -f build-migration.xml migrate-all-1.5-policies` per convertire tutti i criteri DRM FMRMS 1.5 in formato DRM Primetime.

      I criteri DRM convertiti vengono salvati come set di file. Il `DRM PolicyConverter` genera un file in formato CSV che include la mappatura dei vecchi ID dei criteri DRM ai nuovi ID dei criteri DRM. Puoi importare questo file nella tabella [!DNL PolicyConversion] nel database di implementazione di riferimento, dove viene utilizzato da `RefImplMetadataConvReqHandler`.

1. Supporta le richieste di compatibilità 1.x con le proprietà `FMRMSv1RequestHandler` e `FMRMSv1MetadataHandler` :

   1. Dopo la migrazione dei dati rilevanti a un server basato su DRM di Primetime, implementa il supporto per le richieste di compatibilità 1.x.

      Per esempi su come elaborare questi tipi di richieste, consulta `RefImplUpgradeV1ClientHandler` e `RefImplMetadataConvReqHandler` nell’implementazione di riferimento.

