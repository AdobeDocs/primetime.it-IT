---
title: Elenco Bloccati di client DRM con restrizioni all'accesso a contenuti protetti
description: Elenco Bloccati di client DRM con restrizioni all'accesso a contenuti protetti
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---


# Elenco Bloccati di client DRM con restrizioni all&#39;accesso a contenuti protetti {#blocklist-of-drm-clients-restricted-from-accessing-protected-content}

**Le versioni del modulo DRM di Adobe Access non possono accedere a contenuti protetti.**

Specifica il client DRM che non può accedere al contenuto. Specificato dalla versione e dalla piattaforma client DRM.

Esempio di utilizzo: In caso di violazione della sicurezza, è possibile specificare una versione più recente del client DRM come versione minima necessaria per l’acquisizione della licenza e la riproduzione dei contenuti. Il server licenze controlla che il client DRM che effettua la richiesta di licenza soddisfi i requisiti di versione prima di rilasciare una licenza. Il client DRM controlla anche la versione DRM nella licenza prima di riprodurre il contenuto. Questo controllo client è necessario nel caso di domini in cui una licenza può essere trasferita a un altro computer.

Una versione client DRM può essere identificata dagli attributi specificati nella tabella seguente:

| **Attributo** | **Valori supportati** | **Criteri di corrispondenza** | **Descrizione** |
|---|---|---|---|
| Ambiente | &quot;PC&quot;, &quot;PortingKit&quot; | Corrispondenza esatta | Identifica se il client è in esecuzione su un Desktop o su qualsiasi altro dispositivo. |
| OS | &quot;Win&quot;, &quot;Mac&quot;, &quot;Linux&quot;, &quot;Android&quot;, &quot;iOS&quot;, &quot;ChromeOS&quot; | Corrispondenza esatta | Piattaforma |
| Architettura | &quot;32&quot;, &quot;64&quot; | Corrispondenza esatta | 32 bit o 64 bit |
| Tipo di schermo | &quot;PC&quot;, &quot;Mobile&quot;, &quot;TV&quot; | Corrispondenza esatta |  |
| Versione runtime | Numero di versione valido. Ad esempio, &quot;2.0.0&quot;, &quot;3.0&quot;, &quot;4.0&quot;, &quot;11.0&quot;, ecc. | Corrisponde se la versione client è minore o uguale alla versione specificata. | Il numero di versione è specificato come una combinazione di numeri e periodi (&quot;.&quot;) di qualsiasi lunghezza. |
| Versione libreria DRM | Numero di versione valido. Ad esempio, &quot;2.0.0&quot;. | Corrisponde se la versione client è minore o uguale alla versione specificata. | Il numero di versione è specificato come una combinazione di numeri e periodi (&quot;.&quot;) di qualsiasi lunghezza. |
| Fornitore OEM | Stringa fornitore OEM | Corrispondenza esatta | Stringa di identificazione del fornitore OEM per il dispositivo che utilizza il kit di portamento. |
| Modello | Stringa del modello. Ad esempio, &quot;iOS_Mobile&quot;, &quot;Android_Mobile&quot;, &quot;Chrome&quot;, &quot;ChromeOS_ARM&quot;, &quot;WindowsOnARM&quot;, &quot;AVE&quot; | Corrispondenza esatta | Stringa di identificazione del modello di dispositivo per il dispositivo che utilizza il kit di portamento. |

>[!NOTE]
>
>Quando si specifica una voce nell’elenco Bloccati, è possibile impostare valori per uno o più attributi menzionati nella tabella precedente. Qualsiasi attributo non specificato viene trattato come carattere jolly. Se il client DRM corrisponde a tutti i valori specificati in una voce di elenco Bloccati, è possibile che tale client non acceda al contenuto protetto.

