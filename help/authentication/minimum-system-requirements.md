---
title: Requisiti minimi di sistema
description: Requisiti minimi di sistema
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---


# Requisiti minimi di sistema {#minimum-system-requirements}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.


## Panoramica {#overview}

Questo documento presenta i requisiti software e hardware correnti per l’implementazione delle integrazioni di autenticazione Adobe Primetime sulle piattaforme supportate. Tutti i browser web/mobili supportati e i sistemi operativi elencati di seguito beneficeranno del supporto completo del team di autenticazione Adobe Primetime, associato agli SLA concordati.

In qualità di team di autenticazione di Adobe Primetime, incoraggiamo l&#39;uso delle versioni stabili più recenti dei browser e dei sistemi operativi; riconosciamo inoltre l’esistenza di piattaforme e browser non conformi/meno recenti attualmente in uso. Questi dispositivi obsoleti possono ancora funzionare senza problemi, tuttavia saranno più inclini all&#39;errore.

L’approccio iniziale per attenuare eventuali problemi che appaiono su queste piattaforme obsolete deve essere l’aggiornamento alle versioni più recenti; può trattarsi della versione del sistema operativo, del browser o della versione dell’applicazione installata.

Eventuali problemi che appariranno su queste piattaforme verranno affrontati come best practice dal team di autenticazione di Adobe Primetime. 

Adobe Primetime incoraggia i nostri clienti e partner a considerare l’aggiornamento alle versioni più recenti per beneficiare del pieno supporto di Adobe in tutti i potenziali problemi, oltre a miglioramenti a livello di prestazioni, efficienza e sicurezza. 


## Requisiti del browser e del sistema operativo {#browser-OS-system-requirements}


| Browser Web/Mobile (†) | Versioni supportate |
|---|---|
| Google Chrome | **70** o successiva |
| Mozilla Firefox | **57** o successiva |
| Apple Safari | **14** o successiva |
| Microsoft Edge | **100** o successiva |

(†) Adobe sconsiglia di utilizzare la modalità privata o in incognito.

| Sistema operativo | Versioni supportate |
|---|---|
| *Android* | **7,0** (Nougat) o successivo |
| *iOS* | **14** o successiva |
| *iPadOS* | **14** o successiva |
| *tvOS* | **14** o successiva |
| *Fire OS* | **5 (Android 5.1)** o successiva |
| *Mac OS* | **10,13** o successiva |
| *Microsoft Windows* | **10** o successiva |




>[!NOTE]
>
>Cookie di terze parti - I flussi di adesione all’autenticazione di Adobe Primetime potrebbero non riuscire quando i cookie di terze parti sono disabilitati.  Questo problema si verifica solo quando le impostazioni del browser vengono modificate. Per tutti i browser supportati, l&#39;autenticazione Primetime deve funzionare con le impostazioni predefinite.\
 

## Requisiti del dispositivo per implementazioni senza client (REST) {#general_clientless_reqs}

 
Qualsiasi dispositivo che utilizzerà i servizi di autenticazione di Adobe Primetime tramite implementazioni senza client **devono essere in grado di**:

* Specifica un ID dispositivo con hash univoco. Se il dispositivo non fornisce un ID dispositivo con hash univoco, deve essere in grado di mantenere un ID univoco fornito dall&#39;autenticazione Adobe Primetime. Il dispositivo deve essere in grado di mantenere l’ID univoco permanentemente nell’archivio locale e deve fornire l’ID univoco come ID dispositivo quando effettua chiamate alle API di autenticazione di Adobe Primetime.
* Generare firme digitali utilizzando l&#39;algoritmo HMAC-SHA1
* Impostare intestazioni HTTP arbitrarie
* Servizi web RESTful
* Analizzare i formati di dati XML e JSON
* Invia traffico tramite HTTPS
* Gestire i codici di errore HTTP
