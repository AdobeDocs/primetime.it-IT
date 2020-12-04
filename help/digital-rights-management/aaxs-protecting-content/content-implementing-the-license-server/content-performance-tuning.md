---
seo-title: Ottimizzazione delle prestazioni
title: Ottimizzazione delle prestazioni
uuid: bb5321a0-48ef-49cb-aaf0-00d7ab9562fe
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---


# Ottimizzazione delle prestazioni{#performance-tuning}

Utilizzate i seguenti suggerimenti per migliorare le prestazioni:

* L&#39;utilizzo di un HSM di rete può risultare notevolmente più lento rispetto all&#39;utilizzo di un HSM connesso direttamente.
* Per migliorare le prestazioni, puoi facoltativamente abilitare il supporto nativo per le operazioni di crittografia distribuendo le librerie specifiche della piattaforma che si trovano nella cartella &quot;third-party/cryptoj&quot; dell’SDK. Per abilitare il supporto nativo, aggiungete al percorso la libreria per la piattaforma (jsafe.dll per Windows o libjsafe.so per Linux).

   >[!NOTE]
   >
   >Se si eseguono più applicazioni Web nella stessa istanza Tomcat e si trovano nel percorso `jsafe.dll`, solo la prima applicazione Web caricata sarà in grado di caricare la libreria `jsafe.dll`. Pertanto, solo la prima applicazione Web ottiene il vantaggio del supporto nativo. In tali casi, per migliorare le prestazioni di tutte le applicazioni Web, posizionare `cryptoj.jar`all&#39;esterno del file WAR. Ad esempio, nella directory `<tomcat_installation_folder>/lib`.

* Un sistema operativo a 64 bit, come la versione a 64 bit di Red Hat® o Windows, offre prestazioni migliori rispetto a un sistema operativo a 32 bit.

