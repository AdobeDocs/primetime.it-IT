---
title: Ripristino di Temp Pass su iOS
description: Ripristino di Temp Pass su iOS
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 0%

---


# Ripristino di Temp Pass su iOS {#reset-temp-pass-on-ios}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

</br>

L’app Demo di iOS include una schermata dedicata per ripristinare il TTL Temp Pass . Per l&#39;operazione di ripristino sono necessarie le seguenti informazioni:

- **Ambiente:** specifica l&#39;endpoint del server pass Pay-TV Adobe che riceverà la chiamata di rete reset Temp Pass. Valori possibili: **Prequal** (*mgmt-prequal.auth-staging.adobe.com*), **Versione** (*mgmt.auth.adobe.com*) o **Personalizzato** (riservato ad Adobe ai test interni).
- **Token portatore OAuth2:** il token OAuth2 è necessario per autorizzare il programmatore ad Adobe l’autenticazione Pay-TV. Tale token può essere ottenuto dall’endpoint OAuth2 dedicato all’autenticazione Pay-TV (ad esempio *curl -u &quot;\&lt;consumer _key=&quot;&quot;>:\&lt;consumer _secret=&quot;&quot; _key=&quot;&quot;>*&quot; *&quot;https://mgmt.auth.adobe.com/oauth2/permanent\_accesstoken?Grant\_type=client\_credentials&quot;*).
- **ID richiedente:** l&#39;ID univoco del programmatore corrente. Questo valore viene letto dalla schermata principale dell’app Demo (il campo requestor ).
- **ID passaggio temporaneo:** l&#39;ID univoco dell&#39;MVPD di Temp Pass.
- **ID dispositivo:** ID dispositivo con hash calcolato dall’app Demo.
- **Chiave generica:** alcuni MVPD Temp Pass (cioè la prossima funzionalità estensibile Temp Pass) supportano una chiave generica per ripristinare Temp Pass (insieme all&#39;ID dispositivo).

Tutti i parametri di cui sopra (tranne il *Chiave generica*) sono obbligatorie. Ecco un esempio di parametri e la chiamata di rete associata che verranno eseguiti dall&#39;app Demo (l&#39;esempio è sotto forma di un comando *curl *):

- **Ambiente:** Versione (*mgmt.auth.adobe.com*)
- **Token portatore OAuth2:** H4j7cF3GtJX81BrsgDa10GwSizVz
- **ID programmatore:** REF
- **ID passaggio temporaneo:** TempPassREF
- **ID dispositivo:** f23804a37802993fdc8e28a7f244dfe088b6a9ea21457670728e6731fa63999 91 
- **Chiave generica:** null (nessun valore fornito)

```curl
curl -X DELETE -H "Authorization:Bearer* *H4j7cF3GtJX81BrsgDa10GwSizVz" "https://mgmt.auth.adobe.com/reset-tempass/v2.1/reset?device_id=f23804a37802993fdc8e28a7f244dfe088b6a9ea21457670728e6731fa639991&requestor_id=REF&mvpd_id=TempPassREF"
```

viene effettuata una richiesta HTTP di DELETE al **/reset** punto finale, passando *Token portatore OAuth2* nell’intestazione Autorizzazione e nella *ID dispositivo*, *ID richiedente* e *ID passaggio temporaneo (MVPD ID)* come parametri.

Se il programmatore fornisce un valore per *Chiave generica*, viene eseguita un’altra chiamata HTTP (questa volta al **/reset/generico** punto finale), passando *Chiave generica* all&#39;interno del *key* parametro di richiesta.

Ad esempio, l’impostazione della *Chiave generica* a un hash dell&#39;indirizzo e-mail (per gli MVPD Temp Pass che supportano questo tipo di funzionalità) darà la seguente chiamata HTTP (l&#39;e-mail è `user@domain.com` il suo hash SHA-256 è `f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7`):

```curl
curl -X DELETE -H "Authorization:Bearer H4j7cF3GtJX81BrsgDa10GwSizVz"
"https://mgmt.auth.adobe.com/reset-tempass/v2.1/reset/generic?key=f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7&requestor_id=REF&mvpd_id=TempPassREF"
```

È importante sottolineare che reimpostare Temp Pass nell&#39;app Demo potrebbe non avere lo stesso effetto per un&#39;app Programmer sullo stesso dispositivo. Questo è dovuto al fatto che l&#39;ID dispositivo (calcolato dall&#39;app demo e da AccessEnabler) potrebbe non essere lo stesso per tutte le applicazioni sul dispositivo:

- iOS 6 e versioni precedenti: l&#39;ID dispositivo viene calcolato utilizzando l&#39;indirizzo MAC (univoco per tutte le app), quindi reimpostando Temp Pass nell&#39;app Demo lo reimposteremo in tutte le altre app Programmer sul dispositivo.

- iOS 7 e superiore: l&#39;ID dispositivo viene calcolato in base al valore IDFV (ID per fornitore), univoco per tutte le applicazioni con lo stesso prefisso Bundle ID (cioè tutti i componenti eccetto l&#39;ultimo). Poiché l’app Demo e un’app Programmer hanno diversi Bundle ID, il ripristino di Temp Pass nell’app Demo non avrà alcun effetto su un’app Programmer.

L’ultimo caso d’uso (iOS 7 e versioni successive) è il più comune, quindi vediamo come i programmatori possono reimpostare Temp Pass per le loro app in questa situazione. Sono disponibili diverse opzioni:

1. Porta il codice dall’app Demo all’app Programmer. La *TempPassResetViewController* e *DeviceIdDemoApp* Le classi contengono la logica di base per la reimpostazione di Temp Pass e possono essere facilmente modificate e incluse nell&#39;app Programmer.

1. Esegui la richiesta HTTP per reimpostare Temp Pass con *arricciare*. Il parametro device\_Id può essere ottenuto calcolando l&#39;IDFV dell&#39;app Programmer e applicando un hash SHA-256 su di esso (codice di esempio nel *DeviceIdDemoApp* (Classe).

1. È sufficiente eseguire la reimpostazione dall’app Demo specificando l’IDFV con hash dell’app del programmatore come *Chiave generica*. Ciò comporterà due chiamate di rete: uno per reimpostare Temp Pass per l&#39;app Demo (irrilevante per il programmatore) e uno per reimpostare Temp Pass per l&#39;app Programmer.

Tutte le opzioni di cui sopra sono simili, spetta al programmatore sceglierne una a seconda della facilità di implementazione. 

