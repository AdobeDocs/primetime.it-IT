---
seo-title: Distribuzione di chiavi iOS in remoto e locale
title: Distribuzione di chiavi iOS in remoto e locale
uuid: 90f672e7-9301-4e14-adca-db2a8f951a83
translation-type: tm+mt
source-git-commit: 53654b740b03c6a79394d30704a41186d4655237

---


# Distribuzione di chiavi iOS in remoto e locale {#remote-and-local-ios-key-delivery}

Adobe Primetime supporta le seguenti opzioni per la consegna di chiavi ai client iOS:

* **Remote** - Esegue le operazioni specificate nella specifica HTTP Live Streaming (HLS); il manifesto M3U8 specifica un percorso HTTPS che include una chiave AES da utilizzare per decrittografare i seguenti segmenti crittografati nel flusso. Quando si specifica `Remote` nel criterio DRM di Primetime, il dispositivo client deve connettersi a un server HTTPS remoto per ottenere una chiave AES.

* **Locale** - Quando si specifica `Local` in DRM di Primetime invece di connettersi a Internet/rete per la chiave AES, un server HTTPS locale viene incorporato nell&#39;applicazione iOS, che gestisce quindi tutte le richieste di chiave AES. Il server HTTPS incorporato viene automaticamente configurato e configurato nell&#39;applicazione P. Lo sviluppatore dell&#39;applicazione non richiede alcun intervento.

La consegna delle chiavi remote è abilitata tramite il criterio DRM di Primetime utilizzato per creare pacchetti di contenuto. Se desiderate modificare questa impostazione, dovete creare nuovamente un pacchetto per il contenuto. Se si abilita la consegna di chiavi remote, è necessario distribuire un server chiavi DRM Primetime che possa gestire le richieste chiave dai client iOS. Tuttavia, non viene apportata alcuna modifica al flusso di lavoro per i client su altre piattaforme.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>La selezione della consegna chiave interessa solo i client iOS. Tutti gli altri dispositivi che utilizzano contenuto HLS, ad esempio Android e Primetime on Desktop (Flash Player), utilizzano sempre la `Local` consegna delle chiavi, anche se `Remote` è stato specificato.

