---
description: Tutte le richieste di inserimento di annunci utilizzano la stessa struttura URL e gli stessi parametri di query di base. Parametri di query aggiuntivi consentono al server manifest di funzionare con una varietà di client e situazioni.
title: Richieste di inserimento di annunci
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# Richieste di inserimento di annunci {#requests-for-ad-insertion}

Tutte le richieste di inserimento di annunci utilizzano la stessa struttura URL e gli stessi parametri di query di base. Parametri di query aggiuntivi consentono al server manifest di funzionare con una varietà di client e situazioni.

| Parametro | Descrizione |
|--- |--- |
| u | L’ID risorsa è un hash MD5 di ad_request_id dai metadati di Adobe Primetime ad decisioning. Fornito dal tuo Adobe Technical Account Manager. |
| z | ID di zona della risorsa da fornire ad Auditude. Fornito dal tuo Adobe Technical Account Manager. |
| `__sid__` | ID univoco che il server manifesto utilizzerà per generare l&#39;ID sessione. |

>[!NOTE]
>
>Il `__sid__` Il parametro è racchiuso tra due caratteri di sottolineatura.

Il server manifesto mantiene sessioni per singoli client o gruppi di client per garantire che le sequenze di interazioni API per client diversi rimangano separate. Il `__sid__` che il client invia nell&#39;URL di bootstrap al server manifesto deve essere univoco all&#39;interno del relativo ambiente. Il server manifesto lo utilizza per creare un ID univoco globale che restituisce al client.

I parametri di query rimanenti si riferiscono a client e situazioni diversi.