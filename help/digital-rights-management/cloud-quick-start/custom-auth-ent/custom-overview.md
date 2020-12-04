---
seo-title: Panoramica dell'autenticazione/adesione personalizzata (facoltativo)
title: Panoramica dell'autenticazione/adesione personalizzata (facoltativo)
uuid: 8b5e38a5-562c-4781-ac40-4b3d6cdd97fe
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---


# Panoramica dell&#39;autenticazione/adesione personalizzata (facoltativo){#custom-authentication-entitlement-overview-optional}

È possibile configurare DRM di Primetime Cloud per contattare il servizio di autenticazione/adesione back-end per determinare:

* A questo utente è consentito acquisire una licenza?
* Quali diritti/restrizioni devono essere inclusi nella licenza?

Primetime Cloud DRM include un&#39;implementazione di riferimento di un servizio di adesione/autenticazione back-end. A scopo dimostrativo, questo server sta emettendo risposte &quot;consenti&quot; alle richieste BEES. Vedere [!DNL BEESServlet.java] per modificare il comportamento del server.

>[!NOTE]
>
>Precedentemente, si trattava di un prodotto separato denominato *Back End Entitlement Server* (BEES), quindi i riferimenti a BEES in tutto il documento e nei file sorgente.

