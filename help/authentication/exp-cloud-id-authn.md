---
title: Utilizzo dell'ID di Experience Cloud nell'autenticazione di Primetime
description: Utilizzo dell'ID di Experience Cloud nell'autenticazione di Primetime
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---


# Utilizzo dell&#39;ID di Experience Cloud nell&#39;autenticazione di Primetime

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Che cos’è l’ID Experience Cloud e come ottenerlo? {#what-exp-cloud-id-obtain}

L’ID Experience Cloud (ECID per breve) è un ID univoco generato da Adobe Experience Cloud per ogni singolo utente nell’applicazione/sito web. ECID è ampiamente utilizzato in tutti i rapporti di Experience Cloud utilizzati per collegare informazioni su un utente specifico in più applicazioni/siti web.

Se disponi già di un sistema che fornisce un ID visitatore, devi utilizzare lo stesso ID per l’ambito di questo documento.

Un modo per ottenere l&#39;ECID è utilizzare il servizio Experience Cloud ID. Puoi utilizzare il tipo di implementazione preferito, in base a TDM, libreria JS, lato server, integrazione diretta o librerie native per le piattaforme mobili. Per una visualizzazione completa dei servizi, delle librerie, degli SDK e delle guide di implementazione disponibili, consulta: https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-implementation-guides.html





## Qual è il vantaggio dell&#39;utilizzo dell&#39;ID Experience Cloud nell&#39;autenticazione di Primetime? {#benefit-ex-cloud-id}

Se configuri i nostri SDK e API REST senza client per utilizzare il tuo ECID, in seguito sarai in grado di collegare i dati raccolti da Primetime Authentication alle tue soluzioni Experience Cloud esistenti. In questo modo potrai comprendere meglio il percorso e l’esperienza dei clienti in tutte le soluzioni fornite da Adobe.

## Come si utilizza l&#39;ID Experience Cloud nell&#39;autenticazione di Primetime? {#how-to-ex-cloud-id-authn}

Dopo aver ottenuto l’ECID (spiegato in precedenza) devi passare queste informazioni ai nostri SDK e alla nostra API REST Clientless. Queste informazioni verranno successivamente trasmesse ai nostri server su ogni chiamata di rete effettuata dall&#39;SDK. Il processo di configurazione è diverso per ogni SDK nel modo seguente:

### SDK JS {#js-sdk}

Per JavaScript è necessario trasmettere l&#39;ECID in una mappa come terzo parametro alla chiamata setRequestor.

**Esempio di utilizzo:**

```JavaScript
accessEnabler.setRequestor("REQUESTOR_ID", ["ENDPOINT_URL"],
    {
        "visitorID": "THE_ECID_VALUE"
    }
);
```

### SDK iOS/tvOS {#ios-sdk}

Per l&#39;SDK iOS/tvOS esiste un metodo dedicato chiamato setOptions.

**Esempio di utilizzo:**

```JavaScript
accessEnabler.setOptions(
    [
        "visitorID": "THE_ECID_VALUE"
    ]
);
```

### SDK per Android/fireTV {#android-sdk}

Per l&#39;SDK Android/fireTV il meccanismo è simile ad iOS. Solo il nome del parametro è diverso. L’API è documentata qui.

**Esempio di utilizzo:**

```JavaScript
String visitor_id = "THE_ECID_VALUE";

HashMap<String, String> options = new HashMap();
options.put("ap_vi",visitor_id);

accessEnabler.setOptions(options);
```

### API senza client {#clientless-api}

Quando utilizzi Adobe Primetime tramite l’API REST, la **ECID** deve essere inviato **su tutte le API** come parametro denominato **&#39;ap_vi&#39;**.

**Esempio di utilizzo:**

`GET: https://api.auth.adobe.com/api/v1/authorize?...&ap_vi=THE_ECID_VALUE`