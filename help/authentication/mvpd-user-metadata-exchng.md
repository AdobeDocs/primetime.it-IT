---
title: Scambio metadati utente MVPD
description: Scambio metadati utente MVPD
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 0%

---


# Scambio metadati utente MVPD

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Introduzione {#intro-user-metadata-exchange}

Gli MVPD mantengono metadati specifici dell&#39;utente sui propri clienti che in alcuni casi vengono condivisi con i programmatori. L&#39;obiettivo dell&#39;autenticazione Adobe Primetime è quello di broker uno scambio di questi &quot;metadati utente&quot;, ma non di applicare alcun tipo di regole relative allo scambio. Le regole di scambio sono per gli MVPD di lavorare con i loro partner programmatori.

I tipi di metadati utente disponibili per lo scambio includono attualmente:

* Codice postale
* Potenza massima (VChip o MPAA)
* ID utente
* ID famiglia
* ID canale

Utilizzando questa funzione, gli MVPD e i programmatori possono implementare casi d&#39;uso speciali come il controllo dei genitori. Ad esempio, un MVPD può trasmettere i dati di valutazione dei genitori a un programmatore, che quindi utilizza tali dati per filtrare le scelte di visualizzazione disponibili per un utente.

Punti chiave metadati utente:

* Il MVPD trasmette i metadati utente all&#39;applicazione del programmatore durante i flussi di autenticazione e autorizzazione
* L’autenticazione Adobe Primetime salva i valori dei metadati nei token AuthN e AuthZ
* L&#39;autenticazione Adobe Primetime può normalizzare i valori per gli MVPD che forniscono i metadati utente in diversi formati
* Alcuni parametri possono essere crittografati utilizzando la chiave del programmatore
* Valori specifici sono resi disponibili per Adobe tramite una modifica della configurazione

>[!NOTE]
>
>I metadati utente sono un&#39;estensione dei metadati statici (Authentication token TTL, Authorization token TTL e Device ID) precedentemente disponibili nell&#39;autenticazione Adobe Primetime.

## Esempi {#example-mvpd-user-metadata-exch}

### Controllo genitori {#example-parental-control}

Questo esempio mostra lo scambio dei seguenti elementi:

* [Scambio di metadati tra programmatori e MVPD](#progr-mvpd-metadata-exch)

* [Flusso di scambio dei metadati MVPD a programmatore](#mvpd-progr-exchange-flow)

### Scambio di metadati tra programmatori e MVPD {#progr-mvpd-metadata-exch}

Attualmente l’API programmatore, l’autenticazione Adobe Primetime e gli autori MVPD supportano solo l’autorizzazione a livello di canale. Il canale è specificato come stringa di testo normale nella chiamata API getAuthorization() del programmatore. Questa stringa viene propagata fino al backend di autorizzazione dell&#39;MVPD:

Dall&#39;app o dal sito del programmatore, l&#39;utente sceglie un MVPD compatibile XACML (in questo esempio, &quot;TNT&quot;). Per informazioni su XACML, vedi [Linguaggio markup del controllo di accesso espandibile](https://en.wikipedia.org/wiki/XACML){target=_blank}.
L’app del programmatore forma una richiesta AuthZ che include la risorsa e i relativi metadati.  Questo esempio include una classificazione MPAA di &quot;pg&quot; nell&#39;attributo media dell&#39;elemento channel:

```XML
var resource = '<rss version="2.0" xmlns:media="http://video.search.yahoo.com/mrss/">
                    <channel> 
                        <title>TNT</title> 
                        <media:rating scheme="urn:mpaa">pg</media:rating>
                    </channel>
                </rss>';
getAuthorization(resource);
```

L’autenticazione Adobe Primetime supporta in realtà un’autorizzazione più granulare, fino al livello delle risorse, se supportata sia dall’MVPD che dal programmatore. La risorsa e i suoi metadati sono opachi all&#39;Adobe; lo scopo è quello di stabilire un formato standard per specificare l’ID risorsa e i metadati in modo normalizzato, in modo da inviare gli ID risorsa a MVPD diversi.

>[!NOTE]
>
>Se l&#39;utente sceglie un MVPD compatibile solo con il canale, l&#39;autenticazione Adobe Primetime estrae SOLO il titolo del canale (&quot;TNT&quot; nell&#39;esempio precedente) e passa solo il titolo all&#39;MVPD.

### Flusso di scambio dei metadati MVPD a programmatore {#mvpd-progr-exchange-flow}

L’autenticazione Adobe Primetime prevede quanto segue:

* L&#39;MVPD invia il rating massimo come parte della risposta SAML
* Queste informazioni vengono salvate come parte del token di autenticazione
* L’autenticazione Adobe Primetime fornisce un’API che consente ai programmatori di recuperare queste informazioni
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

**Normalizzazione e convalida delle risorse.** Gli ID risorsa possono essere trasmessi come stringa normale o come stringa MRSS. Un programmatore può decidere di utilizzare il formato stringa normale o il MRSS, ma avrà bisogno di un accordo preliminare con il MVPD in modo che il MVPD sappia come trattare quella risorsa.

**ID risorsa e specifiche metadati.** L’autenticazione Adobe Primetime utilizza lo standard RSS con l’estensione Media RSS per specificare una risorsa e i relativi metadati. Insieme all&#39;estensione Media RSS, l&#39;autenticazione Adobe Primetime supporta un&#39;ampia varietà di metadati, come i controlli parentali (tramite `<media:rating>`) o geolocalizzazione (`<media:location>`).

L’autenticazione Adobe Primetime può anche supportare la conversione trasparente dalla stringa di canale legacy alla risorsa RSS corrispondente per gli MVPD che richiedono RSS. Nella direzione opposta, l&#39;autenticazione Adobe Primetime supporta la conversione da RSS+MRSS al titolo del canale normale, per MVPD solo canale.

**L’autenticazione Adobe Primetime garantisce la piena compatibilità con le integrazioni esistenti.** In altre parole, per i programmatori che utilizzano l’autenticazione a livello di canale, l’autenticazione Adobe Primetime si occupa di creare un pacchetto dell’ID canale nel formato necessario prima di inviarlo a un MVPD che comprenda tale formato. Si applica anche il contrario: se un programmatore specifica tutte le risorse in un nuovo formato, l&#39;autenticazione Adobe Primetime traduce il nuovo formato in una stringa di canale semplice se l&#39;autorizzazione viene eseguita su un MVPD che esegue solo l&#39;autorizzazione a livello di canale.

## Casi d’uso dei metadati utente {#user-metadata-use-cases}

I casi d&#39;uso stanno cambiando sempre di più e si espandono man mano che più MVPD prendono accordi legali e aggiungono funzionalità. Di seguito sono riportati alcuni esempi di utilizzo dei metadati utente.

* [ID utente MVPD](#mvpd-user-id)
* [ID famiglia](#household-user-id)
* [Codice postale](#zip-code)
* [Valutazione massima (controllo genitori)](#max-rating-parental-control)
* [Line-up dei canali](#channel-line-up)

### ID utente MVPD {#mvpd-user-id}

* Come fornito dall&#39;MVPD
* Non le informazioni di accesso effettive dell&#39;utente, in quanto sono crittografate dall&#39;MVPD
* Può essere utilizzato per indicare problemi con o per utenti specifici
* Crittografato
* Supporto MVPD: Tutti gli MVPD

### ID utente domestico {#household-user-id}

* Consente di ottenere buone informazioni metriche
* Crittografato
* Supporto MVPD: Alcuni MVPD

### Codice postale {#zip-code}

* Codice postale di fatturazione dell’utente
* Utilizzato principalmente per applicare le regole del periodo di congelamento degli eventi sportivi
* Può essere fornita con la risposta AuthZ per aggiornamenti rapidi
* Supporto MVPD: Alcuni MVPD

### Valutazione massima (controllo genitori) {#max-rating-parental-control}

* AuthN inizialmente, più aggiornamento AuthZ
* Filtrare il contenuto dall’interfaccia utente
* Classificazioni MPAA o VChip
* Supporto MVPD: Alcuni MVPD

### Line-up dei canali {#channel-line-up}

* Gli MVPD possono fornire un elenco di canali che l&#39;utente ha diritto di visualizzare
* Consente di colorare rapidamente l’interfaccia utente
* La specifica OLCA consente questo come AttributeStatement nella risposta AuthN
* Supporta gli MVPD: Alcuni MVPD

<!--
>[!RELATEDINFORMATION]
>
>* [Proxy MVPD Web Service](/help/authentication/proxy-mvpd-webserv.md)
>* [Content Metadata Exhange](/help/authentication/mvpd-content-metadata-exchange.md)
>* [OLCA AuthN / AuthZ Specification](https://www.cablelabs.com/specifications/CL-SP-AUTH1.0-I04-120621.pdf){target=_blank}
>* [User Metadata (Programmer Integration Guide)](/help/authentication/user-metadata-feature.md)
-->
