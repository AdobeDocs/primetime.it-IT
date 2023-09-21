---
description: Quando la riproduzione raggiunge un’interruzione pubblicitaria, passa un’interruzione pubblicitaria o termina in un’interruzione pubblicitaria, TVSDK definisce alcuni comportamenti predefiniti per il posizionamento della testina di riproduzione corrente.
title: Personalizzare la riproduzione con gli annunci
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# Panoramica {#customize-playback-with-ads}

Quando la riproduzione raggiunge un’interruzione pubblicitaria, passa un’interruzione pubblicitaria o termina in un’interruzione pubblicitaria, TVSDK definisce alcuni comportamenti predefiniti per il posizionamento della testina di riproduzione corrente.

>[!TIP]
>
>È possibile ignorare il comportamento predefinito utilizzando `AdBreakPolicySelector` classe.

Il comportamento predefinito varia a seconda che l’utente superi l’interruzione pubblicitaria durante la riproduzione normale o effettuando la ricerca in un video o riposizionandolo con l’avanzamento o il riavvolgimento rapido (riproduzione con trucco).

Puoi personalizzare il comportamento di riproduzione degli annunci nei seguenti modi:

* Salvare la posizione in cui l&#39;utente ha interrotto la visualizzazione del video e riprendere la riproduzione nella stessa posizione in una sessione futura.
* Se viene presentata all’utente un’interruzione pubblicitaria, non visualizzerà annunci aggiuntivi per alcuni minuti, anche se l’utente cerca di trovare una nuova posizione.
* Se dopo alcuni minuti il contenuto non viene riprodotto correttamente, riavviare il flusso o eseguire il failover su un&#39;origine diversa per lo stesso contenuto.

  Nella sessione di riproduzione del failover, per consentire all’utente di saltare gli annunci e riprendere la precedente posizione di errore, puoi disabilitare gli annunci pre-roll e/o mid-roll. TVSDK fornisce metodi per consentire di saltare gli annunci pre-roll e mid-roll.
