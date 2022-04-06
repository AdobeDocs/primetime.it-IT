---
title: Guida introduttiva all’account IQ con account IQ, prerequisiti e onboarding
description: 'Come effettuare l’onboarding, i prerequisiti e iniziare a utilizzare l’Account IQ. '
source-git-commit: 258ce10297aa15086a3ed1c1a825af2a30d34d24
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---


# Come iniziare a usare l&#39;account IQ {#onboarding}

Continua a leggere per conoscere i prerequisiti per utilizzare Account IQ e come può la tua azienda a bordo per iniziare a guardare i punteggi di condivisione account degli abbonati.

## Prerequisiti {#prerequisites}

* L&#39;organizzazione deve essere registrata [!DNL Adobe Marketing Cloud] organizzazioni.

* Gli utenti di tale organizzazione devono essere assegnati in lettura e scrittura al dashboard TVE o in sola lettura al dashboard TVE.

### Prerequisiti per il browser {#browser-prerequisites}

L&#39;account IQ è un servizio Web in hosting. È compatibile con la versione più recente dei seguenti browser:

* Google Chrome
* Mozilla Firefox
* Versione Safari

### Come integrare le organizzazioni su Account IQ? {#steps-to-onboard}


Questo è quello che abbiamo al momento. Il piano è quello di sbarazzarsi del controllo dma_primetime e avere un profilo dedicato per AIQ. Gli utenti che devono accedere alla console avranno bisogno di tale profilo utente. Ciò non è tuttavia attuato al momento.

1. Avere la loro organizzazione integrata in Adobe Marketing Cloud @Eric o @Peter, si può prendere questo.  Penso che ora si chiami &quot;Experience Cloud&quot;, ma è una cosa secondaria.  C&#39;è più dettaglio in questo? Questo è gestito da un altro gruppo? In caso affermativo, forniamo un collegamento, un contatto, ecc.? Questo dovrebbe anche contenere un avvertimento sul controllo della loro organizzazione che fa già parte di un Experience Cloud.

2. Disporre di profili di sola lettura &quot;TVE Dashboard Read-Write&quot; o &quot;TVE Dashboard Read Only&quot; assegnati ai loro utenti in http://adminconsole.adobe.com/.
@Eric, sai come farlo?  Sono presenti passaggi secondari?  È possibile spiegare ai clienti perché hanno scelto Lettura-scrittura rispetto Sola lettura?
@Cristina, può fornire una breve spiegazione del fatto che questo è un approccio temporaneo e forse come funzionerà nella prossima versione?

3. Avere la loro organizzazione è stata inserita nella whitelist sul lato AIQ @Cristina, c&#39;è un processo che possiamo mettere in atto per gestirlo?  Ad esempio, invia un’e-mail a &quot;DL-AdobePass-Eng AdobePass-Eng@adobe.com&quot; con l’ID organizzazione dell’organizzazione, ecc.

<!-- these user groups set dma_primetime product context for the user accounts. In AIQ code we’re checking for this product context when providing access. Internally, in the code we have an additional condition: the org id should be whitelisted in order for the users to get access to their data. -->

Quando accedi all&#39;Adobe Enterprise Dashboard, vedrai i due gruppi di utenti appena creati nella tua organizzazione Adobe Marketing Cloud:

Lettura e scrittura della dashboard TVE - i membri di questo gruppo hanno diritti completi in tutte le sezioni modificabili del dashboard TVE Dashboard Sola lettura - i membri di questo gruppo hanno diritti di visualizzazione solo nell&#39;intero dashboard Aggiungi il tuo account al gruppo utenti di lettura e scrittura della dashboard TVE, nell&#39;Adobe Enterprise Dashboard e accedi in Adobe Primetime TVE Dashboard.  In seguito, potrai gestire le autorizzazioni utente in Adobe Enterprise Dashboard aggiungendo e rimuovendo gli utenti nei due gruppi di utenti elencati sopra.

..........

Nella documentazione fornita è presente la parte &quot;Guida introduttiva al provisioning degli utenti per dashboard TVE di Primetime&quot; che si applica alla console Adobe Pass ma dovrebbe essere simile anche a AIQ.
http://tve.helpdocsonline.com/primetime-tve-dashboard-user-guide L&#39;organizzazione interessata a AIQ dovrebbe essere un&#39;organizzazione registrata in Adobe Marketing Cloud Orgs. Gli utenti di quell’organizzazione devono essere assegnati a Dashboard TVE in modalità di lettura e scrittura oppure a Dashboard TVE in modalità di sola lettura.
Solo per tua conoscenza, questi gruppi di utenti impostano il contesto di prodotto dma_primetime per gli account utente. Nel codice AIQ stiamo verificando il contesto del prodotto quando forniamo l&#39;accesso. Internamente, nel codice abbiamo una condizione aggiuntiva: l’id organizzazione deve essere inserito nella whitelist per consentire agli utenti di accedere ai loro dati.
Questo è quello che abbiamo al momento. Il piano è quello di sbarazzarsi del controllo dma_primetime e avere un profilo dedicato per AIQ. Gli utenti che devono accedere alla console avranno bisogno di tale profilo utente. Ciò non è tuttavia attuato al momento.

.........................

1. Avere la loro organizzazione integrata in Adobe Marketing Cloud
2. Disporre di profili di sola lettura &quot;TVE Dashboard Read-Write&quot; o &quot;TVE Dashboard Read Only&quot; assegnati ai loro utenti in http://adminconsole.adobe.com/.
3. L&#39;organizzazione è stata inserita nella whitelist sul lato AIQ
