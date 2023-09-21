---
description: Puoi tenere traccia dell’utilizzo dei video nell’implementazione di riferimento Android di Primetime configurandola per l’utilizzo con il tuo account Adobe Analytics.
title: Configurazione analisi video
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Configurazione analisi video {#configure-video-analytics}

Puoi tenere traccia dell’utilizzo dei video nell’implementazione di riferimento Android di Primetime configurandola per l’utilizzo con il tuo account Adobe Analytics. L’implementazione di riferimento Android è progettata per inviare i dati sull’utilizzo dei video e sugli heartbeat ad Adobe Analytics. Per abilitare questa funzione, devi prima contattare il rappresentante Adobe Primetime e creare un account Adobe Analytics.

All’interno dell’implementazione di riferimento è necessario configurare due posizioni per abilitare l’integrazione di Adobe Analytics. Le configurazioni di analisi video runtime diventano effettive dopo la selezione di un nuovo video per la riproduzione (ad esempio, dopo la creazione di una nuova attività Player).

1. Configurare le opzioni del tempo di caricamento in `ADBMobileConfig.json` file di risorse.

   Questo file è fornito dal rappresentante del tuo Adobe. Per impostazione predefinita, non è incluso nel bundle Primetime SDK. Per ulteriori informazioni sulle impostazioni di questo file di configurazione, consulta la Guida per programmatori Android qui: Inizializzare e configurare l’analisi video.
1. Configurare le opzioni di runtime nel menu Impostazioni implementazione di riferimento

   ![](assets/img_psdk_ref_impl_va-settings-menu.png)

   | Opzioni di runtime | Descrizione |
   |---|---|
   | Server di tracciamento di Video Analytics | URL dell’endpoint per la raccolta back-end di analisi video. Qui vengono inviate tutte le chiamate di tracciamento heartbeat video. |
   | ID processo | L’identificatore del processo di elaborazione. Indica all’endpoint back-end il tipo di elaborazione da applicare per le chiamate di tracciamento video. |
   | Canale | Il nome del canale in cui l’utente sta guardando il contenuto. Per un’app mobile, in genere si tratta del nome dell’applicazione. |
   | Editore | Nome dell’editore del contenuto |
   | Registrazione debug | Attiva la registrazione estesa. Se questa opzione è disabilitata per impostazione predefinita, può influire sulle prestazioni se è abilitata; pertanto, puoi disabilitarla per un ambiente di produzione. |
   | Modalità non interattiva | Quando questa opzione è abilitata, non vengono effettuate chiamate di rete, quindi ciò sarebbe utile per il debug locale, ma deve essere disabilitato per un ambiente di produzione. |
