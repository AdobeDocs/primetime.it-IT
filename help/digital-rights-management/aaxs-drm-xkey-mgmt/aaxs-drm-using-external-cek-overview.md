---
description: I clienti possono utilizzare Adobe Access (AAXS) DRM con i propri Content Key Management Systems (CKMS) con la funzione External CEK.
title: Panoramica di Adobe Access DRM External CEK
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# Panoramica di Adobe Access DRM External CEK {#adobe-access-drm-external-cek-overview}

I clienti possono utilizzare Adobe Access (AAXS) DRM con i propri Content Key Management Systems (CKMS) con la funzione External CEK.

Adobe Access DRM (AAXS), per impostazione predefinita, elimina la necessità di gestire direttamente chiavi, certificati e metadati DRM durante il processo di creazione dei contenuti. L’SDK Java AAXS genera automaticamente una chiave di crittografia del contenuto casuale (CEK, Content Encryption Key) durante il tempo di creazione del pacchetto e lo utilizza per cifrare il contenuto. Successivamente, l&#39;SDK crittografa la CEK stessa e la inserisce nei metadati del contenuto. Al momento del rilascio della licenza, il server AAXS necessita solo della chiave privata del server licenze AAXS per accedere alla CEK dai metadati per generare una licenza.
