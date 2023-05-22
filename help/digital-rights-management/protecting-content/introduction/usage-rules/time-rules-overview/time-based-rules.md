---
title: Panoramica delle regole basate sul tempo
description: Panoramica delle regole basate sul tempo
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# Regole basate sul tempo {#time-based-rules}

Primetime DRM utilizza l&#39;applicazione flessibile delle restrizioni delle licenze basate sul tempo. Se un diritto di tempo scade durante la riproduzione di un video, il comportamento predefinito di Primetime DRM consiste nel non limitare la riproduzione fino alla successiva creazione del flusso video (effettuando una chiamata `Netstream.stop()` e `Netstream.play()`).

Anche se l&#39;imposizione soft è il comportamento predefinito, è possibile abilitare l&#39;imposizione hard eseguendo una delle seguenti attività:

* Chiedi al lettore video di eseguire periodicamente il polling della licenza per assicurarti che nessuna delle restrizioni di tempo sia scaduta. A tale scopo, è possibile chiamare `DRMManager.loadVoucher(LOCAL_ONLY).` Un codice di errore indica che la licenza archiviata localmente non è più valida.
* Quando l’utente fa clic su **[!UICONTROL Pause]**, puoi registrare la marca temporale del video corrente e quindi chiamare `Netstream.stop()`. Quando l’utente fa clic sul pulsante Play, puoi cercare la posizione registrata e quindi chiamare `Netstream.play()`.