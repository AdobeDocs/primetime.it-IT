---
seo-title: Panoramica delle regole basate sul tempo
title: Panoramica delle regole basate sul tempo
uuid: 10b7766e-3b1a-4d8a-ba15-46976aa0847d
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# Regole basate sul tempo {#time-based-rules}

Primetime DRM utilizza l&#39;applicazione &quot;soft&quot; delle restrizioni di licenza basate sull&#39;ora. Se un diritto di ora scade durante la riproduzione di un video, il comportamento predefinito di Primetime DRM non limita la riproduzione fino alla successiva creazione dello streaming video (mediante chiamata `Netstream.stop()` e `Netstream.play()`).

Anche se l&#39;imposizione non restrittiva è il comportamento predefinito, potete anche abilitare l&#39;imposizione forzata eseguendo una delle seguenti operazioni:

* Accertatevi che il lettore video controlli periodicamente la licenza per verificare che nessuna delle limitazioni di tempo sia scaduta. È possibile eseguire questa operazione chiamando `DRMManager.loadVoucher(LOCAL_ONLY).` Un codice di errore indica che la licenza memorizzata localmente non è più valida.
* Ogni volta che l’utente fa clic **[!UICONTROL Pause]**, potete registrare la marca temporale del video corrente e quindi chiamare `Netstream.stop()`. Quando l&#39;utente fa clic sul pulsante Riproduci, potete cercare il percorso registrato e quindi chiamare `Netstream.play()`.