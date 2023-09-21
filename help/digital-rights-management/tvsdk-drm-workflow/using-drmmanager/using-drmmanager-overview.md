---
title: Utilizzo della panoramica della classe DRMManager
description: Utilizzo della panoramica della classe DRMManager
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# Utilizzo della classe DRMManager {#using-the-drmmanager-class}

Utilizza il `DRMManager` classe per gestire le licenze e le sessioni del server licenze DRM Primetime nelle applicazioni.

**Gestione licenze**

Ogni volta che un dispositivo riproduce un contenuto protetto, il runtime ottiene e memorizza nella cache la licenza necessaria per visualizzarlo. Se l’applicazione salva il contenuto localmente e la licenza consente la riproduzione offline, l’utente può visualizzare il contenuto nell’applicazione senza una connessione di rete. Utilizzo di `DRMManager`, è possibile pre-memorizzare la licenza nella cache. L&#39;applicazione non deve ottenere la licenza necessaria per visualizzare il contenuto. Ad esempio, l&#39;applicazione potrebbe scaricare il file multimediale e quindi ottenere la licenza mentre l&#39;utente è ancora online.

Per precaricare una licenza, utilizzare una `DRMContentData` oggetto. Il `DRMContentData` L&#39;oggetto contiene l&#39;URL del server licenze DRM di Primetime che può fornire la licenza e descrive se è necessaria l&#39;autenticazione utente. Con queste informazioni, puoi chiamare il `DRMManager` `loadVoucher()` per ottenere e memorizzare in cache la licenza. Il flusso di lavoro per il precaricamento delle licenze è descritto più dettagliatamente in *Precaricamento delle licenze per la riproduzione offline*.

**Gestione delle sessioni**

È inoltre possibile utilizzare `DRMManager` per autenticare l&#39;utente su un server licenze DRM Primetime e per gestire sessioni persistenti. Chiama il `DRMManager` `authenticate()` per stabilire una sessione con il server licenze DRM Primetime. Al termine dell’autenticazione, il `DRMManager` invia un `DRMAuthenticationCompleteEvent` oggetto. Questo oggetto contiene un token di sessione. Puoi salvare questo token per stabilire sessioni future in modo che l’utente non debba fornire le credenziali del proprio account. Passa il token a `setAuthenticationToken()` per stabilire una nuova sessione autenticata. (Le impostazioni del server che ha generato il token determinano la scadenza del token e altri attributi).

## Gestione degli eventi DRMStatus {#handling-drmstatus-events}

Il `DRMManager` invia un `DRMStatusEvent` oggetto dopo una chiamata al `loadVoucher()` metodo completato correttamente. Se viene ottenuta una licenza, il valore della proprietà detail dell&#39;oggetto evento è il seguente: `DRM.voucherObtained`e la proprietà voucher contiene `DRMVoucher` oggetto. Se non si ottiene una licenza, la proprietà detail ha ancora il valore: `DRM.voucherObtained`; tuttavia, la proprietà del voucher è null. Non è possibile ottenere una licenza se, ad esempio, si utilizza `LoadVoucherSetting` di `localOnly` e non esiste una licenza memorizzata nella cache locale. Se il `loadVoucher()` chiamata non completata correttamente, probabilmente a causa di un errore di autenticazione o comunicazione, `DRMManager` invia un `DRMErrorEvent` o `DRMAuthenticationErrorEvent` oggetto.

## Gestione degli eventi DRMAuthenticationComplete{#handling-drmauthenticationcomplete-events}

Il `DRMManager` invia un `DRMAuthenticationCompleteEvent` quando un utente viene autenticato correttamente tramite una chiamata al `authenticate()` metodo. Il `DRMAuthenticationCompleteEvent` L&#39;oggetto contiene un token riutilizzabile che può essere utilizzato per mantenere l&#39;autenticazione dell&#39;utente nelle sessioni dell&#39;applicazione. Passa questo token a `DRMManager` `setAuthenticationToken()` per ristabilire la sessione. Il creatore del token imposta gli attributi del token, ad esempio la scadenza. L’Adobe non fornisce un’API per l’esame degli attributi del token.)

## Gestione degli eventi DRMAuthenticationError{#handling-drmauthenticationerror-events}

Il `DRMManager` invia un `DRMAuthenticationErrorEvent` quando un utente non può essere autenticato correttamente tramite una chiamata al `authenticate()` o `setAuthenticationToken()` metodi.
