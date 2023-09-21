---
title: Migrazione da FMRMS 1.0 o 1.5 ad Adobe Access 2.0 e versioni successive
description: Migrazione da FMRMS 1.0 o 1.5 ad Adobe Access 2.0 e versioni successive
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# Migrazione da FMRMS 1.0 o 1.5 ad Adobe Access 2.0 e versioni successive {#migrating-from-fmrms-or-to-adobe-access-and-above}

Per continuare a rilasciare licenze per i contenuti inseriti in pacchetti utilizzando Flash Media Rights Management Server (FMRMS) 1.0 o 1.5, è necessario eseguire la migrazione dei dati delle licenze e dei criteri dal server ES di LiveCycle al nuovo server del cliente in base all&#39;SDK di accesso Adobe. I passaggi importanti sono i seguenti:

1. Importazione delle informazioni sulla licenza
1. Conversione di criteri FMRMS in formato Adobe Access
1. Supporto delle richieste di compatibilità 1.x tramite `FMRMSv1RequestHandler` e `FMRMSv1MetadataHandler`

Per importare le informazioni sulla licenza dal LiveCycle ES nel server basato su Access di Adobe, fare riferimento agli script di database di esempio forniti in [!DNL Reference Implementation\Server\migration\db] cartella. Vengono forniti script di esempio per esportare i dati rilevanti da un database MySQL, Oracle o SQL Server in un formato CSV. Una volta esportati, i dati possono essere importati nel database desiderato. Le informazioni sulla licenza esportata includono l’ID licenza, un ID contenuto assegnato al momento della creazione del pacchetto, l’ID del criterio utilizzato, l’ora in cui il contenuto è stato creato in pacchetto e la chiave di crittografia del contenuto. Ad Adobe Access, queste informazioni sono necessarie per convertire i metadati di contenuto 1.x nel formato di metadati di Access Adobe (consulta `FMRMSv1RequestHandler` e `FMRMSv1MetadataHandler`). Nell’implementazione di riferimento, questi dati vengono memorizzati nella tabella del database delle licenze e utilizzati da `RefImplMetadataConvReqHandler`.

I criteri esistenti dovranno essere convertiti nel formato di accesso Adobe per poter utilizzare tali criteri durante la conversione dei metadati e il rilascio di licenze per contenuti 1.0 o 1.5. La cartella Reference Implementation\Server\migration contiene un codice di esempio per la creazione di un criterio di accesso di Adobe basato su criteri precedenti.

Se si esegue la migrazione da FMRMS 1.0 ad Adobe Access, vedere l&#39;esempio V1_0PolicyConverter.java. Compila il codice di esempio eseguendo &quot; `ant-f build-migration.xml build-1.0-converter`&quot;(lo script prevede che le librerie di accesso 1.0 e Adobe siano in [!DNL libs/1.0] e libs/flashaccess rispettivamente). Modificare il file converter.properties in modo che punti al server ES del LiveCycle. Quindi esegui &quot; `ant -f build-migration.xml migrate-all-1.0-policies`&quot; per convertire tutti i criteri FMRMS 1.0 nel formato di accesso Adobe.

Per la migrazione da FMRMS 1.5 ad Adobe Access, vedere l&#39;esempio V1_5PolicyConverter.java. Compila il codice di esempio eseguendo &quot; `ant-f build-migration.xml build-1.5-converter`&quot;(lo script prevede che le librerie 1.5 e 3.0 siano rispettivamente in libs/1.5 e libs/flashaccess). Modificare il file converter.properties in modo che punti al server ES del LiveCycle. Quindi esegui &quot; `ant -f build-migration.xml migrate-all-1.5-policies`&quot; per convertire tutti i criteri FMRMS 1.5 nel formato di accesso Adobe.

I criteri convertiti verranno scritti in un set di file. PolicyConverter genera inoltre un file CSV contenente la mappatura dei vecchi ID policy ai nuovi ID policy. Questo file può essere importato nella tabella &quot;PolicyConversion&quot; nel database di implementazione di riferimento e verrà utilizzato da `RefImplMetadataConvReqHandler`.

Una volta effettuata la migrazione dei dati rilevanti al server Adobe basato sull’accesso, puoi implementare il supporto per le richieste di compatibilità 1.x. Consulta `RefImplUpgradeV1ClientHandler` e `RefImplMetadataConvReqHandler` nell’implementazione di riferimento per esempi su come elaborare questi tipi di richieste.
