---
title: Autenticazione Adobe Primetime (facoltativo)
description: Autenticazione Adobe Primetime (facoltativo)
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---


# Autenticazione Adobe Primetime (facoltativo) {#adobe-primetime-authentication-optional}

Se il criterio DRM utilizzato per creare il pacchetto del contenuto è un criterio anonimo, verrà rilasciata una licenza a tutte le richieste di licenza. Facoltativamente, Primetime Cloud DRM supporta anche l’autenticazione tramite l’autenticazione Adobe Primetime. Se questa funzione è abilitata, non verrà rilasciata una licenza a meno che il dispositivo client non abbia acquisito per la prima volta un Token di autenticazione Primetime e lo abbia impostato localmente tramite l’API client appropriata ( `setAuthenticationToken`) per l’impostazione dei token di autenticazione personalizzati. Per ulteriori informazioni sull’integrazione dell’autenticazione Primetime nel flusso di lavoro di autenticazione, consulta: [Autenticazione Adobe Primetime.](https://tve.helpdocsonline.com/home)

Durante l&#39;acquisizione della licenza, se la politica DRM stabilisce che è necessaria l&#39;autenticazione metime Pri, il server di licenza analizzerà e convaliderà il Token multimediale breve di Primetime Authentication. Se il criterio DRM specifica un valore `ResourceID` o `RequestorID`, il server licenze convalida anche il token rispetto a queste proprietà. Se non sono impostati, il server licenze specificherà le proprietà come &quot;null&quot; durante la convalida del token. Solo in caso di esito positivo della convalida del token sarà rilasciata una licenza; in caso contrario, il client invierà un 3328 DRMErrorEvent con un codice di errore secondario 305 (Utente non autorizzato).

I parametri di autenticazione di Primetime devono essere specificati nel criterio utilizzato per creare un pacchetto del contenuto destinato a richiedere l’autenticazione di Primetime.

Le proprietà pertinenti sono:

```
#policy.customProp.1=adobePass.required=<TRUE or FALSE> 
#policy.customProp.1=adobePass.requestorID=<Requestor ID String> 
#policy.customProp.1=adobePass.resourceID=<Resource ID String>
```

>[!NOTE]
>
>Quando utilizzi l’autenticazione Primetime insieme alla funzione di rotazione delle licenze (DRM), tieni presente che l’autenticazione di Primetime Short Media Token (SMT) ha una breve data di validità. Se la tua applicazione prevede di utilizzare la funzione Rotazione licenza (ad esempio, per supportare il *Blackouts*, l&#39;applicazione deve esserne a conoscenza e aggiornare il relativo Token multimediale breve di Primetime Authentication prima di ruotare la licenza.