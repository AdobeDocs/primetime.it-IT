---
title: Procedure per l'escalation
description: Procedure per l'escalation
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 0%

---

# Procedure per l&#39;escalation {#escalation-procedures}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

>[!IMPORTANT]
> 
>Chiama il numero verde : **+1-205-693-9813** e invia un’e-mail a **tve-support@adobe.com** compreso **URGENTE - INCIDENTE** nell&#39;oggetto.

## Introduzione {#introduction}

Il presente documento descrive le procedure di supporto per gli incidenti rilevanti(**GRAVITÀ 1** livello) che influisce sull’autenticazione Adobe Primetime, sul monitoraggio della concorrenza di Primetime e sui suoi partner.\
 

## Definizione di un incidente di livello di gravità 1 {#definition-of-a-severity-1-level-incident}

A **GRAVITÀ 1** livello incidente **LIVE** situazione, **in ambiente di produzione**, che non consentono il completamento dei flussi di autenticazione e/o autorizzazione per un canale e un MVPD, che interessano un gran numero di abbonati del MVPD che eseguono il flusso.


## Esempi di incidenti gravi 1 {#examples-of-severity-1-incidentcs}

* L&#39;enabler di accesso alla produzione ospitato in  `https://entitlement.auth.adobe.com/entitlement/v4/AccessEnabler.js` o `https://entitlement.auth.adobe.com/entitlement/js/AccessEnabler.js`) non è disponibile.

* Per un MVPD specifico, Adobe non reindirizzerà più / visualizza la pagina di accesso, dopo che l&#39;utente ha selezionato il MVPD (in uno dei browser supportati).

* Il partner riceve un gran numero di rapporti che gli utenti non possono autenticare/autorizzare con un MVPD specifico.

* Durante il processo di autenticazione, l&#39;utente è bloccato su una pagina di errore Adobe senza la possibilità di riavviare il flusso di autenticazione/autorizzazione.


| Esempi di cosa è **NOT** a Gravità 1 |
|---|
| Per questioni di questo tipo, l&#39;Adobe fornirà supporto per le indagini ma non si tratta di casi di gravità 1:<ul><li>Uno o più sottoscrittori non sono in grado di eseguire il flusso a causa di un problema di versione di Flash (Flash mancante, blocchi di Flash, versione di Flash errata).</li><li>Uno o più sottoscrittori non sono in grado di autenticarsi e rimanere nella pagina di accesso MVPD.</li><li>Uno o più sottoscrittori sono autenticati ma non possono riprodurre video.</li><li>Un/pochi/tutti gli abbonati incontrano un errore JavaScript sul sito Programmer</li></ul> |

## Gravità 1 Flussi di scalabilità {#severity-1-escalation-flows}

I casi di gravità 1 possono essere avviati da un Adobe o da un partner di autenticazione Adobe Primetime. I passaggi per ciascuno di essi sono descritti di seguito.

### Flusso avviato dai partner {#partner-initiated-flow}

1. Il partner identifica un incidente di gravità 1 (come descritto sopra) che richiede l&#39;attenzione immediata del Adobe.
1. Il partner invia un’e-mail a **tve-support@adobe.com** compreso **URGENTE - INCIDENTE** nella riga dell’oggetto e aggiungi le seguenti informazioni:
   * Titolo
   * Descrizione e passaggi da riprodurre
   * Sistema operativo / browser
   * SDK e versione
   * Dispositivi interessati
   * % degli utenti interessati
   * Registri di traccia HTTP o dispositivo che mostrano il problema
   * (facoltativo) eventuali schermate o immagini video disponibili che dimostrano il problema
1. Se l’Adobe non risponde al ticket entro 30 minuti, il partner chiama il seguente numero:
   **1-205-693-9813**

   >[!IMPORTANT]
   >Se non includi &quot;URGENT-INCIDENT&quot; nel titolo del biglietto, non sarà prelevato dal nostro sistema di notifica**.

### Flusso avviato da Adobe {#adobe-initiated-flow}

#### ...per un problema di autenticazione Adobe Primetime {#adobe-initiated-flow-authn-issue}

1. Adobe identifica un problema interno e apre un ticket con il nostro sistema di tracciamento.

1. L&#39;Adobe notifica il responsabile del programma e il contatto tecnico del partner, specificando il numero del biglietto e l&#39;impatto stimato del problema.

1. L&#39;Adobe lavora per la risoluzione dell&#39;incidente e tiene informati tutti i partner interessati.

#### ...per un problema relativo a un partner (Programmer/MVPD) {#adobe-initiated-flow-partner-issue}

1. L&#39;Adobe identifica un problema relativo all&#39;integrazione con un MVPD o su uno dei siti del programmatore.

1. L&#39;Adobe notifica al partner interessato <u>seguendo le procedure di sostegno in vigore con tale partner</u> e apre un ticket con l’organizzazione di supporto del partner.

1. Se, durante l&#39;analisi dell&#39;impatto, l&#39;Adobe rileva che la questione appartiene a una delle decisioni preconcordate sugli scenari di incidente, vedi **Decisioni preconcordate sugli scenari di incidenti**, agirà di conseguenza senza attendere il contributo del partner.

1. Adobe attenderà gli aggiornamenti dal partner e una notifica dal partner quando il servizio è stato ripristinato.

## Decisioni preconcordate sugli scenari di incidenti {#pre-agreed-descn}

In alcune situazioni viene eseguita un’azione predefinita nel caso in cui si verifichi tale scenario:

|  | Scenario | Descrizione | Azioni |
|---|---|---|---|
| S1 | L&#39;Adobe identifica un problema relativo all&#39;integrazione di un MVPD durante le normali operazioni di produzione. | Durante le normali operazioni di produzione, l&#39;Adobe identifica un problema con uno degli MVPD che rende impossibile l&#39;esecuzione dei flussi di autenticazione/autorizzazione (ad esempio certificati scaduti, risposte SAML scadute, porte chiuse, parametri modificati, ecc.) | - l&#39;Adobe avviserà gli MVPD e i programmatori interessati.  </br> </br> - L&#39;Adobe disattiverà questo MVPD per tutti i programmatori interessati. </br> </br> - l&#39;Adobe aprirà un biglietto con l&#39;MVPD secondo la procedura di supporto concordata con tale MVPD |
| S2 | L&#39;Adobe attiva un nuovo MVPD per un programmatore e il programmatore consente l&#39;MVPD prima della data di lancio. | L&#39;Adobe sta attivando un nuovo MVPD per il sito di un programmatore, e il sito sta visualizzando il nuovo MVPD nel selettore, anche se non era previsto. | - Adobe avviserà il programmatore del nuovo MVPD che appare nel selettore prima della data pianificata. </br> </br>  - Se necessario, il programmatore si attiverà per rimuoverlo dal selettore. |
| S3 | L&#39;Adobe attiva un nuovo MVPD per un programmatore anche se l&#39;MVPD non è pronto per la produzione | L&#39;Adobe sta attivando un nuovo MVPD per un programmatore, ma l&#39;MVPD non ha ancora implementato il supporto per l&#39;integrazione in modo che i flussi di autenticazione/autorizzazione non possano essere eseguiti | - L&#39;Adobe eseguirà l&#39;installazione solo se richiesto dal programmatore </br> </br> - Il programmatore sarà responsabile di garantire l&#39;autorizzazione dell&#39;MVPD una volta che tutte le prove sono state eseguite. |

## Aspettative Di Risposta Per Gravità 1 Incidenti {#response-expectations-for-severity-one-incidents}

* Risposta iniziale: 30 minuti (24/7)
* Piano d&#39;azione: 1 ora (24/7)
* Risoluzione: ASAP (24/7)
