---
description: Adobe fornisce un servizio Cloud DRM ai clienti Adobe Primetime DRM che non desiderano sviluppare e mantenere il proprio server licenze Primetime DRM. Utilizzando questo servizio, i clienti possono ridurre la complessità operativa e di sviluppo in relazione al rilascio delle licenze DRM. Primetime Cloud DRM può rilasciare licenze DRM a tutti i dispositivi in grado di eseguire un'applicazione video compatibile con il browser Primetime, come iOS, Android, Desktop e Xbox360. Questo servizio DRM è ospitato e gestito da Adobe, con tempi di attività 24/7.
seo-description: Adobe fornisce un servizio Cloud DRM ai clienti Adobe Primetime DRM che non desiderano sviluppare e mantenere il proprio server licenze Primetime DRM. Utilizzando questo servizio, i clienti possono ridurre la complessità operativa e di sviluppo in relazione al rilascio delle licenze DRM. Primetime Cloud DRM può rilasciare licenze DRM a tutti i dispositivi in grado di eseguire un'applicazione video compatibile con il browser Primetime, come iOS, Android, Desktop e Xbox360. Questo servizio DRM è ospitato e gestito da Adobe, con tempi di attività 24/7.
seo-title: Sfondo
title: Sfondo
uuid: 11a5b9ea-ebd2-47e0-b078-af2a3e1f7bf6
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Sfondo {#background}

Adobe fornisce un servizio Cloud DRM ai clienti Adobe Primetime DRM che non desiderano sviluppare e mantenere il proprio server licenze Primetime DRM. Utilizzando questo servizio, i clienti possono ridurre la complessità operativa e di sviluppo in relazione al rilascio delle licenze DRM. Primetime Cloud DRM può rilasciare licenze DRM a tutti i dispositivi in grado di eseguire un&#39;applicazione video compatibile con il browser Primetime, come iOS, Android, Desktop e Xbox360. Questo servizio DRM è ospitato e gestito da Adobe, con tempi di attività 24/7.

>[!NOTE]
>
>Adobe Primetime DRM era precedentemente denominato Adobe Access e prima di tale data, Flash Access.

## Contenuto con DRM di Primetime Cloud {#section_788D0DD5F6DB41678FD87CFBD21B25FD}

* Modulo di autenticazione/adesione personalizzato e istruzioni su come attivare l&#39;autenticazione personalizzata per il contenuto. Per ulteriori informazioni, consultare la [!DNL Custom Authentication Entitlement] directory.
* Certificato server licenze ( [!DNL .pem/.cer/.der]) per DRM cloud

* Certificato di trasporto del server licenze ( [!DNL .pem/.cer/.der]) per DRM cloud

* Primetime Java Offline Packager
* Criteri DRM di esempio per la creazione di pacchetti

   * **policy_24hr** - Cache delle licenze su disco per 24 ore. Dopo 24 ore, è necessario acquisire una nuova licenza per visualizzare il contenuto. Tutti gli altri criteri di questo kit dispongono anche di 24 ore di cache delle licenze.
   * **policy_ios_remotekeyserver** - Sui dispositivi iOS, la licenza DRM verrà acquisita da Cloud DRM. Inoltre, il client acquisirà tutte le chiavi di decrittazione AES da Cloud DRM. La riproduzione non è consentita sui dispositivi iOS con interruzione del sistema.

   * **policy_ios_localkeyserver** - Sui dispositivi iOS, la licenza DRM verrà acquisita da Cloud DRM. Inoltre, il client acquisirà tutte le chiavi di decrittazione HLS AES da un server HTTP locale, invece di Cloud DRM. La riproduzione non è consentita sui dispositivi iOS con interruzione del sistema.

   * **policy_adobePass** - Il client deve prima autenticarsi (precedentemente denominato Adobe Pass) oppure verrà negata una licenza.

* Strumento Adobe Policy Manager per creare criteri DRM aggiuntivi
* Contenuto video di esempio da usare per la creazione di pacchetti

