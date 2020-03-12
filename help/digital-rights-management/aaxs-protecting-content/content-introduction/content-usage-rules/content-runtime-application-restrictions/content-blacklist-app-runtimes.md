---
seo-title: Lista nera dei tempi di esecuzione delle applicazioni con restrizioni all'accesso al contenuto protetto
title: Lista nera dei tempi di esecuzione delle applicazioni con restrizioni all'accesso al contenuto protetto
uuid: 462a2c09-b335-4768-bd0e-1359db169d69
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Lista nera dei tempi di esecuzione delle applicazioni con restrizioni all&#39;accesso al contenuto protetto {#blacklist-of-application-runtimes-restricted-from-accessing-protected-content}

Specifica la versione di Primetime o Flash Runtime che non può accedere al contenuto. Specificate il runtime limitato (Flash Player, AIR o iOS), la piattaforma e la versione.

Esempio di utilizzo: Analogamente alla blacklist del client DRM, l&#39;ultima versione dei runtime Flash Player, AIR o iOS può essere specificata come versione minima richiesta per l&#39;acquisizione della licenza e la riproduzione dei contenuti.

Il runtime dell&#39;applicazione può essere identificato da uno degli attributi supportati per le versioni client DRM, oltre ai seguenti attributi:

| **Attributo** | **Valori supportati** | **Criteri di corrispondenza** | **Descrizione** |
|---|---|---|---|
| Applicazione | &quot;FlashPlayer&quot;, &quot;AIR&quot;, &quot;DRM_Library&quot;, &quot;AVE&quot; | Corrispondenza esatta | Identifica il nome del runtime dell&#39;applicazione. |

