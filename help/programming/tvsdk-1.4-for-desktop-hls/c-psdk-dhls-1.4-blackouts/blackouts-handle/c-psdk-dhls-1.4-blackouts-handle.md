---
description: È possibile gestire le sospensioni attività nei flussi video live e fornire contenuto alternativo durante una sospensione attività.
title: Gestire le sospensioni attività nei flussi live
exl-id: 2e63fb0c-44b1-46f1-a4b8-f8f67389d183
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---

# Gestire le sospensioni attività nei flussi live{#handle-blackouts-in-live-streams}

È possibile gestire le sospensioni attività nei flussi video live e fornire contenuto alternativo durante una sospensione attività.

Quando si verifica una sospensione attività in un flusso live, il lettore utilizza gestori di eventi per rilevare la sospensione attività e fornire contenuto alternativo agli utenti non idonei a guardare il flusso principale. Il lettore rileva l&#39;inizio e la fine del periodo di sospensione attività, passa la riproduzione dal flusso principale a un flusso alternativo e torna al flusso principale al termine del periodo di sospensione attività.

Nell’app client, effettui l’abbonamento per i tag di sospensione attività in TVSDK. Al momento della notifica di *metadati temporizzati* , si analizzano i dati dell&#39;oggetto metadati temporizzati per identificare se l&#39;oggetto indica una voce di sospensione attività o un&#39;uscita. Per le sospensioni attività identificate, è necessario chiamare gli elementi TVSDK rilevanti per passare al contenuto alternativo all’inizio della sospensione attività e di nuovo per tornare al contenuto principale al termine della sospensione attività.

>[!TIP]
>
>I tasti vengono comunque scaricati dal manifesto prima della riproduzione del contenuto.

Quando un utente si connette a un flusso live dopo la fine del periodo di sospensione attività e scorre indietro nel tempo fino al periodo di sospensione attività, il contenuto viene riprodotto.

>[!IMPORTANT]
>
>Se tutte le richieste chiave hanno esito negativo, viene generato un errore durante l’analisi del manifesto. Se alcune richieste non vanno a buon fine e altre vanno a buon fine, TVSDK tenta di riprodurre il contenuto. Se TVSDK tenta di riprodurre una sezione del contenuto, ma non esiste una chiave valida per decrittografarlo, viene restituito un errore.

Per gestire le sospensioni attività nei flussi live:

1. Imposta l&#39;app per rilevare i tag di sospensione attività mediante l&#39;iscrizione a tali tag in un manifesto live-stream.

   TVSDK non rileva i tag di sospensione attività da solo. È necessario sottoscrivere i tag di sospensione attività per ricevere una notifica quando i tag vengono rilevati durante l&#39;analisi del file manifesto.
1. Crea listener di eventi per i tag a cui il lettore è abbonato.

   Quando si verifica un tag a cui il lettore si è abbonato (ad esempio, un tag di sospensione attività) nei manifesti di flusso in primo piano (contenuto principale) o in background (contenuto alternativo), TVSDK invia un tag `TimedMetadataEvent` e crea un `TimedMetadataObject` per `TimedMetadataEvent`.
1. Implementa gestori per gli eventi di metadati temporizzati per i flussi in primo piano e in background.

   In questi gestori, ottenere gli orari di inizio e fine per il periodo di sospensione attività dagli oggetti evento metadati temporizzati.
1. Prepara il `MediaPlayer` per le sospensioni attività.

   Quando `MediaPlayer` entra nello stato PREPARATO, si calcolano e si preparano gli intervalli di sospensione attività e li si imposta su `MediaPlayer` oggetto.

1. Per ogni aggiornamento della posizione della testina di riproduzione, controlla l’elenco di `TimedMetadataObjects`.

   In questo punto il lettore rileva l&#39;inizio e la fine della sospensione attività e tiene traccia dell&#39;ora in cui si verifica.

1. Creare metodi per cambiare il contenuto all&#39;inizio e alla fine del periodo di sospensione attività.

   All&#39;avvio del periodo di sospensione attività, passa il contenuto principale allo sfondo e cambia il contenuto alternativo in flusso principale. Continua a recuperare e analizzare il manifesto originale in background e continua a verificare la presenza del tag &quot;blackout end&quot;, in modo che il lettore possa unirsi nuovamente al flusso originale al termine della blackout.
