---
title: Elenco Bloccati di client DRM con restrizioni all'accesso a contenuti protetti
description: Elenco Bloccati di client DRM con restrizioni all'accesso a contenuti protetti
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---


# Elenco Bloccati di client DRM con restrizioni all&#39;accesso a contenuti protetti {#blocklist-of-drm-clients-restricted-from-accessing-protected-content}

Questo elenco Bloccati specifica i client DRM di Primetime che non possono accedere al contenuto protetto. elenco Bloccati di client per versione client e piattaforma.

Esempio di utilizzo: In caso di violazione della sicurezza, è possibile specificare una versione più recente del client DRM Primetime come versione minima richiesta per l&#39;acquisizione della licenza e la riproduzione dei contenuti. Il server licenze controlla che il client DRM Primetime che effettua la richiesta di licenza soddisfi i requisiti di versione prima di rilasciare una licenza. Il client DRM di Primetime controlla anche la versione della licenza prima di riprodurre il contenuto. Questo controllo client è necessario nel caso di domini in cui una licenza può essere trasferita a un altro computer.

Una versione client DRM di Primetime può essere identificata dagli attributi specificati nella tabella seguente:

| **Attributo** | **Valori supportati** | **Criteri di corrispondenza** | **Descrizione** |
|---|---|---|---|
| Ambiente | `“PC”, “PortingKit”` | Corrispondenza esatta | Identifica se il client è in esecuzione su un Desktop o su qualsiasi altro dispositivo. |
| OS | `“Win”, “Mac”, “Linux”, “Android”, “iOS”, "ChromeOS"` | Corrispondenza esatta | Piattaforma |
| Architettura | `“32”, “64”` | Corrispondenza esatta | 32 bit o 64 bit |
| Tipo di schermo | `“PC”, “Mobile”, “TV”` | Corrispondenza esatta |  |
| Versione runtime | Numero di versione valido. Ad esempio, `“2.0.0”, "3.0", "4.0", "11.0"`, ecc. | Corrisponde se la versione client è minore o uguale alla versione specificata. | Il numero di versione è specificato come una combinazione di numeri e periodi (&quot;.&quot;) di qualsiasi lunghezza. |
| Versione libreria DRM di Primetime | Numero di versione valido. Ad esempio, `“2.0.0”`. | Corrisponde se la versione client è minore o uguale alla versione specificata. | Il numero di versione è specificato come una combinazione di numeri e periodi (&quot;.&quot;) di qualsiasi lunghezza. |
| Fornitore OEM | Stringa del fornitore OEM che può essere situata nel certificato runtime rilasciato a un cliente che ha trasferito DRM di Primetime a un dispositivo. | Corrispondenza esatta | Stringa di identificazione del fornitore OEM per il dispositivo che utilizza il kit di portamento. |
| Modello | Stringa del modello che può essere situata nel certificato runtime rilasciato a un cliente che ha trasferito DRM di Primetime a un dispositivo. Ad esempio: `"iOS_Mobile", "Android_Mobile", "Chrome", "ChromeOS_ARM", "WindowsOnARM", "AVE"` | Corrispondenza esatta | Stringa di identificazione del modello di dispositivo per il dispositivo che utilizza il kit di portamento. |

>[!NOTE]
>
>Quando si specifica una voce nell’elenco Bloccati, è possibile impostare valori per uno o più attributi menzionati nella tabella precedente. Qualsiasi attributo non specificato viene trattato come carattere jolly. Se il client DRM di Primetime corrisponde a tutti i valori specificati in una voce di elenco Bloccati, è possibile che tale client non acceda al contenuto protetto.

