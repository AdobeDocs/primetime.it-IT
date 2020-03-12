---
seo-title: Consegna chiavi iOS locale e remota
title: Consegna chiavi iOS locale e remota
uuid: 3c20b1d1-f842-438a-ae3a-4ec31da306ad
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Consegna chiavi iOS locale e remota{#remote-and-local-ios-key-delivery}

Adobe Primetime supporta due opzioni per la consegna di chiavi ai client iOS:

* Remoto - Esattamente come specificato nella specifica HLS, il manifesto M3U8 specifica un percorso HTTPS contenente una chiave AES che deve essere utilizzata per decrittografare i segmenti crittografati seguenti nel flusso. Quando si specifica &quot;Remote&quot;, il dispositivo client si collegherà a un server HTTPS remoto per recuperare la chiave AES.
* Locale - Quando si specifica &quot;Local&quot;, invece di connettersi a Internet/rete per la chiave AES, nell&#39;applicazione iOS viene incorporato un server HTTPS locale che gestirà tutte le richieste di chiave AES. Il server HTTPS incorporato viene configurato e configurato automaticamente nell&#39;applicazione Primetime. Lo sviluppatore dell&#39;applicazione non richiede alcun intervento.

La distribuzione delle chiavi remote è abilitata tramite il criterio utilizzato per creare pacchetti di contenuto (la modifica di questa impostazione richiede il ricompilamento del contenuto). Quando la distribuzione delle chiavi remote è abilitata, è necessario distribuire un server di chiavi di Adobe Access per gestire le richieste chiave dei client iOS, ma non si verificano modifiche al flusso di lavoro per i client su altre piattaforme.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>La selezione della consegna chiave interessa solo i client iOS. Tutti gli altri dispositivi che utilizzano contenuto HLS utilizzeranno sempre la chiave &quot;Local&quot;, anche se è stato specificato &quot;Remote&quot;.

Per ulteriori informazioni, vedere *Utilizzo di Adobe Access Key Server*.
