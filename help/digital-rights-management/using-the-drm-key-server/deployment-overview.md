---
title: Panoramica sulla distribuzione di Primetime DRM Key Server
description: Panoramica sulla distribuzione di Primetime DRM Key Server
copied-description: true
exl-id: d70e8315-ed35-4159-842b-5066a2b1c4f0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 0%

---

# Distribuire il server chiavi DRM Primetime {#deploy-the-primetime-drm-key-server}

Prima di distribuire Primetime DRM Key Server, verificare di aver installato le versioni richieste di Java e Tomcat. Vedi, [Requisiti principali del server DRM](../../digital-rights-management/using-the-drm-key-server/requirements.md).

Il download del Key Server DRM di Primetime include [!DNL faxsks.war]. Per distribuire il file WAR, copiatelo nel file Tomcat [!DNL webapps] directory. Se il file WAR è stato distribuito in precedenza, potrebbe essere necessario eliminare manualmente la directory WAR decompressa, [!DNL faxsks] in Tomcat [!DNL webapps] directory). Per evitare che Tomcat decomprima i file WAR, modificare la [!DNL server.xml] file in Tomcat [!DNL conf] e impostare `unpackWARs` attribuire a `false`.

Il server chiavi DRM di Primetime utilizza facoltativamente una libreria specifica della piattaforma (`jsafe.dll` su Windows o `libjsafe.so` su Linux) per migliorare le prestazioni. Copia la libreria appropriata per la piattaforma da `thirdparty/cryptoj/platform` in una posizione specificata da `PATH` variabile di ambiente (o `LD_LIBRARY_PATH` su Linux).

>[!NOTE]
>
>La versione a 64 bit del [!DNL jsafe] utilizza la libreria solo se il sistema operativo e JDK supportano entrambi i formati a 64 bit; in caso contrario, utilizza la versione a 32 bit.

## Configurazione SSL {#ssl-configuration}

SSL è richiesto per la consegna della chiave HTTPS remota. Le connessioni SSL potevano essere gestite dal server applicazioni (ad esempio, configurando SSL in Tomcat) o potevano essere gestite da un altro server (ad esempio, un load balancer, un acceleratore SSL o Apache). La consegna remota della chiave HTTPS richiede una connessione SSL. Il server necessita di un certificato SSL rilasciato da una CA attendibile.

Sono disponibili diverse opzioni per la configurazione di SSL. Di seguito sono riportati alcuni esempi di configurazione di SSL con autenticazione client in Apache e Tomcat.

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

L’esempio seguente mostra la configurazione SSL di Tomcat. Per generare i file di certificati e chiavi:

```
Generate key:  
 openssl genrsa -des3 -out server.key 1024 
Generate CSR: 
 openssl req -new -key server.key -out server.csr 
Generate Certificate: 
 openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.cer
```

Quando viene richiesto il nome comune, utilizzare il nome di dominio completo (FQDN) del server.

Copia [!DNL server.cer], e [!DNL server.key] nella directory Tomcat. Specifica il connettore seguente in [!DNL conf/server.xml]:

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

È possibile impostare le due proprietà di sistema Java seguenti per modificare la posizione dei file di configurazione e di registro per il server chiavi DRM Primetime:

* `KeyServer.ConfigRoot` - Questa directory contiene tutti i file di configurazione per il server chiavi DRM Primetime. Per informazioni dettagliate sul contenuto di questi file, vedi [File di configurazione del server chiavi](#key-server-configuration-files). Se non viene impostato, il valore predefinito è [!DNL CATALINA_BASE/keyserver].

* `KeyServer.LogRoot` : directory di registro contenente i registri dell’applicazione iOS Key Server. Se non viene impostato, il valore predefinito è uguale a `KeyServer.ConfigRoot`

* `XboxKeyServer.LogRoot` - Questa è una directory di registro che contiene i registri dell&#39;applicazione Xbox Key Server. Se non viene impostato, il valore predefinito è uguale a `KeyServer.ConfigRoot`.

Se sta usando [!DNL catalina.bat] o [!DNL catalina.sh] per avviare Tomcat, è possibile impostare facilmente queste proprietà di sistema utilizzando `JAVA_OPTS` variabile di ambiente. Tutte le opzioni Java qui impostate verranno utilizzate all’avvio di Tomcat. Ad esempio, imposta:

```
JAVA_OPTS=-DKeyServer.ConfigRoot=”absolute-path-to-config-folder” 
  -DKeyServer.LogRoot=”absolute-path-to-log-folder”
```

## Credenziali DRM di Primetime {#primetime-drm-credentials}

Per elaborare richieste chiave dai client iOS e Xbox 360 di Primetime DRM, è necessario configurare il server chiave DRM di Primetime con un set di credenziali emesse da Adobe. Queste credenziali possono essere memorizzate in PKCS#12 ( [!DNL .pfx]) o su un HSM.

Il [!DNL .pfx] I file possono essere posizionati ovunque, ma per semplificare la configurazione, l’Adobe consiglia di inserire [!DNL .pfx] file nella directory di configurazione del tenant. Per ulteriori informazioni, consulta [File di configurazione del server chiavi](#key-server-configuration-files).

### Configurazione HSM {#section_13A19E3E32934C5FA00AEF621F369877}

Se si sceglie di utilizzare un HSM per memorizzare le credenziali del server, è necessario caricare le chiavi private e i certificati nell&#39;HSM e creare un *pkcs11.cfg* file di configurazione. Questo file deve trovarsi nel file *KeyServer.ConfigRoot* directory. Consulta la `<Primetime DRM Key Server>/configs` per un file di configurazione PKCS 11 di esempio. Per informazioni sul formato di [!DNL pkcs11.cfg], consultare la documentazione del provider Sun PKCS11.

Per verificare che i file di configurazione di HSM e Sun PKCS11 siano configurati correttamente, è possibile utilizzare il comando seguente dalla directory in cui è [!DNL pkcs11.cfg] il file si trova ( [!DNL keytool] è installato con Java JRE e JDK):

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Se le credenziali sono visualizzate nell&#39;elenco, l&#39;HSM è configurato correttamente e il server chiavi sarà in grado di accedere alle credenziali.

## File di configurazione del server chiavi {#key-server-configuration-files}

Il server chiavi DRM Primetime richiede due tipi di file di configurazione:

* Un file di configurazione globale, [!DNL flashaccess-keyserver-global.xml]
* Un file di configurazione tenant per ogni tenant, [!DNL flashaccess-keyserver-tenant.xml]

Se vengono apportate modifiche ai file di configurazione, è necessario riavviare il server per rendere effettive le modifiche.

Per evitare di rendere disponibili le password in testo non crittografato nei file di configurazione, tutte le password specificate nei file di configurazione globale e tenant devono essere crittografate. Per ulteriori informazioni sulla crittografia delle password, vedere [*Scrambler password* in *Utilizzo del server DRM Primetime per lo streaming protetto*](../protected-streaming/understanding-deployment/drm-for-protected-streaming-utilities/password-scrambler.md).

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

Il [!DNL flashaccess-keyserver-global.xml] Il file di configurazione contiene impostazioni applicabili a tutti i tenant del server chiavi. Questo file deve trovarsi in `KeyServer.ConfigRoot`. Consulta la [!DNL configs] per un esempio di file di configurazione globale. Il file di configurazione globale include quanto segue:

* Registrazione: specifica il livello di registrazione e la frequenza con cui viene eseguito il rollback dei file di registro.
* Password HSM: obbligatoria solo se viene utilizzato un HSM per memorizzare le credenziali del server.

Vedi i commenti nell’esempio di file di configurazione globale che si trova in `<Primetime DRM Key Server>/configs` per ulteriori dettagli.

## File di configurazione tenant {#tenant-configuration-files}

Il [!DNL flashaccess-ioskeyserver-tenant.xml] e [!DNL flashaccess-xboxkeyserver-tenant.xml] I file di configurazione contengono impostazioni applicabili a un tenant specifico del server chiavi DRM di Primetime. Ogni tenant ha la propria istanza di questi file di configurazione che si trova in [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]. Consulta la [!DNL configs/faxsks/tenants/sampletenant] per un esempio di file di configurazione tenant.

È possibile specificare tutti i percorsi dei file nel file di configurazione del tenant come percorsi assoluti o relativi alla directory di configurazione del tenant ( [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]).

Tutti i file di configurazione tenant includono:

* Credenziali server chiavi: specifica una o più credenziali del server chiavi (certificato e chiave privata) rilasciate dall&#39;Adobe. Può essere specificato come percorso di un [!DNL .pfx] e una password o un alias per una credenziale archiviata in un HSM. Qui è possibile specificare diverse credenziali di questo tipo, come percorsi di file, alias chiave o entrambi.

Il **iOS** il file di configurazione tenant include:

* Finestra consegna chiave - (facoltativo) specifica la finestra di validità della marca temporale della richiesta di consegna chiave (in secondi). Il valore predefinito è 500 secondi.

Il **Xbox 360** il file di configurazione tenant include:

* Credenziali XSTS: specifica le credenziali dello sviluppatore dell&#39;applicazione utilizzate per decrittografare i token XSTS
* Certificato di firma XSTS: specifica il certificato utilizzato per verificare la firma sui token XSTS.
* Elenco consentiti Packager: i certificati Packager considerati attendibili dal server chiavi. Se nell&#39;elenco non sono presenti certificati Packager, tutti i certificati Packager verranno considerati attendibili.

## File di registro {#log-files}

File di registro generati dall&#39;applicazione server chiavi DRM Primetime ( [!DNL flashaccess-ioskeyserver_*.log] e [!DNL flashaccess-xboxkeyserver_*.log]) si troverà nella directory specificata da `KeyServer.LogRoot`.

I file di registro sono distinti per tipo di client. Esistono due registri per tipo di client:

* Un *registro di accesso* : monitora solo le richieste e le risposte.
* A *registro di contesto* : contiene messaggi di errore dettagliati e tracce dello stack.

## Avvio del server chiavi {#starting-the-key-server}

Per avviare il server chiavi, avviare Tomcat.
