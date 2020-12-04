---
seo-title: Convalida della configurazione
title: Convalida della configurazione
uuid: 60ebd35c-290a-4f08-9bd0-178903857149
translation-type: tm+mt
source-git-commit: 47b2ed65ff0ea4f54a210cf7627ed535782296b9
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---


# Convalida della configurazione {#configuration-validator}

 Adobe consiglia di eseguire l&#39;utility Configuration Validator prima di avviare il server ogni volta che vengono apportate modifiche al file di configurazione. Questa utility è in grado di rilevare la maggior parte degli errori di configurazione in anticipo, prima che questi causino errori durante l&#39;elaborazione della richiesta.

Per eseguire la convalida, utilizzare il comando:

```
Validator.bat options  
```

o il comando:

```
java -jar libs/flashaccess-validator.jar options 
```

Per ogni file di configurazione del server licenze, la Convalida può eseguire una convalida basata su file, che assicura che il file XML sia ben formato e conforme allo schema del file di configurazione. Per eseguire la convalida basata su file sul file di configurazione globale, eseguire il comando:

```
Validator --file path/flashaccess-global.xml --global
```

Per eseguire una convalida basata su file sul file di configurazione del tenant, eseguire il comando:

```
Validator --file path/flashaccess-tenant.xml --tenant
```

La convalida può anche eseguire una convalida basata sulla distribuzione; oltre a verificare la conformità con lo schema, questo livello di convalida verifica anche la validità dei valori specificati (ad esempio, garantisce l&#39;esistenza di file di riferimento). La convalida basata sulla distribuzione può essere eseguita a due livelli:

* Tenant — Convalida il file di configurazione e le credenziali per un tenant specifico. Per convalidare la configurazione per &quot;tenant1&quot;, eseguire il comando:

```
Validator --root-path-to-LicenseServer.ConfigRoot -d flashaccessserver/tenant1 -t 
```

* Globale — Convalida il file di configurazione globale e la convalida del tenant per tutti i tenant. Per eseguire la convalida globale basata sulla distribuzione, eseguire il comando:

```
Validator --root-path-to-LicenseServer.ConfigRoot -g 
```

