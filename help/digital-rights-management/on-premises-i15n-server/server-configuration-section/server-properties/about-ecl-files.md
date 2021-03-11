---
title: Informazioni sui file ECI
description: Informazioni sui file ECI
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---


# Informazioni sui file ECI{#about-eci-files}

Oltre ai CRL, è inoltre necessario aggiornare periodicamente i file di Interfaccia comune incorporata (ECI). Ogni volta che Adobe aggiunge il supporto per una nuova piattaforma client DRM Primetime (ad esempio: iOS, Android, Windows Flash Player, ecc.), viene creato un nuovo record ECI. Per supportare l’individualizzazione di questo client, è necessario che sul server di Individualization sia presente un record ECI corrispondente.

Poiché il rilascio dei nuovi client DRM di Primetime non è molto frequente, Adobe rilascerà i dati ECI aggiornati in base alle esigenze. Periodicamente, Adobe raccoglierà i file ECI e li ospiterà nella posizione seguente per la distribuzione:

```
http://cdmdownload.adobe.com/indiv/onprem/eci/Latest.txt
```

Il file [!DNL Latest.txt] conterrà l’URL del file di distribuzione CRL più recente.

L’Adobe crea il file zip ECI nel modo descritto di seguito:

Struttura della cartella:

```
ECI\*
```

Il contenuto della cartella viene compresso in modo ricorsivo:

```
zip -R ECI ECI.zip
```

Viene calcolato un digest SHA-256 OpenSSL del file zip:

```
openssl dgst -sha256 -hex ECI.zip
```

Il file zip verrà rinominato in modo da contenere la data di archiviazione e il digest SHA-256:

```
Rename ECI.zip to <DATE_SHA-256>.zip
```

Ad esempio:

```
20150310_aea45bf06241f04fba2b310ff9a8066c6aba73c8d22387b60509481e9cefc43e.zip
```

Controlla periodicamente la posizione di cui sopra per i file ECI aggiornati.

Esegui il seguente processo per l&#39;installazione dopo il download:

1. Osserva il digest SHA-256 e ricalcolalo utilizzando OpenSSL o uno strumento equivalente.
1. Confrontarlo con quello specificato nel nome del file.
1. Rinomina il file in [!DNL ECI.zip].
1. Decomprimere la directory [!DNL ECI].
1. Sostituisci la vecchia directory ECI con quella nuova.
1. Riavvia il server Individualization.

