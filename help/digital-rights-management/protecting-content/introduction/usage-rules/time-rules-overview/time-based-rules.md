---
title: Panoramica delle regole basate su tempo
description: Panoramica delle regole basate su tempo
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# Regole basate sul tempo {#time-based-rules}

Primetime DRM utilizza l’&quot;applicazione morbida&quot; delle restrizioni delle licenze basate sul tempo. Se durante la riproduzione di un video scade un diritto di tempo, il comportamento predefinito di Primetime DRM è quello di non limitare la riproduzione fino alla successiva creazione dello streaming video (chiamando `Netstream.stop()` e `Netstream.play()`).

Anche se l’imposizione soft è il comportamento predefinito, è possibile abilitare l’applicazione forzata eseguendo una delle seguenti attività:

* Chiedi al lettore video di controllare periodicamente la licenza per assicurarsi che nessuna delle restrizioni di tempo sia scaduta. Puoi eseguire questa operazione chiamando `DRMManager.loadVoucher(LOCAL_ONLY).` Un codice di errore indica che la licenza memorizzata localmente non è più valida.
* Ogni volta che l&#39;utente fa clic su **[!UICONTROL Pause]**, è possibile registrare la marca temporale del video corrente e quindi chiamare `Netstream.stop()`. Quando l&#39;utente fa clic sul pulsante Play, è possibile cercare la posizione registrata e quindi chiamare `Netstream.play()`.