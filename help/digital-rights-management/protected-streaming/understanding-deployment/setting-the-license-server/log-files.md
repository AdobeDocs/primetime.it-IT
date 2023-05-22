---
description: I file di registro generati dall'applicazione Adobe Primetime DRM Server for Protected Streaming si trovano nella directory specificata da LicenseServer.LogRoot.
title: File di registro
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# File di registro{#log-files}

I file di registro generati dall&#39;applicazione Adobe Primetime DRM Server for Protected Streaming si trovano nella directory specificata da LicenseServer.LogRoot.

>[!NOTE]
>
>Se i file di registro correnti vengono eliminati o spostati durante l&#39;esecuzione del server, è possibile che il file di registro non venga ricreato. Di conseguenza, alcune informazioni del registro potrebbero essere eliminate.

## Struttura della directory di registro {#section_F490A483D60145ADBC21038914C39203}

Le directory dei registri sono strutturate in modo da semplificarne l’utilizzo. La directory di registro ha la seguente struttura:

```
<i class="+ topic ph hi-d="" i "="">
 LicenseServer.LogRoot/ 
 flashaccess-global.log 
     flashaccessserver/ 
         flashaccess-partition.log 
         tenants/ 
             
 <i class="+ topic ph hi-d="" i "="">
  tenantname/ 
                  flashaccess-tenant.log
 </i class="+ topic>
</i class="+ topic>
```

## File di registro globale {#section_1CFA90748142439C9F3BE380969539DA}

Il file di registro globale, `flashaccess-global.log`, si trova in *LicenseServer.LogRoot*. Il registro può includere messaggi di registro generati dall’SDK Java di Adobe Primetime DRM o messaggi di registro durante il periodo di inizializzazione del server.

## File di registro della partizione {#section_5660137CD6AA40519E72A4315534846B}

Il file di registro della partizione, `flashaccess-partition.log`, si trova in `<LicenseServer.LogRoot>/flashaccesserver` directory. Include i messaggi di registro generati durante l’elaborazione di una richiesta di licenza.

## File di registro tenant {#section_F0257CC0831647F18A746B4F02E3E910}

File di registro tenant di ogni tenant, `flashaccess-tenant.log`, si trova in `<LicenseServer.LogRoot>/flashaccesserver/tenants/<tenantname>`. Il registro tenant include informazioni di audit che descrivono ogni licenza generata per questo tenant.
