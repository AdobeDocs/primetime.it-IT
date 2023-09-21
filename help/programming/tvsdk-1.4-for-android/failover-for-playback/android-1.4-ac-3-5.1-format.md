---
description: Lo streaming via Internet richiede una connessione costante e stabile per riprodurre un flusso da un server remoto. Tuttavia, la variabilità della connessione Internet o della riproduzione in streaming di un utente fa sì che la riproduzione remota possa non avere la qualità dei contenuti multimediali riprodotti localmente.
title: Formato AC-3 5.1
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---

# Formato AC-3 5.1{#ac-format}

Lo streaming via Internet richiede una connessione costante e stabile per riprodurre un flusso da un server remoto. Tuttavia, la variabilità della connessione Internet o della riproduzione in streaming di un utente fa sì che la riproduzione remota possa non avere la qualità dei contenuti multimediali riprodotti localmente.

Primetime non è in grado di proteggere da errori quali un&#39;interruzione del servizio ISP o la disconnessione di un cavo. Tuttavia, lo streaming di Primetime offre protezione da failover per proteggere la riproduzione da determinati guasti del server remoto o da errori operativi, migliorando l&#39;esperienza dei visualizzatori. TVSDK implementa la protezione di failover per ridurre al minimo le interruzioni della riproduzione e ottenere una riproduzione ottimale nonostante i problemi di trasmissione. Il lettore video passa automaticamente a un set di supporti di backup quando non sono disponibili rappresentazioni o frammenti interi.

Il codec audio 3 (AC-3, noto anche come formato Dolby Digital®) 5.1, consente ai content provider di comprimere le dimensioni dei file audio multicanale senza compromettere la qualità del suono. AC-3 è un formato 5.1 che offre cinque canali a banda piena per un&#39;esperienza di utilizzo più ricca.

Per ulteriori informazioni, consulta [Dolby Digital 5.1](https://www.dolby.com/us/en/technologies/dolby-digital.html).

>[!IMPORTANT]
>
>TVSDK versione 1.4 supporta il formato AC-3 5.1 solo su Amazon FireTV.

TVSDK supporta le seguenti funzioni AC-3 5.1:

* Audio surround AC-3
* Flussi misti/non misti per il tipo di audio surround
* Possibilità di interrogare il dispositivo per verificare se il codec audio surround è disponibile sul dispositivo.

  I risultati determinano il tipo di codec audio preferito selezionato. Il manifesto con il tipo di codec audio che il dispositivo non utilizzerà viene scartato. Ad esempio, se è stato selezionato il formato AC-3, i profili con il formato Advanced Audio Coding (AAC) non vengono considerati.
* Modalità pass-through

  In modalità passthrough, invece di decodificare il supporto dal formato AC-3 5.1 a un formato PCM (Pulse-Code Modulation) multicanale, il TVSDK viene modificato o non modificato (a seconda del dispositivo) dal decodificatore. Questo supporto viene inviato al dispositivo audio (altoparlante o ricevitore) in modo che il dispositivo audio possa decodificare e riprodurre il flusso surround Dolby.

TVSDK supporta le funzioni AC-3 5.1 solo sul dispositivo Amazon Fire TV di prima generazione.

Le seguenti funzioni AC-3 5.1 non sono supportate:

* Audio AAC multicanale
* ABR su codec diversi (AAC - AC3)

## Selezione dei supporti supportati {#section_E1DFA1F472EA4BDE846C71A3343E275A}

Di seguito è riportato il flusso di lavoro tipico che si verifica quando TVSDK trova un manifesto con file multimediali AC-3 e AAC:

1. TVSDK interroga i codec che il dispositivo può supportare.
1. Viene selezionato il codec con la qualità più elevata.

   L&#39;ordine di qualità è AC-3 > AAC.
1. TVSDK ignora i profili con altri tipi di codec audio.

>[!TIP]
>
>Impossibile ottenere informazioni sui profili ignorati.

## Determinazione della modalità di output {#section_64145D9824594C36AADBF0482C528767}

Durante l&#39;elaborazione del supporto AC-3, se un dispositivo Android è collegato al sistema di altoparlanti, la decisione di riprodurre il contenuto in modalità surround o stereo dipende da come è configurato il dispositivo.

|   | Audio surround | Altoparlante stereo |
|---|---|---|
| Configurazione del dispositivo Dolby on (o auto) | Configurazione del dispositivo Dolby on (o auto) | Modalità stereo |
| Configurazione dispositivo Dolby off | Modalità stereo | Modalità stereo |
