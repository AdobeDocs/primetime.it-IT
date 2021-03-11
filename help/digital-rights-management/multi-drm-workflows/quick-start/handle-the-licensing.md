---
description: La concessione di licenze è il meccanismo principale tramite il quale gli utenti possono o meno riprodurre contenuti video protetti. A un utente legittimo (autorizzato) può essere rilasciata una licenza (una chiave) per decrittografare e riprodurre un elemento specifico del contenuto crittografato del proprio fornitore di contenuti.
title: Licenze
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---


# Licenze{#licensing}

La concessione di licenze è il meccanismo principale tramite il quale gli utenti possono o meno riprodurre contenuti video protetti. A un utente legittimo (autorizzato) può essere rilasciata una licenza (una chiave) per decrittografare e riprodurre un elemento specifico del contenuto crittografato del proprio fornitore di contenuti.

Prima che l&#39;app o la pagina web sul dispositivo di un utente finale possa riprodurre contenuto protetto da DRM, deve acquisire un token da un server di adesione o vetrina utilizzato dal cliente. Adobe fornisce un esempio di server di riferimento a questo scopo: [Server di riferimento: Esempio di ExpressPlay Entitlement Server (SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md).

L&#39;adesione o il server di vetrina richiederà un token di licenza al relativo server ExpressPlay Server, solo dopo aver verificato con i propri sistemi back-end se l&#39;utente specifico è autorizzato a guardare il contenuto richiesto. La risposta restituita dalla richiesta di token di licenza è un URL pronto all’uso per il server licenze o la risposta contiene l’URL in una struttura JSON, a seconda della soluzione DRM con cui stai lavorando.

>[!NOTE]
>
>Impossibile effettuare la richiesta del token di licenza dal client stesso:
>1. I diritti devono essere controllati in un ambiente affidabile; e
>1. L&#39;autenticatore del cliente deve essere tenuto segreto.


1. Effettua la richiesta del token di licenza.

   Per uno scenario di avvio rapido, in cui desideri semplicemente assicurarti che i vari componenti coinvolti lavorino insieme, puoi utilizzare qualcosa come [!DNL curl] per effettuare la richiesta del token di licenza (invece di ottenere inizialmente un&#39;app attiva e in esecuzione e testare le chiamate da lì). Ad esempio:

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

   Token di prova Widevine di esempio:

   ```
   https://wv.test.expressplay.com/widevine/RightsManager.asmx?ExpressPlayToken= 
      AQAAAJJ2Y0MAAABQbyvnJ6KgEg_w-2yZmU-MsjTEZ3f7UkhUcFhDFAvdonzBk 
      RGQU-xe1G-DMbel5-BVH_PozovdWhKZx0_SXRokfh9-FERmBl6OEfGfPqMI1e 
      O1PqRkx59Q2q1s2cFNrqfml8Y3RQ 
   ```

   La risposta Widevine è una stringa URL &quot;pronta all’uso&quot;.

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

   Token di prova PlayReady di esempio:

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

   Token di test FairPlay di esempio:

   ```
   https://{expressplay_test_domain_license_url}/?ExpressPlayToken= 
   AQAAAJJ2Y0MAAABQbyvnJ6KgEg_w-2yZmU-MsjTEZ3f7UkhUcFhDFAvdonzBk 
   RGQU-xe1G-DMbel5-BVH_PozovdWhKZx0_SXRokfh9-FERmBl6OEfGfPqMI1e 
   O1PqRkx59Q2q1s2cFNrqfml8Y3RQ
   ```

   La risposta FairPlay è una stringa URL &quot;pronta all’uso&quot;.
