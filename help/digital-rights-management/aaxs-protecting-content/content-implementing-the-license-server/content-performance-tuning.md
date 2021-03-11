---
title: Ottimizzazione delle prestazioni
description: Ottimizzazione delle prestazioni
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---


# Ottimizzazione delle prestazioni{#performance-tuning}

Utilizza i seguenti suggerimenti per migliorare le prestazioni:

* L&#39;utilizzo di un HSM di rete può essere notevolmente più lento rispetto all&#39;utilizzo di un HSM collegato direttamente.
* Per migliorare le prestazioni, puoi facoltativamente abilitare il supporto nativo per le operazioni di crittografia distribuendo le librerie specifiche della piattaforma che si trovano nella cartella &quot;thirdparty/cryptoj&quot; dell’SDK. Per abilitare il supporto nativo, aggiungi la libreria per la piattaforma (jsafe.dll per Windows o libjsafe.so per Linux) al percorso.

   >[!NOTE]
   >
   >Se esegui più applicazioni web nella stessa istanza Tomcat e disponi di `jsafe.dll` sul percorso, solo la prima applicazione web che viene caricata sarà in grado di caricare la libreria `jsafe.dll`. Pertanto, solo la prima applicazione web ottiene il vantaggio del supporto nativo. In questi casi, per migliorare le prestazioni di tutte le applicazioni web, posizionare `cryptoj.jar`al di fuori del file WAR. Ad esempio, nella directory `<tomcat_installation_folder>/lib`.

* Un sistema operativo a 64 bit, come la versione a 64 bit di Red Hat® o Windows, offre prestazioni molto migliori rispetto a un sistema operativo a 32 bit.

