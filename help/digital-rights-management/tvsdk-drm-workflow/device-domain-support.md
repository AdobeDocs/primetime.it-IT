---
description: In genere, tutte le licenze DRM di Primetime, al momento della creazione, sono associate a un dispositivo univoco. Questo binding impedisce agli utenti di condividere licenze tra diversi dispositivi senza autorizzazione. Oltre al binding per dispositivo, Primetime DRM consente di associare le licenze a un dominio dispositivo o a un gruppo di dispositivi.
title: Riprodurre contenuto crittografato utilizzando il supporto del dominio
exl-id: 3c9badfc-046b-4c56-bde1-7b3b708bfaa2
source-git-commit: 59f7f8aa82be59c4012ee80648032600590bc4e1
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Supporto del dominio del dispositivo {#device-domain-support}

In genere, tutte le licenze DRM di Primetime, al momento della creazione, sono associate a un dispositivo univoco. Questo binding impedisce agli utenti di condividere licenze tra diversi dispositivi senza autorizzazione. Oltre al binding per dispositivo, Primetime DRM consente di associare le licenze a un dominio dispositivo o a un gruppo di dispositivi.

Se i metadati del contenuto specificano che è richiesta la registrazione al dominio del dispositivo, l&#39;applicazione può richiamare un&#39;API per l&#39;iscrizione a un gruppo di dispositivi. Questa azione attiva l’invio di una richiesta di registrazione del dominio al server di dominio. Una volta rilasciata una licenza a un gruppo di dispositivi, la licenza può essere esportata e condivisa con altri dispositivi che hanno aderito al gruppo di dispositivi.

Le informazioni sul gruppo di dispositivi vengono quindi utilizzate nell&#39;oggetto `DRMContentData` `VoucherAccessInfo` , che verrà quindi utilizzato per presentare le informazioni necessarie per recuperare e utilizzare correttamente una licenza.

## Riprodurre contenuto crittografato utilizzando il supporto del dominio {#play-encrypted-content-using-domain-support}

Per riprodurre contenuto crittografato utilizzando DRM di Primetime , esegui le seguenti operazioni:

1. Utilizzando `VoucherAccessInfo.deviceGroup`, verifica se è richiesta la registrazione al gruppo di dispositivi.
1. Se è richiesta l’autenticazione:
   1. Utilizza la proprietà `DeviceGroupInfo.authenticationMethod` per scoprire se è necessaria l&#39;autenticazione.
   1. Se è richiesta l&#39;autenticazione, autenticare l&#39;utente eseguendo uno dei seguenti passaggi:

      * Ottieni il nome utente e la password dell&#39;utente e richiama `DRMManager.authenticate(deviceGroup.serverURL, deviceGroup.domain, username, password)`.
      * Ottieni un token di autenticazione memorizzato in cache/generato in precedenza e richiama `DRMManager.setAuthenticationToken()`.
   1. Richiama `DRMManager.addToDeviceGroup()`
1. Ottieni la licenza per il contenuto eseguendo una delle seguenti attività:
   1. Utilizzare il metodo `DRMManager.loadVoucher()`.
   1. Ottieni la licenza da un dispositivo diverso registrato nello stesso gruppo di dispositivi e fornisci la licenza al `DRMManager` tramite il metodo `DRMManager.storeVoucher()` .
1. Riproduci il contenuto crittografato utilizzando il metodo `Primetime.play()` .
Per esportare la licenza per il contenuto, uno qualsiasi dei dispositivi può fornire i byte non elaborati della licenza utilizzando il metodo `DRMVoucher.toByteArray()` dopo aver ottenuto la licenza dal server di licenze DRM di Primetime. In genere, i provider di contenuti limitano il numero di dispositivi in un gruppo di dispositivi. Se il limite viene raggiunto, potrebbe essere necessario chiamare il metodo `DRMManager.removeFromDeviceGroup()` su un dispositivo non utilizzato prima di registrare il dispositivo corrente.
