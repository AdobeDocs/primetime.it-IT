---
description: 'Adobe Access Server for Protected Streaming richiede due tipi di file di configurazione: un file di configurazione globale (flashaccess-global.xml) e un file di configurazione tenant per ogni tenant (flashaccess-tenant.xml).'
title: Struttura directory di configurazione
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# File di configurazione del server licenze e struttura della directory di configurazione {#configuration-directory-structure}

Adobe Access Server for Protected Streaming richiede due tipi di file di configurazione: un file di configurazione globale (flashaccess-global.xml) e un file di configurazione tenant per ogni tenant (flashaccess-tenant.xml).

Dopo aver modificato i file di configurazione, Adobe consiglia di utilizzare le utility fornite con Adobe Access Server for Protected Streaming per verificare che i file siano ben formati. Per ulteriori informazioni, consulta la sezione &quot;[Convalida configurazione](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)&quot;.

Per evitare di rendere disponibili le password in testo non crittografato nei file di configurazione, tutte le password specificate nei file di configurazione globale e tenant devono essere crittografate. Per ulteriori informazioni sulla crittografia delle password, vedere &quot;[Scrambler password](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/password-scrambler.md)&quot;.

Le directory di configurazione hanno la seguente struttura:

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
