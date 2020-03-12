---
description: In genere, tutte le licenze DRM di Primetime, al momento della creazione, sono associate a un dispositivo univoco. Questo binding impedisce agli utenti di condividere le licenze tra diversi dispositivi senza autorizzazione. Oltre al binding per dispositivo, Primetime DRM consente di eseguire il binding delle licenze a un dominio dispositivo o a un gruppo di dispositivi.
seo-description: In genere, tutte le licenze DRM di Primetime, al momento della creazione, sono associate a un dispositivo univoco. Questo binding impedisce agli utenti di condividere le licenze tra diversi dispositivi senza autorizzazione. Oltre al binding per dispositivo, Primetime DRM consente di eseguire il binding delle licenze a un dominio dispositivo o a un gruppo di dispositivi.
seo-title: Riproduci contenuto crittografato mediante il supporto del dominio
title: Riproduci contenuto crittografato mediante il supporto del dominio
uuid: 8854cc0f-9bfc-4833-82d7-a3f46ac88e06
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# Supporto del dominio dispositivo {#device-domain-support}

In genere, tutte le licenze DRM di Primetime, al momento della creazione, sono associate a un dispositivo univoco. Questo binding impedisce agli utenti di condividere le licenze tra diversi dispositivi senza autorizzazione. Oltre al binding per dispositivo, Primetime DRM consente di eseguire il binding delle licenze a un dominio dispositivo o a un gruppo di dispositivi.

Se i metadati del contenuto specificano che è necessaria la registrazione del dominio del dispositivo, l&#39;applicazione può richiamare un&#39;API per partecipare a un gruppo di dispositivi. Questa azione attiva una richiesta di registrazione del dominio da inviare al server del dominio. Una volta rilasciata una licenza a un gruppo di dispositivi, la licenza può essere esportata e condivisa con altri dispositivi che hanno aderito al gruppo di dispositivi.

Le informazioni sul gruppo di dispositivi vengono quindi utilizzate nell&#39; `DRMContentData` `VoucherAccessInfo` oggetto, che verrà quindi utilizzato per presentare le informazioni necessarie per recuperare e utilizzare con successo una licenza.

## Riproduci contenuto crittografato mediante il supporto del dominio {#play-encrypted-content-using-domain-support}

Per riprodurre contenuto crittografato con Primetime DRM, eseguire le operazioni seguenti:

1. Utilizzando `VoucherAccessInfo.deviceGroup`, verificate che sia necessaria la registrazione al gruppo di dispositivi.
1. Se è richiesta l&#39;autenticazione:
   1. Utilizzate la `DeviceGroupInfo.authenticationMethod` proprietà per verificare se è necessaria l&#39;autenticazione.
   1. Se è richiesta l&#39;autenticazione, autenticare l&#39;utente eseguendo una delle operazioni seguenti:

      * Ottenete il nome utente e la password dell&#39;utente e richiamate `DRMManager.authenticate(deviceGroup.serverURL, deviceGroup.domain, username, password)`.
      * Ottenete un token di autenticazione memorizzato nella cache/pre-generato e richiamate `DRMManager.setAuthenticationToken()`.
   1. Richiama `DRMManager.addToDeviceGroup()`
1. Ottenete la licenza per il contenuto eseguendo una delle seguenti operazioni:
   1. Utilizzare il `DRMManager.loadVoucher()` metodo.
   1. Ottenere la licenza da un dispositivo diverso registrato nello stesso gruppo di dispositivi e fornire la licenza al ` DRMManager` tramite il `DRMManager.storeVoucher()` metodo.
1. Riprodurre il contenuto crittografato utilizzando il `Primetime.play()` metodo .
Per esportare la licenza per il contenuto, uno qualsiasi dei dispositivi può fornire i byte non elaborati della licenza utilizzando il `DRMVoucher.toByteArray()` metodo dopo aver ottenuto la licenza dal server licenze DRM Primetime. Generalmente, i fornitori di contenuti limitano il numero di dispositivi in un gruppo di dispositivi. Se viene raggiunto il limite, potrebbe essere necessario chiamare il `DRMManager.removeFromDeviceGroup()` metodo su un dispositivo inutilizzato prima di registrare il dispositivo corrente.