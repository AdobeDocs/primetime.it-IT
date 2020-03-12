---
description: Quando la riproduzione raggiunge un’interruzione di annuncio, passa un’interruzione di annuncio o termina in un’interruzione di annuncio, TVSDK definisce alcuni comportamenti predefiniti per il posizionamento dell’indicatore di riproduzione corrente.
seo-description: Quando la riproduzione raggiunge un’interruzione di annuncio, passa un’interruzione di annuncio o termina in un’interruzione di annuncio, TVSDK definisce alcuni comportamenti predefiniti per il posizionamento dell’indicatore di riproduzione corrente.
seo-title: Personalizzare la riproduzione con gli annunci
title: Personalizzare la riproduzione con gli annunci
uuid: e7c9f4b1-15c9-43a2-be00-1ca4bfd17e43
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Panoramica {#customize-playback-with-ads-overview}

Quando la riproduzione raggiunge un’interruzione di annuncio, passa un’interruzione di annuncio o termina in un’interruzione di annuncio, TVSDK definisce alcuni comportamenti predefiniti per il posizionamento dell’indicatore di riproduzione corrente.

>[!TIP]
>
>È possibile ignorare il comportamento predefinito utilizzando la `AdPolicySelector` classe.

Il comportamento predefinito varia a seconda che l’utente superi o meno l’interruzione dell’annuncio durante la riproduzione normale o che desideri inserirla in un video o riposizionarla con avanzamento rapido o riavvolgimento (riproduzione con trucco).

Potete personalizzare il comportamento di riproduzione e riproduzione nei seguenti modi:

* Salvate la posizione in cui l’utente ha smesso di guardare il video e ha ripreso la riproduzione nella stessa posizione in una sessione futura.
* Se un&#39;interruzione di annuncio viene presentata all&#39;utente, non vengono visualizzati annunci aggiuntivi per un certo numero di minuti, anche se l&#39;utente cerca di trovare una nuova posizione.
* Se il contenuto non viene riprodotto dopo alcuni minuti, riavviate il flusso o eseguite il failover su un&#39;altra origine per lo stesso contenuto.

   Nella sessione di riproduzione del failover, per consentire all&#39;utente di saltare gli annunci e riprendere la posizione precedente, è possibile disattivare gli annunci pre-roll e/o mid-roll. TVSDK fornisce metodi per abilitare la disattivazione degli annunci pre-roll e mid-roll.