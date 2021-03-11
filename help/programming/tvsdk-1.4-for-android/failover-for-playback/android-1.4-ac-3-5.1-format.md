---
description: Lo streaming via Internet richiede una connessione costante e stabile per riprodurre un flusso da un server remoto. Tuttavia, la variabilità della connessione Internet o della riproduzione in streaming di un visualizzatore impedisce la riproduzione a distanza di contenuti multimediali riprodotti localmente.
title: Formato AC-3 5.1
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---


# Formato AC-3 5.1{#ac-format}

Lo streaming via Internet richiede una connessione costante e stabile per riprodurre un flusso da un server remoto. Tuttavia, la variabilità della connessione Internet o della riproduzione in streaming di un visualizzatore impedisce la riproduzione a distanza di contenuti multimediali riprodotti localmente.

Primetime non è in grado di proteggere da guasti come un&#39;interruzione dell&#39;ISP o una disconnessione del cavo. Tuttavia, lo streaming Primetime fornisce una protezione di failover per proteggere la riproduzione da alcuni guasti o guasti operativi del server remoto, offrendo ai visualizzatori un&#39;esperienza migliore. TVSDK implementa la protezione del failover per ridurre al minimo le interruzioni di riproduzione e ottenere una riproduzione senza soluzione di continuità nonostante i problemi di trasmissione. Il lettore video passa automaticamente a un set di file multimediali di backup quando non sono disponibili interi rendering o frammenti.

Il codec audio 3 (AC-3, noto anche come formato Dolby Digital®) 5.1, consente ai fornitori di contenuti di comprimere le dimensioni dei file audio multicanale senza compromettere la qualità del suono. L&#39;AC-3 è un formato 5.1, il che significa che offre cinque canali a banda piena per un&#39;esperienza utente più ricca.

Per ulteriori informazioni, consulta [Dolby Digital 5.1](https://www.dolby.com/us/en/technologies/dolby-digital.html).

>[!IMPORTANT]
>
>La versione 1.4 di TVSDK supporta il formato AC-3 5.1 solo su Amazon FireTV.

TVSDK supporta le seguenti funzioni AC-3 5.1:

* Audio surround AC-3
* Flussi misti/non misti per tipo audio surround
* Possibilità di eseguire una query sul dispositivo per verificare se il codec audio surround è disponibile sul dispositivo.

   I risultati determinano quale tipo di codec audio preferito è selezionato. Il manifesto con il tipo di codec audio che il dispositivo non utilizzerà viene scartato. Ad esempio, se è stato selezionato il formato AC-3, i profili con il formato Advanced Audio Coding (AAC) non vengono considerati.
* Modalità passthrough

   In modalità passthrough, invece di decodificare il supporto dal formato AC-3 5.1 a un formato PCM (multicanale pulse-code modulation), il TVSDK viene modificato o non modificato (a seconda del dispositivo) dal Decoder. Questo supporto viene inviato al dispositivo audio (altoparlante o ricevitore) in modo che il dispositivo audio possa decodificare e riprodurre il flusso surround Dolby.

TVSDK supporta le funzioni AC-3 5.1 solo sul dispositivo Amazon Fire TV di prima generazione.

Le seguenti funzioni AC-3 5.1 non sono supportate:

* Audio AAC multicanale
* ABR su diversi codec (AAC - AC3)

## Selezione dei supporti supportati {#section_E1DFA1F472EA4BDE846C71A3343E275A}

Ecco il flusso di lavoro tipico che si verifica quando TVSDK trova un manifesto con supporto AC-3 e AAC:

1. Query TVSDK che codec il dispositivo può supportare.
1. Viene selezionato il codec con la qualità più elevata.

   L&#39;ordine di qualità è AC-3 > AAC.
1. TVSDK ignora i profili con altri tipi di codec audio.

>[!TIP]
>
>Impossibile ottenere informazioni sui profili ignorati.

## Determinazione della modalità di output {#section_64145D9824594C36AADBF0482C528767}

Durante l&#39;elaborazione dei supporti AC-3, se un dispositivo Android è collegato al sistema di altoparlanti, la decisione di riprodurre il contenuto in modalità surround o stereo dipende da come il dispositivo è configurato.

|  | Suono surround | Diffusore stereo |
|---|---|---|
| Configurazione del dispositivo Dolby on (o auto) | Configurazione del dispositivo Dolby on (o auto) | Modalità stereo |
| Configurazione del dispositivo Dolby off | Modalità stereo | Modalità stereo |

