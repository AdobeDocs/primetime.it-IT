---
title: Diritti di riproduzione
description: Diritti di riproduzione
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---

# Diritti di riproduzione {#play-rights}

La tabella seguente descrive le preferenze relative ai diritti di riproduzione:

| Preferenza | Descrizione |
|--- |--- |
| Finestra di riproduzione | La durata di validità di una licenza (in minuti) dopo la prima riproduzione del contenuto protetto da parte dell’utente. |
| Protezione dell&#39;output | Controlla se l&#39;output su dispositivi di rendering esterni deve essere protetto. Le uscite analogiche e digitali possono essere specificate in modo indipendente. |
| Restrizioni | Elenco Bloccati di versioni client a cui non è consentito riprodurre il contenuto. Tutte le colonne sono facoltative. |
| DRM | Specifica un elenco di versioni DRM a cui non è consentito riprodurre contenuto protetto. |
| Runtime | Specifica un elenco di versioni di runtime a cui non è consentito riprodurre contenuto protetto. |
| Livello di sicurezza minimo |  |
| DRM | Livello di sicurezza DRM minimo richiesto per riprodurre i contenuti protetti. |
| Runtime | Livello di sicurezza runtime minimo richiesto per riprodurre il contenuto protetto. |
| Applicazioni consentite | Elenco consentiti di applicazioni client a cui è consentito riprodurre il contenuto. Se non vengono specificate applicazioni, è consentita qualsiasi applicazione SWF o AIR. |
| SWF | Elenco degli URL SWF autorizzati a riprodurre contenuti protetti. |
| AIR | Elenco delle applicazioni AIR autorizzate a riprodurre contenuti protetti. È necessario specificare l&#39;ID dell&#39;editore, i campi rimanenti sono facoltativi. |

Gestione Flash Access supporta i criteri contenenti più diritti di riproduzione. Per creare un criterio con più diritti di riproduzione, utilizzare il pulsante &quot;Aggiungi diritti di riproduzione aggiuntivi&quot; e specificare gli attributi desiderati per ogni diritto di riproduzione.

Quando si utilizza una licenza, il client utilizza il primo diritto di riproduzione per il quale soddisfa tutti i requisiti. È possibile utilizzare più diritti di riproduzione per specificare restrizioni diverse per sistemi operativi diversi. Ad esempio, è possibile specificare un diritto con Protezione output richiesta per Windows (elencando le versioni DRM su Macintosh e Linux) e specificare un secondo diritto con Protezione output &quot;Usa se disponibile&quot; su altre piattaforme (elencando le versioni DRM su Windows).
