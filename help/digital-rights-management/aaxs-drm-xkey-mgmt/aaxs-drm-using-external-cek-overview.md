---
description: I clienti possono utilizzare  DRM di accesso al Adobe (AAXS) con i propri sistemi CKMS (Content Key Management Systems) con la funzione Esterno CEK.
seo-description: I clienti possono utilizzare  DRM di accesso al Adobe (AAXS) con i propri sistemi CKMS (Content Key Management Systems) con la funzione Esterno CEK.
seo-title: ' Accesso al Adobe DRM Panoramica CEK esterna'
title: ' Accesso al Adobe DRM Panoramica CEK esterna'
uuid: ea0bba63-7743-4216-863f-392500998eb6
translation-type: tm+mt
source-git-commit: 92e04cbb5e94f60c8d06e94b826ff9361c10ef97
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


#  Accesso al Adobe DRM Panoramica CEK esterna {#adobe-access-drm-external-cek-overview}

I clienti possono utilizzare  DRM di accesso al Adobe (AAXS) con i propri sistemi CKMS (Content Key Management Systems) con la funzione Esterno CEK.

 DRM (Adobe Access), per impostazione predefinita, elimina la necessità di gestire direttamente chiavi, certificati e metadati DRM durante il processo di creazione dei contenuti. L’SDK Java AXS genererà automaticamente una chiave CEK (Content Encryption Key) casuale durante il tempo di creazione del pacchetto e la utilizzerà per cifrare il contenuto. Successivamente l’SDK crittografa il CEK stesso e lo inserisce nei metadati del contenuto. Al momento del rilascio della licenza, il server AAXS necessita solo della chiave privata del server licenze AAXS per accedere al CEK dai metadati per generare una licenza.
