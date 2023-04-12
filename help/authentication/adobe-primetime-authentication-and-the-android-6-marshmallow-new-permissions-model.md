---
title: Autenticazione Adobe Primetime e il nuovo modello di autorizzazioni "Marshmallow" per Android 6
description: Autenticazione Adobe Primetime e il nuovo modello di autorizzazioni "Marshmallow" per Android 6
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---



# Autenticazione Adobe Primetime e il nuovo modello di autorizzazioni &quot;Marshmallow&quot; per Android 6 {#adobe-primetime-authentication-and-the-android-6-marshmallow-new-permissions-model}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

</br>

La nuova versione di Android 6 Marshmallow introduce alcuni aggiornamenti al modello di autorizzazioni, che possono influenzare il comportamento delle app che utilizzano l&#39;SDK di autenticazione Adobe Primetime esistente versione 1.8 e precedenti. 

Come nuova funzione, il nuovo sistema operativo Android offre [controllo granulare sulle autorizzazioni richieste dalle app al momento dell&#39;installazione e in fase di runtime](https://developer.android.com/about/versions/marshmallow/android-6.0-changes.html).

>[!IMPORTANT]
>
>Le modifiche descritte di seguito **influisce solo sulle applicazioni sviluppate specificamente per Android 6.0** (targetSdkVersion=23). Non influiscono sulle applicazioni meno recenti già installate sul dispositivo dell&#39;utente durante l&#39;aggiornamento ad Android 6.0. 


In particolare, per le app sviluppate in Android Studio utilizzando [Livello API 23](http://developer.android.com/sdk/api_diff/23/changes.html) e che utilizzano l’SDK per l’autenticazione di Adobe Primetime, lo sviluppatore dovrà scrivere un codice personalizzato (vedi lo snippet di codice qui sotto) [per attivare la finestra di dialogo consenti/nega autorizzazioni](https://developer.android.com/training/permissions/requesting.html). 

Di seguito è riportato l&#39;estratto di codice utilizzato per richiedere l&#39;accesso in scrittura all&#39;archiviazione esterna del dispositivo:

```java
// Here, thisActivity is the current activity
if (ContextCompat.checkSelfPermission(thisActivity,
                Manifest.permission.WRITE_EXTERNAL_STORAGE)
        != PackageManager.WRITE_EXTERNAL_STORAGE) {

    // Should we show an explanation?
    if (ActivityCompat.shouldShowRequestPermissionRationale(thisActivity,
            Manifest.permission.WRITE_EXTERNAL_STORAGE)) {

        // Show an expanation to the user *asynchronously* -- don't block
        // this thread waiting for the user's response! After the user
        // sees the explanation, try again to request the permission.

    } else {

        // No explanation needed, we can request the permission.

        ActivityCompat.requestPermissions(thisActivity,
                new String[]{Manifest.permission.WRITE_EXTERNAL_STORAGE},
                MY_PERMISSIONS_REQUEST_WRITE_EXTERNAL_STORAGE);

        // MY_PERMISSIONS_REQUEST_WRITE_EXTERNAL_STORAGE is an
        // app-defined int constant. The callback method gets the
        // result of the request.
    }
}
```




**Dal punto di vista degli utenti**, al momento dell’installazione, gli utenti vengono accolti da una finestra che richiede loro di confermare le autorizzazioni di lettura/scrittura per i file (vedi la figura 2 di seguito). Questo porta a uno dei due risultati seguenti:

1. Se l&#39;utente **conferma** le autorizzazioni, il flusso regolare di autenticazione sarà mantenuto e i token saranno memorizzati nell&#39;archiviazione globale. Gli utenti rimarranno autenticati nell’app e tra le app utilizzando l’autenticazione Adobe Primetime per tutto il tempo in cui i token sono validi.
1. Se l&#39;utente **negazione** le autorizzazioni, le azioni di scrittura nell&#39;archivio avranno esito negativo e gli utenti saranno autenticati solo fino a quando non usciranno dall&#39;app. Tieni presente che alcune applicazioni vengono reinizializzate quando si passa da un primo piano all’altro in background, in modo che gli utenti vengano disconnessi durante l’esecuzione di questa azione. I token NON sono memorizzati e gli utenti dovranno eseguire l’autenticazione ogni volta che utilizzano l’app. 


>[!TIP]
>
>È in fase di sviluppo una funzione che introduce la resilienza dello storage per l’SDK 1.9 per l’autenticazione di Adobe Primetime. Il nuovo SDK è destinato a **rilascio nell’ultima settimana di ottobre**. L&#39;applicazione si basa sulla scrittura nell&#39;archivio sandbox dell&#39;applicazione ogni volta che non è possibile utilizzare l&#39;archiviazione generale. Questo riguarda il caso in cui, per le applicazioni sviluppate nel livello API 23, gli utenti NON accettano le autorizzazioni di lettura/scrittura nell&#39;archiviazione globale. I token vengono memorizzati singolarmente per app, il che significa che il Single-Sign-On tra le app che utilizzano l’autenticazione Adobe Primetime verrà disattivato.


![](assets/android-permissions-request.png)

*Figura: Finestra di dialogo di richiesta delle autorizzazioni per le app scritte con targeting API livello 23*

>[!IMPORTANT]
>
> Consigli Adobi **i suoi partner per sviluppare app utilizzando API di livello 22 (targetSdkVersion=22) o versioni precedenti al fine di garantire la migliore esperienza utente possibile nel processo di autenticazione**. 
