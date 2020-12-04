---
seo-title: Migrazione da FMRMS 1.0 o 1.5 a  accesso al Adobe 2.0 e versioni successive
title: Migrazione da FMRMS 1.0 o 1.5 a  accesso al Adobe 2.0 e versioni successive
uuid: 05caeb39-0c62-4053-87a9-8e89030a188d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---


# Migrazione da FMRMS 1.0 o 1.5 a  accesso al Adobe 2.0 e superiore {#migrating-from-fmrms-or-to-adobe-access-and-above}

Per continuare a rilasciare licenze per il contenuto incluso nel pacchetto utilizzando Flash Media Rights Management Server (FMRMS) 1.0 o 1.5, i dati di licenza e criteri devono essere migrati dal server LiveCycle ES al nuovo server del cliente in base all&#39;SDK  accesso al Adobe. I passi importanti sono:

1. Importazione delle informazioni sulla licenza
1. Conversione dei criteri FMRMS in formato di accesso  Adobe
1. Supporto delle richieste di compatibilità 1.x tramite `FMRMSv1RequestHandler` e `FMRMSv1MetadataHandler`

Per importare informazioni sulla licenza dal LiveCycle ES nel server basato su Access del Adobe , fare riferimento agli script di database di esempio forniti nella cartella [!DNL Reference Implementation\Server\migration\db]. Sono disponibili script di esempio per esportare i dati rilevanti da un database MySQL,  Oracle o SQL Server in un formato di file CSV. Una volta esportati, i dati possono essere importati nel database desiderato. Le informazioni sulla licenza esportata includono l&#39;ID licenza, un ID contenuto assegnato al momento della creazione del pacchetto, l&#39;ID del criterio utilizzato, l&#39;ora in cui è stato creato il pacchetto del contenuto e la chiave di crittografia del contenuto. Per  Accesso Adobe, queste informazioni sono necessarie per convertire i metadati di contenuto 1.x nel formato di metadati Accesso Adobe  (vedere `FMRMSv1RequestHandler` e `FMRMSv1MetadataHandler`). Nell&#39;implementazione di riferimento, questi dati vengono memorizzati nella tabella del database delle licenze e utilizzati da `RefImplMetadataConvReqHandler`.

I criteri esistenti dovranno essere convertiti nel formato di accesso al Adobe  per poter utilizzare tali criteri al momento della conversione dei metadati e del rilascio delle licenze per i contenuti 1.0 o 1.5. Il Riferimento Implementation\Server\migration folder contains sample code for creating an Adobe Access policy based on older policies.

Se state eseguendo la migrazione da FMRMS 1.0 a  accesso al Adobe, consultate l&#39;esempio V1_0PolicyConverter.java. Compilare il codice di esempio eseguendo &quot; `ant-f build-migration.xml build-1.0-converter`&quot; (lo script prevede che le librerie di accesso ai Adobi 1.0 e  siano rispettivamente in [!DNL libs/1.0] e libs/flashaccess). Modificate il file converter.properties per indirizzarlo al server ES del LiveCycle. Quindi, eseguite &quot; `ant -f build-migration.xml migrate-all-1.0-policies`&quot; per convertire tutti i criteri FMRMS 1.0 in  formato di accesso al Adobe.

Se state eseguendo la migrazione da FMRMS 1.5 a  accesso al Adobe, consultate l&#39;esempio V1_5PolicyConverter.java. Compilare il codice di esempio eseguendo &quot; `ant-f build-migration.xml build-1.5-converter`&quot; (lo script prevede che le librerie 1.5 e 3.0 siano rispettivamente in libs/1.5 e libs/flashaccess). Modificate il file converter.properties per indirizzarlo al server ES del LiveCycle. Quindi, eseguite &quot; `ant -f build-migration.xml migrate-all-1.5-policies`&quot; per convertire tutti i criteri FMRMS 1.5 in  formato di accesso al Adobe.

I criteri convertiti verranno scritti in un set di file. Inoltre, PolicyConverter restituirà un file CSV contenente la mappatura degli ID dei criteri obsoleti ai nuovi ID dei criteri. Questo file può essere importato nella tabella &quot;PolicyConversion&quot; nel database di implementazione di riferimento e verrà utilizzato da `RefImplMetadataConvReqHandler`.

Una volta che i dati pertinenti sono stati migrati nel server basato su Access del Adobe , è possibile implementare il supporto per le richieste di compatibilità 1.x. Per esempi sull&#39;elaborazione di questi tipi di richieste, vedete `RefImplUpgradeV1ClientHandler` e `RefImplMetadataConvReqHandler` nell&#39;implementazione di riferimento.
