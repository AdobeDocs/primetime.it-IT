---
description: L’SDK scarica periodicamente i CRL pubblicati da Adobe. È necessario assicurarsi che l'accesso a questi file non sia bloccato o che l'applicazione di tali CRL non sia impedita.
title: Utilizzo dei CRL pubblicati da Adobe
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# Utilizzo dei CRL pubblicati da Adobe{#consuming-crls-published-by-adobe}

L’SDK scarica periodicamente i CRL pubblicati da Adobe. È necessario assicurarsi che l&#39;accesso a questi file non sia bloccato o che l&#39;applicazione di tali CRL non sia impedita.

L’SDK dispone di un’opzione di configurazione per ignorare gli errori durante il recupero dei CRL di Adobe e puoi applicare questa opzione solo negli ambienti di sviluppo. Negli ambienti di produzione, il server licenze deve recuperare i CRL da Adobe. Se il server licenze non è in grado di ottenere un CRL valido, si è verificato un errore.
