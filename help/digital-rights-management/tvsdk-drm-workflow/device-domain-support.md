---
description: In genere, tutte le licenze DRM di Primetime, al momento della creazione, sono associate a un dispositivo univoco. Questo binding impedisce agli utenti di condividere licenze tra dispositivi diversi senza autorizzazione. Oltre al binding per dispositivo, Primetime DRM consente di associare le licenze a un dominio dispositivo o a un gruppo di dispositivi.
title: Riproduci contenuto crittografato utilizzando il supporto del dominio
exl-id: 3c9badfc-046b-4c56-bde1-7b3b708bfaa2
source-git-commit: 59f7f8aa82be59c4012ee80648032600590bc4e1
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Supporto del dominio dispositivo {#device-domain-support}

In genere, tutte le licenze DRM di Primetime, al momento della creazione, sono associate a un dispositivo univoco. Questo binding impedisce agli utenti di condividere licenze tra dispositivi diversi senza autorizzazione. Oltre al binding per dispositivo, Primetime DRM consente di associare le licenze a un dominio dispositivo o a un gruppo di dispositivi.

Se i metadati del contenuto specificano che è necessaria la registrazione del dominio del dispositivo, l’applicazione può richiamare un’API per partecipare a un gruppo di dispositivi. Questa azione attiva una richiesta di registrazione del dominio da inviare al server di dominio. Una volta rilasciata una licenza a un gruppo di dispositivi, la licenza può essere esportata e condivisa con altri dispositivi che sono stati aggiunti al gruppo di dispositivi.

Le informazioni sul gruppo di dispositivi vengono quindi utilizzate nel `DRMContentData` `VoucherAccessInfo` , che verrà quindi utilizzato per presentare le informazioni necessarie per recuperare e utilizzare correttamente una licenza.

## Riproduci contenuto crittografato utilizzando il supporto del dominio {#play-encrypted-content-using-domain-support}

Per riprodurre contenuto crittografato con Primetime DRM, effettuare le seguenti operazioni:

1. Utilizzo di `VoucherAccessInfo.deviceGroup`, verifica se è richiesta la registrazione del gruppo di dispositivi.
1. Se è richiesta l’autenticazione:
   1. Utilizza il `DeviceGroupInfo.authenticationMethod` proprietà scopri se è richiesta l’autenticazione.
   1. Se è richiesta l’autenticazione, autentica l’utente eseguendo UNA delle seguenti operazioni:

      * Ottenere il nome utente e la password dell&#39;utente e richiamare `DRMManager.authenticate(deviceGroup.serverURL, deviceGroup.domain, username, password)`.
      * Ottieni un token di autenticazione memorizzato nella cache/pregenerato e richiama `DRMManager.setAuthenticationToken()`.
   1. Richiama `DRMManager.addToDeviceGroup()`
1. Ottenere la licenza per il contenuto eseguendo una delle attività seguenti:
   1. Utilizza il `DRMManager.loadVoucher()` metodo.
   1. Ottenere la licenza da un dispositivo diverso registrato nello stesso gruppo di dispositivi e fornire la licenza al `DRMManager` tramite `DRMManager.storeVoucher()` metodo.
1. Riproduci il contenuto crittografato utilizzando `Primetime.play()` metodo.
Per esportare la licenza per il contenuto, qualsiasi periferica può fornire i byte non elaborati della licenza utilizzando `DRMVoucher.toByteArray()` dopo aver ottenuto la licenza dal server licenze DRM Primetime. In genere, i provider di contenuti limitano il numero di dispositivi in un gruppo di dispositivi. Se il limite viene raggiunto, potrebbe essere necessario chiamare il `DRMManager.removeFromDeviceGroup()` su un dispositivo inutilizzato prima di registrare il dispositivo corrente.
