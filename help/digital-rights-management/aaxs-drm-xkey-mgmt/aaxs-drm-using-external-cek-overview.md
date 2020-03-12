---
description: I clienti possono utilizzare Adobe Access (AAXS) DRM con i propri sistemi CKMS (Content Key Management Systems) con la funzione Esterno CEK.
seo-description: I clienti possono utilizzare Adobe Access (AAXS) DRM con i propri sistemi CKMS (Content Key Management Systems) con la funzione Esterno CEK.
seo-title: Panoramica di Adobe Access DRM External CEK
title: Panoramica di Adobe Access DRM External CEK
uuid: ea0bba63-7743-4216-863f-392500998eb6
translation-type: tm+mt
source-git-commit: 92e04cbb5e94f60c8d06e94b826ff9361c10ef97

---


# Panoramica di Adobe Access DRM External CEK {#adobe-access-drm-external-cek-overview}

I clienti possono utilizzare Adobe Access (AAXS) DRM con i propri sistemi CKMS (Content Key Management Systems) con la funzione Esterno CEK.

DRM di Adobe Access (AXS), per impostazione predefinita, elimina la necessità di gestire direttamente chiavi, certificati e metadati DRM durante il processo di creazione dei contenuti. L’SDK Java AXS genererà automaticamente una chiave CEK (Content Encryption Key) casuale durante il tempo di creazione del pacchetto e la utilizzerà per cifrare il contenuto. Successivamente l’SDK crittografa il CEK stesso e lo inserisce nei metadati del contenuto. Al momento del rilascio della licenza, il server AAXS necessita solo della chiave privata del server licenze AAXS per accedere al CEK dai metadati per generare una licenza.
