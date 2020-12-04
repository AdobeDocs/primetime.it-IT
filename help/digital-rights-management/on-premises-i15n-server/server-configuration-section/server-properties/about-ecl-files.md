---
seo-title: Informazioni sui file ECI
title: Informazioni sui file ECI
uuid: 124d8ab1-933b-4a1b-992a-919f3d799460
translation-type: tm+mt
source-git-commit: d8e4c39c297d69b154baf0b4d67cf09b5cf0a9d4
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---


# Informazioni su file ECI{#about-eci-files}

Oltre ai CRL, è inoltre necessario aggiornare periodicamente i file dell&#39;interfaccia comune incorporata (ECI). Ogni volta che  Adobe aggiunge il supporto per una nuova piattaforma client Primetime DRM (ad esempio: iOS, Android, Windows Flash Player, ecc.), viene creato un nuovo record ECI. Per supportare l&#39;individualizzazione di questo client, è necessario che sul server di individuazione sia presente un record ECI corrispondente.

Poiché il rilascio di nuovi client Primetime DRM non è molto frequente,  Adobe rilascerà i dati ECI aggiornati in base alle esigenze. Periodicamente,  Adobe raccoglierà i file ECI e li ospiterà nella posizione seguente per la distribuzione:

```
http://cdmdownload.adobe.com/indiv/onprem/eci/Latest.txt
```

Il file [!DNL Latest.txt] conterrà l&#39;URL del file di distribuzione CRL più recente.

 Adobe creerà il file zip ECI nel modo descritto di seguito:

Struttura cartella:

```
ECI\*
```

Il contenuto della cartella verrà compresso in modo ricorsivo:

```
zip -R ECI ECI.zip
```

Viene calcolato un digest OpenSSL SHA-256 del file zip:

```
openssl dgst -sha256 -hex ECI.zip
```

Il file zip verrà rinominato in modo da contenere la data di archiviazione e il riassunto SHA-256:

```
Rename ECI.zip to <DATE_SHA-256>.zip
```

Ad esempio:

```
20150310_aea45bf06241f04fba2b310ff9a8066c6aba73c8d22387b60509481e9cefc43e.zip
```

Controllate periodicamente la posizione indicata sopra per i file ECI aggiornati.

Eseguire il seguente processo per l&#39;installazione dopo il download:

1. Osservate il riassunto SHA-256 e ricalcolatelo utilizzando OpenSSL o uno strumento equivalente.
1. Confrontarlo con quello specificato nel nome del file.
1. Rinominare il file in [!DNL ECI.zip].
1. Decomprimete la directory [!DNL ECI].
1. Sostituire la vecchia directory ECI con quella nuova.
1. Riavviate il server di individuazione.

