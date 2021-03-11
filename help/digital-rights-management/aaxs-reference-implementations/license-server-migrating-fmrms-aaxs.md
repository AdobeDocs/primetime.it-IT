---
title: Migrazione da FMRMS 1.0 o 1.5 ad Adobe Access 2.0 e versioni successive
description: Migrazione da FMRMS 1.0 o 1.5 ad Adobe Access 2.0 e versioni successive
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---


# Migrazione da FMRMS 1.0 o 1.5 ad Adobe Access 2.0 e versioni successive {#migrating-from-fmrms-or-to-adobe-access-and-above}

Per continuare a rilasciare licenze per i contenuti in pacchetto utilizzando Flash Media Rights Management Server (FMRMS) 1.0 o 1.5, i dati delle licenze e dei criteri devono essere migrati dal server ES di LiveCycle al nuovo server del cliente in base all&#39;SDK di Adobe Access. I passaggi importanti sono i seguenti:

1. Importazione delle informazioni sulla licenza
1. Conversione dei criteri FMRMS in formato di accesso Adobe
1. Supporto delle richieste di compatibilità 1.x tramite `FMRMSv1RequestHandler` e `FMRMSv1MetadataHandler`

Per importare le informazioni sulla licenza dal LiveCycle ES nel server basato su Access di Adobe, fare riferimento agli script di database di esempio forniti nella cartella [!DNL Reference Implementation\Server\migration\db]. Vengono forniti script di esempio per l&#39;esportazione dei dati pertinenti da un database MySQL, Oracle o SQL Server in un formato di file CSV. Una volta esportati, i dati possono essere importati nel database desiderato. Le informazioni sulla licenza esportata includono l’ID licenza, un ID contenuto assegnato al momento della creazione del pacchetto, l’ID del criterio utilizzato, l’ora in cui il contenuto è stato compilato e la chiave di crittografia del contenuto. Ad Adobe Access, queste informazioni sono necessarie per convertire i metadati del contenuto 1.x nel formato dei metadati di accesso Adobe (vedi `FMRMSv1RequestHandler` e `FMRMSv1MetadataHandler`). Nell’implementazione di riferimento, questi dati vengono memorizzati nella tabella del database delle licenze e utilizzati da `RefImplMetadataConvReqHandler`.

I criteri esistenti dovranno essere convertiti nel formato Adobe Access per poter utilizzare tali criteri durante la conversione dei metadati e il rilascio delle licenze per contenuti 1.0 o 1.5. Il Riferimento Implementation\Server\migration folder contains sample code for creating an Adobe Access policy based on older policies.

Se stai eseguendo la migrazione da FMRMS 1.0 a Adobe Access, consulta l’esempio V1_0PolicyConverter.java . Compila il codice di esempio eseguendo &quot; `ant-f build-migration.xml build-1.0-converter`&quot; (lo script prevede che le librerie di accesso 1.0 e Adobe si trovino rispettivamente in [!DNL libs/1.0] e libs/flashaccess). Modifica il file converter.properties per puntare al server ES del tuo LiveCycle. Quindi esegui &quot; `ant -f build-migration.xml migrate-all-1.0-policies`&quot; per convertire tutti i criteri FMRMS 1.0 in formato Adobe Access.

Se stai eseguendo la migrazione da FMRMS 1.5 a Adobe Access, consulta l’esempio V1_5PolicyConverter.java . Compila il codice di esempio eseguendo &quot; `ant-f build-migration.xml build-1.5-converter`&quot; (lo script prevede che le librerie 1.5 e 3.0 siano rispettivamente in libs/1.5 e libs/flashaccess). Modifica il file converter.properties per puntare al server ES del tuo LiveCycle. Quindi esegui &quot; `ant -f build-migration.xml migrate-all-1.5-policies`&quot; per convertire tutti i criteri FMRMS 1.5 in formato Adobe Access.

I criteri convertiti verranno scritti in un set di file. Inoltre, PolicyConverter genera un file CSV contenente la mappatura degli ID dei criteri obsoleti su nuovi ID dei criteri. Questo file può essere importato nella tabella &quot;PolicyConversion&quot; nel database di implementazione di riferimento e verrà utilizzato da `RefImplMetadataConvReqHandler`.

Dopo la migrazione dei dati rilevanti al server basato su Access di Adobe, puoi implementare il supporto per le richieste di compatibilità 1.x. Per esempi su come elaborare questi tipi di richieste, consulta `RefImplUpgradeV1ClientHandler` e `RefImplMetadataConvReqHandler` nell’implementazione di riferimento .
