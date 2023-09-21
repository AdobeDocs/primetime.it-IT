---
title: Ottimizzazione delle prestazioni
description: Ottimizzazione delle prestazioni
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# Ottimizzazione delle prestazioni{#performance-tuning}

Utilizza i seguenti suggerimenti per migliorare le prestazioni:

* L&#39;utilizzo di un HSM di rete può essere notevolmente più lento rispetto all&#39;utilizzo di un HSM a connessione diretta.
* Per migliorare le prestazioni, puoi facoltativamente abilitare il supporto nativo per le operazioni di crittografia distribuendo le librerie specifiche per la piattaforma che si trovano nella cartella &quot;third party/cryptoj&quot; dell’SDK. Per abilitare il supporto nativo, aggiungi la libreria per la piattaforma (jsafe.dll per Windows o libjsafe.so per Linux) al percorso.

  >[!NOTE]
  >
  >Se esegui più applicazioni web nella stessa istanza Tomcat e disponi di `jsafe.dll` sul percorso, solo la prima applicazione web che carica è in grado di caricare `jsafe.dll` libreria. Pertanto, solo la prima applicazione web ottiene il vantaggio del supporto nativo. In questi casi, per migliorare le prestazioni di tutte le applicazioni web, inserisci `cryptoj.jar`all&#39;esterno del file WAR. Ad esempio, nel `<tomcat_installation_folder>/lib` directory.

* Un sistema operativo a 64 bit, come la versione a 64 bit di Red Hat® o Windows, offre prestazioni molto migliori rispetto a un sistema operativo a 32 bit.
