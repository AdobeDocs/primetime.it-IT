---
title: Benvenuto in Adobe&reg; Autenticazione Primetime
description: Benvenuto in Adobe&reg; Panoramica sull’autenticazione di Primetime
source-git-commit: 79cdd0b7ae33d7c1d2bec970ecd3654aea4fdab0
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 1%

---


# Benvenuto in Adobe® Primetime Authentication {#overview}

L’autenticazione Adobe Primetime è una soluzione di adesione per TV Everywhere, che fornisce un framework modulare per determinare se qualcuno che richiede l’accesso a una risorsa ne ha diritto. Per partecipare alla soluzione di adesione all&#39;autenticazione Primetime, Content Provider (programmatori) e Pay TV Provider (MVPD) integrano i propri sistemi di adesione con i flussi di lavoro di autenticazione Primetime. Questo sito di documentazione fornisce dettagli sul processo di integrazione e suggerimenti per i partner esistenti.

Il tuo feedback è sempre apprezzato.

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Aiuto e domande frequenti {#help-and-faqs-resources}

|Elementi in primo piano| |-| |<ul>&lt;>Guida utente dell&#39;HBA infografica Primetime TVE Dashboard di iOS Promozionale Temp Pass Home-Based Authentication (HBA)?

| Per programmatori | Per gli MVPD |
|----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
| <ul><li>Guida di Kickstart per programmatori</li><li> Selettore MVPD (&quot;picker&quot;)</li><li>Metadati utente</li></ul> | <ul><li>Guida di Kickstart MVPD</li><li>Autenticazione</li><li>Autorizzazione</li><li>Logout</li></ul> |
| **Per client app nativi** | **Per tutti** |
| <ul><li>Panoramica tecnica di iOS</li><li>Panoramica tecnica di Android</li></ul> | <ul><li>Carta tecnica</li><li>Procedure per l&#39;escalation</li><li>Sistemi supportati</li><li>Glossario</li><li>Note tecniche</li></ul> |
| Per dispositivi avanzati |  |
| <ul><li>Panoramica tecnica senza client</li><li>API senza client</li></ul> |

<div id="startcontainer">

<div class="table">

<table id="start-topic-table" data-border="0" data-cellpadding="0" data-cellspacing="0" style="height: 380px; width: 584px;">
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">Aiuto e domande frequenti</th>
<th style="text-align: left;"> </th>
<th style="text-align: left;"> </th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><p><strong>Per programmatori</strong></p>
<p> </p>
<ul>
<li><a href="#">Guida di Kickstart per programmatori</a></li>
</ul>
<ul>
<li><a href="#obtaining_mvpd_list">Selettore MVPD ("picker")</a></li>
<li><a href="#">Metadati utente</a></li>
</ul>
 
<p><strong>Per client app nativi</strong></p>
<ul>
<li><a href="#">Panoramica tecnica di iOS</a></li>
<li><a href="#">Panoramica tecnica di Android</a></li>
</ul>
<p> </p>
<p><strong>Per dispositivi avanzati</strong></p>
<ul>
<li><a href="http://tve.helpdocsonline.com/rest-api-overview">Panoramica tecnica senza client</a></li>
<li><a href="https://tve.helpdocsonline.com/rest-api-reference">API senza client</a></li>
</ul>
<p> </p></td>
<td style="text-align: left;"><p><strong>Per gli MVPD</strong></p>
<p> </p>
<ul>
<li><a href="#">Guida di Kickstart MVPD</a></li>
<li><a href="#">Autenticazione</a></li>
<li><a href="#">Autorizzazione</a></li>
</ul>
<ul>
<li><a href="#">Logout</a></li>
</ul>
 
<p><strong>Per tutti</strong></p>
<ul>
<li><a href="#">Carta tecnica</a></li>
<li><a href="#">Procedure per l'escalation</a></li>
<li><a href="#">Sistemi supportati</a></li>
<li><a href="#">Glossario</a></li>
<li><a href="#">Note tecniche</a></li>
</ul></td>
<td style="text-align: left;"><p><strong>Elementi in primo piano <img src="https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/1468939180_new.png?dc=201607190941-4" /></strong></p>
<p> </p>
<ul>
<li><a href="http://tve.helpdocsonline.com/ios/tvos-sso-changes">Single Sign-On per iOS</a></li>
<li><a href="#">Passaggio temporaneo promozionale</a></li>
<li><a href="#">Autenticazione basata su Home (HBA)</a></li>
<li><a href="https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/files/AdobeNewsletterHBA.pdf">Infografica HBA</a></li>
<li><a href="#">Guida utente di Primetime TVE Dashboard</a></li>
</ul></td>
</tr>
</tbody>
</table>

</div>

<div class="block">

## Non riesce a trovare una risposta?

[**Invia e-mail**](mailto:tve-support@adobe.com)

[Invia un messaggio e-mail al nostro team di supporto](mailto:tve-support@adobe.com) è anche il primo passo per qualsiasi problema o segnalazione di incidenti.

Se hai [**<span style="color:#ff0000;">SEVERITÀ 1 LIVE</span>**](http://tve.helpdocsonline.com/escalation-procedures-2)
problema, e ci avete mandato una email, e sono trascorsi 30 minuti\
senza una risposta, consulta\
[Procedure per l&#39;escalation](#) documento\
per i numeri di telefono da chiamare.

<div>

 

</div>

</div>

</div>

 

<span style="font-family: verdana, geneva, sans-serif;">Per trovare ciò di cui hai bisogno:</span>

<span style="font-family: verdana, geneva, sans-serif;">** **   **Ricerca** ovunque sull&#39;Helpdesk di autenticazione Primetime per ottenere i risultati che includono questa documentazione.\
     **Sfoglia** tutta la documentazione di autenticazione di Primetime, tramite la gerarchia delle cartelle nel riquadro di navigazione a sinistra.\
     **Filtro** la gerarchia delle cartelle immettendo termini nel campo nella parte superiore del riquadro di navigazione.\
     **Segnalibro** &quot;collegamenti profondi&quot; alle pagine di interesse utilizzando il browser web.</span>
