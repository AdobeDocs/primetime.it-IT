---
title: Panoramica sulla distribuzione del server chiavi DRM di Primetime
description: Panoramica sulla distribuzione del server chiavi DRM di Primetime
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 0%

---


# Implementare il server chiavi DRM di Primetime {#deploy-the-primetime-drm-key-server}

Prima di distribuire il server chiavi DRM di Primetime, assicurati di aver installato le versioni richieste di Java e Tomcat. Vedere [Requisiti del server chiavi DRM](../../digital-rights-management/using-the-drm-key-server/requirements.md).

Il download del server chiavi DRM di Primetime include [!DNL faxsks.war]. Per distribuire questo file WAR, copia il file nella directory [!DNL webapps] di Tomcat. Se in precedenza hai implementato il file WAR, potrebbe essere necessario eliminare manualmente la directory WAR decompressa, [!DNL faxsks] nella directory [!DNL webapps] di Tomcat. Per evitare che Tomcat scompili i file WAR, modifica il file [!DNL server.xml] nella directory [!DNL conf] di Tomcat e imposta l&#39;attributo `unpackWARs` su `false`.

Il server chiavi DRM di Primetime utilizza facoltativamente una libreria specifica per la piattaforma (`jsafe.dll` su Windows o `libjsafe.so` su Linux) per migliorare le prestazioni. Copia la libreria appropriata per la piattaforma da `thirdparty/cryptoj/platform` in una posizione specificata dalla variabile di ambiente `PATH` (o `LD_LIBRARY_PATH` su Linux).

>[!NOTE]
>
>La versione a 64 bit della libreria [!DNL jsafe] deve essere utilizzata solo se sia il sistema operativo che JDK supportano 64-bit, altrimenti utilizza la versione a 32-bit.

## Configurazione SSL {#ssl-configuration}

SSL è richiesto per la consegna chiavi HTTPS remota. Le connessioni SSL possono essere gestite dal server dell’applicazione (ovvero configurando SSL in Tomcat) o possono essere gestite da un altro server (ad esempio, un load balancer, un acceleratore SSL o Apache). La consegna chiavi HTTPS remota richiede una connessione SSL. Il server richiede un certificato SSL rilasciato da una CA attendibile.

Sono disponibili diverse opzioni per la configurazione di SSL. Di seguito sono riportati alcuni esempi per configurare SSL con l’autenticazione client in Apache e Tomcat.

L’esempio seguente mostra la configurazione SSL di Apache:

```
SSLEngineon 
SSLCertificateFile "certs/server_cert.pem" 
SSLCertificateKeyFile "certs/server_key.pem" 
SSLOptions +StdEnvVars +FakeBasicAuth -ExportCertData +StrictRequire 
SSLRequireSSL 
ProxyRequests Off 
ProxyPass /https://keyserver-name:port/ 
ProxyPassReverse /https://keyserver-name:port/
```

L’esempio seguente mostra la configurazione SSL Tomcat. Per generare file di certificato e di chiave:

```
Generate key:  
 openssl genrsa -des3 -out server.key 1024 
Generate CSR: 
 openssl req -new -key server.key -out server.csr 
Generate Certificate: 
 openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.cer
```

Quando viene richiesto il nome comune, utilizzare il nome di dominio completo (FQDN) del server.

Copia [!DNL server.cer] e [!DNL server.key] nella directory Tomcat. Specifica il seguente connettore in [!DNL conf/server.xml]:

```
<Connector port="8443" protocol="HTTP/1.1" SSLEnabled="true" 
 maxThreads="150" scheme="https" secure="true" 
 sslProtocol="TLS" 
 SSLCertificateFile="${catalina.base}/server.cer" 
 SSLCertificateKeyFile="${catalina.base}/server.key" 
 SSLPassword="password-for-key-file" 
 SSLVerifyClient="require"/>
```

## Proprietà del sistema Java {#java-system-properties}

È possibile impostare le due seguenti proprietà del sistema Java per modificare la posizione della configurazione e dei file di registro per il server chiavi DRM di Primetime:

* `KeyServer.ConfigRoot` - Questa directory contiene tutti i file di configurazione per il server chiavi DRM di Primetime. Per informazioni dettagliate sul contenuto di questi file, vedere [File di configurazione del server chiavi](#key-server-configuration-files). Se non è impostato, il valore predefinito è [!DNL CATALINA_BASE/keyserver].

* `KeyServer.LogRoot` - Questa è una directory di registro che contiene i registri dell&#39;applicazione server chiavi iOS. Se non è impostato, il valore predefinito è lo stesso di `KeyServer.ConfigRoot`

* `XboxKeyServer.LogRoot` - Questa è una directory di registro che contiene i registri dell&#39;applicazione del server di chiavi Xbox. Se non è impostato, il valore predefinito è uguale a `KeyServer.ConfigRoot`.

Se utilizzi [!DNL catalina.bat] o [!DNL catalina.sh] per avviare Tomcat, queste proprietà del sistema possono essere facilmente impostate utilizzando la variabile di ambiente `JAVA_OPTS`. Tutte le opzioni Java impostate qui verranno utilizzate all’avvio di Tomcat. Ad esempio, imposta:

```
JAVA_OPTS=-DKeyServer.ConfigRoot=”absolute-path-to-config-folder” 
  -DKeyServer.LogRoot=”absolute-path-to-log-folder”
```

## Credenziali DRM di Primetime {#primetime-drm-credentials}

Per elaborare le richieste chiave dai client iOS e Xbox 360 DRM di Primetime, il server chiavi DRM di Primetime deve essere configurato con un set di credenziali emesse da Adobe. Queste credenziali possono essere archiviate in file PKCS#12 ( [!DNL .pfx]) o in un HSM.

I file [!DNL .pfx] possono trovarsi ovunque, ma per semplificare la configurazione, Adobe consiglia di inserire i file [!DNL .pfx] nella directory di configurazione del tenant. Per ulteriori informazioni, vedere [File di configurazione del server chiavi](#key-server-configuration-files).

### Configurazione HSM {#section_13A19E3E32934C5FA00AEF621F369877}

Se scegli di utilizzare un HSM per memorizzare le credenziali del server, devi caricare le chiavi private e i certificati nell’HSM e creare un file di configurazione *pkcs11.cfg*. Questo file deve trovarsi nella directory *KeyServer.ConfigRoot* . Per un esempio di file di configurazione PKCS 11, vedere la directory `<Primetime DRM Key Server>/configs` . Per informazioni sul formato di [!DNL pkcs11.cfg], consulta la documentazione del provider Sun PKCS11.

Per verificare che i file di configurazione HSM e Sun PKCS11 siano configurati correttamente, puoi usare il seguente comando dalla directory in cui si trova il file [!DNL pkcs11.cfg] ( [!DNL keytool] è installato con Java JRE e JDK):

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Se vengono visualizzate le credenziali nell’elenco, l’HSM è configurato correttamente e il server chiavi sarà in grado di accedere alle credenziali.

## File di configurazione del server chiave {#key-server-configuration-files}

Il server chiavi DRM di Primetime richiede due tipi di file di configurazione:

* Un file di configurazione globale, [!DNL flashaccess-keyserver-global.xml]
* Un file di configurazione tenant per ciascun tenant, [!DNL flashaccess-keyserver-tenant.xml]

Se vengono apportate modifiche ai file di configurazione, è necessario riavviare il server per rendere effettive le modifiche.

Per evitare di rendere le password disponibili in testo libero nei file di configurazione, tutte le password specificate nei file di configurazione globale e tenant devono essere crittografate. Per ulteriori informazioni sulla crittografia delle password, vedere [*Password Scrambler* in *Utilizzo del server DRM di Primetime per lo streaming protetto*](../protected-streaming/understanding-deployment/drm-for-protected-streaming-utilities/password-scrambler.md).

## Struttura della directory di configurazione {#configuration-directory-structure}

Le directory di configurazione hanno la seguente struttura:

```
KeyServer.ConfigRoot/  
--flashaccess-keyserver-global.xml 
--pkcs11.cfg (optional) 
--faxsks/ 
----tenants/ 
------tenantname/
---------flashaccess-keyserver-tenant.xml 
---------credential.pfx (optional) 
```

## File di configurazione globale {#global-configuration-file}

Il file di configurazione [!DNL flashaccess-keyserver-global.xml] contiene impostazioni che si applicano a tutti i tenant del server chiavi. Questo file deve trovarsi in `KeyServer.ConfigRoot`. Per un esempio di file di configurazione globale, vedere la directory [!DNL configs] . Il file di configurazione globale include quanto segue:

* Registrazione - Specifica il livello di registrazione e la frequenza con cui viene eseguito il rollup dei file di registro.
* Password HSM - Obbligatoria solo se viene utilizzato un HSM per memorizzare le credenziali del server.

Per ulteriori informazioni, consulta i commenti nel file di configurazione globale di esempio disponibile in `<Primetime DRM Key Server>/configs` .

## File di configurazione tenant {#tenant-configuration-files}

I file di configurazione [!DNL flashaccess-ioskeyserver-tenant.xml] e [!DNL flashaccess-xboxkeyserver-tenant.xml] contengono impostazioni applicabili a un tenant specifico del server chiavi DRM di Primetime. Ogni tenant ha la propria istanza di questi file di configurazione che si trova in [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]. Vedere la directory [!DNL configs/faxsks/tenants/sampletenant] per un file di configurazione tenant di esempio.

È possibile specificare tutti i percorsi di file nel file di configurazione del tenant come percorsi assoluti o percorsi relativi alla directory di configurazione del tenant ( [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]).

Tutti i file di configurazione del tenant includono:

* Credenziali server chiavi - Specifica una o più credenziali server chiavi (certificato e chiave privata) emesse da Adobe. Può essere specificato come percorso di un file [!DNL .pfx] e di una password oppure come alias di una credenziale memorizzata in un HSM. Diverse credenziali possono essere specificate qui, come percorsi di file, alias di chiave, o entrambi.

Il file di configurazione tenant **iOS** include:

* Finestra di consegna chiavi - (facoltativo) Specifica la finestra di validità della marca temporale della richiesta di consegna chiave (in secondi). Il valore predefinito è 500 secondi.

Il file di configurazione del tenant **Xbox 360** include:

* Credenziale XSTS - Specifica la credenziale dello sviluppatore dell&#39;applicazione utilizzata per decrittografare i token XSTS
* Certificato di firma XSTS - Specifica il certificato utilizzato per verificare la firma sui token XSTS.
* Elenco consentiti di Packager - Certificati di Packager considerati attendibili dal server chiavi. Se nell&#39;elenco non sono presenti certificati del packager, tutti i certificati del packager saranno considerati attendibili.

## File di registro {#log-files}

I file di registro generati dall&#39;applicazione server chiavi DRM di Primetime ( [!DNL flashaccess-ioskeyserver_*.log] e [!DNL flashaccess-xboxkeyserver_*.log]) si troveranno nella directory specificata da `KeyServer.LogRoot`.

I file di registro sono distinti per tipo di client. Esistono due registri per tipo di client:

* Un *log di accesso* - Monitora solo le richieste e le risposte.
* A *log di contesto* - Contiene messaggi di errore dettagliati e tracce di stack.

## Avvio del server chiavi {#starting-the-key-server}

Per avviare il server chiavi, avvia Tomcat.