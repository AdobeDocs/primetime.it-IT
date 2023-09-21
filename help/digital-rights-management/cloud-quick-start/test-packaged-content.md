---
title: Testare il contenuto del pacchetto
description: Testare il contenuto del pacchetto
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# Testare il contenuto del pacchetto {#test-the-packaged-content}

È necessario verificare che l’operazione di creazione pacchetti sia stata completata utilizzando Adobe Primetime Desktop Player disponibile al pubblico (tramite Flash Player). Questo lettore può supportare solo contenuti HDS. Per testare il contenuto HLS, è necessario un lettore abilitato per Primetime Browser TVSDK.

1. Ospita i contenuti su un server web.
1. Avviare il lettore DRM Primetime (precedentemente denominato Adobe Access) all&#39;indirizzo https://drmtest2.adobe.com:8080/AccessPlayer/player.html.
1. Incollare l&#39;URL nel manifesto HDS ( [!DNL .f4m]) nel campo di navigazione del lettore e fai clic sul pulsante **[!UICONTROL Play]** pulsante.
