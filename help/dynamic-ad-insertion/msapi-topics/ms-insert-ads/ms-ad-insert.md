---
description: Tutte le richieste di inserimento di annunci utilizzano la stessa struttura URL e gli stessi parametri di query di base. Parametri di query aggiuntivi consentono al server manifesto di lavorare con diversi client e situazioni.
seo-description: Tutte le richieste di inserimento di annunci utilizzano la stessa struttura URL e gli stessi parametri di query di base. Parametri di query aggiuntivi consentono al server manifesto di lavorare con diversi client e situazioni.
seo-title: Richieste di inserimento annunci
title: Richieste di inserimento annunci
uuid: e42b3228-bff7-4202-86ed-7f631f3016ae
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# Richieste di inserimento annunci {#requests-for-ad-insertion}

Tutte le richieste di inserimento di annunci utilizzano la stessa struttura URL e gli stessi parametri di query di base. Parametri di query aggiuntivi consentono al server manifesto di lavorare con diversi client e situazioni.

| Parametro | Descrizione |
|--- |--- |
| u | L’ID risorsa è un hash MD5 di ad_request_id proveniente da Adobe Primetime e dai metadati di decisione. Fornito dal vostro Adobe Technical Account Manager. |
| z | L’ID di zona per la risorsa che deve essere fornita ad Auditude. Fornito dal vostro Adobe Technical Account Manager. |
| `__sid__` | Un ID univoco che il server manifesto utilizzerà per generare l’ID sessione. |

>[!NOTE]
>
>Il `__sid__` parametro è circondato da due caratteri di sottolineatura.

Il server manifesto mantiene le sessioni per singoli client o gruppi di client per assicurare che le sequenze di interazioni API per i diversi client rimangano separate. L&#39; `__sid__` invio da parte del client dell&#39;URL di avvio al server manifesto deve essere univoco all&#39;interno del relativo ambiente. Il server manifesto lo utilizza per creare un ID univoco globale, che restituisce al client.

I restanti parametri di query riguardano client e situazioni diversi.