---
title: Autenticazione Adobe Primetime (facoltativa)
description: Autenticazione Adobe Primetime (facoltativa)
copied-description: true
exl-id: 59fbbefa-0c84-474a-ace9-141b50ad5f5f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# Autenticazione Adobe Primetime (facoltativa) {#adobe-primetime-authentication-optional}

Se il criterio DRM utilizzato per creare il pacchetto del contenuto è un criterio anonimo, verrà rilasciata una licenza a tutte le richieste di licenza. Facoltativamente, Primetime Cloud DRM supporta anche l’autenticazione tramite Adobe Primetime. Se questa funzione è abilitata, non verrà rilasciata una licenza a meno che il dispositivo client non abbia acquisito un token di autenticazione Primetime e lo abbia impostato localmente tramite l’API client appropriata ( `setAuthenticationToken`) per l&#39;impostazione di token di autenticazione personalizzati. Per ulteriori informazioni sull’integrazione dell’autenticazione Primetime nel flusso di lavoro di autenticazione, consulta: [Autenticazione di Adobe Primetime.](https://tve.helpdocsonline.com/home)

Durante l&#39;acquisizione della licenza, se il criterio DRM indica che è necessaria l&#39;autenticazione Pri metime, il server licenze analizza e convalida il token multimediale breve dell&#39;autenticazione Primetime. Se il criterio DRM specifica un `ResourceID` o `RequestorID`, anche il server licenze convaliderà il token in base a queste proprietà. Se non sono impostate, il server licenze specificherà le proprietà come &quot;null&quot; durante la convalida del token. Solo se la convalida del token ha esito positivo, verrà rilasciata una licenza; in caso contrario, il client invierà un DRMErrorEvent 3328 con un codice di errore secondario 305 (Utente non autorizzato).

I parametri di autenticazione Primetime devono essere specificati nel criterio utilizzato per creare il pacchetto del contenuto destinato a richiedere l’autenticazione Primetime.

Le proprietà pertinenti sono:

```
#policy.customProp.1=adobePass.required=<TRUE or FALSE> 
#policy.customProp.1=adobePass.requestorID=<Requestor ID String> 
#policy.customProp.1=adobePass.resourceID=<Resource ID String>
```

>[!NOTE]
>
>Quando utilizzi l’autenticazione Primetime in combinazione con la funzione di rotazione delle licenze (DRM), tieni presente che l’autenticazione Primetime Short Media Token (SMT) ha una data di validità breve. Se l’applicazione prevede di utilizzare la rotazione delle licenze (ad esempio, per supportare *Sospensioni attività* caso d’uso), l’applicazione deve esserne consapevole e aggiornare il Short Media Token di autenticazione Primetime prima di ruotare la licenza.
