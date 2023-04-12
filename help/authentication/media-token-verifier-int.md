---
title: Integrazione del verificatore del token multimediale
description: Integrazione del verificatore del token multimediale
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 0%

---


# Integrazione del verificatore del token multimediale

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Informazioni su Media Token Verifier {#about-media-token-verifier}

Quando l’autorizzazione ha esito positivo, l’autenticazione Adobe Primetime crea un token di autorizzazione a lungo termine (AuthZ).  Il token AuthZ viene passato al lato client o memorizzato sul lato server, a seconda della piattaforma del client.  (Vedi [Informazioni sui token](/help/authentication/programmer-overview.md#understanding-tokens) per sapere come i token vengono memorizzati su diversi sistemi client, insieme ad altri dettagli.)


Un token AuthZ autorizza l’utente del sito a visualizzare una determinata risorsa.  Il valore TTL (time-to-live) tipico varia da 6 a 24 ore, dopodiché scade il token. **Per l’accesso effettivo alla visualizzazione, l’autenticazione Primetime utilizza il token AuthZ per generare un token multimediale di breve durata che puoi ottenere e passare al server multimediale**. Questi token multimediali di breve durata hanno un TTL molto breve (in genere, alcuni minuti).


Nelle integrazioni di AccessEnabler, puoi ottenere il token multimediale di breve durata tramite il `setToken()` callback. Per le integrazioni API senza client, ottieni il token Media di breve durata con il `<SP_FQDN>/api/v1/tokens/media` Chiamata API. Il token è una stringa inviata in testo non crittografato, firmata per Adobe, utilizzando la protezione dei token basata su PKI (Public Key Infrastructure). Con questa protezione basata su PKI, il token viene firmato utilizzando una chiave asimmetrica, rilasciata ad Adobe da un’autorità di certificazione.


Poiché sul lato client non è presente alcuna convalida per il token, un utente malintenzionato potrebbe utilizzare strumenti per inserire falsi `setToken()` chiamate. Pertanto **impossibile** si affidano semplicemente al fatto che `setToken()` è stato attivato, quando si valuta se un utente è autorizzato o meno. È necessario verificare che il token di breve durata sia legittimo. Lo strumento per eseguire la convalida è la libreria del verificatore di token multimediali.


>[!TIP]
>
>Per eseguire la convalida, devi passare l’intera lunghezza della stringa token restituita al verificatore del token multimediale.

## Convalida di token di breve durata con Media Token Verifier {#validate-short-livedttokens}

È consigliabile che i programmatori inviino il token a un servizio Web che utilizza la libreria del verificatore dei token multimediali, al fine di convalidare il token prima di avviare effettivamente il flusso video. Il TTL molto breve dei token per contenuti multimediali di breve durata è definito come sufficientemente lungo per consentire problemi di sincronizzazione dell’orologio tra il server che genera il token e il server che convalida il token, ma non più.



La [Libreria di verificatori di token multimediali](https://adobeprimetime.zendesk.com/auth/v2/login/signin?return_to=https%3A%2F%2Ftve.zendesk.com%2Fhc%2Fen-us%2Farticles%2F204963159-Media-Token-Verifier-library&amp;theme=hc&amp;locale=en-us&amp;brand_id=343429&amp;auth_origin=343429%2Cfalse%2Ctrue){target=_blank} è disponibile per i partner di autenticazione di Primetime.



La libreria Media Token Verifier è contenuta nell’archivio Java `mediatoken-verifier-VERSION.jar`. La libreria definisce:

* Un’API di verifica del token (`ITokenVerifier` interfaccia), con documentazione JavaDoc
* Chiave pubblica Adobe utilizzata per verificare che il token provenga effettivamente dall’Adobe
* Un&#39;implementazione di riferimento (`com.adobe.entitlement.test.EntitlementVerifierTest.java`) che mostra come utilizzare l’API del verificatore e come utilizzare la chiave pubblica Adobe contenuta nella libreria per verificarne l’origine


L&#39;archivio contiene tutte le dipendenze e gli archivi chiavi dei certificati. La password predefinita per l’archivio chiavi del certificato incluso è &quot;123456&quot;.

* La libreria di verifica richiede JDK versione 1.5 o successiva.
* Utilizza il provider JCE preferito per l’algoritmo di firma &quot;SHA256WithRSA&quot;.


**La libreria dei verificatori deve essere l’unico mezzo utilizzato per analizzare il contenuto del token. I programmatori non devono analizzare il token ed estrarre i dati stessi, perché il formato del token non è garantito ed è soggetto a modifiche future.** Solo l’API del verificatore funziona correttamente. L&#39;analisi diretta della stringa potrebbe funzionare temporaneamente, ma in futuro potrebbe verificarsi un problema in caso di modifica del formato. L’API Verifier recupera informazioni dal token, ad esempio:

* È valido il token (il `isValid()` metodo)?
* L&#39;ID risorsa associato al token (il `getResourceID()` metodo); questo può essere confrontato con (e deve corrispondere) l&#39;altro parametro del `setToken()` callback di funzione. Se non corrisponde, ciò potrebbe indicare un comportamento fraudolento.
* Data e ora di emissione del token (`getTimeIssued()` metodo).
* TTL (`getTimeToLive()` metodo).
* Un GUID di autenticazione anonimo ricevuto dall&#39;MVPD (`getUserSessionGUID()` metodo).
* L&#39;ID del distributore che ha autenticato l&#39;utente e, se è il caso, il proxy-MVPD che ha fornito l&#39;autenticazione per il distributore.

## Utilizzo dell’API del verificatore {#using-verifier-api}

La `ITokenVerifier` La classe definisce i metodi utilizzati per convalidare l&#39;autenticità del token per una determinata risorsa. Utilizza la `ITokenVerifier` metodi per analizzare un token ricevuto in risposta a un `setToken()` richiesta.


La `isValid()` metodo è il mezzo principale per convalidare un token. Richiede un argomento, un ID risorsa. Se trasmetti un ID risorsa nullo, il metodo convalida solo l&#39;autenticità e il periodo di validità del token.


La `isValid()` restituisce uno dei seguenti valori di stato:



| VALID_TOKEN | Tutte le convalide sono state completate |
|--------------------|-----------------------------------------|
| INVALID_TOKEN_FORMAT | Formato del token non valido |
| INVALID_SIGNATURE | Impossibile convalidare l&#39;autenticità del token |
| TOKEN_EXPIRED | Il TTL del token non è valido |
| INVALID_RESOURCE_ID | Token non valido per la risorsa specificata |
| ERROR_UNKNOWN | Il token non è ancora stato convalidato |

I metodi aggiuntivi forniscono l’accesso specifico all’ID risorsa, all’ora di rilascio e al time-to-live per un token specificato.

* Utilizzo `getResourceID()` per recuperare l’ID risorsa associato al token e confrontarlo con l’ID restituito dalla richiesta setToken() .
* Utilizzo `getTimeIssued()` per recuperare l’ora in cui è stato emesso il token.
* Utilizzo `getTimeToLive()` per recuperare il TTL.
* Utilizzo `getUserSessionGUID()` per recuperare un GUID anonimizzato impostato dall&#39;MVPD.
* Utilizzo `getMvpdId()` per recuperare l&#39;ID dell&#39;MVPD che ha autenticato l&#39;utente.
* Utilizzo `getProxyMvpdId()` per recuperare l&#39;ID dell&#39;MVPD proxy che ha autenticato l&#39;utente.

## Codice di esempio {#sample-code}

L’archivio del verificatore dei token multimediali contiene un’implementazione di riferimento (`com.adobe.entitlement.test.EntitlementVerifierTest.java`) e un esempio di chiamata dell&#39;API con la classe test. Questo campione (`com.adobe.entitlement.text.EntitlementVerifierTest.java`) illustra l’integrazione della libreria di verifica token in un server multimediale.


```Java
package com.adobe.entitlement.test; 
import com.adobe.entitlement.verifier.CryptoDataHolder;
import com.adobe.entitlement.verifier.ITokenVerifier;
import com.adobe.entitlement.verifier.ITokenVerifierFactory;
import com.adobe.entitlement.verifier.SimpleTokenPKISignatureVerifierFactory;
import com.adobe.tve.crypto.SignatureVerificationCredential; 
import java.io.InputStream; 

public class EntitlementVerifierTest { 
    String mRequestorID = null;
    String mTokenToVerify = null;
    String mPathToCertificate = null;
    String mKeystoreType = null;
    String mKeystorePasswd = null;
    String mResourceID = null;

    public static void main(String[] args) { 
        if (args == null || args.length < 2 ) {
            System.out.println("Incorrect args: Usage: EntitlementVerifierTest requestorID tokenToVerify [resourceID]");
            return;
        } 
        String requestorID = args[0];
        String tokenToVerify = args[1];
        String pathToCertificate = "media_token_keystore.jks"; // the default keystore provided in the entitlement jar 
        String keystoreType = "jks";
        String keystorePasswd = "123456"; // password for the default keystore 
        if (requestorID == null || tokenToVerify == null) {
            System.out.println("One or more arguments is null");
            return;
        } 
        System.out.println("RequestorID: " + requestorID);
        System.out.println("token: " + tokenToVerify);
        System.out.println("cert: " + pathToCertificate);
        System.out.println("keystoretype: " + keystoreType);
        System.out.println("keystore passwd: " + keystorePasswd);
        String resourceID = null;
        if (args.length > 2) {
            resourceID = args[2];
        }
        System.out.println("Resource ID: " + resourceID);
        EntitlementVerifierTest verifier = new EntitlementVerifierTest(requestorID,
            tokenToVerify, pathToCertificate, keystoreType, keystorePasswd, resourceID);
        verifier.verifyToken();
    } 

    protected EntitlementVerifierTest(String inRequestorID,
                                      String inTokenToVerify,
                                      String inPathToCertificate,
                                      String inKeystoreType,
                                      String inKeystorePasswd, String inResourceID) {
        mRequestorID = inRequestorID;
        mTokenToVerify = inTokenToVerify;
        mPathToCertificate = inPathToCertificate;
        mKeystoreType = inKeystoreType;
        mKeystorePasswd = inKeystorePasswd;
        mResourceID = inResourceID;
    } 

    protected void verifyToken() {
        // It is expected that the SignatureVerificationCredential and 
        // CryptoDataHolder could be created at Init time in a web application 
        // and be reused for all token verifications. 
        CryptoDataHolder cryptoData = createCryptoDataHolder(mPathToCertificate, mKeystoreType, mKeystorePasswd);
        ITokenVerifierFactory tokenVerifierFactory = new SimpleTokenPKISignatureVerifierFactory();
        ITokenVerifier tokenVerifier = tokenVerifierFactory.getInstance(mRequestorID, mTokenToVerify, cryptoData);
        ITokenVerifier.eReturnValue status = tokenVerifier.isValid(mResourceID);
        System.out.println("Is token Valid? : " + status.toString());
        System.out.println("Token User ID: " + tokenVerifier.getUserSessionGUID());
        System.out.println("Token was generated at: " + tokenVerifier.getTimeIssued());

        System.out.println("Token Mvpd ID: " + tokenVerifier.getMvpdId());
        System.out.println("Token Proxy Mvpd ID: " + tokenVerifier.getProxyMvpdId());
    } 
    protected CryptoDataHolder createCryptoDataHolder(String pathToCertificate,
                                                      String keystoreType, String keystorePasswd) {
        SignatureVerificationCredential verificationCredential =
            readShortTokenVerificationCredential(pathToCertificate, keystoreType, keystorePasswd);
        CryptoDataHolder cryptoData = new CryptoDataHolder();
        cryptoData.setCertificateInfo(verificationCredential);
        return cryptoData;
    } 
    protected SignatureVerificationCredential readShortTokenVerificationCredential(String keystoreFile,
                                                                                   String keystoreType,
                                                                                   String keystorePasswd) {
        SignatureVerificationCredential cred = null; 
        if (keystoreFile != null){
            try {
                // load the keystore file 
                ClassLoader loader = EntitlementVerifierTest.class.getClassLoader();
                InputStream certInputStream =  loader.getResourceAsStream(keystoreFile);
                if (certInputStream != null) {
                    cred = new SignatureVerificationCredential(certInputStream, keystorePasswd, keystoreType);          
                }
            }
            catch (Exception e) {
                System.out.println("Error creating short token server credentials: " + e.getMessage());
            }
        }
        if (cred == null) {
            System.out.println("Error creating short token server credentials");
        } 
        return cred;
    } 
}
```
