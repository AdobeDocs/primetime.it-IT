---
description: L’SDK scarica periodicamente i CRL pubblicati da Adobe. Assicurati che l’accesso a questi file non sia bloccato o che l’applicazione di questi CRL non sia impedita.
title: Utilizzo di CRL pubblicati da Adobe
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# Utilizzo di CRL pubblicati da Adobe{#consuming-crls-published-by-adobe}

L’SDK scarica periodicamente i CRL pubblicati da Adobe. Assicurati che l’accesso a questi file non sia bloccato o che l’applicazione di questi CRL non sia impedita.

L’SDK dispone di un’opzione di configurazione che consente di ignorare gli errori durante il recupero dei CRL di Adobe e di applicare questa opzione solo negli ambienti di sviluppo. Negli ambienti di produzione, il server licenze deve recuperare i CRL da Adobe. Se il server licenze non è in grado di ottenere un CRL valido, si è verificato un errore.
