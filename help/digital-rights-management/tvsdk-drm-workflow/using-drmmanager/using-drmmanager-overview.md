---
title: Panoramica sull’utilizzo della classe DRMManager
description: Panoramica sull’utilizzo della classe DRMManager
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---


# Utilizzo della classe DRMManager {#using-the-drmmanager-class}

Utilizza la classe `DRMManager` per gestire le licenze e le sessioni del server licenze DRM di Primetime nelle applicazioni.

**Gestione delle licenze**

Ogni volta che un dispositivo riproduce contenuto protetto, il runtime ottiene e memorizza nella cache la licenza necessaria per visualizzare il contenuto. Se l&#39;applicazione salva il contenuto localmente e la licenza consente la riproduzione offline, l&#39;utente può visualizzare il contenuto dell&#39;applicazione senza una connessione di rete. Utilizzando `DRMManager`, puoi pre-memorizzare la licenza nella cache. L&#39;applicazione non deve ottenere la licenza necessaria per visualizzare il contenuto. Ad esempio, l&#39;applicazione potrebbe scaricare il file multimediale e quindi ottenere la licenza mentre l&#39;utente è ancora online.

Per precaricare una licenza, utilizza un oggetto `DRMContentData` . L&#39;oggetto `DRMContentData` contiene l&#39;URL del server di licenza DRM di Primetime che può fornire la licenza e descrive se è necessaria l&#39;autenticazione dell&#39;utente. Con queste informazioni, puoi chiamare il metodo `DRMManager` `loadVoucher()` per ottenere e memorizzare nella cache la licenza. Il flusso di lavoro per il precaricamento delle licenze è descritto più dettagliatamente in *Pre-loading license for offline playback* (Licenze di precaricamento per la riproduzione offline).

**Gestione delle sessioni**

È inoltre possibile utilizzare `DRMManager` per autenticare l&#39;utente a un server di licenza DRM di Primetime e per gestire sessioni persistenti. Chiama il metodo `DRMManager` `authenticate()` per stabilire una sessione con il server di licenze DRM di Primetime. Al termine dell&#39;autenticazione, `DRMManager` invia un oggetto `DRMAuthenticationCompleteEvent`. Questo oggetto contiene un token di sessione. Puoi salvare questo token per stabilire sessioni future in modo che l’utente non debba fornire le proprie credenziali dell’account. Passa il token al metodo `setAuthenticationToken()` per stabilire una nuova sessione autenticata. (Le impostazioni del server che ha generato il token determinano la scadenza del token e altri attributi).

## Gestione degli eventi DRMStatus {#handling-drmstatus-events}

Il `DRMManager` invia un oggetto `DRMStatusEvent` al completamento di una chiamata al metodo `loadVoucher()` . Se si ottiene una licenza, la proprietà detail dell&#39;oggetto evento ha il valore seguente: `DRM.voucherObtained` e la proprietà voucher contiene l&#39;oggetto `DRMVoucher` . Se non si ottiene una licenza, la proprietà detail presenta ancora il valore seguente: `DRM.voucherObtained`; tuttavia, la proprietà voucher è null. Non è possibile ottenere una licenza se, ad esempio, si utilizza `LoadVoucherSetting` di `localOnly` e non è presente alcuna licenza memorizzata nella cache locale. Se la chiamata `loadVoucher()` non viene completata correttamente, ad esempio a causa di un errore di autenticazione o comunicazione, il `DRMManager` invia un oggetto `DRMErrorEvent` o `DRMAuthenticationErrorEvent` al suo posto.

## Gestione degli eventi DRMAuthAuthenticationComplete{#handling-drmauthenticationcomplete-events}

Il `DRMManager` invia un oggetto `DRMAuthenticationCompleteEvent` quando un utente viene autenticato correttamente tramite una chiamata al metodo `authenticate()` . L&#39;oggetto `DRMAuthenticationCompleteEvent` contiene un token riutilizzabile che può essere utilizzato per mantenere l&#39;autenticazione utente nelle sessioni dell&#39;applicazione. Passa questo token al metodo `DRMManager` `setAuthenticationToken()` per ristabilire la sessione. Il creatore di token imposta gli attributi del token, ad esempio la scadenza. Adobe non fornisce un’API per l’analisi degli attributi del token.)

## Gestione degli eventi DRMAuthAuthenticationError{#handling-drmauthenticationerror-events}

Il `DRMManager` invia un oggetto `DRMAuthenticationErrorEvent` quando un utente non può essere autenticato correttamente tramite una chiamata ai metodi `authenticate()` o `setAuthenticationToken()`.