---
title: Elenco Bloccati di client DRM a cui è limitato l'accesso ai contenuti protetti
description: Elenco Bloccati di client DRM a cui è limitato l'accesso ai contenuti protetti
copied-description: true
exl-id: 74ddb5ed-4e68-4570-9cd5-bfc699609972
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---

# Elenco Bloccati di client DRM a cui è limitato l&#39;accesso ai contenuti protetti {#blocklist-of-drm-clients-restricted-from-accessing-protected-content}

**Adobe Accesso alle versioni del modulo DRM con restrizioni per l’accesso al contenuto protetto.**

Specifica il client DRM che non può accedere al contenuto. Specificato dalla piattaforma e dalla versione client DRM.

Caso d’uso di esempio: in caso di violazione della sicurezza, è possibile specificare una versione più recente del client DRM come versione minima richiesta per l’acquisizione della licenza e la riproduzione del contenuto. Prima di rilasciare una licenza, il server licenze controlla che il client DRM che effettua la richiesta di licenza soddisfi i requisiti di versione. Il client DRM controlla anche la versione DRM nella licenza prima di riprodurre il contenuto. Questo controllo client è richiesto nel caso di domini in cui una licenza può essere trasferita a un altro computer.

Una versione del client DRM può essere identificata dagli attributi specificati nella tabella seguente:

| **Attributo** | **Valori supportati** | **Corrispondenza criteri** | **Descrizione** |
|---|---|---|---|
| Ambiente | &quot;PC&quot;, &quot;PortingKit&quot; | Corrispondenza esatta | Identifica se il client è in esecuzione su un desktop o su qualsiasi altro dispositivo. |
| SO | &quot;Win&quot;, &quot;Mac&quot;, &quot;Linux&quot;, &quot;Android&quot;, &quot;iOS&quot;, &quot;ChromeOS&quot; | Corrispondenza esatta | Piattaforma |
| Architettura | “32”, “64” | Corrispondenza esatta | 32 bit o 64 bit |
| Tipo di schermo | &quot;PC&quot;, &quot;Mobile&quot;, &quot;TV&quot; | Corrispondenza esatta |  |
| Versione runtime | Numero di versione valido. Ad esempio, &quot;2.0.0&quot;, &quot;3.0&quot;, &quot;4.0&quot;, &quot;11.0&quot;, ecc. | Restituisce un risultato se la versione del client è minore o uguale alla versione specificata. | Il numero di versione viene specificato come combinazione di numeri e periodi (&quot;.&quot;) di qualsiasi lunghezza. |
| Versione libreria DRM | Numero di versione valido. Ad esempio, &quot;2.0.0&quot;. | Restituisce un risultato se la versione del client è minore o uguale alla versione specificata. | Il numero di versione viene specificato come combinazione di numeri e periodi (&quot;.&quot;) di qualsiasi lunghezza. |
| Fornitore OEM | Stringa fornitore OEM | Corrispondenza esatta | Stringa di identificazione del fornitore OEM per il dispositivo che utilizza il kit di portabilità. |
| Modello | Stringa modello. Ad esempio, &quot;iOS_Mobile&quot;, &quot;Android_Mobile&quot;, &quot;Chrome&quot;, &quot;ChromeOS_ARM&quot;, &quot;WindowsOnARM&quot;, &quot;AVE&quot; | Corrispondenza esatta | Stringa di identificazione del modello di dispositivo per il dispositivo che utilizza il kit di porta. |

>[!NOTE]
>
>Quando si specifica una voce nell’elenco Bloccati, è possibile impostare valori per uno o più attributi menzionati nella tabella precedente. Qualsiasi attributo non specificato viene considerato come carattere jolly. Se il client DRM corrisponde a tutti i valori specificati in una voce di elenco Bloccati, è possibile che il client non acceda al contenuto protetto.
