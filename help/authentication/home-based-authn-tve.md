---
title: Autenticazione basata su Home per TV Everywhere
description: Autenticazione basata su Home per TV Everywhere
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1676'
ht-degree: 0%

---

# Autenticazione basata su Home per TV Everywhere

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente di Adobe. Non è consentito alcun uso non autorizzato.

## Cos’è l’autenticazione basata su home? {#whatis-home-based-authn}

L&#39;HBA (Home Based Authentication) è una funzionalità di TV Everywhere che consente agli abbonati alla TV a pagamento di visualizzare i contenuti TV online senza immettere le credenziali MVPD quando sono a casa, migliorando in modo significativo l&#39;esperienza utente del flusso di autenticazione.

Home Based Authentication definition del Comitato Tecnologico di Autenticazione Aperta (OATC): &quot;L&#39;autenticazione automatica in casa è il processo mediante il quale un MVPD/OVD utilizza le caratteristiche della rete domestica (o identificatori automaticamente accessibili tra i dispositivi sulla rete domestica) per autenticare quale account abbonato è associato a quella rete domestica, in modo che gli utenti non debbano immettere manualmente le credenziali quando stabiliscono una sessione TVE per accedere al contenuto protetto da TVE.&quot;



Per ulteriori informazioni sull&#39;HBA e sugli standard di settore, consultare [Casi d’uso e requisiti OATC](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/files/Defining%20TVE%20Home-Based%20Authentication%20(HBA)%20%20Use%20Cases%20and%20Requirements%20Recommended%20Practice%20Version%201_0%20FINAL%20DRAFT%20FOR%20BOARD%20APPROVAL.pdf){target=_blank} documentazione e **Linee guida OATC sull&#39;esperienza utente per HBA**.

>[!NOTE]
>
>Alcuni flussi di HBA fanno parte del pacchetto Premium Workflow. Se sei interessato a utilizzare questa funzionalità, contatta il rappresentante commerciale Primetime.

## Perché l&#39;HBA è importante per voi {#why-hba}

L&#39;HBA è importante perché rimuove praticamente la barriera di accesso per i visualizzatori che sono a casa e che dispongono già di un abbonamento via cavo. Inoltre, l&#39;autenticazione basata su Home può aumentare in modo significativo il coinvolgimento degli utenti e offrire una migliore esperienza di utilizzo per i contenuti TV Everywhere.

Attualmente, quasi la metà dei tentativi di accesso non ha esito positivo.

Una volta che l&#39;HBA è stato attivato da uno dei primi 5 MVPD, il relativo tasso di conversione di autenticazione **aumentata del 40%** (da 45% a 63%)

![](assets/authn-conv-pre-post.png)

Di seguito è riportato il tasso di conversione di accesso per un canale integrato con MVPD diversi: quelli che hanno abilitato l&#39;HBA per tale canale e quelli che non ne dispongono. Il tasso di conversione per le schede con HBA è significativamente più elevato rispetto a quelle senza HBA.

![](assets/hba-vs-non-hba.png)

Sei mesi dopo aver abilitato l&#39;HBA per la maggior parte dei canali integrati con questo MVPD, abbiamo notato un aumento dell&#39;82% degli utenti univoci (il numero di utenti che accedono ai canali TV Everywhere tramite questo MVPD è quasi raddoppiato).

2w3Al contrario, come si può vedere nel grafico seguente, altri MVPD che non avevano abilitato HBA hanno registrato un aumento del 26% degli utenti univoci negli ultimi 6 mesi.

![](assets/unique-visitors-incr.png)

Dai dati raccolti 6 mesi prima e 6 mesi dopo l&#39;abilitazione dell&#39;HBA, è emerso un notevole aumento del coinvolgimento dei visualizzatori per i canali abilitati all&#39;HBA. In pratica, gli utenti di MVPD che dispongono di HBA abilitati tendono a guardare in media il 30% di contenuti in più rispetto agli utenti di MVPD che non dispongono di HBA abilitati.

![](assets/user-engagement-increase.png)

## Supporto HBA per autenticazione Primetime {#auth-hba-support}

In questa sezione viene descritto il supporto HBA fornito dall&#39;autenticazione Primetime, il comportamento delle piattaforme di autenticazione Primetime nei flussi HBA e vengono fornite informazioni tecniche utili per l&#39;implementazione dell&#39;HBA.

Funzioni di autenticazione Primetime con supporto dell&#39;HBA

* Possibilità di impostare TTL di autenticazione diversi per le autenticazioni HBA e non HBA (richiede anche il supporto MVPD)
* Possibilità di selezionare automaticamente un MVPD (ignora selettore MVPD) se l&#39;autenticazione è scaduta. Questo è utile soprattutto quando i TTL degli HBA sono di piccole dimensioni.
* Possibilità di esporre ai programmatori se l&#39;autenticazione era HBA o meno (richiede anche il supporto MVPD)

### Esperienza utente HBA sulle piattaforme di autenticazione Primetime {#hba-user-exp}

Le tabelle seguenti forniscono informazioni sull&#39;esperienza utente per le piattaforme supportate quando l&#39;HBA è abilitato e quando l&#39;HBA non è abilitato:

| Flusso utente: tipo di piattaforma | swf, iOS, Android |
|---|---|
| Con HBA abilitato | Quando gli utenti sono a casa, vengono automaticamente autenticati. Dopo la scadenza del token di autenticazione HBA, gli utenti vengono automaticamente riautenticati. |
| Senza HBA | Gli utenti vengono invitati a selezionare il proprio MVPD e a immettere le proprie credenziali, anche se si trovano a casa.Dopo la scadenza del token di autenticazione, gli utenti devono immettere di nuovo le proprie credenziali. |

| Flusso utente: tipo di piattaforma | js, Windows (nativo) |
|---|---|
| Con HBA abilitato | Quando gli utenti sono a casa, vengono automaticamente autenticati. Dopo la scadenza del token di autenticazione HBA, gli utenti devono riselezionare il proprio MVPD dal selettore e verranno automaticamente autenticati. |
| Senza HBA | Gli utenti sono invitati a selezionare il proprio MVPD e a immettere le proprie credenziali, anche se si trovano a casa. Dopo la scadenza del token di autenticazione, gli utenti devono immettere nuovamente le credenziali. |

| Flusso utente: tipo di piattaforma | API REST senza client (autenticazione a seconda schermata) |
|---|---|
| Con HBA abilitato | Quando gli utenti sono a casa e utilizzano un’app API REST senza client, vengono automaticamente autenticati sul secondo dispositivo a schermo dopo aver inserito il codice di registrazione e aver selezionato il proprio MVPD. Dopo la scadenza del token di autenticazione HBA, gli utenti vengono automaticamente autenticati di nuovo (nella seconda periferica a schermo). |
| Senza HBA | Gli utenti sono invitati a selezionare il proprio MVPD e a immettere le proprie credenziali, anche se si trovano a casa. Dopo la scadenza del token di autenticazione, gli utenti devono immettere nuovamente le credenziali. |

### Dettagli tecnici dell&#39;implementazione dell&#39;HBA {#tech-details-hba}

#### Protocollo OAuth 2.0 {#oauth-2-protocol}

Nel flusso HBA per MVPD integrati con il protocollo di autenticazione OAuth 2.0, MVPD emette un token di aggiornamento e un Adobe emette un token di autenticazione HBA:

* Il token di aggiornamento ha un TTL determinato dai requisiti aziendali di MVPD.
* Il TTL del token di autenticazione HBA **deve essere minore di o uguale a** TTL del token di aggiornamento.


*Descrizione del flusso di autenticazione HBA per il protocollo OAuth 2.0*


| Azioni utente | Azioni di sistema |
|---|---|
| L’utente passa al sito del programmatore. Quando si tenta di riprodurre un video, viene visualizzato il selettore MVPD. L’utente seleziona il proprio MVPD e fa clic sull’accesso. | Viene eseguito un controllo dei precedenti personali. L&#39;MVPD applica il proprio insieme di regole per il rilevamento utente (ad esempio, mappare l&#39;indirizzo IP dell&#39;utente con l&#39;indirizzo MAC dei modem forniti dal distributore o dei set-top box connessi a banda larga). |
| Viene visualizzata una schermata, che persiste per circa 3 secondi. È possibile visualizzare una pagina interstiziale per informare l&#39;utente che l&#39;accesso viene eseguito automaticamente utilizzando il proprio account MVPD. | <ol><li>AccessEnabler, installato sul lato del programmatore, invia una richiesta di autenticazione (come richiesta HTTP) all’endpoint di autenticazione di Adobe Primetime.</li><li>L’endpoint di autenticazione Primetime reindirizza la richiesta all’endpoint di autenticazione MVPD. <br />**Nota:** La richiesta contiene `hba_flag` parametro (tentativo HBA = true) che indica che MVPD deve tentare l&#39;autenticazione HBA.</li><li>L’endpoint di autenticazione MVPD invia un codice di autorizzazione all’endpoint di autenticazione Adobe Primetime.</li><li>L’autenticazione di Adobe Primetime utilizza il codice di autorizzazione per richiedere un token di aggiornamento e un token di accesso dall’endpoint del token MVPD.</li><li>MVPD invia una decisione di autenticazione e `hba_status` (true/false) in `id_token`.</li><li>Viene inviata una chiamata all&#39;endpoint del profilo utente MVPD per esporre [chiave hba_status nei metadati utente](/help/authentication/user-metadata-feature.md#obtaining).</li><li>MVPD imposta il TTL del token di aggiornamento su un valore concordato con MVPD e Adobe imposta il TTL del token di autenticazione su un valore minore o uguale al valore del token di aggiornamento.</li></ol> |
| L’utente è autenticato e ora può sfogliare contenuti TV Everywhere autorizzati. | Il token di autenticazione viene passato all’utente che ora può esplorare correttamente il sito del programmatore. |

#### Protocollo SAML {#saml-protocol}

Descrizione del flusso di autenticazione HBA per il protocollo di autenticazione SAML

| Azioni utente | Azioni di sistema |
|---|---|
| L’utente passa al sito del programmatore. Quando si tenta di riprodurre un video, viene visualizzato il selettore MVPD. L’utente seleziona il proprio MVPD e fa clic sull’accesso. | Viene eseguito un controllo dei precedenti personali. L&#39;MVPD applica il proprio insieme di regole per il rilevamento utente (ad esempio, mappare l&#39;indirizzo IP dell&#39;utente con l&#39;indirizzo MAC dei modem forniti dal distributore o dei set-top box connessi a banda larga). |
| Viene visualizzata una schermata, che persiste per circa 3 secondi. È possibile visualizzare una pagina interstiziale per informare l&#39;utente che l&#39;accesso viene eseguito automaticamente utilizzando il proprio account MVPD. | <ol><li>AccessEnabler, installato sul lato del programmatore, invia una richiesta di autenticazione (come richiesta HTTP) all’endpoint di autenticazione di Adobe Primetime.</li><li>L’endpoint di autenticazione Primetime reindirizza la richiesta all’endpoint di autenticazione MVPD.</li><li>MVPD deve inviare una decisione di autenticazione sotto forma di risposta SAML che deve contenere il flag HBA: hba_status (true/false).</li><li>Viene inviata una chiamata all&#39;endpoint del profilo utente MVPD per esporre [chiave hba_status nei metadati utente](/help/authentication/user-metadata-feature.md#obtaining).</li></ol> |
| L’utente è autenticato e ora può sfogliare contenuti TV Everywhere autorizzati. | Il token di autenticazione viene passato all’utente che ora può esplorare correttamente il sito del programmatore. |


## Come attivare l&#39;HBA {#how-to-activate-hba}

* **Protocollo OAuth:**
   * Per l&#39;abilitazione dell&#39;HBA, vedere [Guida utente al dashboard di Primetime TVE](/help/authentication/tve-dashboard-user-guide.md)
* **Protocollo SAML:** Autenticazione basata su Home è attivata sul lato MVPD. Non è richiesta alcuna azione da parte del programmatore o dell’Adobe.
Per ulteriori informazioni sugli MVPD che supportano l&#39;autenticazione basata su home, vedere [Stato HBA per MVPD](/help/authentication/hba-status-mvpds.md).

## Domande frequenti {#faqs}


**Domanda:** Perché la separazione tra autenticazione basata sulla home con protocolli SAML e OAuth2?

**Risposta:** Il flusso HBA è diverso per i due protocolli. Dal punto di vista di un programmatore, non è necessario intervenire per garantire che l&#39;HBA sia abilitato per gli MVPD SAML, mentre per gli MVPD OAuth2, l&#39;HBA può essere attivato o disattivato nella dashboard di Primetime TVE.



**Domanda:** Gli utenti devono immettere un nome utente e una password la prima volta che si autenticano quando l&#39;HBA è abilitato?

**Risposta:** No, nome utente e password non sono obbligatori.



**Domanda:** Come si applica il controllo genitori?

**Risposta 1:** L&#39;Adobe può disabilitare l&#39;HBA per le integrazioni con canali che richiedono l&#39;approvazione del controllo genitori.

**Risposta 2:** Adobe sta lavorando con OATC su un documento UX che consiglia come impostare l&#39;esperienza HBA con il controllo genitori.



**Domanda:** I provider che supportano l&#39;HBA dispongono di finestre TTL più brevi per l&#39;HBA rispetto all&#39;autenticazione regolare?

**Risposta:** L’impostazione TTL è configurabile. È consigliabile impostare un valore TTL più breve per i token di autenticazione HBA per evitare errori di gestione.


## Informazioni utili {#useful-info}

* [HBA (Instant Access) Recommendations](http://www.ctamtve.com/instantaccess){target=_blank} - da CTAM
* [Implementazione di esempio dell&#39;HBA nell&#39;app del programmatore](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/files/HBA_Flow_Sample.pdf?dc=201604222139-1346){target=_blank} - per Adobe
  <!--* [Home Based Authentication User Experience Guidelines for TV Everywhere](http://oatc.us/Standards/DownloadRecommendedPractices.aspx){target=_blank} - by OATC-->
* [Casi di utilizzo e requisiti dell’autenticazione basata sulla home page](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/files/Defining%20TVE%20Home-Based%20Authentication%20(HBA)%20%20Use%20Cases%20and%20Requirements%20Recommended%20Practice%20Version%201_0%20FINAL%20DRAFT%20FOR%20BOARD%20APPROVAL.pdf){target=_blank} dall&#39;OATC
* [Infografica dell’autenticazione basata sulla home](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/files/AdobeNewsletterHBA.pdf?dc=201604260953-2640){target=_blank} - per Adobe
* [Autenticazione tramite il protocollo OAuth 2.0](/help/authentication/authn-oauth2-protocol.md)
* [Autenticazione con MVPD SAML](/help/authentication/authn-usecase.md)
* [Guida utente al dashboard di Primetime TVE](/help/authentication/tve-dashboard-user-guide.md)
* [hba_status Metadati utente](/help/authentication/user-metadata-feature.md#obtaining)
