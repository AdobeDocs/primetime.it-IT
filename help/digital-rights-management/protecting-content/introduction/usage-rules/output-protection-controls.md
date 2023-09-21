---
title: Controlli di protezione dell'output
description: Controlli di protezione dell'output
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 0%

---

# Controlli di protezione dell&#39;output{#output-protection-controls}

Il parametro dei controlli di protezione dell&#39;output controlla se l&#39;output su dispositivi di rendering esterni è protetto. È possibile specificare restrizioni per le uscite analogiche e digitali in modo indipendente.

Controlla se l&#39;output su dispositivi di rendering esterni deve essere limitato. Per periferica esterna si intende qualsiasi periferica video o audio non incorporata nel computer. I display integrati, ad esempio nei notebook, non sono considerati esterni nello scenario dei controlli di protezione dell&#39;output.

I tipi di connessione Over the air (OTA) sono tutti elencati per impostazione predefinita, ma possono essere elencati esplicitamente se necessario. Le connessioni OTA supportate includono: Miracast, AirPlay, DLNA e WIDI.

**Protezione dell&#39;output basata sulla risoluzione: (disponibile dalla versione 5.3 in avanti). ** Questa funzione fornisce una protezione dell&#39;output in base al numero di pixel verticali del contenuto, consentendo di specificare una varietà di requisiti di protezione in base al numero di pixel verticali.

Sono disponibili le seguenti opzioni/livelli di applicazione:

| Opzione | Supportato in dispositivi analogici | Supportato in dispositivi digitali |
|---|---|---|
| **Obbligatorio** — È necessario abilitare la protezione dell&#39;output Analog Copy Protection (ACP) o Copy Generation Management System - Analog (CGMS-A) per riprodurre i contenuti su una periferica esterna. I client DRM di Primetime devono abilitare la protezione dell&#39;output utilizzando ACP o CGMS-A. Sui dispositivi che supportano entrambi, i client Primetime DRM 3.0 tentano di abilitare entrambi. Tuttavia, per riprodurre il contenuto è necessario abilitarne solo uno. | SÌ | SÌ |
| **ACP richiesto** — È necessaria la protezione dell&#39;output ACP. La riproduzione non è consentita su CGMS-A. I client DRM 2.0 di Primetime non supportano questa opzione. Se questa opzione è impostata, un client Primetime DRM 2.0 si comporta come se fosse stata specificata l&#39;opzione &quot;No Playback&quot; (Nessuna riproduzione). | SÌ | - |
| **Usa se disponibile** — Se disponibile, tentare di abilitare la protezione dell&#39;output ACP e CGMS-A e di consentire la riproduzione, se non disponibile. Se possibile, i client DRM 3.0 di Primetime tentano di abilitare sia ACP che CGMS-A. I client DRM 2.0 di Primetime tentano di abilitare solo ACP o CGMS-A. Ad esempio, il client DRM di Primetime tenta di abilitare ACP o CGMS-A. Se il tentativo ha esito positivo, l’altra opzione non può essere abilitata. Se il tentativo non riesce, viene eseguito un secondo tentativo per abilitare l’altra opzione. Anche se entrambi i tentativi non vanno a buon fine, il contenuto viene riprodotto comunque. | SÌ | SÌ |
| **Usa ACP se disponibile** — Se disponibile, tentare di abilitare la protezione dell&#39;output ACP, ma consentire la riproduzione se non disponibile. La protezione non è disponibile su CGMS-A. I client DRM 2.0 di Primetime non supportano questa opzione. Se questa opzione è impostata, un client Primetime DRM 2.0 si comporta come se fosse stata specificata l&#39;opzione &quot;Nessuna protezione&quot;. | SÌ | - |
| **Utilizzare CGMS-A se disponibile **: tentare di abilitare la protezione dell&#39;output CGMS-A se disponibile, ma consentire la riproduzione se non disponibile. La protezione non è disponibile su ACP. I client DRM 2.0 di Primetime non supportano questa opzione. Se questa opzione è impostata, un client Primetime DRM 2.0 si comporta come se fosse stata specificata l&#39;opzione &quot;Nessuna protezione&quot;. | SÌ | - |
| **Nessuna protezione** — Le uscite analogiche e digitali non supportano la protezione dell&#39;uscita. | SÌ | SÌ |
| **Nessuna riproduzione** — Non consentire la riproduzione su un dispositivo esterno per le uscite analogiche e digitali. | SÌ | SÌ |

>[!NOTE]
>
>Anche se queste regole vengono applicate in modo coerente su tutte le piattaforme, puoi attivare in modo sicuro la protezione dell’output solo sulle piattaforme Windows. Su altre piattaforme, come Macintosh e Linux, non sono disponibili funzioni di sistema operativo di supporto per applicazioni di terze parti.

Caso d’uso di esempio: alcuni contenuti possono applicare controlli di protezione dell’output e pertanto il distributore di contenuti può impostare il livello di protezione. Se si specifica &quot;Required&quot; e si tenta la riproduzione su un Macintosh, il client non riproduce il contenuto su dispositivi esterni. I contenuti possono essere riprodotti su monitor interni.

Se si specifica &quot;Required&quot; e si tenta la riproduzione su Linux, il client non riproduce il contenuto su alcun dispositivo perché non è in grado di distinguere tra dispositivi interni ed esterni.

Se si specifica &quot;Usa se disponibile&quot;, la protezione dell&#39;output viene attivata ove possibile. Ad esempio, nei sistemi Windows che supportano il protocollo COPP (Certified Output Protection Protocol), il contenuto viene trasmesso con protezione dell&#39;output a uno schermo esterno. Questo esempio è talvolta noto come *`selectable output control`*.
