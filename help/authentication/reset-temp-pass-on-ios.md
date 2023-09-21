---
title: Ripristina passaggio temporaneo su iOS
description: Ripristina passaggio temporaneo su iOS
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 0%

---

# Ripristina passaggio temporaneo su iOS {#reset-temp-pass-on-ios}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente di Adobe. Non è consentito alcun uso non autorizzato.

</br>

L’app di dimostrazione iOS include una schermata dedicata per il ripristino del TTL di Temp Pass. Per l&#39;operazione di ripristino sono necessarie le seguenti informazioni:

- **Ambiente:** specifica l&#39;endpoint Adobe del server di pass Pay-TV che riceverà la chiamata di rete Reset Temp Pass. Valori possibili: **Prequal** (*mgmt-prequal.auth-staging.adobe.com*), **Versione** (*mgmt.auth.adobe.com*) o **Personalizzato** (riservato ad Adobe ai test interni).
- **Token Bearer OAuth2:** il token OAuth2 è necessario per autorizzare il programmatore, ad Adobe per l’autenticazione a pagamento. Tale token può essere ottenuto dall’endpoint dedicato di autenticazione Pay-TV OAuth2 (ad esempio *curl -u &quot;\&lt;consumer _key=&quot;&quot;>:\&lt;consumer _secret=&quot;&quot; _key=&quot;&quot;>*&quot; *&quot;https://mgmt.auth.adobe.com/oauth2/permanent\_accesstoken?grant\_type=client\_credentials&quot;*).
- **ID richiedente:** ID univoco del programmatore corrente. Questo valore viene letto dalla schermata principale dell’app demo (il campo richiedente).
- **ID passaggio temporaneo:** l’ID univoco dell’MVPD di Passaggio Temp.
- **ID dispositivo:** ID dispositivo con hash calcolato dall&#39;app demo.
- **Chiave generica:** alcuni MVPD di Passaggio Temp (ovvero la funzionalità Passaggio Temp estensibile successiva) supportano una chiave generica per la reimpostazione di Passaggio Temp (insieme all&#39;ID dispositivo).

Tutti i parametri di cui sopra (ad eccezione di *Chiave generica*) sono obbligatori. Ecco un esempio di parametri e la chiamata di rete associata che verrà eseguita dall’app demo (l’esempio è sotto forma di un comando *curl *):

- **Ambiente:** Versione (*mgmt.auth.adobe.com*)
- **Token Bearer OAuth2:** H4j7cF3GtJX81BrsgDa10GwSizVz
- **ID programmatore:** RIF
- **ID passaggio temporaneo:** TempPassREF
- **ID dispositivo:** f23804a37802993fdc8e28a7f244dfe088b6a9ea21457670728e6731fa639991
- **Chiave generica:** null (nessun valore specificato)

```curl
curl -X DELETE -H "Authorization:Bearer* *H4j7cF3GtJX81BrsgDa10GwSizVz" "https://mgmt.auth.adobe.com/reset-tempass/v2.1/reset?device_id=f23804a37802993fdc8e28a7f244dfe088b6a9ea21457670728e6731fa639991&requestor_id=REF&mvpd_id=TempPassREF"
```

verrà effettuata una richiesta HTTP di DELETE al **/reset** endpoint, passaggio di *Token Bearer OAuth2* nell’intestazione Autorizzazione e nella sezione *ID dispositivo*, *ID richiedente* e *ID passaggio temporaneo (ID MVPD)* come parametri.

Se il programmatore fornisce un valore per *Chiave generica*, verrà eseguita un&#39;altra chiamata HTTP (questa volta al **/reset/generic** endpoint), passando il *Chiave generica* all&#39;interno del *chiave* parametro di richiesta.

Ad esempio, impostando *Chiave generica* a un hash di indirizzo e-mail (per gli MVPD che supportano questo tipo di funzionalità) genererà la seguente chiamata HTTP (l’e-mail è `user@domain.com` il relativo hash SHA-256 è `f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7`):

```curl
curl -X DELETE -H "Authorization:Bearer H4j7cF3GtJX81BrsgDa10GwSizVz"
"https://mgmt.auth.adobe.com/reset-tempass/v2.1/reset/generic?key=f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7&requestor_id=REF&mvpd_id=TempPassREF"
```

È importante sottolineare che il ripristino di Passata temporanea nell’app demo potrebbe non avere lo stesso effetto per un’app Programmatore sullo stesso dispositivo. Ciò è dovuto al fatto che l’ID dispositivo (calcolato dall’app demo e da AccessEnabler) potrebbe non essere lo stesso per tutte le applicazioni sul dispositivo:

- iOS 6 e versioni precedenti: l’ID dispositivo viene calcolato utilizzando l’indirizzo MAC (che è univoco per tutte le app), pertanto il ripristino di Passaggio temporaneo nell’app demo lo reimposterà in tutte le altre app Programmatore sul dispositivo.

- iOS 7 e versione superiore: l’ID dispositivo viene calcolato in base al valore IDFV (ID per fornitore), che è univoco per tutte le applicazioni che hanno lo stesso prefisso dell’ID bundle (ovvero tutti i componenti tranne l’ultimo). Poiché l’app demo e un’app programmatore hanno ID bundle diversi, il ripristino di Passaggio temporaneo nell’app demo non avrà alcun effetto su un’app programmatore.

L’ultimo caso d’uso (iOS 7 e versioni successive) è il più comune, quindi vediamo come i programmatori possono reimpostare il passaggio temporaneo per le loro app in questa situazione. Sono disponibili diverse opzioni:

1. Porta il codice dall’app demo all’app programmatore. Il *TempPassResetViewController* e *DeviceIdDemoApp* Le classi contengono la logica di base per il ripristino di Passaggio Temp e possono essere facilmente modificate e incluse nell’app Programmatore.

1. Esegui la richiesta HTTP per reimpostare il passaggio temporaneo con *ricciolo*. Il parametro device\_Id può essere ottenuto calcolando l’IDFV dell’app Programmer e applicando un hash SHA-256 su di esso (codice di esempio nel *DeviceIdDemoApp* classe).

1. È sufficiente eseguire il ripristino dall’app demo specificando l’IDFV con hash dell’app del programmatore come *Chiave generica*. Ciò comporterà due chiamate di rete: una per la reimpostazione del passaggio temporaneo per l&#39;app demo (irrilevante per il programmatore) e una per la reimpostazione del passaggio temporaneo per l&#39;app programmatore.

Tutte le opzioni di cui sopra sono simili, spetta al programmatore sceglierne una a seconda della facilità di implementazione.
