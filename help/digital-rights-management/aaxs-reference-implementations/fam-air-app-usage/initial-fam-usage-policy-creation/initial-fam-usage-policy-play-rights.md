---
title: Diritti di riproduzione
description: Diritti di riproduzione
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---


# Diritti di riproduzione {#play-rights}

La tabella seguente descrive le preferenze di Play Rights:

| Preferenza | Descrizione |
|--- |--- |
| Finestra di riproduzione | La durata della validità di una licenza (in minuti) dopo la prima riproduzione del contenuto protetto da parte dell’utente. |
| Protezione dell&#39;uscita | Controlla se l&#39;output su dispositivi di rendering esterni deve essere protetto. Le uscite analogiche e digitali possono essere specificate in modo indipendente. |
| Restrizioni | Elenco Bloccati di versioni client non consentite per la riproduzione di contenuto. Tutte le colonne sono facoltative. |
| DRM | Specifica un elenco di versioni DRM che non possono riprodurre contenuto protetto. |
| Runtime | Specifica un elenco di versioni Runtime non autorizzate a riprodurre contenuto protetto. |
| Livello minimo di sicurezza |  |
| DRM | Livello minimo di sicurezza DRM necessario per riprodurre contenuti protetti. |
| Runtime | Livello minimo di sicurezza Runtime necessario per riprodurre contenuto protetto. |
| Applicazioni consentite | Elenco consentiti di applicazioni client consentite per la riproduzione di contenuti. Se non sono specificate applicazioni, è consentita qualsiasi applicazione SWF o AIR. |
| SWF | Elenco degli URL SWF consentiti per riprodurre contenuto protetto. |
| ARIA | Elenco delle applicazioni AIR autorizzate a riprodurre contenuti protetti. L’ID dell’editore è obbligatorio. I campi rimanenti sono facoltativi. |

Flash Access Manager supporta i criteri contenenti più diritti di riproduzione. Per creare un criterio con più di un diritto di riproduzione, utilizza il pulsante &quot;Aggiungi diritto di riproduzione aggiuntivo&quot; e compila gli attributi desiderati per ogni diritto di riproduzione.

Quando si utilizza una licenza, il cliente utilizza il primo diritto di riproduzione per il quale soddisfa tutti i requisiti. È possibile utilizzare più diritti di riproduzione per specificare diverse restrizioni per i diversi sistemi operativi. Ad esempio, è possibile specificare un diritto con Protezione output richiesto per Windows (per blocco elencando le versioni DRM su Macintosh e Linux) e specificare un secondo diritto con Protezione output &quot;Usa se disponibile&quot; su altre piattaforme (per blocco elencando le versioni DRM su Windows).
