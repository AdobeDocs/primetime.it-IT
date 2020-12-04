---
seo-title: Utilizzo della panoramica della classe DRMManager
title: Utilizzo della panoramica della classe DRMManager
uuid: 71ce061b-75b6-4ab5-8bbd-cafe7c3e4592
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---


# Utilizzo della classe DRMManager {#using-the-drmmanager-class}

Utilizzate la classe `DRMManager` per gestire le licenze e le sessioni del server licenze Primetime DRM nelle applicazioni.

**Gestione delle licenze**

Ogni volta che un dispositivo riproduce contenuto protetto, il runtime ottiene e memorizza nella cache la licenza necessaria per visualizzare il contenuto. Se l&#39;applicazione salva il contenuto localmente e la licenza consente la riproduzione offline, l&#39;utente può visualizzare il contenuto nell&#39;applicazione senza una connessione di rete. Utilizzando la `DRMManager`, è possibile pre-memorizzare la licenza nella cache. L&#39;applicazione non deve ottenere la licenza necessaria per visualizzare il contenuto. Ad esempio, l&#39;applicazione potrebbe scaricare il file multimediale e quindi ottenere la licenza mentre l&#39;utente è ancora online.

Per precaricare una licenza, utilizzare un oggetto `DRMContentData`. L&#39;oggetto `DRMContentData` contiene l&#39;URL del server licenze DRM Primetime che può fornire la licenza e descrive se è necessaria l&#39;autenticazione dell&#39;utente. Con queste informazioni, potete chiamare il metodo `DRMManager` `loadVoucher()` per ottenere e memorizzare nella cache la licenza. Il flusso di lavoro per il precaricamento delle licenze è descritto più dettagliatamente in *Precaricamento delle licenze per la riproduzione offline*.

**Gestione delle sessioni**

È inoltre possibile utilizzare `DRMManager` per autenticare l&#39;utente in un server licenze DRM Primetime e per gestire le sessioni persistenti. Chiamate il metodo `DRMManager` `authenticate()` per stabilire una sessione con il server licenze DRM Primetime. Una volta completata l&#39;autenticazione, l&#39;oggetto `DRMManager` invia un oggetto `DRMAuthenticationCompleteEvent`. Questo oggetto contiene un token di sessione. È possibile salvare questo token per stabilire sessioni future in modo che l&#39;utente non debba fornire le credenziali del proprio account. Passa il token al metodo `setAuthenticationToken()` per stabilire una nuova sessione autenticata. (Le impostazioni del server che ha generato il token determinano la scadenza del token e altri attributi).

## Gestione degli eventi DRMStatus {#handling-drmstatus-events}

L&#39;oggetto `DRMManager` invia un oggetto `DRMStatusEvent` al completamento corretto di una chiamata al metodo `loadVoucher()`. Se viene ottenuta una licenza, la proprietà detail dell&#39;oggetto evento ha il valore seguente: `DRM.voucherObtained` e la proprietà voucher contiene l&#39;oggetto `DRMVoucher`. Se non si ottiene una licenza, la proprietà detail ha comunque il valore seguente: `DRM.voucherObtained`; tuttavia, la proprietà voucher è null. Non è possibile ottenere una licenza se, ad esempio, si utilizza `LoadVoucherSetting` di `localOnly` e non esiste una licenza memorizzata nella cache locale. Se la chiamata `loadVoucher()` non viene completata correttamente, ad esempio a causa di un errore di autenticazione o di comunicazione, l&#39;oggetto `DRMManager` invia invece un oggetto `DRMErrorEvent` o `DRMAuthenticationErrorEvent`.

## Gestione di eventi DRMAuthenticationComplete{#handling-drmauthenticationcomplete-events}

L&#39;oggetto `DRMManager` invia un oggetto `DRMAuthenticationCompleteEvent` quando un utente viene autenticato correttamente tramite una chiamata al metodo `authenticate()`. L&#39;oggetto `DRMAuthenticationCompleteEvent` contiene un token riutilizzabile che può essere utilizzato per mantenere l&#39;autenticazione utente nelle sessioni dell&#39;applicazione. Passa questo token al metodo `DRMManager` `setAuthenticationToken()` per ripristinare la sessione. (Il creatore di token imposta gli attributi del token, ad esempio scadenza.  Adobe non fornisce un&#39;API per l&#39;esame degli attributi del token.

## Gestione degli eventi DRMAuthenticationError{#handling-drmauthenticationerror-events}

L&#39;oggetto `DRMManager` invia un oggetto `DRMAuthenticationErrorEvent` quando un utente non può essere autenticato correttamente tramite una chiamata ai metodi `authenticate()` o `setAuthenticationToken()`.