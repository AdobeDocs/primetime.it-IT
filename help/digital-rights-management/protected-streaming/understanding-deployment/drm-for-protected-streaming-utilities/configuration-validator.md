---
description: Adobe consiglia di eseguire l'utility Configuration Validator se si apportano modifiche nel file di configurazione prima di avviare il server. Questa utility è in grado di rilevare la maggior parte degli errori di configurazione in anticipo, prima che questi causino errori durante l'elaborazione della richiesta.
seo-description: Adobe consiglia di eseguire l'utility Configuration Validator se si apportano modifiche nel file di configurazione prima di avviare il server. Questa utility è in grado di rilevare la maggior parte degli errori di configurazione in anticipo, prima che questi causino errori durante l'elaborazione della richiesta.
seo-title: Convalida della configurazione
title: Convalida della configurazione
uuid: 7b44919a-0319-4675-95e2-ad1ad72ec0cb
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Convalida della configurazione{#configuration-validator}

Adobe consiglia di eseguire l&#39;utility Configuration Validator se si apportano modifiche nel file di configurazione prima di avviare il server. Questa utility è in grado di rilevare la maggior parte degli errori di configurazione in anticipo, prima che questi causino errori durante l&#39;elaborazione della richiesta.

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

Per ogni file di configurazione del server licenze, la Convalida può eseguire una convalida basata su file, che assicura che il file XML sia ben formato e conforme allo schema del file di configurazione.

Per eseguire la convalida basata su file sul file di configurazione globale, digitare:

```
Validator --<file path>/flashaccess-global.xml --global
```

Per eseguire la convalida basata su file sul file di configurazione del tenant, digitare:

```
Validator --<file path>/flashaccess-tenant.xml --tenant
```

La funzione Convalida può inoltre eseguire una convalida basata sulla distribuzione. Oltre a verificare la conformità con lo schema, questo livello di convalida verifica anche la validità dei valori specificati. Ad esempio, garantisce l&#39;esistenza di file di riferimento.

La convalida basata sulla distribuzione può essere eseguita ai seguenti livelli:

* `Tenant` — Convalida il file di configurazione e le credenziali per un tenant specifico. Se si desidera convalidare la configurazione per `<tenant1>`, digitare:

   ```
       Validator --<root-path-to-LicenseServer.ConfigRoot> -d flashaccessserver/tenant1 -t
   ```

* `Global` — Convalida il file di configurazione globale e la convalida del tenant per tutti i tenant. Se si desidera eseguire una convalida globale basata sulla distribuzione, digitare:

   ```
       Validator --<root-path-to-LicenseServer.ConfigRoot> -g
   ```

