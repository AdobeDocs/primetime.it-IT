---
title: Utilizza CRL pubblicati da Adobe
description: Utilizza CRL pubblicati da Adobe
copied-description: true
exl-id: b7f68a29-f834-4613-b64d-e610f660e6fc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---

# Utilizza CRL pubblicati da Adobe{#consume-crls-published-by-adobe}

L’SDK scarica periodicamente i CRL pubblicati da Adobe. Non bloccare l’accesso a questi file o impedire l’applicazione di questi CRL.

L’SDK dispone di un’opzione di configurazione che consente di ignorare gli errori durante il recupero dei CRL di Adobe. Questa opzione può essere utilizzata solo in ambienti di sviluppo. Negli ambienti di produzione, il server licenze deve essere in grado di recuperare i CRL da Adobe. Errore: non è possibile ottenere un CRL valido.
