---
description: L'Adobe consiglia di eseguire l'utilità Convalida configurazione prima di avviare il server se si apportano modifiche al file di configurazione. Questa utility può rilevare la maggior parte degli errori di configurazione in anticipo, prima che causino errori durante l’elaborazione delle richieste.
title: Convalida configurazione
exl-id: 41d0a926-4e12-442c-886e-5f12cf10eed8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Convalida configurazione{#configuration-validator}

L&#39;Adobe consiglia di eseguire l&#39;utilità Convalida configurazione prima di avviare il server se si apportano modifiche al file di configurazione. Questa utility può rilevare la maggior parte degli errori di configurazione in anticipo, prima che causino errori durante l’elaborazione delle richieste.

Per eseguire la convalida, digitare:

```
Validator.bat  
<i class="+ topic ph hi-d="" i "="">
  options  
</i class="+ topic>
```

o

```
java -jar libs/flashaccess-validator.jar  
<i class="+ topic ph hi-d="" i "="">
  options 
</i class="+ topic>
```

Per ciascuno dei file di configurazione del server licenze, Validator può eseguire la convalida basata su file, in modo da garantire che il file XML sia ben formato e conforme allo schema del file di configurazione.

Per eseguire la convalida basata su file sul file di configurazione globale, digitare:

```
Validator --<file path>/flashaccess-global.xml --global
```

Per eseguire la convalida basata su file sul file di configurazione tenant, digitare:

```
Validator --<file path>/flashaccess-tenant.xml --tenant
```

La convalida può inoltre eseguire la convalida basata sulla distribuzione. Oltre a verificare la conformità allo schema, questo livello di convalida verifica anche la validità dei valori specificati. Ad esempio, assicura che esistano i file di riferimento.

La convalida basata sulla distribuzione può essere eseguita ai seguenti livelli:

* `Tenant` — convalida il file di configurazione e le credenziali per un tenant specifico. Se desideri convalidare la configurazione per `<tenant1>`, tipo:

   ```
       Validator --<root-path-to-LicenseServer.ConfigRoot> -d flashaccessserver/tenant1 -t
   ```

* `Global` — convalida il file di configurazione globale e la convalida del tenant per tutti i tenant. Se si desidera eseguire la convalida globale basata sulla distribuzione, digitare:

   ```
       Validator --<root-path-to-LicenseServer.ConfigRoot> -g
   ```
