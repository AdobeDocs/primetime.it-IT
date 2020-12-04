---
description: Potete tenere traccia dell’utilizzo dei video nell’implementazione di riferimento Android di Primetime configurandolo in modo che funzioni con il vostro account Adobe Analytics .
seo-description: Potete tenere traccia dell’utilizzo dei video nell’implementazione di riferimento Android di Primetime configurandolo in modo che funzioni con il vostro account Adobe Analytics .
seo-title: Configurare l'analisi video
title: Configurare l'analisi video
uuid: ce2ebab3-b3c8-472a-9c54-16ddb1c3cc4e
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---


# Configurare l&#39;analisi video {#configure-video-analytics}

Potete tenere traccia dell’utilizzo dei video nell’implementazione di riferimento Android di Primetime configurandolo in modo che funzioni con il vostro account Adobe Analytics . L’implementazione di riferimento per Android è stata progettata per inviare dati sull’utilizzo di video e heartbeat a  Adobe Analytics. Per abilitare questa funzione, è necessario contattare il rappresentante Adobe Primetime  e creare un account Adobe Analytics .

All&#39;interno dell&#39;implementazione di riferimento sono disponibili due posizioni da configurare per abilitare l&#39;integrazione  Adobe Analytics. Le configurazioni di analisi video in fase di esecuzione hanno effetto una volta che un nuovo video viene selezionato per la riproduzione (ovvero dopo la creazione di una nuova attività Player).

1. Configurare le opzioni di caricamento nel file di risorse `ADBMobileConfig.json`.

   Questo file viene fornito dal rappresentante del Adobe . Per impostazione predefinita, non è incluso nel pacchetto SDK Primetime. Per ulteriori informazioni sulle impostazioni in questo file di configurazione, consulta la Guida per i programmatori Android qui: Inizializzare e configurare l&#39;analisi video.
1. Configurare le opzioni di esecuzione nel menu Impostazioni di implementazione riferimenti

   ![](assets/img_psdk_ref_impl_va-settings-menu.png)

   | Opzioni di esecuzione | Descrizione |
   |---|---|
   | Server di monitoraggio di Analytics Video | URL del punto finale della raccolta back-end di analisi video. Qui vengono inviate tutte le chiamate di tracciamento heartbeat video. |
   | ID processo | Identificatore del processo di elaborazione. Indica all’endpoint back-end quale tipo di elaborazione applicare per le chiamate di tracciamento video. |
   | Canale | Nome del canale in cui l&#39;utente sta visualizzando il contenuto. Per un’applicazione mobile, si tratta in genere del nome dell’applicazione. |
   | Editore | Nome dell’autore del contenuto |
   | Debug Logging | Attiva la registrazione estesa. Disattivato per impostazione predefinita, questo può influire sulle prestazioni quando attivato, pertanto puoi disattivare questo per un ambiente di produzione. |
   | Modalità silenziosa | Se questa opzione è attivata, non viene eseguita alcuna chiamata di rete; ciò sarebbe utile per il debug locale, ma deve essere disabilitato per un ambiente di produzione. |