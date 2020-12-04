---
seo-title: ' Elenco Bloccati di client DRM con restrizioni all''accesso al contenuto protetto'
title: ' Elenco Bloccati di client DRM con restrizioni all''accesso al contenuto protetto'
uuid: c05aa6f8-32d9-42aa-a9c5-0d0629d49778
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---


#  Elenco Bloccati di client DRM non autorizzati ad accedere al contenuto protetto {#blocklist-of-drm-clients-restricted-from-accessing-protected-content}

**versioni del modulo DRM di accesso al Adobe non consentivano l&#39;accesso al contenuto protetto.**

Specifica il client DRM che non può accedere al contenuto. Specificato dalla versione client e dalla piattaforma DRM.

Esempio di utilizzo: In caso di violazione della sicurezza, una versione più recente del client DRM può essere specificata come versione minima richiesta per l&#39;acquisizione della licenza e la riproduzione dei contenuti. Il server licenze verifica che il client DRM che effettua la richiesta di licenza soddisfi i requisiti di versione prima di rilasciare una licenza. Il client DRM controlla anche la versione DRM nella licenza prima di riprodurre il contenuto. Questo controllo client è richiesto per i domini in cui una licenza può essere trasferita a un altro computer.

Una versione client DRM può essere identificata dagli attributi specificati nella tabella seguente:

| **Attributo** | **Valori supportati** | **Criteri di corrispondenza** | **Descrizione** |
|---|---|---|---|
| Ambiente | &quot;PC&quot;, &quot;PortingKit&quot; | Corrispondenza esatta | Identifica se il client è in esecuzione su un desktop o su un altro dispositivo. |
| OS | &quot;Win&quot;, &quot;Mac&quot;, &quot;Linux&quot;, &quot;Android&quot;, &quot;iOS&quot;, &quot;ChromeOS&quot; | Corrispondenza esatta | Piattaforma |
| Architettura | &quot;32&quot;, &quot;64&quot; | Corrispondenza esatta | 32 bit o 64 bit |
| Tipo di schermo | &quot;PC&quot;, &quot;Mobile&quot;, &quot;TV&quot; | Corrispondenza esatta |  |
| Versione runtime | Un numero di versione valido. Ad esempio, &quot;2.0.0&quot;, &quot;3.0&quot;, &quot;4.0&quot;, &quot;11.0&quot;, ecc. | Corrisponde se la versione client è minore o uguale alla versione specificata. | Il numero di versione è specificato come combinazione di numeri e punti (&quot;.&quot;) di qualsiasi lunghezza. |
| Versione libreria DRM | Un numero di versione valido. Ad esempio, &quot;2.0.0&quot;. | Corrisponde se la versione client è minore o uguale alla versione specificata. | Il numero di versione è specificato come combinazione di numeri e punti (&quot;.&quot;) di qualsiasi lunghezza. |
| Fornitore OEM | Stringa fornitore OEM | Corrispondenza esatta | Stringa di identificazione del fornitore OEM per il dispositivo che utilizza il kit di porta. |
| Modello | Stringa del modello. Ad esempio, &quot;iOS_Mobile&quot;, &quot;Android_Mobile&quot;, &quot;Chrome&quot;, &quot;ChromeOS_ARM&quot;, &quot;WindowsOnARM&quot;, &quot;AVE&quot; | Corrispondenza esatta | Stringa di identificazione del modello di dispositivo per il dispositivo che utilizza il kit di portamento. |

>[!NOTE]
>
>Quando si specifica una voce nel elenco Bloccati di , i valori possono essere impostati per uno o più degli attributi indicati nella tabella precedente. Qualsiasi attributo non specificato viene trattato come carattere jolly. Se il client DRM corrisponde a tutti i valori specificati in una voce di elenco Bloccati , il client potrebbe non essere in grado di accedere al contenuto protetto.

