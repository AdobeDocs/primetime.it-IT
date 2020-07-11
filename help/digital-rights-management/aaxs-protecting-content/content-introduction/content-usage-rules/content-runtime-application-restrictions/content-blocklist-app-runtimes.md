---
seo-title: ' Elenco Bloccati di runtime dell''applicazione non è consentito l''accesso al contenuto protetto'
title: ' Elenco Bloccati di runtime dell''applicazione non è consentito l''accesso al contenuto protetto'
uuid: 462a2c09-b335-4768-bd0e-1359db169d69
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


#  Elenco Bloccati di runtime dell&#39;applicazione non è consentito l&#39;accesso al contenuto protetto {#blocklist-of-application-runtimes-restricted-from-accessing-protected-content}

Specifica la versione di Primetime o Flash Runtime che non può accedere al contenuto. Specificate il runtime limitato (Flash Player, AIR o iOS), la piattaforma e la versione.

Esempio di utilizzo: Analogamente al elenco Bloccati di  DRM Client, l&#39;ultima versione dei runtime Flash Player, AIR o iOS può essere specificata come versione minima richiesta per l&#39;acquisizione della licenza e la riproduzione di contenuto.

Il runtime dell&#39;applicazione può essere identificato da uno degli attributi supportati per le versioni client DRM, oltre ai seguenti attributi:

| **Attributo** | **Valori supportati** | **Criteri di corrispondenza** | **Descrizione** |
|---|---|---|---|
| Applicazione | &quot;FlashPlayer&quot;, &quot;AIR&quot;, &quot;DRM_Library&quot;, &quot;AVE&quot; | Corrispondenza esatta | Identifica il nome del runtime dell&#39;applicazione. |
