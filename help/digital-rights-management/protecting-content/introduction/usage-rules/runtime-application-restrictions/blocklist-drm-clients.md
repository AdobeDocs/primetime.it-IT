---
description: 'null'
seo-description: 'null'
seo-title: ' Elenco Bloccati di client DRM con restrizioni all''accesso al contenuto protetto'
title: ' Elenco Bloccati di client DRM con restrizioni all''accesso al contenuto protetto'
uuid: 38bc024e-0c5b-4c1c-8d4b-94b9e0fec67e
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


#  Elenco Bloccati di client DRM non autorizzati ad accedere al contenuto protetto {#blocklist-of-drm-clients-restricted-from-accessing-protected-content}

Questo elenco Bloccati  specifica i client DRM Primetime che non possono accedere al contenuto protetto.  client di elenco Bloccati per versione client e piattaforma.

Esempio di utilizzo: In caso di violazione della sicurezza, una versione più recente del client DRM Primetime può essere specificata come versione minima richiesta per l&#39;acquisizione della licenza e la riproduzione del contenuto. Il server licenze verifica che il client DRM Primetime che effettua la richiesta di licenza soddisfi i requisiti di versione prima di rilasciare una licenza. Il client DRM Primetime controlla anche la versione della licenza prima di riprodurre il contenuto. Questo controllo client è richiesto per i domini in cui una licenza può essere trasferita a un altro computer.

Una versione client DRM Primetime può essere identificata dagli attributi specificati nella tabella seguente:

| **Attributo** | **Valori supportati** | **Criteri di corrispondenza** | **Descrizione** |
|---|---|---|---|
| Ambiente | `“PC”, “PortingKit”` | Corrispondenza esatta | Identifica se il client è in esecuzione su un desktop o su un altro dispositivo. |
| OS | `“Win”, “Mac”, “Linux”, “Android”, “iOS”, "ChromeOS"` | Corrispondenza esatta | Piattaforma |
| Architettura | `“32”, “64”` | Corrispondenza esatta | 32 bit o 64 bit |
| Tipo di schermo | `“PC”, “Mobile”, “TV”` | Corrispondenza esatta |  |
| Versione runtime | Un numero di versione valido. Ad esempio, `“2.0.0”, "3.0", "4.0", "11.0"`, ecc. | Corrisponde se la versione client è minore o uguale alla versione specificata. | Il numero di versione è specificato come combinazione di numeri e punti (&quot;.&quot;) di qualsiasi lunghezza. |
| Versione libreria DRM di Primetime | Un numero di versione valido. Ad esempio, `“2.0.0”`. | Corrisponde se la versione client è minore o uguale alla versione specificata. | Il numero di versione è specificato come combinazione di numeri e punti (&quot;.&quot;) di qualsiasi lunghezza. |
| Fornitore OEM | Stringa Fornitore OEM che può essere individuata nel certificato Runtime emesso per un cliente che ha portato DRM Primetime a un dispositivo. | Corrispondenza esatta | Stringa di identificazione del fornitore OEM per il dispositivo che utilizza il kit di porta. |
| Modello | Stringa del modello che può essere individuata nel certificato Runtime emesso per un cliente che ha trasferito Primetime DRM a un dispositivo. Ad esempio: `"iOS_Mobile", "Android_Mobile", "Chrome", "ChromeOS_ARM", "WindowsOnARM", "AVE"` | Corrispondenza esatta | Stringa di identificazione del modello di dispositivo per il dispositivo che utilizza il kit di portamento. |

>[!NOTE]
>
>Quando si specifica una voce nel elenco Bloccati , è possibile impostare i valori per uno o più degli attributi indicati nella tabella precedente. Qualsiasi attributo non specificato viene trattato come carattere jolly. Se il client DRM Primetime corrisponde a tutti i valori specificati in una voce di elenco Bloccati , il client potrebbe non essere in grado di accedere al contenuto protetto.

