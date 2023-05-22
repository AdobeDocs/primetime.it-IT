---
title: Informazioni sui file ECI
description: Informazioni sui file ECI
copied-description: true
exl-id: ac452897-3c64-4481-a3b7-4b69ef6edb61
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# Informazioni sui file ECI{#about-eci-files}

Oltre ai CRL, è necessario aggiornare periodicamente i file ECI (Embedded Common Interface). Ogni volta che Adobe aggiunge il supporto per una nuova piattaforma client DRM Primetime (ad esempio: iOS, Android, Windows FlashPlayer, ecc.), viene creato un nuovo record ECI. Per supportare l’individualizzazione di questo client, è necessario che sul server di personalizzazione sia presente un record ECI corrispondente.

Poiché il rilascio di nuovi client DRM di Primetime non è molto frequente, Adobe rilascerà dati ECI aggiornati in base alle necessità. Periodicamente, Adobe raccoglierà i file ECI e li ospiterà nella posizione seguente per la distribuzione:

```
http://cdmdownload.adobe.com/indiv/onprem/eci/Latest.txt
```

Il [!DNL Latest.txt] Il file conterrà l&#39;URL del file di distribuzione CRL più recente.

Adobe creerà il file zip ECI nel modo descritto di seguito:

Struttura cartella:

```
ECI\*
```

Il contenuto della cartella verrà compresso in modo ricorsivo:

```
zip -R ECI ECI.zip
```

Verrà calcolato un digest OpenSSL SHA-256 del file zip:

```
openssl dgst -sha256 -hex ECI.zip
```

Il file zip verrà rinominato per contenere la data di archivio e il digest SHA-256:

```
Rename ECI.zip to <DATE_SHA-256>.zip
```

Ad esempio:

```
20150310_aea45bf06241f04fba2b310ff9a8066c6aba73c8d22387b60509481e9cefc43e.zip
```

Controllate periodicamente la posizione qui sopra per trovare i file ECI aggiornati.

Dopo il download, eseguire la seguente procedura di installazione:

1. Prendi nota del digest SHA-256 e ricalcolalo utilizzando OpenSSL o uno strumento equivalente.
1. Confrontalo con quello specificato nel nome del file.
1. Rinomina il file in [!DNL ECI.zip].
1. Decomprimi il [!DNL ECI] directory.
1. Sostituire il vecchio elenco ECI con quello nuovo.
1. Riavviare il server di personalizzazione.
