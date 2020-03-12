---
seo-title: Controlli di protezione dell'uscita
title: Controlli di protezione dell'uscita
uuid: a0518392-cd33-4ef0-834c-f90145a9b421
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Controlli di protezione dell&#39;uscita{#output-protection-controls}

La protezione dell&#39;output controlla il parametro che controlla se l&#39;output su dispositivi di rendering esterni è protetto. Potete specificare restrizioni per le uscite analogiche e digitali in modo indipendente.

Controlla se l&#39;output su dispositivi di rendering esterni deve essere limitato. Per dispositivo esterno si intende qualsiasi dispositivo video o audio non incorporato nel computer. I display integrati, come nei notebook, non sono considerati esterni nello scenario dei controlli di protezione dell&#39;output.

I tipi di connessione per l&#39;aria (OTA) sono tutti inseriti in blacklist per impostazione predefinita, ma possono essere inseriti in una whitelist se necessario. Le connessioni OTA supportate includono: Miracast, AirPlay, DLNA e WIDI.

**Protezione dell&#39;uscita basata sulla risoluzione: (Disponibile dalla versione 5.3 in avanti). ** Offre una protezione dell&#39;output basata sul numero verticale di pixel del contenuto, che consente di specificare una serie di requisiti di protezione in base al numero verticale di pixel.

Sono disponibili le seguenti opzioni/livelli di applicazione:

| Opzione | Supportato in dispositivi analogici | Supportato nei dispositivi digitali |
|---|---|---|
| **Obbligatorio** — La protezione dell&#39;uscita analogica per la copia (ACP) o il sistema di gestione della generazione di copie (CGMS-A) deve essere attivata per poter riprodurre il contenuto su un dispositivo esterno. I client DRM Primetime devono abilitare la protezione dell&#39;output tramite ACP o CGMS-A. Sui dispositivi che supportano entrambi, i client Primetime DRM 3.0 tentano di abilitare entrambi. Tuttavia, per riprodurre il contenuto è necessario abilitare solo uno. | SÌ | SÌ |
| **ACP richiesto** — È richiesta la protezione dell&#39;output ACP. La riproduzione non è consentita su CGMS-A. I client Primetime DRM 2.0 non supportano questa opzione. Se impostato, un client Primetime DRM 2.0 si comporta come se fosse stata specificata l&#39;opzione &quot;Nessuna riproduzione&quot;. | SÌ | - |
| **Usa se disponibile** : Cercate di abilitare la protezione dell&#39;output ACP e CGMS-A se disponibile e di consentire la riproduzione se non disponibile. I client Primetime DRM 3.0 tentano di abilitare sia ACP che CGMS-A, se possibile. I client Primetime DRM 2.0 cercano solo di abilitare ACP o CGMS-A. Ad esempio, il client DRM Primetime tenta di abilitare ACP o CGMS-A. Se il tentativo ha esito positivo, l&#39;altra opzione non può essere abilitata. Se il tentativo non riesce, viene effettuato un secondo tentativo per attivare l’altra opzione. Anche se entrambi i tentativi non riescono, il contenuto viene riprodotto comunque. | SÌ | SÌ |
| **Usa ACP se disponibile** — Se disponibile, provate a abilitare la protezione dell&#39;output ACP, ma consentite la riproduzione se non disponibile. La protezione non è disponibile su CGMS-A. I client Primetime DRM 2.0 non supportano questa opzione. Se impostato, un client Primetime DRM 2.0 si comporta come se fosse stata specificata l&#39;opzione &quot;Nessuna protezione&quot;. | SÌ | - |
| **Utilizzare CGMS-A se disponibile **— Tentate di abilitare la protezione dell&#39;output CGMS-A se disponibile, ma consentite la riproduzione se non disponibile. La protezione non è disponibile sugli ACP. I client Primetime DRM 2.0 non supportano questa opzione. Se impostato, un client Primetime DRM 2.0 si comporta come se fosse stata specificata l&#39;opzione &quot;Nessuna protezione&quot;. | SÌ | - |
| **Nessuna protezione** — Per le uscite analogiche e digitali non viene applicata alcuna abilitazione alla protezione dell&#39;uscita. | SÌ | SÌ |
| **Nessuna riproduzione** — Non consentire la riproduzione su dispositivi esterni per le uscite analogiche e digitali. | SÌ | SÌ |

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Sebbene queste regole siano applicate in modo coerente su tutte le piattaforme, è possibile attivare la protezione dell&#39;output solo in modo sicuro sulle piattaforme Windows. Su altre piattaforme, come Macintosh e Linux, non sono disponibili funzioni del sistema operativo supportate per le applicazioni di terze parti.

Esempio di utilizzo: Alcuni contenuti possono applicare controlli di protezione dell&#39;output e pertanto il distributore di contenuti può impostare il livello di protezione. Se si specifica &quot;Obbligatorio&quot; e si tenta di riprodurre il contenuto su un Macintosh, il client non riproduce il contenuto su dispositivi esterni. I contenuti possono essere riprodotti su monitor interni.

Se si specifica &quot;Obbligatorio&quot; e si tenta di riprodurre su Linux, il client non riproduce il contenuto su alcun dispositivo perché non può distinguere tra dispositivi interni ed esterni.

Se si specifica &quot;Usa se disponibile&quot;, la protezione dell&#39;output viene attivata laddove possibile. Ad esempio, nei sistemi Windows che supportano il protocollo COPP (Certified Output Protection Protocol), il contenuto viene trasmesso con protezione dell&#39;output a uno schermo esterno. Questo esempio è talvolta noto come *`selectable output control`*.
