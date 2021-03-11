---
description: L'Adobe consiglia di eseguire l'utility Configuration Validator se si apportano modifiche al file di configurazione prima di avviare il server. Questa utility è in grado di rilevare la maggior parte degli errori di configurazione in anticipo, prima che essi causino errori durante l'elaborazione della richiesta.
title: Convalida della configurazione
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# Convalida della configurazione{#configuration-validator}

L&#39;Adobe consiglia di eseguire l&#39;utility Configuration Validator se si apportano modifiche al file di configurazione prima di avviare il server. Questa utility è in grado di rilevare la maggior parte degli errori di configurazione in anticipo, prima che essi causino errori durante l&#39;elaborazione della richiesta.

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

Per ciascuno dei file di configurazione del server di licenza, il Convalida può eseguire una convalida basata su file, che assicura che il file XML sia ben formato e conforme allo schema del file di configurazione.

Per eseguire la convalida basata su file sul file di configurazione globale, digitare:

```
Validator --<file path>/flashaccess-global.xml --global
```

Per eseguire la convalida basata su file sul file di configurazione del tenant, digitare:

```
Validator --<file path>/flashaccess-tenant.xml --tenant
```

La convalida può inoltre eseguire una convalida basata sulla distribuzione. Oltre a verificare la conformità allo schema, questo livello di convalida verifica anche la validità dei valori specificati. Ad esempio, garantisce l’esistenza di file di riferimento.

La convalida basata sulla distribuzione può essere eseguita ai seguenti livelli:

* `Tenant` — convalida il file di configurazione e le credenziali per un tenant specifico. Se desideri convalidare la configurazione per `<tenant1>`, digita:

   ```
       Validator --<root-path-to-LicenseServer.ConfigRoot> -d flashaccessserver/tenant1 -t
   ```

* `Global` — convalida il file di configurazione globale e la convalida tenant per tutti gli tenant. Se si desidera eseguire una convalida globale basata sulla distribuzione, digitare:

   ```
       Validator --<root-path-to-LicenseServer.ConfigRoot> -g
   ```

