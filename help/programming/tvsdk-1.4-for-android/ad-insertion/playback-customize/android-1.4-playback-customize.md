---
description: Quando la riproduzione raggiunge un'interruzione pubblicitaria, passa un'interruzione pubblicitaria o termina in un'interruzione pubblicitaria, TVSDK definisce un comportamento predefinito per il posizionamento della testina di riproduzione corrente.
title: Personalizzare la riproduzione con gli annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---


# Panoramica {#customize-playback-with-ads-overview}

Quando la riproduzione raggiunge un&#39;interruzione pubblicitaria, passa un&#39;interruzione pubblicitaria o termina in un&#39;interruzione pubblicitaria, TVSDK definisce un comportamento predefinito per il posizionamento della testina di riproduzione corrente.

>[!TIP]
>
>È possibile ignorare il comportamento predefinito utilizzando la classe `AdBreakPolicySelector` .

Il comportamento predefinito varia a seconda che l’utente passi l’interruzione dell’annuncio durante la riproduzione normale o ricercando in un video o riposizionandolo con avanzamento rapido o riavvolgimento (riproduzione a trucco).

Puoi personalizzare il comportamento della riproduzione di annunci nei seguenti modi:

* Salvare la posizione in cui l’utente ha interrotto la visualizzazione del video e riprendere la riproduzione nella stessa posizione in una sessione futura.
* Se all’utente viene presentata un’interruzione pubblicitaria, non vengono visualizzati annunci aggiuntivi per un numero di minuti, anche se l’utente cerca una nuova posizione.
* Se la riproduzione del contenuto non riesce dopo alcuni minuti, riavviare il flusso o eseguire il failover su un&#39;altra origine per lo stesso contenuto.

   Nella sessione di riproduzione del failover, per consentire all&#39;utente di saltare gli annunci e riprendere la precedente posizione di errore, è possibile disabilitare gli annunci pre-roll e/o mid-roll. TVSDK fornisce metodi per abilitare l’eliminazione degli annunci pre-roll e mid-roll.