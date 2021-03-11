---
description: Puoi tenere traccia dell’utilizzo dei video nell’implementazione di riferimento Android di Primetime configurandolo per l’utilizzo con il tuo account Adobe Analytics.
title: Configurare Video Analytics
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---


# Configurare Video Analytics {#configure-video-analytics}

Puoi tenere traccia dell’utilizzo dei video nell’implementazione di riferimento Android di Primetime configurandolo per l’utilizzo con il tuo account Adobe Analytics. L’implementazione di riferimento per Android è progettata per inviare dati di utilizzo video e heartbeat ad Adobe Analytics. Per abilitare questa funzione, contatta prima il tuo rappresentante Adobe Primetime e crea un account Adobe Analytics.

Per abilitare l’integrazione Adobe Analytics, è necessario configurare due posizioni all’interno dell’implementazione di riferimento. Le configurazioni di analisi video in fase di esecuzione hanno effetto una volta selezionato un nuovo video per la riproduzione (cioè una volta creato un nuovo PlayerActivy).

1. Configura le opzioni di caricamento nel file di risorse `ADBMobileConfig.json` .

   Questo file viene fornito dal rappresentante Adobe. Per impostazione predefinita non è incluso nel bundle SDK Primetime. Per ulteriori informazioni sulle impostazioni in questo file di configurazione, consulta la Guida per il programmatore Android qui: Inizializzare e configurare l&#39;analisi video.
1. Configurare le opzioni di esecuzione nel menu Impostazioni di implementazione di riferimento

   ![](assets/img_psdk_ref_impl_va-settings-menu.png)

   | Opzioni di esecuzione | Descrizione |
   |---|---|
   | Server di tracciamento di Video Analytics | URL del punto finale della raccolta back-end di analisi video. Qui vengono inviate tutte le chiamate di tracciamento heartbeat video. |
   | ID processo | Identificatore del processo di elaborazione. Questo indica all’endpoint back-end quale tipo di elaborazione applicare per le chiamate di tracciamento video. |
   | Canale | Nome del canale in cui l’utente sta guardando il contenuto. Per un’app mobile, in genere è il nome dell’applicazione. |
   | Editore | Nome dell’autore del contenuto |
   | Debug Logging | Attiva registrazioni estese. Disabilitata per impostazione predefinita, questa impostazione può influire sulle prestazioni quando è attivata, per cui puoi disabilitarla per un ambiente di produzione. |
   | Modalità silenziosa | Se questa opzione è abilitata, non vengono effettuate chiamate di rete; questa opzione risulta utile per il debug locale, ma deve essere disabilitata per un ambiente di produzione. |