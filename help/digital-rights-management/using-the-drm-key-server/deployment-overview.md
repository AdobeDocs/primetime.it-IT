---
seo-title: Implementazione della panoramica del server chiavi DRM di Primetime
title: Implementazione della panoramica del server chiavi DRM di Primetime
uuid: 86630675-c15d-4f32-8212-d7343f4f92e0
translation-type: tm+mt
source-git-commit: 105dedcfe47a5f454a067e66a95827e638290742

---


# Implementare il server chiavi DRM Primetime {#deploy-the-primetime-drm-key-server}

Prima di distribuire il server chiavi DRM di Primetime, accertatevi di aver installato le versioni necessarie di Java e Tomcat. Consultate Requisiti [del server di chiavi](../../digital-rights-management/using-the-drm-key-server/requirements.md)DRM.

Il download del server chiavi DRM Primetime include [!DNL faxsks.war]. Per distribuire questo file WAR, copiare il file nella [!DNL webapps] directory di Tomcat. Se avete già distribuito il file WAR, potrebbe essere necessario eliminare manualmente la directory WAR non imballata, [!DNL faxsks] nella directory di Tomcat [!DNL webapps] ). Per impedire a Tomcat di disfare i file WAR, modificare il [!DNL server.xml] file nella [!DNL conf] directory di Tomcat e impostare l&#39; `unpackWARs` attributo su `false`.

Il server chiavi DRM di Primetime utilizza facoltativamente una libreria specifica per la piattaforma (`jsafe.dll` in Windows o `libjsafe.so` in Linux) per migliorare le prestazioni. Copiate la libreria appropriata per la piattaforma da `thirdparty/cryptoj/platform` una posizione specificata dalla variabile di `PATH` ambiente (o `LD_LIBRARY_PATH` su Linux).

>[!NOTE]
>
>La versione a 64 bit della [!DNL jsafe] libreria deve essere utilizzata solo se sia il sistema operativo che il JDK supportano la versione a 64 bit, altrimenti la versione a 32 bit viene utilizzata.

## Configurazione SSL {#ssl-configuration}

SSL è richiesto per la distribuzione della chiave HTTPS remota. Le connessioni SSL possono essere gestite dal server dell’applicazione (ovvero configurando SSL in Tomcat) o possono essere gestite da un altro server (ad esempio, un sistema di bilanciamento del carico, un acceleratore SSL o Apache). La consegna remota della chiave HTTPS richiede una connessione SSL. Il server richiede un certificato SSL emesso da una CA affidabile.

Sono disponibili diverse opzioni per configurare SSL. Di seguito sono riportati alcuni esempi per configurare SSL con l’autenticazione client in Apache e Tomcat.

L’esempio seguente mostra la configurazione Apache SSL:

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

L’esempio seguente mostra la configurazione Tomcat SSL. Per generare file di certificato e di chiave:

```
Generate key:  
 openssl genrsa -des3 -out server.key 1024 
Generate CSR: 
 openssl req -new -key server.key -out server.csr 
Generate Certificate: 
 openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.cer
```

Quando viene richiesto il nome comune, utilizzate il nome di dominio completo (FQDN, Fully Qualified Domain Name) del vostro server.

Copiare [!DNL server.cer]e [!DNL server.key] nella directory Tomcat. Specificare il seguente connettore in [!DNL conf/server.xml]:

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

È possibile impostare le due seguenti proprietà del sistema Java per modificare la posizione dei file di configurazione e di registro per il server chiavi DRM Primetime:

* `KeyServer.ConfigRoot` - Questa directory contiene tutti i file di configurazione per il server chiavi DRM Primetime. Per informazioni dettagliate sul contenuto di questi file, consultate File [di configurazione del server](#key-server-configuration-files)chiavi. Se non è impostato, il valore predefinito è [!DNL CATALINA_BASE/keyserver].

* `KeyServer.LogRoot` - Si tratta di una directory di registro che contiene i registri delle applicazioni server chiavi iOS. Se non è impostato, il valore predefinito è uguale a `KeyServer.ConfigRoot`

* `XboxKeyServer.LogRoot` - Si tratta di una directory di registro che contiene i registri dell&#39;applicazione Xbox Key Server. Se non è impostato, il valore predefinito è uguale a `KeyServer.ConfigRoot`.

Se si utilizza [!DNL catalina.bat] o [!DNL catalina.sh] per avviare Tomcat, queste proprietà del sistema possono essere facilmente impostate utilizzando la variabile di `JAVA_OPTS` ambiente. Tutte le opzioni Java impostate qui verranno utilizzate all&#39;avvio di Tomcat. Ad esempio, set:

```
JAVA_OPTS=-DKeyServer.ConfigRoot=”absolute-path-to-config-folder” 
  -DKeyServer.LogRoot=”absolute-path-to-log-folder”
```

## Credenziali DRM di Primetime {#primetime-drm-credentials}

Per elaborare le richieste chiave dai client iOS e Xbox 360 DRM di Primetime, il server chiavi DRM di Primetime deve essere configurato con un set di credenziali emesse da Adobe. Queste credenziali possono essere archiviate in file PKCS#12 ( [!DNL .pfx]) o in un file HSM.

I [!DNL .pfx] file possono trovarsi ovunque, ma per semplificare la configurazione, Adobe consiglia di collocare i [!DNL .pfx] file nella directory di configurazione del tenant. Per ulteriori informazioni, vedere File [di configurazione del server](#key-server-configuration-files)chiavi.

### Configurazione HSM {#section_13A19E3E32934C5FA00AEF621F369877}

Se scegliete di utilizzare un HSM per memorizzare le credenziali del server, dovete caricare le chiavi private e i certificati nell&#39;HSM e creare un file di configurazione *pkcs11.cfg* . Questo file deve trovarsi nella directory *KeyServer.ConfigRoot* . Consulta [!DNL <Primetime DRM Key Server>/configs] directory per un file di configurazione PKCS 11 di esempio. Per informazioni sul formato di [!DNL pkcs11.cfg], consultate la documentazione del fornitore Sun PKCS11.

Per verificare che i file di configurazione HSM e Sun PKCS11 siano configurati correttamente, potete utilizzare il seguente comando dalla directory in cui si trova il [!DNL pkcs11.cfg] file ( [!DNL keytool] è installato con Java JRE e JDK):

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Se nell’elenco vengono visualizzate le credenziali, l’HSM è configurato correttamente e il server chiavi sarà in grado di accedere alle credenziali.

## File di configurazione del server chiavi {#key-server-configuration-files}

Il server chiavi DRM di Primetime richiede due tipi di file di configurazione:

* Un file di configurazione globale, [!DNL flashaccess-keyserver-global.xml]
* Un file di configurazione tenant per ciascun tenant, [!DNL flashaccess-keyserver-tenant.xml]

Se vengono apportate modifiche ai file di configurazione, il server deve essere riavviato affinché le modifiche abbiano effetto.

Per evitare di rendere le password disponibili in testo chiaro nei file di configurazione, tutte le password specificate nei file di configurazione globali e tenant devono essere crittografate. Per ulteriori informazioni sulla cifratura delle password, vedere [*Password Scrambler *in* Utilizzo del server DRM di Primetime per lo streaming *](../protected-streaming/understanding-deployment/drm-for-protected-streaming-utilities/password-scrambler.md)protetto.

## Struttura della directory di configurazione {#configuration-directory-structure}

Le directory di configurazione hanno la struttura seguente:

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

Il file di [!DNL flashaccess-keyserver-global.xml] configurazione contiene impostazioni che si applicano a tutti i tenant del Server chiavi. Questo file deve essere ubicato in `KeyServer.ConfigRoot`. Vedere la [!DNL configs] directory di un file di configurazione globale di esempio. Il file di configurazione globale include quanto segue:

* Registrazione - Specifica il livello di registrazione e la frequenza di scorrimento dei file di registro.
* Password HSM - necessaria solo se viene utilizzato un HSM per memorizzare le credenziali del server.

Vedere i commenti nel file di configurazione globale di esempio che si trova in [!DNL <Primetime DRM Key Server>/configs] per ulteriori dettagli.

## File di configurazione tenant {#tenant-configuration-files}

I file [!DNL flashaccess-ioskeyserver-tenant.xml] e [!DNL flashaccess-xboxkeyserver-tenant.xml] di configurazione contengono impostazioni che si applicano a un tenant specifico del server chiavi DRM di Primetime. Ogni tenant ha una propria istanza di questi file di configurazione che si trova in [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]. Vedere la [!DNL configs/faxsks/tenants/sampletenant] directory per un file di configurazione tenant di esempio.

È possibile specificare tutti i percorsi di file nel file di configurazione del tenant come percorsi assoluti o percorsi relativi alla directory di configurazione del tenant ( [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]).

Tutti i file di configurazione del tenant includono:

* Credenziali server chiavi - Specifica una o più credenziali server chiavi (certificato e chiave privata) emesse da Adobe. Può essere specificato come percorso di un [!DNL .pfx] file e di una password, o come alias di una credenziale memorizzata in un HSM. Diverse credenziali possono essere specificate qui, come percorsi di file, alias chiave, o entrambi.

Il file di configurazione del tenant **iOS** include:

* Finestra consegna chiave - (facoltativo) Specifica la finestra di validità della marca temporale della richiesta di consegna chiave (in secondi). Il valore predefinito è 500 secondi.

Il file di configurazione tenant **Xbox 360** include:

* Credenziali XSTS - Specifica la credenziale dello sviluppatore di applicazioni utilizzata per decifrare i token XSTS
* Certificato di firma XSTS - Specifica il certificato utilizzato per verificare la firma sui token XSTS.
* Whitelist di Packager - Certificati Packager attendibili dal server chiavi. Se nell&#39;elenco non sono presenti certificati packager, tutti i certificati packager saranno considerati attendibili.

## File di registro {#log-files}

I file di registro generati dall&#39;applicazione server chiavi DRM di Primetime ( [!DNL flashaccess-ioskeyserver_*.log] e [!DNL flashaccess-xboxkeyserver_*.log]) si troveranno nella directory specificata da `KeyServer.LogRoot`.

I file di registro sono distinti per tipo di client. Esistono due registri per tipo di client:

* Un registro *di* accesso: consente di monitorare solo le richieste e le risposte.
* Un registro *di* contesto: contiene messaggi di errore dettagliati e tracce dello stack.

## Avvio del server chiavi {#starting-the-key-server}

Per avviare il server chiavi, avviate Tomcat.