---
description: I file di registro generati dal server DRM  Adobe Primetime per l'applicazione di streaming protetto si trovano nella directory specificata da LicenseServer.LogRoot.
seo-description: I file di registro generati dal server DRM  Adobe Primetime per l'applicazione di streaming protetto si trovano nella directory specificata da LicenseServer.LogRoot.
seo-title: File di registro
title: File di registro
uuid: 4498fe60-65af-4f99-8f9b-e85013d0c9e9
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# File di registro{#log-files}

I file di registro generati dal server DRM  Adobe Primetime per l&#39;applicazione di streaming protetto si trovano nella directory specificata da LicenseServer.LogRoot.

>[!NOTE]
>
>Se i file di registro correnti vengono eliminati o spostati durante l&#39;esecuzione del server, il file di registro potrebbe non essere ricreato. È pertanto possibile eliminare alcune informazioni di registro.

## Struttura directory di registro {#section_F490A483D60145ADBC21038914C39203}

Le directory di registro sono strutturate per semplificare l&#39;utilizzo. La directory di registro ha la struttura seguente:

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

Il file di registro globale, `flashaccess-global.log`, si trova in *LicenseServer.LogRoot*. Il registro può includere messaggi di registro che l&#39;SDK Java  Adobe Primetime DRM o i messaggi di registro possono aver generato durante il momento in cui il server è stato inizializzato.

## File di registro delle partizioni {#section_5660137CD6AA40519E72A4315534846B}

Il file di registro della partizione, `flashaccess-partition.log`, si trova nella directory `<LicenseServer.LogRoot>/flashaccesserver`. Include i messaggi di registro generati durante l&#39;elaborazione di una richiesta di licenza.

## File di registro tenant {#section_F0257CC0831647F18A746B4F02E3E910}

Il file di registro del tenant di ciascun tenant, `flashaccess-tenant.log`, si trova in `<LicenseServer.LogRoot>/flashaccesserver/tenants/<tenantname>`. Il registro tenant include informazioni di controllo che descrivono ogni licenza generata per questo tenant.
