---
title: Utilizza CRL pubblicati da Adobe
description: Utilizza CRL pubblicati da Adobe
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---

# Utilizza CRL pubblicati da Adobe{#consume-crls-published-by-adobe}

L’SDK scarica periodicamente i CRL pubblicati da Adobe. Non bloccare l’accesso a questi file o impedire l’applicazione di questi CRL.

L’SDK dispone di un’opzione di configurazione che consente di ignorare gli errori durante il recupero dei CRL di Adobe. Questa opzione può essere utilizzata solo in ambienti di sviluppo. Negli ambienti di produzione, il server licenze deve essere in grado di recuperare i CRL da Adobe. Errore: non è possibile ottenere un CRL valido.
