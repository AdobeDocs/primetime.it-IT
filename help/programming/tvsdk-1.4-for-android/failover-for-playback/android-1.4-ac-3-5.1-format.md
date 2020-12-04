---
description: Lo streaming su Internet richiede una connessione costante e stabile per riprodurre un flusso da un server remoto. Tuttavia, la variabilità della connessione Internet o della riproduzione in streaming di un visualizzatore impedisce la riproduzione da remoto dei contenuti multimediali riprodotti localmente.
seo-description: Lo streaming su Internet richiede una connessione costante e stabile per riprodurre un flusso da un server remoto. Tuttavia, la variabilità della connessione Internet o della riproduzione in streaming di un visualizzatore impedisce la riproduzione da remoto dei contenuti multimediali riprodotti localmente.
seo-title: Formato AC-3 5.1
title: Formato AC-3 5.1
uuid: d5e77bb5-ed51-4f9f-b34f-e9082f5ee4de
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 0%

---


# Formato AC-3 5.1{#ac-format}

Lo streaming su Internet richiede una connessione costante e stabile per riprodurre un flusso da un server remoto. Tuttavia, la variabilità della connessione Internet o della riproduzione in streaming di un visualizzatore impedisce la riproduzione da remoto dei contenuti multimediali riprodotti localmente.

Primetime non è in grado di proteggere da guasti come un&#39;interruzione dell&#39;ISP o una disconnessione del cavo. Tuttavia, lo streaming Primetime fornisce una protezione di failover per proteggere la riproduzione da alcuni guasti del server remoto o da errori operativi, migliorando l&#39;esperienza dei visualizzatori. TVSDK implementa la protezione del failover per ridurre al minimo le interruzioni di riproduzione e ottenere una riproduzione senza soluzione di continuità nonostante i problemi di trasmissione. Il lettore video passa automaticamente a un set di supporti di backup quando le rappresentazioni o i frammenti interi non sono disponibili.

Il codec audio 3 (AC-3, noto anche come formato Dolby Digital®) 5.1, consente ai fornitori di contenuti di comprimere le dimensioni dei file audio multicanale senza compromettere la qualità audio. L&#39;AC-3 è un formato 5.1, che offre cinque canali a larghezza di banda completa per un&#39;esperienza utente più completa.

Per ulteriori informazioni, vedere [Dolby Digital 5.1](https://www.dolby.com/us/en/technologies/dolby-digital.html).

>[!IMPORTANT]
>
>La versione 1.4 di TVSDK supporta il formato AC-3 5.1 solo su  Amazon FireTV.

TVSDK supporta le seguenti funzionalità AC-3 5.1:

* Audio surround AC-3
* Flussi misti/non misti per il tipo audio surround
* Possibilità di eseguire una query sul dispositivo per verificare se il codec audio surround è disponibile sul dispositivo.

   I risultati determinano il tipo di codec audio preferito selezionato. Il manifesto con il tipo di codec audio che il dispositivo non utilizzerà viene eliminato. Ad esempio, se è stato selezionato il formato AC-3, i profili con il formato AAC (Advanced Audio Coding) non vengono considerati.
* Modalità passthrough

   In modalità passthrough, invece di decodificare il supporto dal formato AC-3 5.1 a un formato PCM (Multi-hannel pulse-code modulation), il TVSDK viene modificato o non modificato (a seconda del dispositivo) dal decoder. Questo supporto viene inviato al dispositivo audio (altoparlante o ricevitore) in modo che il dispositivo audio possa decodificare e riprodurre il flusso Dolby surround.

TVSDK supporta le funzioni AC-3 5.1 solo sul dispositivo  Amazon Fire TV di prima generazione.

Le seguenti funzioni AC-3 5.1 non sono supportate:

* Audio AAC multicanale
* ABR tra diversi codec (AAC - AC3)

## Selezione di supporti supportati {#section_E1DFA1F472EA4BDE846C71A3343E275A}

Di seguito è riportato il flusso di lavoro tipico che si verifica quando TVSDK trova un manifesto con supporti AC-3 e AAC:

1. Query TVSDK che codec può essere supportato dal dispositivo.
1. Viene selezionato il codec con una qualità maggiore.

   L&#39;ordine di qualità è AC-3 > AAC.
1. TVSDK ignora i profili con altri tipi di codec audio.

>[!TIP]
>
>L&#39;applicazione non è in grado di ottenere informazioni sui profili ignorati.

## Determinazione della modalità di output {#section_64145D9824594C36AADBF0482C528767}

Durante l&#39;elaborazione dei supporti AC-3, se un dispositivo Android è collegato al sistema di altoparlanti, la decisione di riprodurre il contenuto in modalità surround o stereo dipende dalla configurazione del dispositivo.

|  | Suono surround | Diffusore stereo |
|---|---|---|
| Configurazione dispositivo Dolby on (o auto) | Configurazione dispositivo Dolby on (o auto) | Modalità stereo |
| Configurazione dispositivo Dolby disattivata | Modalità stereo | Modalità stereo |

