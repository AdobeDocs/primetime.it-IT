---
seo-title: Autenticazione Adobe Primetime (facoltativo)
title: Autenticazione Adobe Primetime (facoltativo)
uuid: fa6225d6-e0e5-4fcc-ac26-4ff54f9f334a
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# Autenticazione Adobe Primetime (facoltativo) {#adobe-primetime-authentication-optional}

Se il criterio DRM utilizzato per creare il pacchetto del contenuto è un criterio anonimo, verrà rilasciata una licenza a tutte le richieste di licenza. Facoltativamente, Primetime Cloud DRM supporta anche l&#39;autenticazione tramite l&#39;autenticazione Adobe Primetime. Se questa funzione è abilitata, non verrà rilasciata una licenza a meno che il dispositivo client non abbia acquisito per la prima volta un Token di autenticazione Primetime e lo abbia impostato localmente tramite l&#39;API client appropriata ( `setAuthenticationToken`) per l&#39;impostazione dei token di autenticazione personalizzati. Per ulteriori informazioni sull&#39;integrazione dell&#39;autenticazione Primetime nel flusso di lavoro di autenticazione, fare riferimento a: Autenticazione [Adobe Primetime.](https://tve.helpdocsonline.com/home)

Durante l&#39;acquisizione della licenza, se il criterio DRM stabilisce che è necessaria l&#39;autenticazione Pri metime, il server licenze analizzerà e convalida il token multimediale breve dell&#39;autenticazione Primetime. Se il criterio DRM specifica una `ResourceID` o `RequestorID`, il server licenze convalida anche il token rispetto a tali proprietà. Se non sono impostati, il server licenze specifica le proprietà come &quot;null&quot; durante la convalida del token. Solo in caso di esito positivo della convalida del token sarà rilasciata una licenza; in caso contrario, il client invierà un codice di errore secondario 3328 DRMErrorEvent con un codice di errore 305 (Utente non autorizzato).

I parametri di autenticazione Primetime devono essere specificati nel criterio utilizzato per creare il pacchetto del contenuto destinato a richiedere l&#39;autenticazione Primetime.

Le proprietà pertinenti sono:

```
#policy.customProp.1=adobePass.required=<TRUE or FALSE> 
#policy.customProp.1=adobePass.requestorID=<Requestor ID String> 
#policy.customProp.1=adobePass.resourceID=<Resource ID String>
```

>[!NOTE]
>
>Quando si utilizza l&#39;autenticazione Primetime insieme alla funzione di rotazione della licenza (DRM), tenere presente che l&#39;autenticazione Primetime Short Media Token (SMT) ha una data di validità breve. Se l&#39;applicazione prevede di utilizzare la rotazione della licenza (ad esempio, per supportare il caso d&#39;uso *Blackout* ), l&#39;applicazione deve esserne a conoscenza e aggiornare il token multimediale breve per l&#39;autenticazione Primetime prima di ruotare la licenza.