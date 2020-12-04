---
description: Quando la riproduzione raggiunge un’interruzione di annuncio, passa un’interruzione di annuncio o termina in un’interruzione di annuncio, TVSDK definisce alcuni comportamenti predefiniti per il posizionamento dell’indicatore di riproduzione corrente.
seo-description: Quando la riproduzione raggiunge un’interruzione di annuncio, passa un’interruzione di annuncio o termina in un’interruzione di annuncio, TVSDK definisce alcuni comportamenti predefiniti per il posizionamento dell’indicatore di riproduzione corrente.
seo-title: Personalizzare la riproduzione con gli annunci
title: Personalizzare la riproduzione con gli annunci
uuid: 20b5bfb2-83d8-4517-b821-8c542afa387d
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# Panoramica {#customize-playback-with-ads}

Quando la riproduzione raggiunge un’interruzione di annuncio, passa un’interruzione di annuncio o termina in un’interruzione di annuncio, TVSDK definisce alcuni comportamenti predefiniti per il posizionamento dell’indicatore di riproduzione corrente.

>[!TIP]
>
>È possibile ignorare il comportamento predefinito utilizzando la classe `AdBreakPolicySelector`.

Il comportamento predefinito varia a seconda che l’utente superi o meno l’interruzione dell’annuncio durante la riproduzione normale o che desideri inserirla in un video o riposizionarla con avanzamento rapido o riavvolgimento (riproduzione con trucco).

Potete personalizzare il comportamento di riproduzione e riproduzione nei seguenti modi:

* Salvate la posizione in cui l’utente ha smesso di guardare il video e ha ripreso la riproduzione nella stessa posizione in una sessione futura.
* Se all&#39;utente viene presentata un&#39;interruzione di annuncio, non vengono visualizzati annunci aggiuntivi per alcuni minuti, anche se l&#39;utente cerca una nuova posizione.
* Se il contenuto non viene riprodotto dopo alcuni minuti, riavviate il flusso o eseguite il failover su un&#39;altra origine per lo stesso contenuto.

   Nella sessione di riproduzione del failover, per consentire all&#39;utente di saltare gli annunci e riprendere la posizione precedente, è possibile disattivare gli annunci pre-roll e/o mid-roll. TVSDK fornisce metodi per abilitare la disattivazione degli annunci pre-roll e mid-roll.