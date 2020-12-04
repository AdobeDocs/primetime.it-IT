---
description: L'SDK scarica periodicamente i CRL pubblicati da  Adobe. È necessario assicurarsi che l'accesso a questi file non sia bloccato o che l'applicazione di tali CRL non sia impedita.
seo-description: L'SDK scarica periodicamente i CRL pubblicati da  Adobe. È necessario assicurarsi che l'accesso a questi file non sia bloccato o che l'applicazione di tali CRL non sia impedita.
seo-title: Utilizzo di CRL pubblicati da  Adobe
title: Utilizzo di CRL pubblicati da  Adobe
uuid: 7a9088bd-dde6-4445-958c-3e7272215b3c
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---


# Utilizzo di CRL pubblicati da  Adobe{#consuming-crls-published-by-adobe}

L&#39;SDK scarica periodicamente i CRL pubblicati da  Adobe. È necessario assicurarsi che l&#39;accesso a questi file non sia bloccato o che l&#39;applicazione di tali CRL non sia impedita.

L&#39;SDK dispone di un&#39;opzione di configurazione che consente di ignorare gli errori durante il recupero  CRL di Adobe e potete applicare questa opzione solo in ambienti di sviluppo. Negli ambienti di produzione, il server licenze deve recuperare i CRL da  Adobe. Se il server licenze non è in grado di ottenere un CRL valido, si è verificato un errore.
