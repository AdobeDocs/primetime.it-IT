---
title: Convalida configurazione
description: Convalida configurazione
copied-description: true
exl-id: 9b73e107-6ab7-4089-b415-0af8c9f86995
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# Convalida configurazione {#configuration-validator}

L&#39;Adobe consiglia di eseguire l&#39;utilità Convalida configurazione prima di avviare il server ogni volta che vengono apportate modifiche al file di configurazione. Questa utility può rilevare la maggior parte degli errori di configurazione in anticipo, prima che causino errori durante l’elaborazione delle richieste.

Per eseguire la convalida, utilizzare il comando:

```
Validator.bat options  
```

oppure il comando:

```
java -jar libs/flashaccess-validator.jar options 
```

Per ciascuno dei file di configurazione del server licenze, Validator può eseguire la convalida basata su file, che garantisce che il file XML sia ben formato e conforme allo schema del file di configurazione. Per eseguire la convalida basata su file sul file di configurazione globale, eseguire il comando:

```
Validator --file path/flashaccess-global.xml --global
```

Per eseguire la convalida basata su file sul file di configurazione tenant, eseguire il comando:

```
Validator --file path/flashaccess-tenant.xml --tenant
```

La convalida può anche eseguire la convalida basata sulla distribuzione; oltre a verificare la conformità con lo schema, questo livello di convalida controlla anche la validità dei valori specificati (ad esempio, garantisce l&#39;esistenza dei file di riferimento). La convalida basata sulla distribuzione può essere eseguita a due livelli:

* Tenant: convalida il file di configurazione e le credenziali per un tenant specifico. Per convalidare la configurazione per &quot;tenant1&quot;, esegui il comando:

```
Validator --root-path-to-LicenseServer.ConfigRoot -d flashaccessserver/tenant1 -t 
```

* Globale — convalida il file di configurazione globale e la convalida del tenant per tutti i tenant. Per eseguire la convalida globale basata sulla distribuzione, eseguire il comando:

```
Validator --root-path-to-LicenseServer.ConfigRoot -g 
```
