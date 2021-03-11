---
title: Verificare il contenuto del pacchetto
description: Verificare il contenuto del pacchetto
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---


# Verifica il contenuto del pacchetto {#test-the-packaged-content}

È necessario verificare che l&#39;operazione di packaging sia riuscita utilizzando Adobe Primetime Desktop Player disponibile al pubblico (tramite Flash Player). Questo lettore può supportare solo il contenuto HDS. Per testare il contenuto HLS è necessario un lettore abilitato per TVSDK del browser Primetime.

1. Ospita il contenuto su un server web.
1. Avvia il lettore DRM di Primetime (precedentemente denominato Adobe Access) all&#39;indirizzo https://drmtest2.adobe.com:8080/AccessPlayer/player.html.
1. Incolla l&#39;URL del manifesto HDS ( [!DNL .f4m]) nel campo di navigazione del lettore e fai clic sul pulsante **[!UICONTROL Play]** .
