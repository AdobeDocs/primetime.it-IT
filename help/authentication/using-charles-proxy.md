---
title: Utilizzo di Charles Proxy
description: Utilizzo di Charles Proxy
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---


# Utilizzo di Charles Proxy {#using-charles-proxy}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.


**Charles:** <http://charlesproxy.com>

 
## Scarica, installa e inizia con Charles Proxy {#download-install-and-get-stared-with-charles-proxy}

- **Scarica** - <http://www.charlesproxy.com/download/>
- **Installa** - <http://www.charlesproxy.com/documentation/installation/>
- **Introduzione** - <http://www.charlesproxy.com/documentation/getting-started/>

 
## Struttura e schede di sequenza {#structure-vs-sequence-tabs}

Esistono due modi diversi per visualizzare il traffico:

1. **Struttura** - Richieste raggruppate per host
1. **Sequenza** - Le richieste sono elencate nell’ordine in cui vengono chiamate


## SSL e certificati {#ssl-and-certificates}

Abilita proxy SSL `\[ *Proxy -\> Proxy Settings... -\> SSL* \]`

Seleziona la casella di controllo &quot;Abilita proxy SSL&quot; e aggiungi tutte le posizioni HTTPS.


![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/ProxySettings.PNG) ![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/SSLSettings.PNG) ![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/AddHttpsLocations.PNG)



- Proxy SSL - <http://www.charlesproxy.com/documentation/proxying/ssl-proxying/>
- Certificati SSL - <http://www.charlesproxy.com/documentation/using-charles/ssl-certificates/>
- Proxy SSL da dispositivi mobili - Vedi sotto.

 
## Ignora/Escludi host {#ignore-/-exclude-hosts}

Se l&#39;output diventa troppo limitato, puoi scegliere di ignorare o escludere le posizioni Puoi ignorare o escludere le posizioni eseguendo una delle seguenti operazioni:

- Fai clic con il pulsante destro del mouse sulle richieste da ignorare e seleziona &quot;Ignora&quot;
- Aggiungi manualmente le posizioni da escludere `\[ *Proxy -\> Recording Settings... -\> Exclude* \]`

 
## Spoofing DNS {#dns-spoffing}

`\[ *Tools -\> DNS Spoofing...* \]`

 

Lo spoofing DNS è molto utile quando si tenta di reindirizzare una richiesta a un IP diverso, soprattutto quando si lavora con i dispositivi mobili:

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/DNSSpoofing.PNG)

<http://www.charlesproxy.com/documentation/tools/dns-spoofing/>

 
## Mappa remota {#map-remote}

`\[ *Tools -\> Map Remote...* \]`

 

Con map remote è possibile reindirizzare una richiesta &quot;in arrivo&quot; a un endpoint diverso. Il caso d’uso più comune per questa funzione è &quot;Mappa&quot; `AccessEnabler.swf` a `AccessEnablerDebug.swf:`

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/MapRemote.PNG) ![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/MapRemoteAdd.PNG)

<http://www.charlesproxy.com/documentation/tools/map-remote/>

 

## Proxy inverso {#reverse-proxy}

<http://www.charlesproxy.com/documentation/proxying/reverse-proxy/>

## Mobile {#mobile}

### Usa Charles su un dispositivo iOS (iPhone / iPad) {#use-charles-on-an-ios-device-(iphone-/-ipad)}

#### Connessione SSL da iPhone {#ssl-connection-from-iphone}

Sfoglia per <http://charlesproxy.com/charles.crt> dal tuo dispositivo iOS.  Verrà avviata la finestra di dialogo di installazione del certificato:

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceSSLCertificate1\(1\).PNG)![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceSSLCertificate2\(1\).PNG)![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceSSLCertificate3.PNG)

 </br>

Fai clic su `\[ *Install*... *Install*... *Done* \]` per completare l’installazione del certificato.

<http://www.charlesproxy.com/documentation/faqs/ssl-connections-from-within-iphone-applications/>

 

#### Utilizzo di Charles da un dispositivo iOS {#using-charles-from-an-ios-device}

Sul tuo dispositivo iOS seleziona `\[ *Settings* -\> *Wi-FI* -\> (*YOUR\_WIFI\_NETWORK)* \]`. Fare clic sulla piccola freccia blu accanto alla rete, quindi scendere a Proxy HTTP e selezionare &quot;Manuale&quot;: 


 </br>

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceManualProxy1.png)![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceManualProxy2.PNG)


 </br>
Qui è necessario specificare l&#39;IP e la porta della macchina in cui si esegue Charles. <span style="line-height: 1.6em;">Se ora apri Safari sul tuo dispositivo iOS e provi ad aprire una pagina web, dovresti ottenere la seguente finestra a comparsa sul computer che esegue Charles:
 
 </br>

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceManualProxy3.PNG)

</br>
Fai clic su "Consenti" per consentire al dispositivo di utilizzare Charles per delegare tutte le sue richieste.

<http://www.charlesproxy.com/documentation/faqs/using-charles-from-an-iphone/>


#### iOS - Considera attendibili tutti i certificati {#ios-trust-any-certificates}

<http://stackoverflow.com/questions/933331/how-to-use-nsurlconnection-to-connect-with-ssl-for-an-untrusted-cert>

#### Errore di autenticazione iOS - impossibile trovare adobepass.ios.app

<https://tve.zendesk.com/entries/22135907-ios-authentication-error-adobepass-ios-app-cannot-be-found>


## Usa Charles per Android

<http://jaanus.com/post/17476995356/debugging-http-on-an-android-phone-or-tablet-with>

<http://www.charlesproxy.com/documentation/configuration/browser-and-system-configuration>


Sfoglia per [proxy Charles](http://charlesproxy.com/charles.crt) dal tuo dispositivo Android.
