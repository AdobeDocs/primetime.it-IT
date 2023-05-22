---
description: I clienti possono utilizzare Adobe Access (AAXS) DRM con il proprio sistema di gestione delle chiavi di contenuto (CKMS) con la funzione External CEK.
title: Panoramica sul controllo esterno DRM di accesso Adobe
exl-id: 4131863b-5773-4222-aae9-d984267cdb86
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# Panoramica sul controllo esterno DRM di accesso Adobe {#adobe-access-drm-external-cek-overview}

I clienti possono utilizzare Adobe Access (AAXS) DRM con il proprio sistema di gestione delle chiavi di contenuto (CKMS) con la funzione External CEK.

Per impostazione predefinita, Adobe Access (AAXS) DRM elimina la necessità di gestire direttamente chiavi, certificati e metadati DRM durante il processo di creazione dei pacchetti di contenuti. L’SDK Java AAXS genera automaticamente una chiave di crittografia del contenuto (CEK) casuale durante il tempo di creazione del pacchetto e la utilizza per crittografare il contenuto. Successivamente, l’SDK crittografa il codice CEK stesso e lo inserisce nei metadati del contenuto. Al momento del rilascio della licenza, il server AAXS necessita solo della chiave privata del server licenze AAXS per accedere al CEK dai metadati per generare una licenza.
