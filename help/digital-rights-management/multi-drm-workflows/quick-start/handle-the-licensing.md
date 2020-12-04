---
description: La licenza è il meccanismo principale mediante il quale gli utenti possono o meno riprodurre contenuti video protetti. A un utente legittimo (autorizzato) può essere rilasciata una licenza (una chiave) per decifrare e riprodurre uno specifico elemento del contenuto crittografato del suo fornitore di contenuti.
seo-description: La licenza è il meccanismo principale mediante il quale gli utenti possono o meno riprodurre contenuti video protetti. A un utente legittimo (autorizzato) può essere rilasciata una licenza (una chiave) per decifrare e riprodurre uno specifico elemento del contenuto crittografato del suo fornitore di contenuti.
seo-title: Licenze
title: Licenze
uuid: 9f433d62-5609-4d88-95fd-c1e7c0f6aa75
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 0%

---


# Licensing{#licensing}

La licenza è il meccanismo principale mediante il quale gli utenti possono o meno riprodurre contenuti video protetti. A un utente legittimo (autorizzato) può essere rilasciata una licenza (una chiave) per decifrare e riprodurre uno specifico elemento del contenuto crittografato del suo fornitore di contenuti.

Prima che l&#39;app o la pagina Web sul dispositivo dell&#39;utente finale possa riprodurre contenuto protetto da DRM, l&#39;app deve acquisire un token da un server di adesione o storefront che l&#39;utente, il cliente, utilizza.  Adobe fornisce un server di riferimento di esempio a tal fine: [Server di riferimento: Esempio di ExpressPlay Entitlement Server (SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md).

L&#39;adesione o il server di storefront richiederà un token di licenza dal server ExpressPlay interessato, solo dopo aver verificato con i propri sistemi back-end se l&#39;utente specifico ha diritto di visualizzare il contenuto richiesto. La risposta restituita dalla richiesta di token di licenza è un URL pronto per l’uso per il server licenze oppure contiene l’URL in una struttura JSON, a seconda della soluzione DRM con cui state lavorando.

>[!NOTE]
>
>Impossibile eseguire la richiesta del token di licenza dal client stesso:
>1. Le autorizzazioni devono essere verificate in un ambiente affidabile; e
>1. L&#39;autenticatore del cliente deve essere tenuto segreto.


1. Eseguite la richiesta del token di licenza.

   Per uno scenario di avvio rapido, in cui si desidera solo assicurarsi che i vari componenti coinvolti stiano funzionando insieme, è possibile utilizzare qualcosa come [!DNL curl] per effettuare la richiesta di token di licenza, (invece di ottenere inizialmente un&#39;app attiva e in esecuzione e testare le chiamate da lì). Ad esempio:

   * Widevine:

   ```
   curl "https://wv-gen.test.expressplay.com/hms/wv/token?customerAuthenticator= 
   <Customer Authenticator> 
   &kid 
   <indexterm>
   CEKSID 
     <indexterm>
     as query parameter kid 
    <indexterm>
    Widevine 
    </indexterm> 
    </indexterm> 
    </indexterm>=<CEKSID> 
      &contentKey 
    <indexterm>
    CEK 
    <indexterm>
    as query parameter contentKey 
    <indexterm>
    Widevine 
    </indexterm> 
    </indexterm> 
    </indexterm>=<CEK> 
      &<Any additional licensing attributes desired>" >>WidevineToken 
   ```

   Token di test Widevine di esempio:

   ```
   https://wv.test.expressplay.com/widevine/RightsManager.asmx?ExpressPlayToken= 
      AQAAAJJ2Y0MAAABQbyvnJ6KgEg_w-2yZmU-MsjTEZ3f7UkhUcFhDFAvdonzBk 
      RGQU-xe1G-DMbel5-BVH_PozovdWhKZx0_SXRokfh9-FERmBl6OEfGfPqMI1e 
      O1PqRkx59Q2q1s2cFNrqfml8Y3RQ 
   ```

   La risposta Widevine è una stringa URL &quot;pronta per l’uso&quot;.

   * PlayReady:

   ```
   curl "https://pr-gen.test.expressplay.com/hms/pr/token?customerAuthenticator= 
   <Customer Authenticator> 
      &kid 
   <indexterm>
   CEKSID 
   <indexterm>
   as query parameter kid 
   <indexterm>
    PlayReady 
   </indexterm> 
   </indexterm> 
   </indexterm>=<Key ID> 
      &contentKey 
   <indexterm>
    CEK 
    <indexterm>
    as query parameter contentKey 
    <indexterm>
    PlayReady 
   </indexterm> 
   </indexterm> 
   </indexterm>=<CEK> 
      &<Any additional licensing attributes desired>" >>playreadyToken
   ```

   Token di test PlayReady di esempio:

   ```
   {"licenseAcquisitionUrl":"https://pr.test.expressplay.com/playready/RightsManager.asmx", 
   "token":"AQAAAxBbWv4AAABgV8_GaWjU80mObLQdfwEdy1lenXmcqvx5VLyqixigtwXLthzjPxq9QDT-TYbudNrMSOpUAy 
   G_2Qt8RdTGJ2_Q_xtRfnj7H6C-yt6By40IhNaSQ0nNYUsY1_MtCrHXIltlVhN2Ekr_RNyTNvCjYs0V5TqzOPY"} 
   ```

   La risposta PlayReady è un oggetto JSON, con elementi URL e token separati.

   * FairPlay:

   ```
   curl "https://fp-gen.test.expressplay.com/hms/fp/token?customerAuthenticator= 
    <Customer Authenticator> 
    &kid 
    <indexterm>
      CEKSID 
    <indexterm>
      as query parameter kid 
      <indexterm>
        FairPlay 
      </indexterm> 
    </indexterm> 
    </indexterm>=<Key ID> 
          &contentKey 
    <indexterm>
      CEK 
    <indexterm>
      as query parameter contentKey 
      <indexterm>
        FairPlay 
      </indexterm> 
    </indexterm> 
    </indexterm>=<CEK> 
    &iv=<IV ID> 
    &<Any additional licensing attributes desired>"
   ```

   Token test FairPlay di esempio:

   ```
   https://{expressplay_test_domain_license_url}/?ExpressPlayToken= 
   AQAAAJJ2Y0MAAABQbyvnJ6KgEg_w-2yZmU-MsjTEZ3f7UkhUcFhDFAvdonzBk 
   RGQU-xe1G-DMbel5-BVH_PozovdWhKZx0_SXRokfh9-FERmBl6OEfGfPqMI1e 
   O1PqRkx59Q2q1s2cFNrqfml8Y3RQ
   ```

   La risposta FairPlay è una stringa URL &quot;pronta per l’uso&quot;.
