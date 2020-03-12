---
seo-title: Utilizzo della panoramica della classe DRMManager
title: Utilizzo della panoramica della classe DRMManager
uuid: 71ce061b-75b6-4ab5-8bbd-cafe7c3e4592
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# Utilizzo della classe DRMManager {#using-the-drmmanager-class}

Utilizzate la `DRMManager` classe per gestire le licenze e le sessioni del server licenze Primetime DRM nelle applicazioni.

**Gestione delle licenze**

Ogni volta che un dispositivo riproduce contenuto protetto, il runtime ottiene e memorizza nella cache la licenza necessaria per visualizzare il contenuto. Se l&#39;applicazione salva il contenuto localmente e la licenza consente la riproduzione offline, l&#39;utente può visualizzare il contenuto nell&#39;applicazione senza una connessione di rete. Utilizzando `DRMManager`, è possibile pre-memorizzare la licenza nella cache. L&#39;applicazione non deve ottenere la licenza necessaria per visualizzare il contenuto. Ad esempio, l&#39;applicazione potrebbe scaricare il file multimediale e quindi ottenere la licenza mentre l&#39;utente è ancora online.

Per precaricare una licenza, utilizzare un `DRMContentData` oggetto. L&#39; `DRMContentData` oggetto contiene l&#39;URL del server licenze DRM Primetime che può fornire la licenza e descrive se è necessaria l&#39;autenticazione dell&#39;utente. Con queste informazioni, potete chiamare il `DRMManager` `loadVoucher()` metodo per ottenere e memorizzare nella cache la licenza. Il flusso di lavoro per il precaricamento delle licenze è descritto più dettagliatamente in *Precaricamento delle licenze per la riproduzione* offline.

**Gestione delle sessioni**

Potete inoltre utilizzare l&#39;icona `DRMManager` per autenticare l&#39;utente su un server licenze DRM Primetime e per gestire le sessioni persistenti. Chiamate il `DRMManager` `authenticate()` metodo per stabilire una sessione con il server licenze DRM Primetime. Quando l&#39;autenticazione viene completata correttamente, l&#39; `DRMManager` oggetto invia un `DRMAuthenticationCompleteEvent` oggetto. Questo oggetto contiene un token di sessione. È possibile salvare questo token per stabilire sessioni future in modo che l&#39;utente non debba fornire le credenziali del proprio account. Passa il token al `setAuthenticationToken()` metodo per stabilire una nuova sessione autenticata. (Le impostazioni del server che ha generato il token determinano la scadenza del token e altri attributi).

## Gestione degli eventi DRMStatus {#handling-drmstatus-events}

L&#39;oggetto `DRMManager` invia un `DRMStatusEvent` oggetto dopo che una chiamata al `loadVoucher()` metodo è stata completata correttamente. Se viene ottenuta una licenza, la proprietà detail dell&#39;oggetto evento ha il valore seguente: e `DRM.voucherObtained`la proprietà voucher contiene l&#39; `DRMVoucher` oggetto. Se non si ottiene una licenza, la proprietà detail ha comunque il valore seguente: `DRM.voucherObtained`; tuttavia, la proprietà voucher è null. Non è possibile ottenere una licenza se, ad esempio, si utilizza il `LoadVoucherSetting` carattere di `localOnly` e non esiste una licenza memorizzata nella cache locale. Se la `loadVoucher()` chiamata non viene completata correttamente, ad esempio a causa di un errore di autenticazione o di comunicazione, l&#39;utente `DRMManager` invia invece un `DRMErrorEvent` oggetto o `DRMAuthenticationErrorEvent` .

## Gestione di eventi DRMAuthenticationComplete{#handling-drmauthenticationcomplete-events}

L&#39; `DRMManager` oggetto invia un `DRMAuthenticationCompleteEvent` oggetto quando un utente viene autenticato correttamente tramite una chiamata al `authenticate()` metodo. L&#39; `DRMAuthenticationCompleteEvent` oggetto contiene un token riutilizzabile che può essere utilizzato per mantenere l&#39;autenticazione dell&#39;utente nelle sessioni dell&#39;applicazione. Passate questo token a `DRMManager` un `setAuthenticationToken()` metodo per ripristinare la sessione. (Il creatore di token imposta gli attributi del token, ad esempio scadenza. Adobe non fornisce un&#39;API per l&#39;esame degli attributi del token.

## Gestione degli eventi DRMAuthenticationError{#handling-drmauthenticationerror-events}

L&#39; `DRMManager` oggetto invia un `DRMAuthenticationErrorEvent` oggetto quando un utente non può essere autenticato correttamente tramite una chiamata ai metodi `authenticate()` o `setAuthenticationToken()` .