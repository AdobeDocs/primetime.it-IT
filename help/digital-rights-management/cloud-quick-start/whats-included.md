---
description: Adobe fornisce un servizio Cloud DRM ai clienti Adobe Primetime DRM che non desiderano sviluppare e mantenere il proprio server licenze Primetime DRM. Utilizzando questo servizio, i clienti possono ridurre la complessità operativa e di sviluppo rispetto al rilascio della licenza DRM. Primetime Cloud DRM può rilasciare licenze DRM a tutti i dispositivi in grado di eseguire un'applicazione video abilitata per TVSDK del browser Primetime, come iOS, Android, Desktop e Xbox360. Questo servizio DRM è ospitato e gestito da Adobe, con tempi di attività 24/7.
title: Sfondo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# Sfondo {#background}

Adobe fornisce un servizio Cloud DRM ai clienti Adobe Primetime DRM che non desiderano sviluppare e mantenere il proprio server licenze Primetime DRM. Utilizzando questo servizio, i clienti possono ridurre la complessità operativa e di sviluppo rispetto al rilascio della licenza DRM. Primetime Cloud DRM può rilasciare licenze DRM a tutti i dispositivi in grado di eseguire un&#39;applicazione video abilitata per TVSDK del browser Primetime, come iOS, Android, Desktop e Xbox360. Questo servizio DRM è ospitato e gestito da Adobe, con tempi di attività 24/7.

>[!NOTE]
>
>Adobe Primetime DRM era precedentemente denominato accesso Adobe e prima di tale Flash Access.

## Cosa è incluso con Primetime Cloud DRM {#section_788D0DD5F6DB41678FD87CFBD21B25FD}

* Modulo di autenticazione/adesione personalizzato e istruzioni su come interagire con l’autenticazione personalizzata per i contenuti. Per ulteriori informazioni, consulta la directory [!DNL Custom Authentication Entitlement] .
* Certificato del server licenze specifico per DRM cloud ( [!DNL .pem/.cer/.der])

* Certificato di trasporto del server licenze specifico per DRM cloud ( [!DNL .pem/.cer/.der])

* Pacchetto offline Java di Primetime
* Criteri DRM di esempio per il pacchetto

   * **policy_24hr**  - Licenza cache su disco per 24 ore. Dopo 24 ore, è necessario acquisire una nuova licenza per visualizzare il contenuto. Tutte le altre politiche in questo kit hanno anche 24 ore di memorizzazione in cache delle licenze.
   * **policy_ios_remotekeyserver**  - Su dispositivi iOS, la licenza DRM verrà acquisita da Cloud DRM. Inoltre, il cliente acquisirà tutte le chiavi di decrittografia AES da Cloud DRM. Riproduzione non consentita su dispositivi iOS jailbreak.

   * **policy_ios_localkeyserver**  - Su dispositivi iOS, la licenza DRM verrà acquisita da Cloud DRM. Inoltre, il client acquisirà tutte le chiavi di decrittografia AES HLS da un server HTTP locale, invece di Cloud DRM. Riproduzione non consentita su dispositivi iOS jailbreak.

   * **policy_adobePass** : il client deve prima eseguire l&#39;autenticazione con (precedentemente denominato Adobe Pass) oppure viene negata una licenza.

* Strumento Adobe Policy Manager per creare criteri DRM aggiuntivi
* Contenuto video di esempio da utilizzare per la creazione di pacchetti

