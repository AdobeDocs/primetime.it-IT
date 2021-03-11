---
description: Tutte le richieste di inserimento annunci utilizzano la stessa struttura URL e gli stessi parametri di query di base. Parametri di query aggiuntivi consentono al server manifest di lavorare con una varietà di client e situazioni.
title: Richieste di inserimento annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# Richieste di inserimento annunci {#requests-for-ad-insertion}

Tutte le richieste di inserimento annunci utilizzano la stessa struttura URL e gli stessi parametri di query di base. Parametri di query aggiuntivi consentono al server manifest di lavorare con una varietà di client e situazioni.

| Parametro | Descrizione |
|--- |--- |
| u | L’ID risorsa è un hash MD5 dell’ad_request_id dai metadati Adobe Primetime e decisioning. Fornito dal tuo Adobe Technical Account Manager. |
| z | L’ID di zona della risorsa che deve essere fornita ad Auditude. Fornito dal tuo Adobe Technical Account Manager. |
| `__sid__` | Un ID univoco che il server manifesto utilizzerà per generare l&#39;ID sessione. |

>[!NOTE]
>
>Il parametro `__sid__` è circondato da caratteri di sottolineatura doppi.

Il server manifest mantiene sessioni per singoli client o gruppi di client per garantire che le sequenze di interazioni API per diversi client rimangano separate. Il `__sid__` che il client invia nell&#39;URL di avvio al server manifest deve essere univoco all&#39;interno del proprio ambiente. Il server manifest lo utilizza per creare un ID univoco globale che restituisce al client.

I parametri di query rimanenti riguardano client e situazioni diversi.