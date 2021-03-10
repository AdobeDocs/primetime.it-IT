---
description: È possibile gestire i blackout nei flussi video in diretta e fornire contenuti alternativi durante una sospensione attività.
title: Gestire i blackout nei flussi live
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---


# Gestire i blackout nei flussi live{#handle-blackouts-in-live-streams}

È possibile gestire i blackout nei flussi video in diretta e fornire contenuti alternativi durante una sospensione attività.

Quando si verifica un blackout in un flusso live, il lettore utilizza gestori eventi per rilevare la blackout e fornire contenuti alternativi agli utenti che non sono idonei a guardare il flusso principale. Il lettore rileva l&#39;inizio e la fine del periodo di sospensione attività, passa la riproduzione dal flusso principale a un flusso alternativo e torna al flusso principale al termine del periodo di sospensione attività.

Nell’app client, ti abboni per i tag di blackout in TVSDK. Dopo aver ricevuto la notifica dei nuovi oggetti *metadati temporizzati*, analizzare i dati dell&#39;oggetto metadati temporizzati per identificare se l&#39;oggetto indica una voce di sospensione attività o un&#39;uscita. Per le blackout identificate, chiama gli elementi TVSDK pertinenti per passare al contenuto alternativo all’inizio della blackout e di nuovo per tornare al contenuto principale quando la blackout è terminata.

>[!TIP]
>
>Le chiavi vengono ancora scaricate dal manifesto prima della riproduzione del contenuto.

Quando un utente si connette a un flusso live al termine del periodo di sospensione attività e lo fa scorrere indietro nel tempo fino al periodo di inattività, il contenuto verrà riprodotto.

>[!IMPORTANT]
>
>Se tutte le richieste chiave non riescono, viene generato un errore durante l&#39;analisi del manifesto. Se alcune richieste hanno esito negativo e alcune hanno esito positivo, TVSDK tenta di riprodurre il contenuto. Se TVSDK tenta di riprodurre una sezione del contenuto, ma non esiste una chiave valida per decrittografare il contenuto, restituisce un errore.

Per gestire i blackout nei flussi live:

1. Imposta l’app per rilevare i tag di blackout mediante l’iscrizione ai tag di blackout in un manifesto in streaming live.

   TVSDK non rileva i tag di blackout da solo; devi abbonarti ai tag di blackout per ricevere la notifica quando i tag vengono rilevati durante l’analisi dei file manifest.
1. Crea listener di eventi per i tag a cui il lettore è iscritto.

   Quando si verifica un tag a cui il lettore ha effettuato la sottoscrizione (ad esempio, un tag blackout) in primo piano (contenuto principale) o in background (contenuto alternativo), il TVSDK invia un `TimedMetadataEvent` e crea un `TimedMetadataObject` per il `TimedMetadataEvent`.
1. Implementa i gestori per gli eventi di metadati temporizzati sia per i flussi in primo piano che per quelli in background.

   In questi gestori, ottieni gli orari di inizio e fine del periodo di sospensione attività dagli oggetti evento metadati temporizzati.
1. Prepara i `MediaPlayer` per i blackout.

   Quando `MediaPlayer` entra nello stato PREPARATO, calcola e prepara gli intervalli di sospensione attività e li imposta sull&#39;oggetto `MediaPlayer` .

1. Per ogni aggiornamento della posizione della testina di riproduzione, controllare l&#39;elenco di `TimedMetadataObjects`.

   Qui il lettore rileva l&#39;inizio e la fine del blackout e tiene traccia dell&#39;ora del blackout mentre si verifica.

1. Crea metodi per cambiare contenuto all’inizio e alla fine del periodo di sospensione attività.

   All’avvio del periodo di sospensione attività, sposta il contenuto principale in background e cambia il contenuto alternativo in modo che diventi il flusso principale. Continua a recuperare e analizzare il manifesto originale in background e continua a controllare il tag &quot;blackout end end&quot;, in modo che il lettore possa ricongiungersi al flusso originale al termine del blackout.

