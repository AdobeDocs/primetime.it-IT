---
description: ' Adobe fornisce un servizio Cloud DRM per  clienti Adobe Primetime DRM che non desiderano sviluppare e mantenere il proprio server licenze Primetime DRM. Utilizzando questo servizio, i clienti possono ridurre la complessità operativa e di sviluppo in relazione al rilascio delle licenze DRM. Primetime Cloud DRM può rilasciare licenze DRM a tutti i dispositivi in grado di eseguire un''applicazione video compatibile con il browser Primetime, come iOS, Android, Desktop e Xbox360. Questo servizio DRM è ospitato e gestito dal Adobe , con tempi di attività 24/7.'
seo-description: ' Adobe fornisce un servizio Cloud DRM per  clienti Adobe Primetime DRM che non desiderano sviluppare e mantenere il proprio server licenze Primetime DRM. Utilizzando questo servizio, i clienti possono ridurre la complessità operativa e di sviluppo in relazione al rilascio delle licenze DRM. Primetime Cloud DRM può rilasciare licenze DRM a tutti i dispositivi in grado di eseguire un''applicazione video compatibile con il browser Primetime, come iOS, Android, Desktop e Xbox360. Questo servizio DRM è ospitato e gestito dal Adobe , con tempi di attività 24/7.'
seo-title: Sfondo
title: Sfondo
uuid: 11a5b9ea-ebd2-47e0-b078-af2a3e1f7bf6
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---


# Sfondo {#background}

 Adobe fornisce un servizio Cloud DRM per  clienti Adobe Primetime DRM che non desiderano sviluppare e mantenere il proprio server licenze Primetime DRM. Utilizzando questo servizio, i clienti possono ridurre la complessità operativa e di sviluppo in relazione al rilascio delle licenze DRM. Primetime Cloud DRM può rilasciare licenze DRM a tutti i dispositivi in grado di eseguire un&#39;applicazione video compatibile con il browser Primetime, come iOS, Android, Desktop e Xbox360. Questo servizio DRM è ospitato e gestito dal Adobe , con tempi di attività 24/7.

>[!NOTE]
>
> Adobe Primetime DRM era precedentemente denominato  accesso al Adobe e prima di tale, Flash Access.

## Contenuto con DRM di Primetime Cloud {#section_788D0DD5F6DB41678FD87CFBD21B25FD}

* Modulo di autenticazione/adesione personalizzato e istruzioni su come attivare l&#39;autenticazione personalizzata per il contenuto. Per ulteriori informazioni, fare riferimento alla directory [!DNL Custom Authentication Entitlement].
* Certificato server licenze DRM per cloud ( [!DNL .pem/.cer/.der])

* Certificato di trasporto del server licenze DRM ( [!DNL .pem/.cer/.der])

* Primetime Java Offline Packager
* Criteri DRM di esempio per la creazione di pacchetti

   * **policy_24hr**  - Cache delle licenze su disco per 24 ore. Dopo 24 ore, è necessario acquisire una nuova licenza per visualizzare il contenuto. Tutti gli altri criteri di questo kit dispongono anche di 24 ore di cache delle licenze.
   * **policy_ios_remotekeyserver**  - Sui dispositivi iOS, la licenza DRM verrà acquisita da Cloud DRM. Inoltre, il client acquisirà tutte le chiavi di decrittazione AES da Cloud DRM. La riproduzione non è consentita sui dispositivi iOS danneggiati.

   * **policy_ios_localkeyserver**  - Sui dispositivi iOS, la licenza DRM verrà acquisita da Cloud DRM. Inoltre, il client acquisirà tutte le chiavi di decrittazione HLS AES da un server HTTP locale, invece di Cloud DRM. La riproduzione non è consentita sui dispositivi iOS danneggiati.

   * **policy_adobePass** : il client deve prima effettuare l&#39;autenticazione (precedentemente denominato  Adobe Pass), altrimenti viene negata una licenza.

*  strumento di gestione dei criteri di Adobe per creare criteri DRM aggiuntivi
* Contenuto video di esempio da usare per la creazione di pacchetti

