---
description: 'Adobe Access Server per lo streaming protetto richiede due tipi di file di configurazione: un file di configurazione globale (flashaccess-global.xml) e un file di configurazione tenant per ciascun tenant (flashaccess-tenant.xml).'
seo-description: 'Adobe Access Server per lo streaming protetto richiede due tipi di file di configurazione: un file di configurazione globale (flashaccess-global.xml) e un file di configurazione tenant per ciascun tenant (flashaccess-tenant.xml).'
seo-title: Struttura directory di configurazione
title: Struttura directory di configurazione
uuid: c6cfc734-6b7c-4502-9bdb-c7aaca156e0e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---


# File di configurazione del server licenze e struttura della directory di configurazione {#configuration-directory-structure}

Adobe Access Server per lo streaming protetto richiede due tipi di file di configurazione: un file di configurazione globale (flashaccess-global.xml) e un file di configurazione tenant per ciascun tenant (flashaccess-tenant.xml).

Dopo aver modificato i file di configurazione,  Adobe consiglia di utilizzare le utility fornite con Adobe Access Server per lo streaming protetto per verificare che i file siano ben formati. Per ulteriori informazioni, vedere &quot;[Convalida della configurazione](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)&quot;.

Per evitare di rendere le password disponibili in testo chiaro nei file di configurazione, tutte le password specificate nei file di configurazione globali e tenant devono essere crittografate. Per ulteriori informazioni sulla cifratura delle password, vedere &quot;[Password Scrambler](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/password-scrambler.md)&quot;.

Le directory di configurazione hanno la struttura seguente:

```
<i class="+ topic ph hi-d="" i "="">
  LicenseServer.ConfigRoot/  
  flashaccess-global.xml  
  pkcs11.cfg (optional)  
  flashaccessserver/  
   libs/ (optional)  
   tenants/  
     
 <i class="+ topic ph hi-d="" i "="">
   tenantname/  
      flashaccess-tenant.xml  
       
  <i class="+ topic ph hi-d="" i "="">
    credential.pfx (optional)  
        
   <i class="+ topic ph hi-d="" i "="">
     packagercert.cer (optional) 
   </i class="+ topic> 
  </i class="+ topic> 
 </i class="+ topic> 
</i class="+ topic>
```

