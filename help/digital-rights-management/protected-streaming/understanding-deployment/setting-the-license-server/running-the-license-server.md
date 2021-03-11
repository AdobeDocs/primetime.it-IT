---
title: Esecuzione del server DRM per lo streaming protetto
description: Esecuzione del server DRM per lo streaming protetto
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 0%

---


# Esecuzione del server DRM per lo streaming protetto {#running-the-drm-server-for-protected-streaming}

Prima di avviare Adobe Primetime DRM Server for Protected Streaming, è consigliabile verificare la validità delle impostazioni nei file di configurazione.

Puoi verificare la validità delle impostazioni utilizzando le utility fornite con il server licenze. (Vedi *Convalida della configurazione* in questa guida.

Per avviare Tomcat e il server licenze, è necessario eseguire [!DNL catalina.bat start] o [!DNL catalina.sh start] dalla directory [!DNL bin] di Tomcat.

Dopo aver avviato il server, devi verificare che sia stato configurato correttamente aprendo `https://<lic<span></span>ense-server-host:port>/flashaccessserver/<tenant-name>/flashaccess/license/v1` in una finestra del browser. Se la configurazione del tenant è stata caricata correttamente, viene visualizzato un messaggio di conferma.

## File di registro {#log-files}

I file di registro generati dal server DRM di Adobe Primetime per l&#39;applicazione di streaming protetto si trovano nella directory specificata da LicenseServer.LogRoot.

>[!NOTE]
>
>Se i file di registro correnti vengono eliminati o spostati durante l&#39;esecuzione del server, il file di registro potrebbe non essere ricreato. Pertanto alcune informazioni di log possono essere eliminate.

### Struttura della directory dei log {#section_F490A483D60145ADBC21038914C39203}

Le directory dei log sono strutturate per facilità d&#39;uso. La directory di log ha la seguente struttura:

```
<i class="+ topic ph hi-d="" i "="">
 LicenseServer.LogRoot/ 
 flashaccess-global.log 
     flashaccessserver/ 
         flashaccess-partition.log 
         tenants/ 
             
 <i class="+ topic ph hi-d="" i "="">
  tenantname/ 
                  flashaccess-tenant.log
 </i class="+ topic>
</i class="+ topic>
```

### File di registro globale {#section_1CFA90748142439C9F3BE380969539DA}

Il file di registro globale [!DNL flashaccess-global.log] si trova in *LicenseServer.LogRoot*. Il registro può includere messaggi di registro che l’SDK Java DRM di Adobe Primetime o i messaggi di registro potrebbero aver generato durante il momento in cui il server è stato inizializzato.

### File di registro delle partizioni {#section_5660137CD6AA40519E72A4315534846B}

Il file di registro della partizione [!DNL flashaccess-partition.log] si trova nella directory `<LicenseServer.LogRoot>/flashaccesserver`. Include i messaggi di registro generati durante l’elaborazione di una richiesta di licenza.

### File di registro tenant {#section_F0257CC0831647F18A746B4F02E3E910}

Il file di registro tenant di ciascun tenant, [!DNL flashaccess-tenant.log], si trova in `<LicenseServer.LogRoot>/flashaccesserver/tenants/<tenantname>`. Il registro tenant include informazioni di controllo che descrivono ogni licenza generata per questo tenant.

## Aggiornamento dei file di configurazione {#updating-configuration-files}

Non appena il server licenze legge uno dei file di configurazione del server licenze (configurazione globale o tenant), le informazioni di configurazione vengono memorizzate nella cache. Pertanto i file non devono essere letti dal disco per ogni richiesta di licenza. Tuttavia, il server consente anche di modificare la maggior parte dei valori nei file di configurazione senza richiedere il riavvio del server per rendere effettive le modifiche.

Ogni volta che si modifica il file di configurazione, il server licenze memorizza l&#39;ora dell&#39;ultima modifica apportata al file. A un intervallo configurabile, il server controlla se l&#39;ora di modifica del file è cambiata. Se è stato modificato, il server ricarica automaticamente il contenuto del file di configurazione.

Se desideri controllare la frequenza con cui il server controlla gli aggiornamenti, devi impostare l’attributo `refreshDelaySeconds` nell’elemento `Caching` del file di configurazione globale. Ad esempio, se `refreshDelaySeconds` è impostato su 3600 secondi, il server aggiornerà la configurazione entro al massimo un&#39;ora dal momento della modifica del file di configurazione. Se `refreshDelaySeconds` è impostato su 0, il server verifica la presenza di aggiornamenti di configurazione a ogni richiesta. Si sconsiglia di impostare `refreshDelaySeconds` su un valore basso in qualsiasi ambiente di produzione perché questo può influire sulle prestazioni.

L’elemento `Caching` controlla anche quante configurazioni dei tenant vengono memorizzate nella cache contemporaneamente. Puoi impostare questo valore su un numero inferiore al numero totale di tenant per limitare la quantità di memoria utilizzata per memorizzare nella cache le informazioni di configurazione. Se viene ricevuta una richiesta per un tenant non presente nella cache, la configurazione viene caricata prima che la richiesta possa essere elaborata. Se la cache è piena, il tenant utilizzato meno di recente viene rimosso dalla cache.

La versione cache della configurazione continua a essere utilizzata nelle seguenti situazioni (fino alla successiva verifica degli aggiornamenti da parte del server):

* Se una modifica viene salvata in un file di configurazione o in uno qualsiasi dei file di certificato a cui si fa riferimento nel file [!DNL flashaccess-tenant.xml] mentre il server tenta di leggere il file
* Se la marca temporale del file è inferiore a un secondo prima dell&#39;ora corrente
* Se la marca temporale del file è futura

Se non è presente alcuna versione cache, il caricamento della configurazione non riesce e viene restituito un errore al client. Il server tenta quindi di caricare nuovamente il file alla successiva ricezione di una richiesta per quel tenant.

### Aggiornamento del file di configurazione globale {#section_AA546C72442646CFB8906AEEBDF50587}

Puoi modificare la password HSM in [!DNL flashaccess-global.xml] in qualsiasi momento. Le modifiche avranno effetto alla successiva ricarica del file di configurazione da parte del server. Tuttavia, le modifiche agli elementi di registrazione e memorizzazione in cache non vengono ricaricate. È necessario riavviare il server prima che eventuali modifiche per questi elementi diventino effettive.

### Aggiornamento del file di configurazione del tenant {#section_71624DB8DF28480F84F34F0FF7FD4365}

Puoi modificare in qualsiasi momento tutti i valori specificati nel file [!DNL flashaccess-tenant.xml] . Le modifiche avranno effetto alla successiva ricarica del file di configurazione da parte del server. Inoltre, il server verifica la presenza di eventuali modifiche in tutti i file di credenziali ( [!DNL .pfx]) e nei file di certificato di elenco consentiti del packager a cui si fa riferimento nel file di configurazione del tenant.