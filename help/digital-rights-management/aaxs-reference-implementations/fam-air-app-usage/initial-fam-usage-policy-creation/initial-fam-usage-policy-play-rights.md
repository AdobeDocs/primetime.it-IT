---
seo-title: Riproduci diritti
title: Riproduci diritti
uuid: 90f2a7a6-6637-4d10-9afe-6d2e77fc4185
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---


# Riproduci diritti {#play-rights}

Nella tabella seguente sono descritte le preferenze per i diritti di riproduzione:

| Preferenza | Descrizione |
|--- |--- |
| Finestra di riproduzione | La durata di validità di una licenza (in minuti) dopo la prima riproduzione del contenuto protetto da parte dell&#39;utente. |
| Protezione dell&#39;output | Controlla se l&#39;output su dispositivi di rendering esterni deve essere protetto. Le uscite analogiche e digitali possono essere specificate in modo indipendente. |
| Restrizioni | Blocco dell&#39;elenco delle versioni client non consentite per la riproduzione del contenuto. Tutte le colonne sono facoltative. |
| DRM | Specifica un elenco di versioni DRM alle quali non è consentito riprodurre contenuto protetto. |
| Runtime | Specifica un elenco di versioni Runtime alle quali non è consentito riprodurre contenuto protetto. |
| Livello di protezione minimo |  |
| DRM | Livello di protezione DRM minimo necessario per riprodurre il contenuto protetto. |
| Runtime | Livello di protezione Runtime minimo necessario per riprodurre il contenuto protetto. |
| Applicazioni consentite | Consenti elenco delle applicazioni client consentite per la riproduzione del contenuto. Se non vengono specificate applicazioni, è consentita qualsiasi applicazione SWF o AIR. |
| SWF | Elenco di URL SWF consentiti per riprodurre contenuto protetto. |
| AIR | Elenco delle applicazioni AIR consentite per riprodurre contenuto protetto. L&#39;ID editore è obbligatorio. I campi rimanenti sono facoltativi. |

Flash Access Manager supporta criteri contenenti più diritti di riproduzione. Per creare un criterio con più di un diritto di riproduzione, utilizzate il pulsante &quot;Aggiungi diritto di riproduzione aggiuntivo&quot; e inserite gli attributi desiderati per ogni diritto di riproduzione.

Quando si utilizza una licenza, il client utilizza il primo diritto di riproduzione per il quale soddisfa tutti i requisiti. È possibile utilizzare più diritti di riproduzione per specificare diverse restrizioni per i diversi sistemi operativi. Ad esempio, è possibile specificare un diritto con Protezione output richiesta per Windows (tramite blocco che elenca le versioni DRM su Macintosh e Linux) e specificare un secondo diritto con Protezione output &quot;Usa se disponibile&quot; su altre piattaforme (tramite blocco che elenca le versioni DRM su Windows).
