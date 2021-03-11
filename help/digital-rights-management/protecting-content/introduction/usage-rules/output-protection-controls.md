---
title: Controlli di protezione dell'uscita
description: Controlli di protezione dell'uscita
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 0%

---


# Controlli di protezione dell&#39;output{#output-protection-controls}

La protezione dell&#39;output controlla il parametro se l&#39;output su dispositivi di rendering esterni è protetto. È possibile specificare restrizioni per le uscite analogiche e digitali in modo indipendente.

Controlla se l&#39;output su dispositivi di rendering esterni deve essere limitato. Per dispositivo esterno si intende qualsiasi dispositivo video o audio non incorporato nel computer. I display integrati, ad esempio nei computer portatili, non sono considerati esterni nello scenario di controllo della protezione dell&#39;output.

Per impostazione predefinita, i tipi di connessione OTA (Air) sono tutti bloccati elencati, ma possono essere elencati in modo esplicito se necessario. Le connessioni OTA supportate includono: Miracast, AirPlay, DLNA e WIDI.

**Protezione dell&#39;uscita basata sulla risoluzione: Disponibile dalla versione 5.3 in avanti. ** Offre una protezione dell&#39;output basata sul conteggio verticale dei pixel del contenuto, consentendo di specificare una serie di requisiti di protezione in base al numero verticale dei pixel.

Sono disponibili le seguenti opzioni/livelli di applicazione:

| Opzione | Supportato in dispositivi analogici | Supportato nei dispositivi digitali |
|---|---|---|
| **Obbligatorio** : per riprodurre i contenuti su un dispositivo esterno, è necessario abilitare la protezione dall&#39;uscita analogica (CGMS-A) o il sistema di gestione della generazione di copie analogiche (ACP). I client DRM di Primetime devono abilitare la protezione dell&#39;output utilizzando ACP o CGMS-A. Sui dispositivi che supportano entrambi, i client Primetime DRM 3.0 tentano di abilitare entrambi. Tuttavia, per riprodurre il contenuto è necessario abilitare solo uno. | SÌ | SÌ |
| **ACP Obbligatorio** : è necessaria la protezione della produzione ACP. Riproduzione non consentita su CGMS-A. I client DRM 2.0 di Primetime non supportano questa opzione. Se impostato, un client Primetime DRM 2.0 si comporta come se fosse stata specificata l&#39;opzione &quot;No Playback&quot;. | SÌ | - |
| **Usa se disponibile**  - Prova ad abilitare la protezione dell&#39;output ACP e CGMS-A se disponibile e consenti la riproduzione se non disponibile. I client DRM 3.0 di Primetime tentano di abilitare sia ACP che CGMS-A, se possibile. I client DRM 2.0 di Primetime tentano solo di abilitare ACP o CGMS-A. Ad esempio, il client DRM Primetime tenta di abilitare ACP o CGMS-A. Se il tentativo ha esito positivo, l’altra opzione non può essere abilitata. Se il tentativo non riesce, viene quindi effettuato un secondo tentativo per abilitare l’altra opzione. Anche se entrambi i tentativi falliscono, il contenuto viene riprodotto comunque. | SÌ | SÌ |
| **Utilizza ACP se disponibile**  - Prova ad abilitare la protezione dell&#39;output ACP se disponibile, ma consenti la riproduzione se non disponibile. La protezione non è disponibile su CGMS-A. I client DRM 2.0 di Primetime non supportano questa opzione. Se impostato, un client DRM 2.0 di Primetime si comporta come se fosse stata specificata l&#39;opzione &quot;Nessuna protezione&quot;. | SÌ | - |
| **Utilizzare CGMS-A se disponibile **— Tentativo di abilitare la protezione dall&#39;uscita CGMS-A se disponibile, ma consentire la riproduzione se non disponibile. La protezione non è disponibile su ACP. I client DRM 2.0 di Primetime non supportano questa opzione. Se impostato, un client DRM 2.0 di Primetime si comporta come se fosse stata specificata l&#39;opzione &quot;Nessuna protezione&quot;. | SÌ | - |
| **Nessuna protezione** : nessuna abilitazione alla protezione dell&#39;output viene applicata alle uscite analogiche e digitali. | SÌ | SÌ |
| **Nessuna riproduzione** : non consentire la riproduzione su dispositivi esterni per le uscite analogiche e digitali. | SÌ | SÌ |

>[!NOTE]
>
>Sebbene queste regole siano applicate in modo coerente in tutte le piattaforme, è possibile attivare la protezione dell&#39;output solo in modo sicuro sulle piattaforme Windows. Su altre piattaforme, come Macintosh e Linux, non sono disponibili funzioni di supporto del sistema operativo per applicazioni di terze parti.

Esempio di utilizzo: Alcuni contenuti possono applicare controlli di protezione dell&#39;output e quindi il distributore di contenuti può impostare il livello di protezione. Se si specifica &quot;Obbligatorio&quot; e si tenta la riproduzione su un Macintosh, il client non riproduce il contenuto su dispositivi esterni. I contenuti possono essere riprodotti su monitor interni.

Se si specifica &quot;Obbligatorio&quot; e si tenta la riproduzione su Linux, il client non riproduce il contenuto su alcun dispositivo perché non può distinguere tra dispositivi interni ed esterni.

Se si specifica &quot;Usa se disponibile&quot;, la protezione dell&#39;output viene attivata laddove possibile. Ad esempio, nei sistemi Windows che supportano il protocollo di protezione dell’output certificato (COPP), il contenuto viene trasmesso con protezione dell’output a uno schermo esterno. Questo esempio è talvolta noto come *`selectable output control`*.
