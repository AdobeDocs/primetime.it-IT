---
description: I file di registro generati dal server DRM di Adobe Primetime per l'applicazione di streaming protetto si trovano nella directory specificata da LicenseServer.LogRoot.
title: File di registro
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# File di registro{#log-files}

I file di registro generati dal server DRM di Adobe Primetime per l&#39;applicazione di streaming protetto si trovano nella directory specificata da LicenseServer.LogRoot.

>[!NOTE]
>
>Se i file di registro correnti vengono eliminati o spostati durante l&#39;esecuzione del server, il file di registro potrebbe non essere ricreato. Pertanto alcune informazioni di log possono essere eliminate.

## Struttura della directory dei log {#section_F490A483D60145ADBC21038914C39203}

Le directory dei log sono strutturate per facilità d&#39;uso. La directory di log ha la seguente struttura:

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

Il file di registro globale `flashaccess-global.log` si trova in *LicenseServer.LogRoot*. Il registro può includere messaggi di registro che l’SDK Java DRM di Adobe Primetime o i messaggi di registro potrebbero aver generato durante il momento in cui il server è stato inizializzato.

## File di registro delle partizioni {#section_5660137CD6AA40519E72A4315534846B}

Il file di registro della partizione `flashaccess-partition.log` si trova nella directory `<LicenseServer.LogRoot>/flashaccesserver`. Include i messaggi di registro generati durante l’elaborazione di una richiesta di licenza.

## File di registro tenant {#section_F0257CC0831647F18A746B4F02E3E910}

Il file di registro tenant di ciascun tenant, `flashaccess-tenant.log`, si trova in `<LicenseServer.LogRoot>/flashaccesserver/tenants/<tenantname>`. Il registro tenant include informazioni di controllo che descrivono ogni licenza generata per questo tenant.
