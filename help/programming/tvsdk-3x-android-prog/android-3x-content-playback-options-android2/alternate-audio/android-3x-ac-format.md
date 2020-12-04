---
description: Il codec audio 3 (AC-3, noto anche come formato Dolby Digital®) 5.1, consente ai fornitori di contenuti di comprimere le dimensioni dei file audio multicanale senza compromettere la qualità audio. L'AC-3 è un formato 5.1, che offre cinque canali a larghezza di banda completa per un'esperienza utente più completa.
seo-description: Il codec audio 3 (AC-3, noto anche come formato Dolby Digital®) 5.1, consente ai fornitori di contenuti di comprimere le dimensioni dei file audio multicanale senza compromettere la qualità audio. L'AC-3 è un formato 5.1, che offre cinque canali a larghezza di banda completa per un'esperienza utente più completa.
seo-title: Formato AC-3 5.1
title: Formato AC-3 5.1
uuid: 9d1adf33-4c9b-4d31-8212-ac301f3e44c5
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---


# Formato AC-3 5.1 {#ac-format}

Il codec audio 3 (AC-3, noto anche come formato Dolby Digital®) 5.1, consente ai fornitori di contenuti di comprimere le dimensioni dei file audio multicanale senza compromettere la qualità audio. L&#39;AC-3 è un formato 5.1, che offre cinque canali a larghezza di banda completa per un&#39;esperienza utente più completa.

Per ulteriori informazioni, vedere [Dolby Digital 5.1](https://www.dolby.com/us/en/technologies/dolby-digital.html).

TVSDK supporta le seguenti funzionalità AC-3 5.1:

* Audio surround AC-3
* Flussi misti/non misti per il tipo audio surround
* Possibilità di eseguire una query sul dispositivo per verificare se il codec audio surround è disponibile sul dispositivo.

   I risultati determinano il tipo di codec audio preferito selezionato. Il manifesto con il tipo di codec audio che il dispositivo non utilizzerà viene eliminato. Ad esempio, se è stato selezionato il formato AC-3, i profili con il formato AAC (Advanced Audio Coding) non vengono considerati.
* Modalità passthrough

   In modalità passthrough, invece di decodificare il supporto dal formato AC-3 5.1 a un formato PCM (Multi-hannel pulse-code modulation), il TVSDK viene modificato o non modificato (a seconda del dispositivo) dal decoder. Questo supporto viene inviato al dispositivo audio (altoparlante o ricevitore) in modo che il dispositivo audio possa decodificare e riprodurre il flusso Dolby surround.

>[!IMPORTANT]
>
>TVSDK supporta le funzioni AC-3 5.1 solo sul dispositivo  Amazon Fire TV di prima generazione.

Le seguenti funzioni AC-3 5.1 non sono supportate:

* Audio AAC multicanale
* ABR tra diversi codec (AAC - AC3)

## Selezionare i supporti supportati {#section_0D7E717BE18B418D817EE017EF2375D1}

Di seguito è riportato il flusso di lavoro tipico che si verifica quando TVSDK trova un manifesto con supporti AC-3 e AAC:

1. Query TVSDK che codec può essere supportato dal dispositivo.
1. Viene selezionato il codec con una qualità maggiore.

   Di seguito è riportato l&#39;ordine in cui è selezionata la qualità:

   1. AC-3
   1. AAC

1. TVSDK ignora i profili con altri tipi di codec audio.

>[!TIP]
>
>L&#39;applicazione non è in grado di ottenere informazioni sui profili ignorati.

## Determinare la modalità di output {#section_D2AFBF33D3904AC2A7C653A60C3A0CD3}

Durante l&#39;elaborazione dei supporti AC-3, se un dispositivo Android è collegato al sistema di altoparlanti, la decisione di riprodurre il contenuto in modalità surround o stereo dipende dalla configurazione del dispositivo.

|  | **Suono surround** | **Diffusore stereo** |
|---|---|---|
| Configurazione dispositivo Dolby on (o auto) | Configurazione dispositivo Dolby on (o auto) | Modalità stereo |
| Configurazione dispositivo Dolby disattivata | Modalità stereo | Modalità stereo |