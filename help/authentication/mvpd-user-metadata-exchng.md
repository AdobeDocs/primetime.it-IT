---
title: Scambio metadati utenti MVPD
description: Scambio metadati utenti MVPD
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 0%

---

# Scambio metadati utenti MVPD

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente di Adobe. Non è consentito alcun uso non autorizzato.

## Introduzione {#intro-user-metadata-exchange}

Gli MVPD gestiscono metadati specifici per l&#39;utente sui propri clienti che in alcuni casi vengono condivisi con i programmatori. Lo scopo dell’autenticazione Adobe Primetime è quello di gestire uno scambio di questi &quot;metadati utente&quot;, ma non di applicare alcun tipo di regola relativa allo scambio. Le regole di scambio sono per gli MVPD di lavorare con i loro partner programmatori.

I tipi di metadati utente disponibili per Exchange includono attualmente i seguenti:

* Codice postale
* Classificazione massima (VChip o MPAA)
* ID utente
* ID famiglia
* ID canale

Utilizzando questa funzione, MVPD e programmatori possono implementare casi d&#39;uso speciali come il controllo parentale. Ad esempio, un MVPD può trasmettere i dati di valutazione dei genitori a un programmatore, che utilizza tali dati per filtrare le scelte di visualizzazione disponibili per un utente.

Punti chiave metadati utente:

* MVPD trasmette i metadati utente all&#39;applicazione del programmatore durante i flussi di autenticazione e autorizzazione
* L’autenticazione Adobe Primetime salva i valori dei metadati nei token AuthN e AuthZ
* L’autenticazione Adobe Primetime può normalizzare i valori per MVPD che forniscono metadati utente in formati diversi
* Alcuni parametri possono essere crittografati utilizzando la chiave del programmatore
* Valori specifici sono resi disponibili da Adobe tramite una modifica alla configurazione

>[!NOTE]
>
>I metadati utente sono un’estensione dei metadati statici (TTL del token di autenticazione, TTL del token di autorizzazione e ID dispositivo) precedentemente disponibili nell’autenticazione di Adobe Primetime.

## Esempi {#example-mvpd-user-metadata-exch}

### Controllo genitori {#example-parental-control}

Questo esempio mostra lo scambio dei seguenti elementi:

* [Da programmatore a MVPD Metadata Exchange](#progr-mvpd-metadata-exch)

* [Flusso di scambio metadati da MVPD a programmatore](#mvpd-progr-exchange-flow)

### Da programmatore a MVPD Metadata Exchange {#progr-mvpd-metadata-exch}

Attualmente l’API del programmatore, l’autenticazione Adobe Primetime e gli autorizzatori MVPD supportano solo l’autorizzazione a livello di canale. Il canale viene specificato come stringa di testo normale nella chiamata API getAuthorization() del programmatore. Questa stringa viene propagata fino al backend di autorizzazione MVPD:

Dall&#39;app o dal sito del programmatore, l&#39;utente sceglie un MVPD compatibile con XACML (in questo esempio, &quot;TNT&quot;). Per informazioni su XACML, vedere [Linguaggio di markup del controllo di accesso estensibile](https://en.wikipedia.org/wiki/XACML){target=_blank}.
L’app del programmatore forma una richiesta AuthZ che include la risorsa e i relativi metadati.  Questo esempio include una valutazione MPAA di &quot;pg&quot; nell’attributo media dell’elemento channel:

```XML
var resource = '<rss version="2.0" xmlns:media="http://video.search.yahoo.com/mrss/">
                    <channel> 
                        <title>TNT</title> 
                        <media:rating scheme="urn:mpaa">pg</media:rating>
                    </channel>
                </rss>';
getAuthorization(resource);
```

L’autenticazione Adobe Primetime supporta in realtà un’autorizzazione più granulare, fino al livello della risorsa, se supportata sia da MVPD che dal programmatore. La risorsa e i relativi metadati sono opachi da Adobe; l’obiettivo è quello di stabilire un formato standard per specificare l’ID della risorsa e i metadati in modo normalizzato, per inviare gli ID delle risorse a diversi MVPD.

>[!NOTE]
>
>Se l’utente sceglie un MVPD compatibile solo con il canale, l’autenticazione Adobe Primetime estrae SOLO il titolo del canale (&quot;TNT&quot; nell’esempio precedente) e passa solo il titolo all’MVPD.

### Flusso di scambio metadati da MVPD a programmatore {#mvpd-progr-exchange-flow}

L’autenticazione Adobe Primetime si basa sui seguenti presupposti:

* MVPD invia la valutazione massima come parte della risposta SAML
* Informazioni salvate come parte del token di autenticazione
* L’autenticazione Adobe Primetime fornisce un’API per consentire ai programmatori di recuperare tali informazioni
* I programmatori implementano questa funzione sul sito o sull’app (ad esempio, per nascondere i video che superano la valutazione massima per l’utente)

```XML
<saml:Assertion ID="pfxec5f92e0-8589-3fc3-c708-f4fb8e2fad59"
                 IssueInstant="2010-07-20T10:05:41Z" Version="2.0"
                 xmlns:xs="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <saml:AttributeStatement>
        <saml:Attribute
                Name="MaxTVRating"
                NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
            <saml:AttributeValue xsi:type="xs:string">tv-ma</saml:AttributeValue>
        </saml:Attribute>
        <saml:Attribute
                Name="MaxMovieRating"
                NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
            <saml:AttributeValue xsi:type="xs:string">nc-17</saml:AttributeValue>
        </saml:Attribute>
    </saml:AttributeStatement>
</saml:Assertion>
```

### Note {#notes-mvpd-progr-metadata-exch-flow}

**Normalizzazione e convalida delle risorse.** Gli ID risorsa possono essere trasmessi come stringa semplice o come stringa MRSS. Un programmatore può decidere di utilizzare il formato di stringa semplice o il MRSS, ma avrà bisogno di un accordo preventivo con il MVPD in modo che il MVPD sappia come trattare tale risorsa.

**ID risorsa e specifica metadati.** L’autenticazione Adobe Primetime utilizza lo standard RSS con l’estensione Media RSS per specificare una risorsa e i relativi metadati. Insieme all’estensione Media RSS, l’autenticazione Adobe Primetime supporta un’ampia gamma di metadati, come il controllo genitori (tramite `<media:rating>`) o geolocalizzazione (`<media:location>`).

L’autenticazione Adobe Primetime può inoltre supportare la conversione trasparente dalla stringa di canale legacy alla risorsa RSS corrispondente per gli MVPD che richiedono RSS. Nell’altra direzione, l’autenticazione Adobe Primetime supporta la conversione da RSS+MRSS a titolo di canale semplice, per gli MVPD solo per canale.

**L’autenticazione Adobe Primetime garantisce la piena compatibilità con le versioni precedenti delle integrazioni esistenti.** In altre parole, per i programmatori che utilizzano l’autenticazione a livello di canale, l’autenticazione Adobe Primetime si occupa di creare un pacchetto dell’ID di canale nel formato necessario prima di inviarlo a un MVPD che lo capisca. Si applica anche il contrario: se un programmatore specifica tutte le sue risorse in un nuovo formato, l&#39;autenticazione Adobe Primetime traduce il nuovo formato in una semplice stringa di canale se autorizza per un MVPD che esegue solo l&#39;autorizzazione a livello di canale.

## Casi di utilizzo dei metadati utente {#user-metadata-use-cases}

I casi d&#39;uso sono in continua evoluzione e in continua espansione, in quanto sempre più MVPD adottano disposizioni legali e aggiungono funzionalità. Di seguito sono riportati alcuni esempi dei metadati utilizzabili dagli utenti.

* [ID utente MVPD](#mvpd-user-id)
* [ID famiglia](#household-user-id)
* [Codice postale](#zip-code)
* [Valutazione massima (controllo genitori)](#max-rating-parental-control)
* [Line-up canali](#channel-line-up)

### ID utente MVPD {#mvpd-user-id}

* Come previsto dall&#39;MVPD
* Non le informazioni di accesso effettive dell’utente, poiché viene eseguito l’hashing da MVPD
* Può essere utilizzato per indicare problemi con o per utenti specifici
* Crittografato
* Supporto MVPD: tutti gli MVPD

### ID utente domestico {#household-user-id}

* Consente di ottenere informazioni metriche corrette
* Crittografato
* Supporto MVPD: alcuni MVPD

### Codice postale {#zip-code}

* Codice postale di fatturazione dell’utente
* Utilizzato principalmente per applicare le regole del periodo di blocco degli eventi sportivi
* Può essere fornita con la risposta AuthZ per aggiornamenti rapidi
* Supporto MVPD: alcuni MVPD

### Valutazione massima (controllo genitori) {#max-rating-parental-control}

* AuthN inizialmente, più aggiornamento AuthZ
* Filtrare i contenuti dall’interfaccia utente
* Valutazioni MPAA o VChip
* Supporto MVPD: alcuni MVPD

### Line-up canali {#channel-line-up}

* Gli MVPD possono fornire un elenco di canali che l’utente è autorizzato a visualizzare
* Consente la colorazione rapida dell’interfaccia utente
* La specifica OLCA lo consente come AttributeStatement nella risposta AuthN
* MVPD di supporto: alcuni MVPD

<!--
>[!RELATEDINFORMATION]
>
>* [Proxy MVPD Web Service](/help/authentication/proxy-mvpd-webserv.md)
>* [Content Metadata Exhange](/help/authentication/mvpd-content-metadata-exchange.md)
>* [OLCA AuthN / AuthZ Specification](https://www.cablelabs.com/specifications/CL-SP-AUTH1.0-I04-120621.pdf){target=_blank}
>* [User Metadata (Programmer Integration Guide)](/help/authentication/user-metadata-feature.md)
-->
