---
title: Accesso a Single Sign-On (SSO) per Android SDK Enabler su Android 10 app
description: Accesso a Single Sign-On (SSO) per Android SDK Enabler su Android 10 app
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---



# Accesso a Single Sign-On (SSO) per Android SDK Enabler su Android 10 app {#access-enabler-android-sdk-single-sign-on-sso-on-android-10-apps}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Panoramica

Il Single Sign-On (SSO) tra le app basate sull&#39;autenticazione Adobe Primetime è disponibile sui dispositivi che utilizzano il sistema operativo Android tramite Access Enabler Android SDK. Per poter offrire Single Sign-On (SSO) sui dispositivi Android, Access Enabler Android SDK versione 3.2.1 (più recente) e versioni precedenti utilizza un file di database condiviso salvato in un&#39;implementazione di archiviazione Android, accessibile da tutte le app basate sull&#39;autenticazione Adobe Primetime.

Tuttavia, Google nell&#39;ultima versione di Android 10 ha prodotto alcune modifiche &quot;per dare agli utenti un maggiore controllo sui loro file e per limitare il disordine dei file, le app che puntano ad Android 10 (livello API 29) e superiore sono dati accesso con ambito in un dispositivo di archiviazione esterno, o archiviazione con ambito, per impostazione predefinita. Tali app possono vedere solo la loro directory specifica dell&#39;app `\[...\]`&quot;. Maggiori dettagli relativi a queste modifiche all&#39;archiviazione Android 10 sono presentati in [Documentazione sull&#39;archiviazione dei dati e dei file per Android](https://developer.android.com/training/data-storage/files/external-scoped).

A seguito di queste modifiche, l&#39;SSO (Single Sign-On) offerto dalla versione Android di Access Enabler **3.2.1 SDK (più recente)** Le versioni precedenti e possono essere influenzate sui dispositivi Android 10 come spiegato nella sezione successiva.

Vedi [Panoramica di Roku SSO](/help/authentication/roku-sso-overview.md).

## Comportamento

A seconda delle **livello SDK di target** o l&#39;uso di **android:requestLegacyExternalStorage** l&#39;attributo manifest del Single Sign-On (SSO) offerto da Access Enabler Android versione 3.2.1 SDK (più recente) e versioni precedenti si comporta attualmente come segue:

- Le tue destinazioni app **Android 9 (livello API 28)** o inferiore **-\>** Single Sign-On (SSO) **lavorerà**
- Le tue destinazioni app **Android 10** **(livello API 29)** e fa **set** il valore **requestLegacyExternalStorage su true** nel file manifesto dell&#39;app **-\>** Single Sign-On (SSO) **lavorerà**
- Le tue destinazioni app **Android 10** **(livello API 29)** e fa **non impostato** il valore **requestLegacyExternalStorage su true** nel file manifesto dell&#39;app **-\>** Single Sign-On (SSO) **non funzionerà**


>[!TIP]
>
> Prima che l&#39;SDK Android di Access Enabler per l&#39;autenticazione di Adobe Primetime sia completamente compatibile con l&#39;archiviazione con ambito, puoi temporaneamente rinunciare in base al livello SDK di destinazione dell&#39;app o all&#39;attributo manifesto requestLegacyExternalStorage, come spiegato in pubblico [Documentazione Android](https://developer.android.com/training/data-storage/files/external-scoped#opt-out-of-scoped-storage).

