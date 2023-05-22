---
description: Il codec audio 3 (AC-3, noto anche come formato Dolby Digital®) 5.1, consente ai content provider di comprimere le dimensioni dei file audio multicanale senza compromettere la qualità del suono. AC-3 è un formato 5.1 che offre cinque canali a banda piena per un'esperienza di utilizzo più ricca.
title: Formato AC-3 5.1
exl-id: 16647d69-9cb4-4bb8-8ad9-cac8811ea66d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---

# Formato AC-3 5.1 {#ac-format}

Il codec audio 3 (AC-3, noto anche come formato Dolby Digital®) 5.1, consente ai content provider di comprimere le dimensioni dei file audio multicanale senza compromettere la qualità del suono. AC-3 è un formato 5.1 che offre cinque canali a banda piena per un&#39;esperienza di utilizzo più ricca.

Per ulteriori informazioni, consulta [Dolby Digital 5.1](https://www.dolby.com/us/en/technologies/dolby-digital.html).

TVSDK supporta le seguenti funzioni AC-3 5.1:

* Audio surround AC-3
* Flussi misti/non misti per il tipo di audio surround
* Possibilità di interrogare il dispositivo per verificare se il codec audio surround è disponibile sul dispositivo.

   I risultati determinano il tipo di codec audio preferito selezionato. Il manifesto con il tipo di codec audio che il dispositivo non utilizzerà viene scartato. Ad esempio, se è stato selezionato il formato AC-3, i profili con il formato Advanced Audio Coding (AAC) non vengono considerati.
* Modalità pass-through

   In modalità passthrough, invece di decodificare il supporto dal formato AC-3 5.1 a un formato PCM (Pulse-Code Modulation) multicanale, il TVSDK viene modificato o non modificato (a seconda del dispositivo) dal decodificatore. Questo supporto viene inviato al dispositivo audio (altoparlante o ricevitore) in modo che il dispositivo audio possa decodificare e riprodurre il flusso surround Dolby.

>[!IMPORTANT]
>
>TVSDK supporta le funzioni AC-3 5.1 solo sul dispositivo Amazon Fire TV di prima generazione.

Le seguenti funzioni AC-3 5.1 non sono supportate:

* Audio AAC multicanale
* ABR su codec diversi (AAC - AC3)

## Seleziona supporti supportati {#section_0D7E717BE18B418D817EE017EF2375D1}

Di seguito è riportato il flusso di lavoro tipico che si verifica quando TVSDK trova un manifesto con file multimediali AC-3 e AAC:

1. TVSDK interroga i codec che il dispositivo può supportare.
1. Viene selezionato il codec con la qualità più elevata.

   Di seguito è riportato l&#39;ordine di selezione della qualità:

   1. AC-3
   1. AAC

1. TVSDK ignora i profili con altri tipi di codec audio.

>[!TIP]
>
>Impossibile ottenere informazioni sui profili ignorati.

## Determinare la modalità di output {#section_D2AFBF33D3904AC2A7C653A60C3A0CD3}

Durante l&#39;elaborazione del supporto AC-3, se un dispositivo Android è collegato al sistema di altoparlanti, la decisione di riprodurre il contenuto in modalità surround o stereo dipende da come è configurato il dispositivo.

|  | Audio surround | Altoparlante stereo |
|---|---|---|
| Configurazione del dispositivo Dolby on (o auto) | Configurazione del dispositivo Dolby on (o auto) | Modalità stereo |
| Configurazione dispositivo Dolby off | Modalità stereo | Modalità stereo |
