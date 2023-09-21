---
description: Adobe fornisce un servizio Cloud DRM ai clienti di Adobe Primetime DRM che non desiderano sviluppare e mantenere il proprio server di licenze DRM Primetime. Grazie a questo servizio, i clienti possono ridurre la complessità operativa e di sviluppo legata al rilascio delle licenze DRM. Primetime Cloud DRM può rilasciare licenze DRM a tutti i dispositivi in grado di eseguire un’applicazione video abilitata per Primetime Browser TVSDK, come iOS, Android, Desktops e Xbox360. Questo servizio DRM è ospitato e gestito da Adobe, con un tempo di attività 24 ore su 24, 7 giorni su 7.
title: Sfondo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# Sfondo {#background}

Adobe fornisce un servizio Cloud DRM ai clienti di Adobe Primetime DRM che non desiderano sviluppare e mantenere il proprio server di licenze DRM Primetime. Grazie a questo servizio, i clienti possono ridurre la complessità operativa e di sviluppo legata al rilascio delle licenze DRM. Primetime Cloud DRM può rilasciare licenze DRM a tutti i dispositivi in grado di eseguire un’applicazione video abilitata per Primetime Browser TVSDK, come iOS, Android, Desktops e Xbox360. Questo servizio DRM è ospitato e gestito da Adobe, con un tempo di attività 24 ore su 24, 7 giorni su 7.

>[!NOTE]
>
>Adobe Primetime DRM era precedentemente denominato Adobe Access e, prima di questo, Flash Access.

## Cosa è incluso con Primetime Cloud DRM {#section_788D0DD5F6DB41678FD87CFBD21B25FD}

* Modulo di autenticazione/adesione personalizzato e istruzioni su come attivare l’autenticazione personalizzata per il contenuto. Per ulteriori informazioni, consulta [!DNL Custom Authentication Entitlement] directory.
* Certificato server licenze specifico per DRM cloud ( [!DNL .pem/.cer/.der])

* Certificato di trasporto del server licenze specifico per DRM cloud ( [!DNL .pem/.cer/.der])

* Primetime Java Offline Packager
* Criteri DRM di esempio per la creazione di pacchetti

   * **policy_24hr** - Licenze memorizzate su disco per 24 ore. Dopo 24 ore, è necessario acquisire una nuova licenza per visualizzare il contenuto. Anche tutti gli altri criteri di questo kit dispongono di memorizzazione nella cache delle licenze 24 ore.
   * **policy_ios_remotekeyserver** - Sui dispositivi iOS, la licenza DRM verrà acquisita da Cloud DRM. Inoltre, il client acquisirà tutte le chiavi di decrittografia AES da Cloud DRM. La riproduzione non è consentita sui dispositivi iOS jailbroken.

   * **policy_ios_localkeyserver** - Sui dispositivi iOS, la licenza DRM verrà acquisita da Cloud DRM. Inoltre, il client acquisirà tutte le chiavi di decrittografia AES HLS da un server HTTP locale, anziché da Cloud DRM. La riproduzione non è consentita sui dispositivi iOS jailbroken.

   * **policy_adobePass** : il client deve prima autenticarsi con (precedentemente denominato Adobe Pass) altrimenti la licenza verrà negata.

* Strumento Adobe Policy Manager per la creazione di ulteriori criteri DRM
* Contenuto video di esempio da utilizzare per la creazione di pacchetti
