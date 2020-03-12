---
description: Potete gestire i blackout nei flussi video live e fornire contenuto alternativo durante un blackout.
seo-description: Potete gestire i blackout nei flussi video live e fornire contenuto alternativo durante un blackout.
seo-title: Gestione dei blackout nei flussi live
title: Gestione dei blackout nei flussi live
uuid: df933087-c8a8-49eb-a016-6dfd971c219c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Gestione dei blackout nei flussi live{#handle-blackouts-in-live-streams}

Potete gestire i blackout nei flussi video live e fornire contenuto alternativo durante un blackout.

Quando si verifica un blackout in un flusso live, il lettore utilizza i gestori eventi per rilevare il blackout e fornire contenuto alternativo agli utenti non idonei a guardare il flusso principale. Il lettore rileva l&#39;inizio e la fine del periodo di blackout, passa la riproduzione dal flusso principale a un flusso alternativo e ritorna al flusso principale al termine del periodo di blackout.

Nell’app client, ti iscrivi ai tag blackout in TVSDK. Dopo aver ricevuto una notifica di nuovi oggetti metadati ** temporizzati, analizzate i dati dell&#39;oggetto metadati temporizzati per identificare se l&#39;oggetto indica una voce di blackout o un&#39;uscita. Per le interruzioni identificate, gli elementi TVSDK pertinenti vengono chiamati per passare al contenuto alternativo all&#39;inizio della blackout e per tornare nuovamente al contenuto principale al termine della blackout.

>[!TIP]
>
>Le chiavi vengono ancora scaricate dal manifest prima della riproduzione del contenuto.

Quando un utente si connette a un flusso live dopo che il periodo di sospensione attività è terminato e torna indietro nel tempo al periodo di assenza, il contenuto viene riprodotto.

>[!IMPORTANT]
>
>Se tutte le richieste chiave non vanno a buon fine, viene generato un errore durante l&#39;analisi del manifesto. Se alcune richieste hanno esito negativo e alcune hanno esito positivo, TVSDK tenta di riprodurre il contenuto. Se TVSDK tenta di riprodurre una sezione del contenuto, ma non esiste una chiave valida per decifrare il contenuto, restituisce un errore.

Per gestire i blackout nei flussi live:

1. Configurate l&#39;app per rilevare i tag di blackout iscrivendosi ai tag di blackout in un manifesto in streaming live.

   TVSDK non rileva tag blackout autonomamente; per ricevere la notifica quando i tag vengono rilevati durante l&#39;analisi del file manifesto, dovete abbonarvi ai tag blackout.
1. Creare listener di eventi per i tag sottoscritti dal lettore.

   Quando si verifica un tag a cui il lettore ha effettuato la sottoscrizione (ad esempio, un tag blackout) nei manifesti del flusso in primo piano (contenuto principale) o in background (contenuto alternativo), TVSDK invia un `TimedMetadataEvent` e crea un `TimedMetadataObject` nome per il `TimedMetadataEvent`.
1. Implementate i gestori per gli eventi di metadati temporizzati per i flussi in primo piano e in background.

   In questi gestori, ottenete l&#39;ora di inizio e di fine del periodo di sospensione dagli oggetti evento metadati temporizzati.
1. Preparate i `MediaPlayer` blackout.

   Quando `MediaPlayer` entra nello stato PREPARATO, si calcolano e si preparano gli intervalli di blackout e li si imposta sull&#39; `MediaPlayer` oggetto.

1. Per ogni aggiornamento alla posizione dell&#39;indicatore di riproduzione, controllare l&#39;elenco di `TimedMetadataObjects`.

   Qui è dove il giocatore rileva l&#39;inizio e la fine del blackout, e tiene traccia del tempo del blackout mentre si verifica.

1. Creare metodi per cambiare il contenuto all’inizio e alla fine del periodo di sospensione attività.

   All&#39;avvio del periodo di sospensione attività, passate il contenuto principale allo sfondo e passate il contenuto alternativo in modo che diventi il flusso principale. Continuare a recuperare e analizzare il manifesto originale in background e continuare a controllare il tag &quot;blackout end end&quot;, in modo che il lettore possa rientrare nel flusso originale al termine del blackout.

