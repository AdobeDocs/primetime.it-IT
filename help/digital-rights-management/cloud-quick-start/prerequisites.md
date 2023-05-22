---
title: Prerequisiti
description: Prerequisiti
copied-description: true
exl-id: 1b66f7fd-ea2f-4217-b327-910e90ab889d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# Prerequisiti {#prerequisites}

Prima di creare il pacchetto di contenuto, è necessario un certificato di Primetime DRM Packager. Deve essere richiesto tramite il processo di registrazione dei certificati DRM di Primetime. È necessario solo un certificato packager (nessun server licenze o trasporto). Indicare nel messaggio di posta elettronica di richiesta del certificato che la richiesta è relativa a un certificato da utilizzare con il servizio DRM.

[Guida alla registrazione dei certificati](../../digital-rights-management/certificate-enrollment-guide/about-certs.md)

Esistono due livelli di certificati di imballaggio: PRODUZIONE e PROVA. Il contenuto creato con certificati TRIAL è solo per uso di sviluppo e non verrà riprodotto dopo la scadenza del certificato. Tutte le licenze rilasciate per il contenuto TRIAL avranno una data di scadenza massima dei criteri hardcoded uguale alla data di scadenza del certificato (se non impostata nei criteri DRM).
