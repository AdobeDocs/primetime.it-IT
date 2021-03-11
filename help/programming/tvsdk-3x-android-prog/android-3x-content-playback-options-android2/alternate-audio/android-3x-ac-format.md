---
description: Il codec audio 3 (AC-3, noto anche come formato Dolby Digital®) 5.1, consente ai fornitori di contenuti di comprimere le dimensioni dei file audio multicanale senza compromettere la qualità del suono. L'AC-3 è un formato 5.1, il che significa che offre cinque canali a banda piena per un'esperienza utente più ricca.
title: Formato AC-3 5.1
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---


# Formato AC-3 5.1 {#ac-format}

Il codec audio 3 (AC-3, noto anche come formato Dolby Digital®) 5.1, consente ai fornitori di contenuti di comprimere le dimensioni dei file audio multicanale senza compromettere la qualità del suono. L&#39;AC-3 è un formato 5.1, il che significa che offre cinque canali a banda piena per un&#39;esperienza utente più ricca.

Per ulteriori informazioni, consulta [Dolby Digital 5.1](https://www.dolby.com/us/en/technologies/dolby-digital.html).

TVSDK supporta le seguenti funzioni AC-3 5.1:

* Audio surround AC-3
* Flussi misti/non misti per tipo audio surround
* Possibilità di eseguire una query sul dispositivo per verificare se il codec audio surround è disponibile sul dispositivo.

   I risultati determinano quale tipo di codec audio preferito è selezionato. Il manifesto con il tipo di codec audio che il dispositivo non utilizzerà viene scartato. Ad esempio, se è stato selezionato il formato AC-3, i profili con il formato Advanced Audio Coding (AAC) non vengono considerati.
* Modalità passthrough

   In modalità passthrough, invece di decodificare il supporto dal formato AC-3 5.1 a un formato PCM (multicanale pulse-code modulation), il TVSDK viene modificato o non modificato (a seconda del dispositivo) dal Decoder. Questo supporto viene inviato al dispositivo audio (altoparlante o ricevitore) in modo che il dispositivo audio possa decodificare e riprodurre il flusso surround Dolby.

>[!IMPORTANT]
>
>TVSDK supporta le funzioni AC-3 5.1 solo sul dispositivo Amazon Fire TV di prima generazione.

Le seguenti funzioni AC-3 5.1 non sono supportate:

* Audio AAC multicanale
* ABR su diversi codec (AAC - AC3)

## Selezionare i supporti supportati {#section_0D7E717BE18B418D817EE017EF2375D1}

Ecco il flusso di lavoro tipico che si verifica quando TVSDK trova un manifesto con supporto AC-3 e AAC:

1. Query TVSDK che codec il dispositivo può supportare.
1. Viene selezionato il codec con la qualità più elevata.

   Ordine in cui viene selezionata la qualità:

   1. AC-3
   1. AAC

1. TVSDK ignora i profili con altri tipi di codec audio.

>[!TIP]
>
>Impossibile ottenere informazioni sui profili ignorati.

## Determinare la modalità di output {#section_D2AFBF33D3904AC2A7C653A60C3A0CD3}

Durante l&#39;elaborazione dei supporti AC-3, se un dispositivo Android è collegato al sistema di altoparlanti, la decisione di riprodurre il contenuto in modalità surround o stereo dipende da come il dispositivo è configurato.

|  | **Suono surround** | **Diffusore stereo** |
|---|---|---|
| Configurazione del dispositivo Dolby on (o auto) | Configurazione del dispositivo Dolby on (o auto) | Modalità stereo |
| Configurazione del dispositivo Dolby off | Modalità stereo | Modalità stereo |