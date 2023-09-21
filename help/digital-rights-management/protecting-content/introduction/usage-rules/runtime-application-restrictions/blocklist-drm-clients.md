---
title: Elenco Bloccati di client DRM a cui è limitato l'accesso ai contenuti protetti
description: Elenco Bloccati di client DRM a cui è limitato l'accesso ai contenuti protetti
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Elenco Bloccati di client DRM a cui è limitato l&#39;accesso ai contenuti protetti {#blocklist-of-drm-clients-restricted-from-accessing-protected-content}

Questo elenco Bloccati specifica i client DRM Primetime che non possono accedere al contenuto protetto. I client vengono elenchi Bloccati per versione client e piattaforma.

Caso d’uso di esempio: in caso di violazione della sicurezza, è possibile specificare una versione più recente del client DRM di Primetime come versione minima richiesta per l’acquisizione della licenza e la riproduzione del contenuto. Prima di rilasciare una licenza, il server licenze controlla che il client DRM Primetime che effettua la richiesta di licenza soddisfi i requisiti di versione. Il client DRM di Primetime controlla anche la versione nella licenza prima di riprodurre il contenuto. Questo controllo client è richiesto nel caso di domini in cui una licenza può essere trasferita a un altro computer.

Una versione client DRM di Primetime può essere identificata dagli attributi specificati nella tabella seguente:

| **Attributo** | **Valori supportati** | **Corrispondenza criteri** | **Descrizione** |
|---|---|---|---|
| Ambiente | `“PC”, “PortingKit”` | Corrispondenza esatta | Identifica se il client è in esecuzione su un desktop o su qualsiasi altro dispositivo. |
| SO | `“Win”, “Mac”, “Linux”, “Android”, “iOS”, "ChromeOS"` | Corrispondenza esatta | Piattaforma |
| Architettura | `“32”, “64”` | Corrispondenza esatta | 32 bit o 64 bit |
| Tipo di schermo | `“PC”, “Mobile”, “TV”` | Corrispondenza esatta | |
| Versione runtime | Numero di versione valido. Ad esempio: `“2.0.0”, "3.0", "4.0", "11.0"`, ecc. | Restituisce un risultato se la versione del client è minore o uguale alla versione specificata. | Il numero di versione viene specificato come combinazione di numeri e periodi (&quot;.&quot;) di qualsiasi lunghezza. |
| Versione libreria DRM Primetime | Numero di versione valido. Ad esempio: `“2.0.0”`. | Restituisce un risultato se la versione del client è minore o uguale alla versione specificata. | Il numero di versione viene specificato come combinazione di numeri e periodi (&quot;.&quot;) di qualsiasi lunghezza. |
| Fornitore OEM | Stringa del fornitore OEM che può trovarsi nel certificato di runtime rilasciato a un cliente che ha eseguito il porting di Primetime DRM su un dispositivo. | Corrispondenza esatta | Stringa di identificazione del fornitore OEM per il dispositivo che utilizza il kit di portabilità. |
| Modello | Stringa di modello che può trovarsi nel certificato di runtime rilasciato a un cliente che ha eseguito il porting di Primetime DRM su un dispositivo. Ad esempio: `"iOS_Mobile", "Android_Mobile", "Chrome", "ChromeOS_ARM", "WindowsOnARM", "AVE"` | Corrispondenza esatta | Stringa di identificazione del modello di dispositivo per il dispositivo che utilizza il kit di porta. |

>[!NOTE]
>
>Quando si specifica una voce nell&#39;elenco Bloccati, è possibile impostare i valori per uno o più attributi indicati nella tabella precedente. Qualsiasi attributo non specificato viene considerato come carattere jolly. Se il client DRM Primetime corrisponde a tutti i valori specificati in una voce di elenco Bloccati, è possibile che il client non acceda al contenuto protetto.
